---
title: Proteja os computadores contra malware
titleSuffix: Configuration Manager
description: Aprenda a implementar a Proteção de Pontofinal no Gestor de Configuração para proteger os computadores de ataques de malware.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722390"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Cenário de exemplo: Use endpoint protection para proteger computadores de malware

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece um cenário de exemplo para como pode implementar endpoint Protection in Configuration Manager para proteger computadores na sua organização contra ataques de malware.  



## <a name="scenario-overview"></a>Descrição geral do cenário

 O Gestor de Configuração é instalado e utilizado no Woodgrove Bank. Atualmente, o banco utiliza o System Center Endpoint Protection para proteger os computadores contra ataques de malware. Além disso, o banco utiliza a Política de Grupo do Windows para assegurar que a Firewall do Windows está ativada em todos os computadores da empresa e que os utilizadores são notificados quando esta bloqueia um programa novo.  

Foi pedido aos administradores do Gestor de Configuração que atualizassem o software antimalware do Woodgrove Bank para system Center Endpoint Protection para que o banco possa beneficiar das mais recentes funcionalidades antimalware e ser capaz de gerir centralmente a solução antimalware a partir da consola Do Gestor de Configuração. 


## <a name="business-requirements"></a>Requisitos empresariais

Esta implementação tem os seguintes requisitos:  

- Utilize o Gestor de Configuração para gerir as definições do Windows Firewall que são atualmente geridas pela Política do Grupo.  

- Utilize atualizações de software do Gestor de Configuração para descarregar definições de malware para computadores. Se as atualizações de software não estiverem disponíveis, por exemplo, se o computador não estiver ligado à rede corporativa, os computadores devem descarregar atualizações de definição a partir do Microsoft Update.  

- Os computadores dos utilizadores devem realizar uma rápida varredura de malware todos os dias. No entanto, os servidores têm de efetuar uma análise completa todos os sábados, fora do horário comercial, à 1:00.  

- Enviar um alerta por e-mail sempre que ocorrer qualquer um dos seguintes eventos:  

  -   É detetado software maligno num computador  

  -   A mesma ameaça de software maligno é detetada em mais de cinco por cento dos computadores  

  -   A mesma ameaça de malware é detetada mais de 5 vezes em qualquer período de 24 horas  

  -   Mais de 3 tipos diferentes de malware são detetados em qualquer período de 24 horas  

  Os administradores então fazem os seguintes passos para implementar a Proteção do Ponto Final:  



##  <a name="steps-to-implement-endpoint-protection"></a> Passos para implementar o Endpoint Protection  

|Processo|Referência|  
|-------------|---------------|  
|Os administradores revêem as informações disponíveis sobre os conceitos básicos de Proteção de Pontofinal em Gestor de Configuração.|Para obter informações sobre a Proteção do Ponto Final, consulte a [Proteção](endpoint-protection.md)do Ponto Final .|  
|Os administradores revêem e implementam os pré-requisitos necessários para utilizar a Proteção do Ponto Final.|Para obter informações sobre os pré-requisitos para a proteção do ponto final, consulte planeamento para proteção de [pontos finais](../plan-design/planning-for-endpoint-protection.md).|  
|Os administradores instalam a função do sistema de proteção de pontos finais apenas num servidor de sistema de site, no topo da hierarquia do Woodgrove Bank.|Para obter mais informações sobre como instalar a função do sistema de proteção de pontos finais, consulte "Pré-requisitos" na Configuração de [Proteção de Pontofinal](endpoint-protection-configure.md).|  
|Os administradores configuram o Gestor de Configuração para utilizar um servidor SMTP para enviar os alertas de e-mail.<br /><br /> **Nota:** Só deve configurar um servidor SMTP se pretender ser notificado por e-mail quando for gerado um alerta de Proteção de Pontofinal.|Para mais informações, consulte [os alertas de Configuração na Proteção](endpoint-configure-alerts.md)do Ponto Final .|  
|Os administradores criam uma coleção de dispositivos que contém todos os computadores e servidores para instalar o cliente endpoint Protection. Eles nomeiam esta coleção **Todos os Computadores Protegidos pela Proteção**do Ponto Final .<br /><br /> **Dica:** Não é possível configurar alertas para as coleções dos utilizadores.|Para mais informações sobre como criar coleções, consulte [Como criar coleções](../../core/clients/manage/collections/create-collections.md)|  
|Os administradores configuram os seguintes alertas para a recolha: <br /><br />1) **É detetado malware**: Os administradores configuram uma gravidade de alerta de **Critical**. <br /><br />2) **O mesmo tipo de malware é detetado em vários computadores**: Os administradores configuram uma gravidade de alerta da **Critical** e especificam que o alerta será gerado quando mais de 5% dos computadores tiverem malware detetado. <br /><br />3) **O mesmo tipo de malware é repetidamente detetado dentro do intervalo especificado num computador**: Os administradores configuram uma gravidade de alerta da Critical e especificam que o alerta será gerado quando o malware for detetado mais de 5 vezes num período de 24 horas. <br /><br />4) **Vários tipos de malware são detetados no mesmo computador dentro do intervalo especificado**: Os administradores configuram uma gravidade de alerta da Critical e especificam que o alerta será gerado quando mais de 3 tipos de malware forem gerados num período de 24 horas.<br /><br /> O valor da **Severidade do Alerta** indica o nível de alerta que será exibido na consola do Gestor de Configuração e em alertas que recebem numa mensagem de correio eletrónico.<br /><br /> Eles também selecionam a opção Ver esta coleção no painel de **proteção endpoint** para que possam monitorizar os alertas na consola Do Gestor de Configuração.|Consulte "Configurar alertas para proteção de pontos finais" na configuração da [proteção do ponto final](endpoint-configure-alerts.md).|  
|Os administradores configuram atualizações de software do ConfigurManager para descarregar e implementar atualizações de definição três vezes por dia, utilizando uma regra de implementação automática.|Para mais informações, consulte a secção "Utilizar atualizações de software do Gestor de Configuração para entregar atualizações de definição" nas atualizações do software do Gestor de [Configuração de Utilização para fornecer atualizações](endpoint-definitions-configmgr.md)de definição .|  
|Os administradores examinam as definições na política antimalware predefinida, que contém definições de segurança recomendadas da Microsoft. Para que os computadores realizem uma sondagem rápida todos os dias, alteram as seguintes definições:<br /><br /> 1) **Ecorra uma varredura rápida diária nos computadores dos clientes**: **Sim**.<br /><br /> 2) Horário diário de **digitalização rápida:** **9:00 AM**.<br /><br /> Os administradores notam que **as Atualizações distribuídas a partir do Microsoft Update** são selecionadas por padrão como fonte de atualização de definição. Isto cumpre o requisito de negócio que os computadores descarregam definições a partir do Microsoft Update quando não podem receber atualizações de software do Gestor de Configuração.|Ver [Como criar e implementar políticas antimalware para proteção de pontos finais](endpoint-antimalware-policies.md).|  
|Os administradores criam uma coleção que contém apenas os servidores do Woodgrove **Bank chamados Woodgrove Bank Servers**.|Ver [Como criar coleções](../../core/clients/manage/collections/create-collections.md)|  
|Os administradores criam uma política antimalware personalizada chamada **Woodgrove Bank Server Policy**. Adicionam apenas as definições para **digitalizações agendadas** e fazem as seguintes alterações:<br /><br /> **Tipo de análise**:  **Completa**<br /><br /> **Dia da análise**:  **Sábado**<br /><br /> **Hora da análise**: **1:00**<br /><br /> **Executar uma análise rápida diária nos computadores cliente**:  **Não**.|Ver [Como criar e implementar políticas antimalware para proteção de pontos finais](endpoint-antimalware-policies.md).|  
|Os administradores implementam a política antimalware personalizada da **Woodgrove Bank Server Policy** para a coleção **woodgrove Bank Servers.**|Consulte "Implementar uma política antimalware nos computadores dos clientes" Como criar e implementar políticas antimalware para artigo de [Proteção de Pontofinal.](endpoint-antimalware-policies.md)|  
|Os administradores criam um novo conjunto de configurações personalizadas de dispositivos de cliente para proteção de pontos finais e nomeia estas Definições de **Proteção de Endpoint Woodgrove Bank**.<br /><br /> **Nota:** Se não quiser instalar e ativar a Endpoint Protection em todos os clientes da sua hierarquia, certifique-se de que as opções De Gerir o **cliente de Proteção Endpoint nos computadores dos clientes** e instalar o cliente **Endpoint Protection nos computadores dos clientes** são configuradas como **Não** nas definições padrão do cliente.|Para mais informações, consulte [configurar as definições personalizadas do cliente para proteção de pontos finais](endpoint-protection-configure-client.md).|  
|Configuram as seguintes definições para a Proteção do Ponto Final:<br /><br /> **Gerir o cliente do Endpoint Protection nos computadores cliente**:  **Sim**<br /><br /> Esta definição e valor garante mato que qualquer cliente de Proteção endpoint existente que esteja instalado se torne gerido pelo Gestor de Configuração.<br /><br /> **Instalar o cliente do Endpoint Protection nos computadores cliente**:  **Sim**.</br></br>**Nota** A partir do 'Gestor de Configuração' 1802, os dispositivos do Windows 10 não precisam de ter o agente de proteção de ponto final instalado. Se já estiver instalado nos dispositivos do Windows 10, o Gestor de Configuração não o removerá. Os administradores podem remover o agente de proteção de ponto final nos dispositivos do Windows 10 que estão a executar pelo menos a versão cliente de 1802.|Para mais informações, consulte [configurar as definições personalizadas do cliente para proteção de pontos finais](endpoint-protection-configure-client.md).|  
|Os administradores implementam as definições de cliente de Definições de Proteção de **Endpoint woodgrove Bank** para a coleção de proteção de **pontos finais de todos os computadores protegidos por endpoint.**|Consulte "Configure as definições personalizadas do cliente para proteção de pontofinal" na configuração da proteção do ponto final no Gestor de [Configuração](endpoint-antimalware-policies.md).|  
|Os administradores utilizam o Assistente de Política de Firewall do Windows para criar uma política configurando as seguintes definições para o perfil de domínio:<br /><br /> 1) **Ativar firewall do Windows**: **Sim**<br /><br /> 2)<br />                    **Notificar o utilizador quando a Firewall do Windows bloquear um programa novo**: **Sim**|Ver [como criar e implementar políticas de Firewall do Windows para proteção de pontos finais](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Os administradores implementam a nova política de firewall para a coleção **All Computers Protected by Endpoint Protection** que criaram anteriormente.|Consulte "Para implementar uma política de Firewall do Windows" na forma de [criar e implementar políticas de Firewall do Windows para proteção de pontos finais](create-windows-firewall-policies.md)|  
|Os administradores utilizam as tarefas de gestão disponíveis para a Endpoint Protection para gerir as políticas antimalware e Windows Firewall, realizar pesquisas a pedido de computadores quando necessário, forçar os computadores a descarregar as definições mais recentes e especificar quaisquer outras ações a tomar quando o malware é detetado.|Ver [como gerir políticas antimalware e configurações de firewall para proteção de pontofinal](endpoint-antimalware-firewall.md)|  
|Os administradores utilizam os seguintes métodos para monitorizar o estado da proteção do ponto final e as ações tomadas pela Proteção do Ponto Final:<br /><br /> 1) Utilizando o nó de **proteção** do ponto final sob **segurança** no espaço de trabalho **de monitorização.**<br /><br /> 2) Utilizando o nó de **proteção** do ponto final no espaço de trabalho **Ativos e Compliance.**<br /><br /> 3) Utilizando os relatórios do Gestor de Configuração incorporados.|Ver [Como monitorizar a Proteção de Pontos Finais](monitor-endpoint-protection.md)|  

 Os administradores reportam uma implementação bem sucedida da Endpoint Protection ao seu gestor, e confirmam que os computadores do Woodgrove Bank estão agora protegidos contra antimalware, de acordo com os requisitos de negócio que lhes foram dados. 

## <a name="next-steps"></a>Passos seguintes

Para mais informações, consulte [Como Configurar a Proteção de Pontofinal](endpoint-protection-configure.md)