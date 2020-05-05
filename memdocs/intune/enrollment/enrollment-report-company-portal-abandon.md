---
title: Relatório de inscrições incompletas de utilizadores em Intune
titleSuffix: Microsoft Intune
description: Conheça o relatório de inscrições incompleto do utilizador.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d754076537fb8014b3e66a05413379637a67ba32
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077976"
---
# <a name="incomplete-user-enrollments-report"></a>Relatório de inscrições incompletas dos utilizadores

Este relatório diz-lhe onde no processo de inscrição do Portal da Empresa os utilizadores não estão a concluir o processo de inscrição.

Para ver o relatório, escolha**inscrição** >  **intune** > Dispositivo**Incomplete user registrations**.

Utilizando estas informações, pode atualizar os seus documentos de embarque para ajudar os utilizadores a completar a inscrição. Por exemplo, se existirem muitos utilizadores a desistir nos Termos de Utilização, pode investigar essa área e torná-la mais intuitiva para os utilizadores.

## <a name="what-is-an-incomplete-enrollment"></a>O que é uma inscrição incompleta?

Uma inscrição incompleta é quando um utilizador faz qualquer um dos seguintes:

- Seleciona explicitamente uma ação para parar a inscrição
- Fecha o Portal da Empresa durante a inscrição
- Demora mais de 30 minutos entre as secções da inscrição

Se um utilizador optar por parar de matricular-se e reiniciar várias vezes, aparece como múltiplas tentativas e múltiplas matrículas incompletas. Se um utilizador esperar 30 minutos entre diferentes ecrãs de inscrição, é considerado múltiplas matrículas incompletas.

## <a name="what-does-the-report-show"></a>O que mostra o relatório?

Os relatórios incluem dados para dispositivos iOS/iPadOS e Android.

Os relatórios mostram os dados correspondentes às últimas duas semanas, mas pode filtrar o relatório para apresentar qualquer período até 30 dias anteriores.

Pode filtrar o intervalo de datas, o sistema operativo e a secção de inscrição através da opção **Filtro**.

### <a name="number-and-percentage-tiles"></a>Mosaicos de número e percentagem

No topo do relatório, pode ver o número e a percentagem de matrículas incompletas em relação a todas as matrículas.

- Inscrições iniciadas: o número de tentativas de inscrição.
- Inscrições incompletas: O número de tentativas de matrículas que não resultaram num dispositivo totalmente matriculado e compatível.
- Taxa incompleta: A percentagem de tentativas de inscrição que foram abandonadas (Matrículas abandonadas/ Inscrições iniciadas).

### <a name="line-graph"></a>Gráfico de linha

O gráfico de linha mostra as inscrições diárias incompletas para cada uma das quatro secções de inscrição principais:

- Lista de verificação da configuração
- Ecrãs de plataforma
- Termos de utilização
- Conformidade/Ativação

### <a name="user-abandonment-actions"></a>Ações de abandono do utilizador

As tabelas seguintes mostram a lista de ações dos utilizadores que se qualificam como solicitando uma inscrição incompleta. Para ver exemplos de ecrãs de inscrição, pode ver os vídeos de inscrição do [iOS](https://channel9.msdn.com/Series/IntuneEnrollment/iOS-Enrollment) e [Android](https://channel9.msdn.com/Series/IntuneEnrollment/Android-Enrollment). 


#### <a name="setup-checklist-section"></a>Secção da lista de verificação da configuração

| Nome de ação | Ecrã ou fluxo | Plataforma | Ação |
| ---- |---- |---- |---- |
| EnrollmentWrapUp | Pedido para abrir uma página no Portal da Empresa | iOS/Android | **Cancelar** |
| EnrollmentWrapUp | Ecrã de inscrição do dispositivo até à conclusão da operação **A carregar recursos da empresa** | iOS/Android | Demorou mais de 30 minutos |
| DeviceCategory | Seleção da Categoria do Dispositivo (se configurado pelo administrador) até clicar em **Concluído** | iOS/Android | Demorou mais de 30 minutos |
| PreEnrollmentWizard | Ecrã de configuração do acesso quando inicia a inscrição, mas voltou à secção Configurar acesso | iOS/Android| **Adiar** |
| PreEnrollmentWizard | Configurar o ecrã de acesso até clicar em **Seguida** no **ecrã What's Next** | iOS/Android | Demorou mais de 30 minutos |

#### <a name="platform-screens-section"></a>Secção dos ecrãs de plataforma

| Nome de ação | Ecrã ou fluxo | Plataforma | Ação |
| ---- |---- |---- |---- |
| iOSProfileLaunch | Pedido para mostrar um perfil de configuração | iOS/iPadOS | **Ignorar** |
| iOSProfileLaunch | Ecrã de instalação do perfil | iOS/iPadOS | **Cancelar** |
| iOSProfileLaunch | Solicita-me que confie na fonte do perfil para inscrever o dispositivo | iOS/iPadOS | **Cancelar** |
| iOSProfileLaunch | Ecrã de instalação do perfil até à instalação com êxito do perfil | iOS/iPadOS | Demorou mais de 30 minutos |
| AndroidPermissions | Ecrã de ativação do administrador do dispositivo | Android | **Cancelar** |
| AndroidPermissions | Desde o pedido de aprovação para efetuar e gerir chamadas telefónicas até o administrador do dispositivo selecionar **Ativar** | Android | Demorou mais de 30 minutos |
| KnoxActivation | Ativação do agente KLMS (apenas Samsung) | Android| **Cancelar** |
| KnoxActivation | Ativação do agente KLMS até **Confirmar** | Android | Demorou mais de 30 minutos|

#### <a name="terms-of-use-section"></a>Secção dos termos de utilização

| Nome de ação | Ecrã ou fluxo | Plataforma | Ação |
| ---- |---- |---- |---- |
| TermsofUse | Termos de utilização (se configurado pelo administrador) | iOS/Android | **Recusar Tudo** |
| TermsofUse | Termos de utilização até **Aceitar tudo** | iOS/Android | Demorou mais de 30 minutos |

#### <a name="complianceactivation-section"></a>Secção de Conformidade/Ativação

| Nome de ação | Ecrã ou fluxo | Plataforma | Ação |
| ---- |---- |---- |---- |
| Conformidade | A conformidade do dispositivo (se configurado pelo administrador) é apresentada como não verde na fase de pós-inscrição da configuração do acesso| iOS/Android | **Adiar** |
| Conformidade | A conformidade do dispositivo é apresentada como não verde até ser atualizada e ficar a verde | iOS/Android | Demorou mais de 30 minutos |
| Ativação | A ativação da inscrição (se configurado pelo administrador) é apresentada como não verde na configuração do acesso | iOS/Android | **Adiar** |
| Conformidade | A ativação do dispositivo é apresentada como não verde até ser atualizada e ficar a verde | iOS/Android | Demorou mais de 30 minutos |

## <a name="next-steps"></a>Passos seguintes

Depois de verificar as suas taxas de inscrição incompletas, pode rever as opções de [inscrição](enrollment-options.md) para ver se pode fazer alterações para melhorar a inscrição.
