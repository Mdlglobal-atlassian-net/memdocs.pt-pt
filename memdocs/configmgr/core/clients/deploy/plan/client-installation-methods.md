---
title: Métodos de instalação de cliente
titleSuffix: Configuration Manager
description: Conheça os métodos de instalação do cliente do Gestor de Configuração.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713311"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Métodos de instalação do cliente no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar diferentes métodos para instalar o software cliente do Gestor de Configuração. Use um método, ou uma combinação de métodos. Este artigo descreve cada método, para que possa aprender qual é o melhor para a sua organização.  

## <a name="client-push-installation"></a>Instalação push do cliente  

**Plataforma de clientes suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode ser utilizado para instalar o cliente num único computador, numa coleção de computadores ou para os resultados de uma consulta.  

-   Pode ser utilizado para instalar automaticamente o cliente em todos os computadores detetados.  

-   Utiliza automaticamente as propriedades de instalação do cliente definidas no separador **Cliente** na caixa de diálogo **Propriedades da Instalação Push do Cliente**.  

#### <a name="disadvantages"></a>Desvantagens  

-   Pode causar tráfego de rede elevado quando efetuar instalações push em coleções de grandes dimensões.  

-   Só pode ser utilizado em computadores que tenham sido descobertos pelo Gestor de Configuração.  

-   Não pode ser usado para instalar clientes num grupo de trabalho.  

-   Deve ser especificada uma conta de instalação push de cliente com direitos administrativos no computador cliente pretendido.  

-   O Windows Firewall deve ser configurado com exceções nos computadores dos clientes.   

-   Não pode cancelar a instalação de pressão do cliente. O Gestor de Configuração tenta instalar o cliente em todos os recursos descobertos. Tenta voltar a falhar durante sete dias.  

Para mais informações, consulte [Como instalar clientes com pressão](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)do cliente .  



## <a name="software-update-point-based-installation"></a>Instalação baseada em pontos de atualizações de software  

**Plataforma de clientes suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Pode utilizar a infraestrutura de atualizações de software existente para gerir o software de cliente.  

-   Se os Serviços de Atualização do Servidor windows (WSUS) e as definições de política do grupo em Serviços de Domínio de Diretório Ativo estiverem configuradas corretamente, pode instalar automaticamente o software do cliente em novos computadores.  

-   Não requer que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Se o cliente for removido, este método reinstala-o.  

-   Não requer que configure e mantenha uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Como pré-requisito, requer uma infraestrutura de atualizações de software a funcionar.  

-   Deve utilizar o mesmo servidor para atualizações de instalação e software do cliente. Este servidor deve residir num local primário.  

-   Para instalar novos clientes, deve configurar um objeto de política de grupo nos Serviços de Domínio de Diretório Ativo com o ponto de atualização de software ativo do cliente e porta.  

-   Se o esquema de Diretório Ativo não for estendido para O Gestor de Configuração, deve utilizar as definições de política do grupo para fornecer computadores com propriedades de instalação do cliente.  

Para mais informações, consulte [Como instalar clientes com instalação baseada em atualizações de software.](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)  



## <a name="group-policy-installation"></a>Instalação da política de grupo  

**Plataforma de clientes suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não requer que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Pode ser utilizada para novas instalações de cliente ou para atualizações.  

-   Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

-   Não requer que configure e mantenha uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se um grande número de clientes estiver em instalação, pode causar tráfego de rede elevado.  

-   Se o esquema de Diretório Ativo não for estendido para O Gestor de Configuração, deve utilizar as definições de política do grupo para adicionar propriedades de instalação de clientes a computadores no seu site.  

Para mais informações, consulte Como instalar clientes com a política de [grupo.](../deploy-clients-to-windows-computers.md#BKMK_ClientGP)  



## <a name="logon-script-installation"></a>Instalação do script de início de sessão  

**Plataforma de clientes suportada**: Windows  

#### <a name="advantages"></a>Vantagens  

-   Não requer que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Se um grande número de clientes estiver em instalação durante um curto período de tempo, pode causar tráfego de rede elevado.  

-   Se os utilizadores não iniciarem frequentemente sessão na rede, pode demorar muito tempo a instalar em todos os computadores clientes.  

Para mais informações, consulte [Como instalar clientes com scripts](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript)de logon .  



## <a name="manual-installation"></a>Instalação manual  

**Plataforma de clientes suportada**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Vantagens  

-   Não requer que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Pode ser útil para fins de teste.  

-   Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

-   Sem automatização, portanto demorada.  

Para obter mais informações sobre como instalar manualmente o cliente em cada uma das plataformas, consulte os seguintes artigos:  

-   [Como implementar clientes em computadores Windows](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Como implementar clientes em servidores UNIX e Linux](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Como implementar clientes em Macs](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Instalação do MICROSOFT Intune MDM

**Plataformas de clientes suportadas**: Windows 10

#### <a name="advantages"></a>Vantagens  

-   Não requer que os computadores sejam descobertos antes que o cliente possa ser instalado.  

-   Não requer que configure e mantenha uma conta de instalação para o computador cliente pretendido.  

-   Pode usar a autenticação moderna com o Diretório Ativo Azure.  

-   Pode instalar e atribuir computadores na internet.  

-   Pode automatizar com o Windows AutoPilot e microsoft Intune para cogestão.  

#### <a name="disadvantages"></a>Desvantagens  

-   Requer tecnologias adicionais fora do Gestor de Configuração.  

-   Requer que o dispositivo tenha acesso à internet, mesmo que não seja baseado na Internet.  

Para obter mais informações, veja os artigos seguintes:  

-   [Como instalar clientes em dispositivos Windows geridos por MDM do Intune](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Instalar e atribuir clientes do Gestor de Configuração do Windows 10 utilizando a AD Azure para autenticação](../deploy-clients-cmg-azure.md)  

