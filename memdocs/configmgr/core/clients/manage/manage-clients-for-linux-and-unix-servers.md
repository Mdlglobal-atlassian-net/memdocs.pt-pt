---
title: Gerir clientes Linux e UNIX
titleSuffix: Configuration Manager
description: Gerencie os clientes em servidores Linux e UNIX no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710644"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Como gerir clientes para servidores Linux e UNIX em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Quando gere os servidores Linux e UNIX com O Gestor de Configuração, pode configurar coleções, janelas de manutenção e configurações do cliente para ajudar a gerir os servidores. Além disso, embora o cliente do Gestor de Configuração do Linux e da UNIX não tenha uma interface de utilizador, pode forçar o cliente a fazer uma sondagem manual para a política do cliente.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Utilize coleções para gerir grupos de servidores Linux e UNIX da mesma forma que utiliza coleções para gerir outros tipos de clientes. As coleções podem ser coleções de membros diretos ou coleções baseadas em consultas. As coleções baseadas em consultas identificam sistemas operativos do cliente, configurações de hardware ou outros detalhes sobre o cliente que estão armazenados na base de dados do site. Por exemplo, pode utilizar coleções que incluam servidores Linux e UNIX para gerir as seguintes definições:  

- Definições do cliente  

- Implementações de software  

- Impor janelas de manutenção  

  Antes de poder identificar um cliente Linux ou UNIX pelo seu sistema operativo ou distribuição, deve recolher o inventário de [hardware](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) do cliente.  

  As definições padrão do cliente para o inventário de hardware incluem informações sobre o sistema operativo de um cliente. Pode utilizar a propriedade **Legenda** da classe **Sistema Operativo** para identificar o sistema operativo de um servidor Linux ou UNIX.  

  Pode visualizar detalhes sobre computadores que executam o cliente do Gestor de Configuração para o Linux e uniX no nó de **Dispositivos** do espaço de trabalho **De Ativos e Compliance** na consola Do Gestor de Configuração. No espaço de trabalho **de Ativo e Conformidade** da consola 'Gestor de Configuração', pode ver o nome do sistema operativo de cada computador na coluna do Sistema **Operativo.**  

  Por predefinição, os servidores Linux e UNIX são membros da coleção **Todos os Sistemas** . Recomendamos que construa coleções personalizadas que incluam apenas servidores Linux e UNIX, ou um subconjunto deles. As coleções personalizadas permitem-lhe gerir operações como implementar software ou atribuir configurações de clientes a grupos de computadores similares, para que possa medir com precisão o sucesso de uma implementação.   

  Quando criar uma coleção personalizada para servidores Linux e UNIX, inclua as consultas de regra de associação que contenham o atributo Legenda para o atributo Sistema Operativo. Para obter informações sobre a criação de coleções, consulte [como criar coleções.](../../../core/clients/manage/collections/create-collections.md)  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a>Janelas de manutenção para servidores Linux e UNIX  
 O cliente do Gestor de Configuração dos servidores Linux e UNIX suporta a utilização de [janelas](../../../core/clients/manage/collections/use-maintenance-windows.md)de manutenção . Este suporte é inalterado em com os clientes baseados no Windows.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a>Definições de cliente para servidores Linux e UNIX  
 Pode [configurar as definições](../../../core/clients/deploy/configure-client-settings.md) do cliente que se aplicam aos servidores Linux e UNIX da mesma forma que configura as definições para outros clientes.  

 Por predefinição, as **Predefinições de Agente do Cliente** aplicam-se a servidores Linux e UNIX. Também pode criar configurações personalizadas de clientes e implantá-las em coleções de clientes específicos.  

 Não existem definições de cliente adicionais que se apliquem apenas a clientes Linux e UNIX. No entanto, existem configurações de clientes padrão que não se aplicam aos clientes Linux e UNIX. O cliente da Linux e da UNIX apenas aplica configurações para a funcionalidade que suporta.  

 Por exemplo, uma definição personalizada do dispositivo cliente que permite e configuraas de controlo remoto seria ignorada pelos servidores Linux e UNIX, porque o cliente para Linux e UNIX não suporta controlo remoto.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a>Política informática para servidores Linux e UNIX  
 O cliente dos servidores Linux e UNIX faz uma sondagem periódica no seu site para que a política do computador aprenda sobre configurações solicitadas e verifique se há implementações.  

 Pode também forçar o cliente num servidor Linux ou UNIX a consultar imediatamente a política do computador. Para isso, utilize credenciais **de raiz** no servidor para executar o seguinte comando: **/opt/microsoft/configmgr/bin/ccmexec -rs**  

 Os detalhes da consulta de política do computador são introduzidos no ficheiro de registo de cliente partilhado, **scxcm.log**.  

> [!NOTE]  
>  O cliente do Gestor de Configuração da Linux e da UNIX nunca solicita nem processa a política do utilizador.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a>Como gerir certificados sobre o cliente para linux e UNIX  
 Depois de instalar o cliente para Linux e UNIX, pode utilizar a ferramenta **certutil** para atualizar o cliente com um novo certificado PKI e para importar uma nova lista de Revogação de Certificados (CRL). Quando instala o cliente para linux e UNIX, esta ferramenta é colocada em `/opt/microsoft/configmgr/bin/certutil`. 

 Para gerir os certificados, execute o certutil em cada cliente com uma das seguintes opções:  

|Opção|Mais informações|  
|------------|----------------------|  
|`importPFX`|Utilize esta opção para especificar um certificado para substituir o certificado que está a ser utilizado por um cliente.<br /><br /> Quando utilizar, `-importPFX`deve também `-password` utilizar o parâmetro da linha de comando para fornecer a palavra-passe associada ao ficheiro PKCS#12.<br /><br /> Utilize `-rootcerts` para especificar quaisquer requisitos adicionais de certificado de raiz.<br /><br /> Exemplo: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Utilize esta opção para atualizar o certificado de assinatura do servidor de site que se encontra no servidor de gestão.<br /><br /> Exemplo: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Utilize esta opção para atualizar a CRL no cliente com um ou mais caminhos de ficheiro CRL.<br /><br /> Exemplo: `certutil -importcrl <comma separated CRL file paths>`|  
