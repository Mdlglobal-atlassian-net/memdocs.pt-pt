---
title: Ajuda ao cliente de proteção endpoint
titleSuffix: Configuration Manager
description: Aprenda sobre funcionalidades e melhorias na Proteção de Pontofinal que melhor o ajudem a proteger o seu computador de ameaças.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724343"
---
# <a name="endpoint-protection-client-help"></a>Ajuda ao cliente de proteção endpoint

*Aplica-se a: Gestor de Configuração (ramo atual)*


Esta versão do Windows Defender ou Endpoint Protection inclui as seguintes funcionalidades para ajudar a proteger o seu computador de ameaças:  

-   **Integração do Windows Firewall.** A configuração do Endpoint Protection permite-lhe ativar ou desativar a Firewall do Windows.  
-   **Sistema de Inspeção de Rede.** Esta funcionalidade melhora a proteção em tempo real ao inspecionar o tráfego de rede para ajudar a bloquear de forma pró-ativa a exploração de vulnerabilidades conhecidas baseadas na rede.  
-   **Motor de proteção.** A proteção em tempo real encontra e impede que o malware instale ou execute no seu PC. O motor atualizado oferece deteção melhorada e capacidades de limpeza com melhor desempenho.  

O Windows Defender faz parte do sistema operativo Windows 10.  Em versões anteriores do Windows, o seu administrador pode fornecer o Windows Defender ou endpoint Protection utilizando software de gestão.

Também pode encontrar uma lista de [perguntas frequentes para o Windows Defender e endpoint Protection](endpoint-protection-client-faq.md). Para obter ajuda na resolução de problemas, consulte [o Windows Defender ou o cliente Endpoint Protection](troubleshoot-endpoint-client.md). Para obter uma lista de novas funcionalidades, consulte [o novo cliente do Windows Defender.](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender)

## <a name="windows-firewall-integration"></a>Integração da Firewall do Windows  
 A Firewall do Windows pode ajudar a evitar que atacantes ou software malicioso obtenham acesso ao seu computador através da Internet ou de uma rede. Agora, quando instalar o Endpoint Protection, o assistente de instalação verifica se a Firewall do Windows está ativada. Se desativou a Firewall do Windows intencionalmente, pode desmarcar uma caixa de verificação para evitar ativá-la. Pode alterar as definições da Firewall do Windows a qualquer altura através das definições de Sistema e Segurança no Painel de Controlo.  

## <a name="network-inspection-system"></a>Sistema de Inspeção de Rede  
 Cada vez mais os atacantes levam a cabo ataques baseados na rede contra vulnerabilidades expostas, antes que os fabricantes de software consigam desenvolver e distribuir atualizações de segurança. Os estudos de vulnerabilidades demonstram que pode demorar um mês ou mais desde o momento em que é criado um relatório de ataque inicial até que uma atualização de segurança adequada seja desenvolvida, testada e lançada. Esta falha na proteção deixa muitos computadores vulneráveis a ataques e a exploração durante um período de tempo substancial. O Sistema de Inspeção de Rede funciona com proteção em tempo real para o ajudar a proteger contra ataques baseados na rede, reduzindo significativamente o período de tempo entre as divulgações de vulnerabilidade e a implementação de atualizações de semanas para algumas horas.  

## <a name="award-winning-protection-engine"></a>Motor de proteção premiado  
 Sob a capa do Windows Defender ou Endpoint Protection está o seu premiado motor de proteção que é atualizado regularmente. O motor é suportado por uma equipa de investigadores de antimalware do Centro Microsoft de Proteção Contra Software Maligno, respondendo às mais recentes ameaças de software maligno 24 horas por dia.  

## <a name="windows-defender-settings"></a>Definições do Windows Defender
As definições do Windows Defender permitem configurações que ajudam a proteger o seu PC de software malicioso. O seu administrador poderá gerir algumas definições do Windows Defender para si. Pode gerir outros utilizando as definições do Windows Defender. Recomendamos que ative as definições do Windows Defender para ajudar a proteger o seu PC e os seus dados.

Para visualizar as definições do Windows Defender, procure `Windows Defender` no seu PC. Abra **o Windows Defender** e selecione **Definições**. As definições do Windows Defender incluem:
- **Proteção em tempo real** - Encontre e impeça que malware instale ou execute no seu PC.
- **Proteção baseada na Nuvem** - O Windows Defender envia informações à Microsoft sobre potenciais ameaças à segurança.
- **Submissão automática de amostras** - Permita que o Windows Defender envie amostras de ficheiros suspeitos para a Microsoft para ajudar a melhorar a deteção de malware.
- **Exclusões** - Pode exliro ficheiros, pastas, extensões de ficheiros ou processos específicos da digitalização do Windows Defender.
- **Notificação melhorada** - Permite notificações que informem sobre a saúde do seu PC. Mesmo **off** receberá notificações críticas.
- **Windows Defender Offline** - Pode executar o Windows Defender Offline para ajudar a encontrar e remover software malicioso. Esta digitalização reiniciará o seu PC e demorará cerca de 15 minutos.

### <a name="see-also"></a>Consulte também  
 [Cliente endpoint protection frequentemente fez perguntas](endpoint-protection-client-faq.md)   
 [Resolução de problemas Windows Defender ou cliente de Proteção de Pontofinal](troubleshoot-endpoint-client.md)
