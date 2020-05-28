---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como gerir as políticas antimalware e a segurança do Windows Firewall para os clientes.
ms.date: 03/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bdfd566682156e39e1dbed7c55af85b20a78671
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906685"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Aplica-se a: Gestor de Configuração (ramo atual)*

Endpoint Protection gere políticas antimalware e segurança do Windows Firewall para computadores clientes na sua hierarquia de Gestor de Configuração.  

> [!IMPORTANT]  
>  Tem de ser licenciado para utilizar a Endpoint Protection para gerir os clientes na sua hierarquia do Gestor de Configuração.  

 Quando utilizar a Proteção de Pontofinal com o Gestor de Configuração, tem os seguintes benefícios:  

-   Configure políticas antimalware, definições do Windows Firewall e gerencie a Proteção avançada de ameaças do Microsoft Defender para grupos selecionados de computadores  
-   Utilize as atualizações de software do Gestor de Configuração para descarregar os mais recentes ficheiros de definição antimalware para manter os computadores dos clientes atualizados  
-   Envie notificações por e-mail, utilize a monitorização na consola e veja os relatórios. Estas ações informam os utilizadores administrativos quando o malware é detetado em computadores clientes.  

A partir dos computadores Windows 10 e Windows Server 2016, o Windows Defender já está instalado. Para estes sistemas operativos, é instalado um cliente de gestão para o Windows Defender quando o cliente do Gestor de Configuração instala. Nos computadores Windows 8.1 e anteriores, o cliente Endpoint Protection está instalado com o cliente do Gestor de Configuração. O Windows Defender e o cliente Endpoint Protection têm as seguintes capacidades:  

-   Deteção e remediação de software maligno e spyware  
-   Deteção e remediação de rootkit  
-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  
-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  
-   Integração com o Serviço de Proteção de Nuvem para reportar malware à Microsoft. Quando se junta a este serviço, o cliente endpoint Protection ou o Windows Defender descarrega as definições mais recentes do Centro de Proteção contra Malware quando é detetado malware não identificado num computador.  

> [!NOTE]  
>  O cliente Endpoint Protection pode ser instalado num servidor que executa hiper-V e em máquinas virtuais de hóspedes com sistemas operativos suportados. Para evitar uma utilização excessiva da CPU, as ações de proteção do ponto final têm um atraso aleatório incorporado para que os serviços de proteção não funcionam simultaneamente.  

 Além disso, gere as definições do Windows Firewall com a Proteção de Pontofinal na consola do Gestor de Configuração.  

 [Cenário de exemplo: Utilização da Proteção de Pontofinal do Centro](scenarios-endpoint-protection.md) de Sistema para proteger computadores de malware Proteção do ponto final e firewall do Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  
 Endpoint Protection in Configuration Manager permite-lhe criar políticas antimalware que contenham configurações para configurações de clientes de proteção de pontofinal. Implemente estas políticas antimalware para computadores clientes. Em seguida, monitorize a conformidade no nó de **proteção** do ponto final sob **segurança** no espaço de trabalho **de monitorização.** Utilize também relatórios de proteção de ponto final no nó **de reporte.**  

 Informações adicionais:  

-   [Como criar e implementar políticas antimalware para proteção de pontos finais](endpoint-antimalware-policies.md) - Criar, implementar e monitorizar políticas antimalware com uma lista das definições que pode configurar  

-   [Como monitorizar a Proteção do Ponto Final](monitor-endpoint-protection.md) - Relatórios de atividadede monitorização, computadores de clientes infetados e muito mais.  

-   [Como gerir políticas antimalware e configurações de firewall para proteção de endpoint](endpoint-antimalware-firewall.md) - Remediar malware encontrado em computadores de cliente  

-   [Ficheiros de registo para proteção de pontofinal](../../core/plan-design/hierarchy/log-files.md#BKMK_EPLog)  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerir a Firewall do Windows com o Endpoint Protection  
 Endpoint Protection in Configuration Manager fornece uma gestão básica do Firewall do Windows nos computadores dos clientes. Para cada perfil de rede, pode configurar as seguintes definições:  

-   Ativar ou desativar a Firewall do Windows.  

-   Bloquear as ligações recebidas, incluindo as que se encontram na lista de programas permitidos.  

-   Notificar o utilizador quando a Firewall do Windows bloquear um programa novo.  

> [!NOTE]  
>  O Endpoint Protection suporta apenas a gestão da Firewall do Windows.  


 Para mais informações, consulte [como criar e implementar políticas de Firewall do Windows para proteção de pontos finais](create-windows-firewall-policies.md).  


## <a name="microsoft-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Microsoft Defender

Endpoint Protection gere e monitoriza a Microsoft Defender Advanced Threat Protection (ATP), anteriormente conhecida como Windows Defender ATP. O serviço ATP Microsoft Defender ajuda as empresas a detetar, investigar e responder a ataques avançados à rede corporativa. Para mais informações, consulte a [Microsoft Defender Advanced Threat Protection](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de Trabalho do Endpoint Protection  
 Utilize o seguinte diagrama para o ajudar a compreender o fluxo de trabalho para implementar a Proteção de Pontofinal na hierarquia do Gestor de Configuração.  

 ![Fluxo de Trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para Computadores Mac e Servidores Linux  

> [!Important]  
> Suporte para System Center Endpoint Protection (SCEP) para Mac e Linux (todas as versões) termina em 31 de dezembro de 2018. A disponibilidade de novas definições de vírus para SCEP para Mac e SCEP para Linux pode ser descontinuada após o fim do suporte. Para mais informações, consulte [End of support blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).  

 System Center Endpoint Protection inclui um cliente de Proteção de Ponto final para Linux e para computadores Mac. Estes clientes não são fornecidos com O Gestor de Configuração. Descarregue os seguintes produtos do [Microsoft Volume Licensing Service Center:](https://www.microsoft.com/licensing/servicecenter/default.aspx)  

-   Proteção de ponto final do centro do sistema para Mac  

-   Proteção de ponto final do centro do sistema para Linux  


> [!Note]  
>  Tem de ser um cliente de Licenciamento em Volume da Microsoft para transferir os ficheiros de instalação do Endpoint Protection para Linux e Mac.  

 Estes produtos não podem ser geridos a partir da consola Do Gestor de Configuração. Um pacote de gestão de gestão de Gestão de Operações do System Center é fornecido com os ficheiros de instalação, que lhe permite gerir o cliente para o Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Como obter o cliente endpoint Protection para computadores Mac e servidores Linux

Utilize os seguintes passos para descarregar o ficheiro de imagem que contém o software do cliente Endpoint Protection e documentação para computadores Mac e servidores Linux.
1. Inscreva-se no [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Selecione o separador **Downloads e Chaves** no topo do site.
3. Filtro na proteção do ponto final do centro do sistema do produto **(ramo atual)**.
4. Clique no link para **Descarregar**
5. Clique em **Continue** (Continuar). Deve ver vários ficheiros, incluindo um nomeado: **System Center Endpoint Protection (atual ramo - versão 1606) para Linux OS e Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. Para descarregar o ficheiro, clique no ícone da seta. O nome do ficheiro é **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050. ISO.**

A atualização de janeiro de 2018 (X21-67050) inclui as seguintes versões:

- Proteção do ponto final do Centro de Sistema para Mac 4.5.32.0 (suporte para macOS 10.13 High Sierra)
- Proteção de ponto final do Centro de Sistema para Linux 4.5.20.0 

  Para obter mais informações sobre como instalar e gerir os clientes Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos. Esta documentação do produto está na pasta **documentação** do . Ficheiro ISO.
