---
title: Inventário de hardware para Linux e UNIX
titleSuffix: Configuration Manager
description: Saiba como utilizar o inventário de hardware para Linux e UNIX no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f4b822475111352c5dcf23f4868a1fa43ec3a7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906278"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Inventário de hardware para Linux e UNIX no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

O cliente do Gestor de Configuração da Linux e da UNIX suporta o inventário de hardware. Depois de recolher o inventário de hardware, pode executar o inventário de visualização nos relatórios do explorador de recursos ou do Gestor de Configuração, e usar estas informações para criar consultas e coleções que permitam as seguintes operações:  

- Implementação de software  

- Impor janelas de manutenção  

- Implementar definições de cliente personalizadas  

O inventário de hardware para servidores Linux e UNIX utiliza um servidor de Modelo de Informação Comum (CIM) baseado em padrões. O servidor CIM é executado como serviço de software (ou daemon) e fornece uma infraestrutura de gestão baseada em normas DMTF (Distributed Management Task Force). O servidor CIM proporciona uma funcionalidade semelhante às capacidades CIM do Windows Management Infrastructure (WMI) que estão disponíveis nos computadores baseados em Windows.  

Começando com a atualização acumulada 1, o cliente do Linux e da UNIX utiliza a versão **omiserver** de código aberto 1.0.6 do **Open Group**. (Antes da atualização cumulativa 1, o cliente utilizava **nanowbem** como o servidor CIM).  

O servidor CIM é instalado como parte do cliente para Linux e UNIX. O cliente do Linux e da UNIX comunica diretamente com o servidor CIM e não utiliza a interface WS-MAN do servidor CIM. A porta WS-MAN no servidor CIM está desativada quando o cliente é instalado. A Microsoft desenvolveu o servidor CIM que está agora disponível como código aberto através do projeto Open Management Infrastructure (OMI). Para obter mais informações sobre o projeto Open Management Infrastructure, veja o Web site [The Open Group](https://www.opengroup.org/) .  

O Inventário de Hardware nos servidores Linux e UNIX funciona mediante o mapeamento de classes e propriedades WMI Win32 existentes para as classes e propriedades equivalentes dos servidores Linux e UNIX. Este mapeamento de classes e propriedades one-to-one permite que o inventário de hardware Linux e UNIX se integre com o Gestor de Configuração. Os dados de inventário dos servidores Linux e UNIX exibem juntamente com o inventário de computadores baseados no Windows na consola e relatórios do Gestor de Configuração. Este comportamento proporciona uma experiência de gestão heterogénea consistente.  

> [!TIP]  
>  Pode utilizar o valor **Legenda** para a classe **Sistema Operativo** para identificar os diferentes sistemas operativos Linux e UNIX em consultas e coleções.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Configurar o inventário de hardware para servidores Linux e UNIX  
 Pode utilizar as predefinições de cliente ou criar definições de dispositivos cliente personalizadas para configurar o inventário de hardware. Quando utiliza as definições personalizadas do dispositivo do cliente, pode configurar as classes e propriedades que pretende recolher apartir apenas dos seus servidores Linux e UNIX. Também pode especificar agendamentos personalizados para recolher inventários completos e diferenciais dos servidores Linux e UNIX.  

 O cliente para Linux e UNIX suporta as seguintes classes de inventário de hardware, que estão disponíveis em servidores Linux e UNIX:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Nem todas as propriedades para estas classes de inventário estão ativadas para computadores Linux e UNIX no Gestor de Configuração.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Operações de inventário de hardware  
 Depois de recolher o inventário de hardware dos servidores Linux e UNIX, pode ver e utilizar estas informações da mesma forma que visualiza o inventário recolhido dos outros computadores:  

- Utilize o Explorador de Recursos para ver informações detalhadas sobre o inventário de hardware dos servidores Linux e UNIX  

- Criar consultas baseadas em configurações de hardware específicas  

- Crie coleções baseadas em consultas que se baseiam em configurações de hardware específicas  

- Execute relatórios que apresentam detalhes específicos sobre as configurações de hardware  

O inventário de hardware em servidores Linux ou UNIX é executado de acordo com o agendamento que configurar nas definições de cliente. Por defeito, este horário é a cada sete dias. O cliente para Linux e UNIX suporta ciclos de inventário completo e ciclos de inventário diferencial.  

Pode também forçar o cliente num servidor Linux ou UNIX a executar imediatamente o inventário de hardware. Para executar o inventário de hardware, num cliente use credenciais **de raiz** para executar o seguinte comando para iniciar um ciclo de inventário de hardware:`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

As ações do inventário de hardware são introduzidas no ficheiro de registo do cliente, **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Como utilizar a Open Management Infrastructure para criar um inventário de hardware personalizado  
 O cliente para Linux e UNIX suporta o inventário de hardware personalizado, que pode criar com a Open Management Infrastructure (OMI). Para isso, utiliza os seguintes passos:  

1.  Criar um fornecedor de inventário personalizado ao utilizar a fonte OMI  

2.  Configurar computadores para utilizar o novo fornecedor para comunicar inventário  

3.  Ativar o Gestor de Configuração para apoiar o novo fornecedor  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Criar um fornecedor de inventário de hardware personalizado para computadores Linux e UNIX:  
 Para criar um fornecedor personalizado de inventário de hardware para o cliente do Gestor de Configuração para o Linux e uniX, utilize a **Fonte OMI - v.1.0.6** e siga as instruções do Guia de Arranque do OMI. Este processo inclui a criação de um ficheiro MOF (Managed Object Format) que define o esquema do novo fornecedor. Mais tarde, importa o ficheiro MOF para O Gestor de Configuração para permitir o suporte da nova classe de inventário personalizado.  

 Tanto o OMI Source - v.1.0.6, como o Guia de Introdução da OMI, estão disponíveis para transferência a partir do Web site [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Pode localizar estas transferências no separador **Documents** (Documentos) da página Web seguinte do Web site OpenGroup.org: [Open Management Infrastructure (OMI)](https://collaboration.opengroup.org/omi/).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Configure cada computador com Linux ou UNIX com o fornecedor de inventário de hardware personalizado:  
 Depois de criar um fornecedor de inventário personalizado, tem de copiar e, em seguida, registar o ficheiro da biblioteca de fornecedores em cada computador que tem o inventário que pretende recolher.  

1.  Copie a biblioteca de fornecedores para cada computador Linux e UNIX a partir do qual pretende recolher o inventário. O nome da biblioteca do fornecedor assemelha-se ao seguinte nome: **XYZ_MyProvider.so**  

2.  Depois, em cada computador Linux e UNIX, registe a biblioteca de fornecedores no servidor OMI. O servidor OMI instala-se no computador quando instala o cliente do Gestor de Configuração para o Linux e o UNIX, mas tem de registar manualmente fornecedores personalizados. Utilize a seguinte linha de comando para registar o fornecedor:`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  Depois de registar o novo fornecedor, utilize a ferramenta **omicli** para testar o fornecedor. A ferramenta **omicli** é instalada em cada computador Linux e UNIX quando instalar o cliente do Gestor de Configuração para Linux e UNIX. Por exemplo, quando **XYZ_MyProvider** for o nome do fornecedor que criou, execute o seguinte comando no computador: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Para obter informações sobre o **omicli** e para testar fornecedores personalizados, veja o Guia de Introdução da OMI.  

> [!TIP]  
>  Utilize a distribuição de software para implementar e registar fornecedores personalizados em cada computador cliente Linux e UNIX.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Ative a nova classe de inventário no Configuration Manager:  
 Antes de o Gestor de Configuração poder reportar o inventário que é reportado pelo novo fornecedor nos computadores Linux e UNIX, deve importar o ficheiro 'Formato de Objeto Gerido ' (MOF) que define o esquema do seu fornecedor personalizado.  

 Para importar um ficheiro MOF personalizado para o Gestor de Configuração, consulte [como configurar o inventário](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)de hardware .  
