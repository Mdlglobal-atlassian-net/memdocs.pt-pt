---
title: Plano do Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 720b5060c913ff3157624c4b6060802af396d221
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722173"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Planeamento para Proteção de Pontofinal em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


Endpoint Protection in Configuration Manager permite-lhe gerir políticas antimalware e segurança do Windows Firewall para computadores clientes na sua hierarquia de Gestor de Configuração.  

> [!IMPORTANT]  
>  Tem de ser licenciado para utilizar a Endpoint Protection para gerir os clientes na sua hierarquia do Gestor de Configuração.  

Quando utilizar a Proteção de Pontofinal com o Gestor de Configuração, tem os seguintes benefícios:  

-   Configure políticas antimalware, definições do Windows Firewall e gerencie a Proteção avançada de ameaças do Microsoft Defender para grupos selecionados de computadores  

-   Utilize as atualizações de software do Gestor de Configuração para descarregar os mais recentes ficheiros de definição antimalware para manter os computadores dos clientes atualizados  

-   Enviar notificações por e-mail, utilizar a monitorização na consola e ver relatórios para manter os utilizadores administrativos informados quando for detetado software maligno em computadores cliente  

Os computadores Windows 10 não requerem nenhum cliente adicional para a gestão da proteção de pontos finais. Nos computadores Windows 8.1 e anteriores, a Endpoint Protection instala o seu próprio cliente para além do cliente do Gestor de Configuração. O cliente do Endpoint Protection tem as seguintes capacidades:  

-   Deteção e remediação de software maligno e spyware  

-   Deteção e remediação de rootkit  

-   Avaliação de vulnerabilidades críticas e atualizações automáticas de definições e de motor  

-   Deteção de vulnerabilidades de rede através do Sistema de Inspeção de Rede  

-   Integração com o Serviço de Proteção de Nuvem para reportar malware à Microsoft. Quando se junta a este serviço, o Windows Defender ou o cliente Endpoint Protection podem descarregar as definições mais recentes do Centro de Proteção contra Malware quando for detetado malware não identificado num computador.  

> [!NOTE]  
>  O cliente Endpoint Protection pode ser instalado num servidor que executa hiper-V e em máquinas virtuais de hóspedes com sistemas operativos suportados. Para evitar o uso excessivo da CPU, as ações de proteção do ponto final têm um atraso incorporado e aleatório para que os serviços não sejam executados simultaneamente.  

  Além disso, a Proteção de Pontofinal no Gestor de Configuração permite-lhe gerir as definições do Windows Firewall na consola 'Gestor de Configuração'.  

 [Cenário de exemplo: A utilização da Proteção do Ponto Final](../deploy-use/scenarios-endpoint-protection.md) do System Center para proteger os computadores de malware mostra como pode configurar e gerir a Proteção de Pontos Finais e o Firewall do Windows.  

## <a name="managing-malware-with-endpoint-protection"></a>Gerir o Software Maligno com o Endpoint Protection  

Endpoint Protection in Configuration Manager permite-lhe criar políticas antimalware que contenham configurações para configurações de clientes de proteção de pontofinal. Em seguida, pode implementar estas políticas antimalware para computadores clientes e monitorá-las no nó de Status de **Proteção de Ponto Final** no espaço de trabalho **de Monitorização,** ou utilizando relatórios do Gestor de Configuração.  

 Informações adicionais:  

-   [Crie e implemente políticas antimalware para proteção de pontos finais](../deploy-use/endpoint-antimalware-policies.md) - Crie, implemente e monitorize as políticas antimalware com uma lista das definições que pode configurar  

-   [Monitor Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) - Relatórios de atividadede monitorização, computadores de clientes infetados e muito mais.   

-   [Gerir políticas antimalware e configurações](../deploy-use/endpoint-antimalware-firewall.md) de firewall para proteção de pontofinal - Pode alterar prioridade de política para [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) ou [firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [remediar malware encontrado em computadores de clientes](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware), e outras tarefas

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gerir a Firewall do Windows com o Endpoint Protection  
 Endpoint Protection in Configuration Manager fornece uma gestão básica do Firewall do Windows nos computadores dos clientes. Para cada perfil de rede, pode configurar as seguintes definições:  

-   Ativar ou desativar a Firewall do Windows.  

-   Bloquear as ligações recebidas, incluindo as que se encontram na lista de programas permitidos.  

-   Notificar o utilizador quando a Firewall do Windows bloquear um programa novo.  

> [!NOTE]  
>  O Endpoint Protection suporta apenas a gestão da Firewall do Windows.  

  Para obter mais informações sobre como criar e implementar políticas de Firewall do Windows para proteção de pontos finais, consulte [como criar e implementar políticas de Firewall do Windows para proteção de pontos finais](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Proteção Avançada Contra Ameaças do Microsoft Defender

Começando com a versão 1606 do Gestor de Configuração (atual ramo), a Endpoint Protection pode ajudar a gerir e monitorizar a Proteção avançada de ameaças (ATP) do Microsoft Defender, anteriormente conhecida como WINDOWS Defender ATP. O Microsoft Defender ATP é um serviço que ajudará as empresas a detetar, investigar e responder a ataques avançados nas suas redes. Ver [Microsoft Defender Advanced Threat Protection](../deploy-use/windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Fluxo de Trabalho do Endpoint Protection  
 Utilize o seguinte diagrama para o ajudar a compreender o fluxo de trabalho para implementar a Proteção de Pontofinal na hierarquia do Gestor de Configuração.  

 ![Fluxo de Trabalho do Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente do Endpoint Protection para Computadores Mac e Servidores Linux  
 O System Center inclui um cliente de Proteção de Ponto Final para Linux e para computadores Mac. Estes clientes não são fornecidos com O Gestor de Configuração; em vez disso, deve descarregar os seguintes produtos do [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Tem de ser um cliente de Licenciamento em Volume da Microsoft para transferir os ficheiros de instalação do Endpoint Protection para Linux e Mac.  

 Estes produtos não podem ser geridos a partir da consola do Configuration Manager. No entanto, um pacote de gestão do System Center Operations Manager é fornecido com os ficheiros de instalação, permitindo gerir o cliente para Linux ao utilizar o Operations Manager.  

 Para mais informações sobre como instalar e gerir os clientes do Endpoint Protection para computadores Linux e Mac, utilize a documentação que acompanha estes produtos, que está localizada na pasta **Documentação** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Exemplos de Melhores Práticas para o Endpoint Protection no Configuration Manager  
 Utilize as seguintes melhores práticas no Endpoint Protection do System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições personalizadas de cliente para o Endpoint Protection  
 Quando configurar as definições do cliente para a Proteção de Pontofinal, não utilize as definições padrão do cliente porque aplicam definições a todos os computadores da sua hierarquia. Em vez disso, configure definições de cliente personalizadas e atribua estas definições a coleções de computadores na sua hierarquia.  

 Ao configurar definições de cliente personalizadas, pode:  

-   Personalizar as definições de antimalware e de segurança para diferentes partes da organização.  
-   Teste os efeitos da execução da Proteção do Ponto Final num pequeno grupo de computadores antes de o implantar em toda a hierarquia.  
-   Adicione mais clientes à coleção ao longo do tempo para fasear a sua implementação do cliente Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuir atualizações de definições ao utilizar atualizações de software  
 Se estiver a utilizar atualizações de software do Gestor de Configuração para distribuir atualizações de definição, considere colocar atualizações de definição num pacote que não contenha outras atualizações de software. Esta opção mantém o tamanho do pacote de atualizações de definições mais pequeno, permitindo-lhe replicar para pontos de distribuição mais rapidamente.
