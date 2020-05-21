---
title: Definições de política antivírus do Windows 10 para experiência de Segurança do Windows para Intune Microsoft Docs
description: Definições de política antivírus de segurança endpoint para a aplicação De segurança do Windows no Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431331"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Definições para o perfil de experiência de Segurança do Windows no Microsoft Intune

Ver as definições da política Antivírus que pode configurar para o perfil **Windows Security Experience** para windows 10 no Microsoft Intune como parte de uma política de segurança [endpoint](../protect/endpoint-security-policy.md).

**Segurança do Windows**

- **Ativar a proteção contra adulteração para evitar que o Microsoft Defender seja desativado**  
  [Evitar alterações nas definições de segurança com a Proteção contra adulteração](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Não configurado** *(predefinido*) - Quando o estado *de Ativação* ou *Desativação* existe num cliente, a implementação *Não configurada* não tem qualquer impacto na definição. 
  - **Ativar** - Ativar a restrição de proteção contra adulteração. Para alterar o estado de ativação ou desativado, implante a definição oposta para ter efeito.
  - **Desativar** - Desative as restrições de proteção contra adulteração. Para alterar o estado de ativação ou desativado, implante a definição oposta para ter efeito.

- **Ocultar a área de proteção contra vírus e ameaças na aplicação De segurança do Windows**  
  CSP: [Disablevirusui](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A área de proteção contra vírus e ameaças na aplicação Windows Security está escondida dos utilizadores finais. As notificações relacionadas com o vírus e a proteção contra ameaças são suprimidas.

  - **Ocultar a opção de recuperação de dados do Ransomware na aplicação De segurança do Windows**  
    CSP:[](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A área de recuperação de dados de ransomware na aplicação Windows Security está escondida dos utilizadores finais. As notificações relacionadas com ransomware são suprimidas.

- **Ocultar a área de proteção de conta na aplicação De segurança do Windows**  
  CSP: [Desativação AccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A área de proteção de conta na aplicação De segurança do Windows está escondida dos utilizadores finais. As notificações relacionadas com a proteção de contas são suprimidas.

- **Ocultar a firewall e a área de proteção de rede na aplicação De segurança do Windows**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A firewall e a área de proteção de rede no Windows Security estão escondidas dos utilizadores finais. As notificações relacionadas com a firewall e a proteção da rede são suprimidas.

- **Ocultar a app e a área de controlo do navegador na aplicação De segurança do Windows**  
  CSP: [DisableAppbrowserui](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A aplicação e a área de controlo de navegador no Windows Security estão escondidas dos utilizadores finais. As notificações relacionadas com o controlo de aplicações e navegadores são suprimidas.

- **Ocultar a área de segurança do Dispositivo na aplicação De segurança do Windows**  
  CSP: [Desativação SecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A área de proteção de hardware na aplicação Windows Security está escondida dos utilizadores finais. As notificações relacionadas com a proteção do hardware serão suprimidas.
  
- **Ocultar o desempenho do Dispositivo e a área de saúde na aplicação De segurança do Windows**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - O desempenho do dispositivo e a área de saúde na aplicação Windows Security estão escondidos dos utilizadores finais. Desempenho do dispositivo e produtos de notificações relacionados com a saúde suprimidos

- **Ocultar a área de opções familiares na aplicação De segurança do Windows**  
  CSP: [DisableFamilyui](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Não configurado** *(predefinido*) - A definição devolve-se ao predefinido do cliente, que é permitir o acesso e notificações do utilizador.
  - **Sim** - A área de opções familiares na aplicação Windows Security está escondida dos utilizadores finais. Além disso, as notificações relacionadas com opções familiares são suprimidas.

- **Notificações de aplicativos de Segurança do Windows**  
  CSP:[](https://go.microsoft.com/fwlink/?linkid=873675)

  Utilize esta definição para bloquear as notificações do Windows Security aos seus utilizadores para todas as definições de funcionalidades anteriores. Em alternativa, pode gerir as notificações da aplicação De segurança do Windows por funcionalidade, utilizando as definições de procedimento.

  - **Não configurado** *(predefinido*) - Todas as notificações da aplicação De Segurança do Windows que não sejam controladas por outra definição são permitidas.
  - **Bloquear notificação não crítica** - Notificações como a realização de exames estão bloqueadas.
  - **Bloqueie todas as notificações** - Notificações críticas e não críticas estão bloqueadas para todas as funcionalidades de Segurança do Windows.

- **Ocultar o ícone de Segurança do Windows da área de notificação**  
  CSP: [HidewindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  Para que esta definição tenha efeito, o utilizador precisa de assinar e voltar a entrar ou reiniciar o computador.
  - **Não configurado** *(predefinido*) - A definição devolve o cliente ao predefinido, que é mostrar o ícone.
  - **Sim** - Ocultar o ícone de Segurança do Windows da bandeja do sistema de utilizadores.
  
- **Desative a opção Clear TPM na aplicação Windows Security**  
  CSP: [DesactiveClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Não configurado** *(predefinido*) - A definição retorna ao predefinido do cliente, o que permite o acesso ao botão.
  - **Sim** - Desative o acesso ao botão TPM claro na aplicação De segurança do Windows.

- **Solicita aos utilizadores atualizarem firmware TPM se a vulnerabilidade for descoberta**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Não configurado** *(predefinido)*- A definição devolve-se ao predefinido do cliente, o que não é para não solicitar aos utilizadores.
  - **Sim** - Permita que o Windows provoque os utilizadores finais quando uma potencial vulnerabilidade for encontrada no seu firmware TPM. São então encorajados a executar atualizações de firmware para resolver a vulnerabilidade.

- **Informações de contacto de suporte da organização**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Declare onde deseja a informação da sua organização de TI exibida na aplicação e notificações do Windows Security.
  - **Não configurado** *(predefinido)*
  - **Exibição na app e em notificações**
  - **Exibir apenas na aplicação**
  - **Exibir apenas em notificações**