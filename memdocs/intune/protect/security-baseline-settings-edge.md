---
title: Definições de base de segurança insinadas para Microsoft Edge
titleSuffix: Microsoft Intune
description: Definições de base de segurança suportadas pela Intune para gerir o navegador Microsoft Edge
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 861d7f526711f2169e8fd03b3df09659440523b9
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693448"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Definições de linha de base do Microsoft Edge para Intune

Ver as definições de linha de base do navegador Web do Microsoft Edge que são suportadas pelo Microsoft Intune. Os predefinições de base do Microsoft Edge representam a configuração recomendada para os navegadores Microsoft Edge, e podem não corresponder aos predefinidos de base para outras linhas de segurança.

::: zone pivot="edge-october-2019"

> [!NOTE]
> A linha de base do Microsoft Edge para outubro de 2019 está em Pré-visualização Pública.

::: zone-end
::: zone pivot="edge-april-2020"

*Esta nova linha de base vai ser lançada para os inquilinos nas próximas semanas. Esperamos que todos os inquilinos tenham esta nova linha de base no início de maio.*
Para entender o que mudou com esta versão da linha de base de versões anteriores, use a ação [compare baselines](../protect/security-baselines.md#compare-baseline-versions) que está disponível ao visualizar o painel *veras versões* para esta linha de base. Para entender o que mudou com esta versão da linha de base de versões anteriores, use a ação [compare baselines](../protect/security-baselines.md#compare-baseline-versions) que está disponível ao visualizar o painel *veras versões* para esta linha de base.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Regimes de autenticação suportados**  
  Especifica quais os regimes de autenticação HTTP suportados. Pode configurar a política utilizando estes valores: *básico,* *digestivo,* *ntlm,* e *negociar.* Separe vários valores com vírgulas. Se não configurar esta política, todos os quatro esquemas são usados.

  - **Os** esquemas que selecionar são utilizados.*default*
  - **Desativado**
  - **Não configurado** - Todos os quatro esquemas são usados.
  
  Quando programado para *ativar,* pode configurar a seguinte definição onde seleciona qual a autenticação a utilizar:

  - **Regimes de autenticação suportados**  
    Selecione entre as seguintes opções:
    - **Básico**
    - **Digerir**
    - **NTLM** *(Selecionado por padrão)*
    - **Negociar** *(Selecionado por defeito)*

- **Definição padrão de Flash Adobe**  
  CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash), e [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Ative o acesso à seguinte definição onde pode configurar o comportamento para executar o plug-in Adobe Flash.  

  - **Ativado** *(predefinido)*
  - **Desativado**
  - **Não configurado**

  Quando definido para *ativado,* pode configurar a seguinte definição.

  - **Definição padrão de Flash Adobe**

    - **Bloqueie o plugin Adobe Flash** *(predefinido*) - Bloco Adobe Flash em todos os sites
    - **Clique para reproduzir** - O Adobe Flash corre, mas o utilizador deve selecionar a opção para iniciá-lo.

- **Controlo quais extensões não podem ser instaladas**  
  Ativar a utilização de uma lista que especifica extensões que os utilizadores não podem instalar no Microsoft Edge. Quando a lista está em uso, quaisquer definições na lista que foram previamente instaladas são desativadas e o utilizador não pode ativar. Se remover um item da lista de extensões bloqueadas, essa extensão é automaticamente reativada em qualquer lugar onde foi previamente instalada.

  - **Ativado** *(predefinido*) - Ativar a utilização da lista para bloquear extensões.
  - **Desativado**
  - **Não configurado** - Os utilizadores podem instalar qualquer extensão no Microsoft Edge.
  
  Quando definido para *Ativado,* pode configurar a seguinte definição que define a lista de extensões para bloquear.

  - **IDs de extensão o utilizador deve ser impedido de instalar (ou * para todos)**

    Selecione **Adicionar** e especificar extensões adicionais. **\*** é selecionado por defeito.

- **Permitir anfitriões de mensagens nativas ao nível do utilizador (instalados sem permissões de administração)**  
  Permite a instalação ao nível do utilizador de anfitriões de mensagens nativas.

  - **Ativado**
  - **Desativado** *(predefinido*) - o Microsoft Edge utiliza apenas anfitriões de mensagens nativas instalados a nível do sistema.
  - **Não configurado** - Por padrão, o Microsoft Edge permite a utilização de anfitriões de mensagens nativas ao nível do utilizador.

- **Ativar palavras-passe para guardar palavras-passe para o gestor de passwords**  
  Microsoft Edge CSP: [Browser/AllowpasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Ative o Microsoft Edge para guardar as palavras-passe dos utilizadores.

  - **Ativado** - Os utilizadores podem guardar as suas palavras-passe no Microsoft Edge. Da próxima vez que visitarem o site, o Microsoft Edge introduzirá automaticamente a palavra-passe. Os utilizadores não podem alterar ou anular esta política no Microsoft Edge.
  - **Desativado** *(predefinido)*- Os utilizadores não podem guardar novas palavras-passe, mas podem continuar a utilizar senhas previamente guardadas. Os utilizadores não podem alterar ou anular esta política no Microsoft Edge.
  - **Não configurado** - Os utilizadores podem guardar palavras-passe e desligar esta funcionalidade.

- **Evite contornar as solicitações do Microsoft Defender SmartScreen para sites**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Decida se os utilizadores podem anular os avisos do Microsoft Defender SmartScreen sobre sites potencialmente maliciosos.

  - **Ativado** *(predefinido*) - Os utilizadores não podem ignorar os avisos do Microsoft Defender SmartScreen e estão impedidos de continuar no site.
  - **Desativado** - Os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e continuar no site.
  - **Não configurado** Os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e continuar no site

- **Evitar contornar os avisos do Microsoft Defender SmartScreen sobre downloads**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Determine se os utilizadores podem substituir os avisos do Microsoft Defender SmartScreen sobre transferências não verificadas.

  - **Ativado** *(predefinido*) - Os utilizadores não podem ignorar os avisos do Microsoft Defender SmartScreen e estão impedidos de concluir os downloads não verificados.
  - **Desativado** - Os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e completar downloads não verificados.
  - **Não configurado** - Os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e completar downloads não verificados.

- **Ativar o isolamento do site para cada site**  
  Configure o isolamento do site para evitar que os utilizadores optem pelo comportamento padrão de isolar todos os sites.
  
  - **Ativado** *(predefinido)*- Os utilizadores não podem optar pelo comportamento predefinido onde cada site funciona no seu próprio processo.
  - **Desativado** - Os utilizadores podem optar por não se isentar em isolamento do local. O isolamento do local não está desligado.
  - **Não configurado** - Os utilizadores podem optar por não o isolamento do local. O isolamento do local não está desligado.

  O Microsoft Edge também suporta a política [IsolateOrigins](https://docs.microsoft.com/deployedge/microsoft-edge-policies#isolateorigins) que pode isolar origens adicionais e mais finas.  Intune não suporta configurar a política IsolateOrigins.
  
- **Configure Microsoft Defender SmartScreen**  
  CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  O Microsoft Defender SmartScreen fornece mensagens de aviso para ajudar a proteger os utilizadores de potenciais esquemas de phishing e software malicioso. Por predefinição, o Microsoft Defender SmartScreen está ligado.
  
  - **Ativado** *(predefinido*) - O Microsoft Defender SmartScreen está ligado e os utilizadores não podem desligá-lo.
  - **Desativado** - O Microsoft Defender SmartScreen está desligado e os utilizadores não podem ligá-lo.
  - **Não configurado**  Os utilizadores podem escolher se utilizam o Microsoft Defender SmartScreen.

  Esta política está disponível apenas em casos do Windows que se juntam a um domínio do Microsoft Ative Diretor, ou em casos do Windows 10 Pro ou Da Enterprise que estão inscritos para a gestão do dispositivo.

- **Configure o Microsoft Defender SmartScreen para bloquear aplicações potencialmente indesejadas**  
    Configure o comportamento do Microsoft Defender SmartScreen para bloquear aplicações potencialmente indesejadas. O Microsoft Defender SmartScreen pode fornecer uma mensagem de aviso para ajudar a proteger os utilizadores de adware, mineiros de moedas, pacoteware e outras aplicações de baixa reputação que são hospedadas por websites. O bloqueio de aplicações potencialmente indesejado no Microsoft Defender SmartScreen é desligado por padrão.

  - **Ativadas** *(predefinido*) - As aplicações potencialmente indesejadas estão bloqueadas.
  - **Desativado** - As aplicações potencialmente indesejadas não estão bloqueadas.
  - **Não configurado** - Os utilizadores podem escolher se utilizam um bloqueio de aplicações potencialmente indesejado no Microsoft Defender SmartScreen.

  Esta política está disponível apenas em casos do Windows que se juntam a um domínio do Microsoft Ative Diretor, ou em casos do Windows 10 Pro ou Da Enterprise que estão inscritos para a gestão do dispositivo.

- **Permitir que os utilizadores procedam da página de aviso SSL**  
   CSP: [Navegador/Prevenção DeErrooverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  O Microsoft Edge mostra uma página de aviso quando os utilizadores visitam sites com erros SSL.
  - **Ativado** - Os utilizadores podem clicar nas páginas de aviso.
  - **Desativado** *(predefinido*) - Os utilizadores estão impedidos de clicar em qualquer página de aviso.
  - **Não configurado** - Os utilizadores podem clicar nestas páginas de aviso.

- **Versão SSL mínima ativada**  
  Ative a opção de definir uma versão mínima suportada do SSL.

  - **Ativado** *(predefinido*) - Ative o acesso à próxima definição onde especifica a versão mínima do TLS a utilizar.
  - **Desativado**
  - **Não configurado** - O Microsoft Edge utiliza uma versão mínima predefinida de *TLS 1.0*.

  Quando definido para *ativado,* pode configurar o TLS utilizando a seguinte definição.

  - **Versão SSL mínima ativada** Desloque a versão mínima do TLS a utilizar. O Microsoft Edge não utilizará nenhuma versão do SSL/TLS inferior à versão especificada.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** *(padrão)*

::: zone-end

::: zone pivot="edge-october-2019"

- **Evite contornar as solicitações do Microsoft Defender SmartScreen para sites**  
  **Predefinição**: Ativado  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Esta definição de política permite-lhe decidir se os utilizadores podem anular os avisos do Microsoft Defender SmartScreen sobre websites potencialmente maliciosos. 
  - Se ativar esta definição, os utilizadores não podem ignorar os avisos do Microsoft Defender SmartScreen e estão impedidos de continuar no site. 
  - Se desativar ou não configurar esta definição, os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e continuar no site.

- **Versão SSL mínima ativada**  
  **Predefinição**: Ativado  

  Detete uma versão mínima suportada do SSL. Se definir esta política para *não configurado,* o Microsoft Edge utiliza uma versão mínima predefinida de *TLS 1.0*. Quando definido para *Ativado,* pode selecionar uma versão mínima a partir dos seguintes valores:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Versão SSL mínima ativada**  
    **Predefinição**: TLS 1.2

- **Evitar contornar os avisos do Microsoft Defender SmartScreen sobre downloads**  
  **Predefinição**: Ativado  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOveroverforFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Esta política permite-lhe determinar se os utilizadores podem substituir os avisos do Microsoft Defender SmartScreen sobre transferências não verificadas.
  - Se ativar esta política, os utilizadores da sua organização não podem ignorar os avisos do Microsoft Defender SmartScreen e estão impedidos de concluir os downloads não verificados.
  - Se desativar ou não configurar esta política, os utilizadores podem ignorar os avisos do Microsoft Defender SmartScreen e concluir downloads não verificados.

- **Permitir que os utilizadores procedam da página de aviso SSL**  
  **Predefinição**: Desativado  
  Microsoft Edge CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  O Microsoft Edge mostra uma página de aviso quando os utilizadores visitam sites com erros SSL. Se definir esta política para *Ativado* ou *Não Configurado,* os utilizadores podem clicar nestas páginas de aviso. Quando esta política é *desativada,* os utilizadores estão impedidos de clicar em qualquer página de aviso. 

- **Definição padrão de Flash Adobe**  
  **Predefinição**: Ativado  
  Microsoft Edge CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash), e [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Determina se os websites que não estão cobertos por 'PluginsAllowedForUrls' ou 'PluginsBlockedForUrls' podem executar automaticamente o plug-in Adobe Flash. 

  - Selecione 'BlockPlugins' para bloquear O Adobe Flash em todos os sites
  - Selecione 'ClickToPlay' para permitir a execução do Adobe Flash, mas exija que o utilizador clique no espaço reservado para o iniciar.
  
  Em todo o caso, as políticas 'PluginsAllowedForUrls' e 'PluginsBlockedForUrls' têm precedência sobre 'DefaultPluginsSetting'. A reprodução automática só é permitida para domínios explicitamente listados na política 'PluginsAllowedForUrls'. 
   Se quiser ativar a reprodução automática para todos os sites, considere adicionar http://* e https://* a esta lista.

  - Se definir esta política para *não configurar,* o utilizador pode alterar esta definição manualmente. * 2 = Bloqueie o plug-in Adobe Flash * 3 = Clique para reproduzir o conjunto de opções '1' anterior, mas esta funcionalidade é agora apenas manuseada pela política 'PluginsAllowedForUrls'. As políticas existentes utilizando o '1' funcionarão no modo Click-to-play.  

  - **Definição padrão de Flash Adobe**  
    **Predefinição**: Bloqueie o plugin Adobe Flash

- **Ativar o isolamento do site para cada site**  
  **Predefinição**: Ativado  

  A política 'SitePerProcess' pode ser utilizada para impedir que os utilizadores optem pelo comportamento predefinido de isolar todos os sites. Também pode utilizar a política IsolateOrigins para isolar origens adicionais e mais finas.

  - Quando esta política está definida para *ativar,* os utilizadores não podem optar pelo comportamento padrão em que cada site funciona no seu próprio processo. 
  - Se utilizar *Desativado* ou *Não Configurado,* um utilizador pode optar por não o isolamento do local. (Por exemplo, utilizando a entrada "Desativar o isolamento do local" em edge://flags.) Desativar a política ou não configurar a política não desliga o Isolamento do Site.

- **Regimes de autenticação suportados**  
  **Predefinição**: Ativado  

  Especifica quais os regimes de autenticação HTTP suportados. Pode configurar a política utilizando estes valores: "básico", "digestivo", "ntlm" e "negociar". Separe vários valores com vírgulas. Se não configurar esta política, todos os quatro esquemas são usados.

  - **Regimes de autenticação suportados**  
    Selecione entre as seguintes opções:
    - Básico
    - Digerir
    - NTLM *(Selecionado por padrão)*
    - Negociar *(Selecionado por defeito)*

- **Ativar palavras-passe para guardar palavras-passe para o gestor de passwords**  
  **Predefinição**: Desativado  
  Microsoft Edge CSP: [Browser/AllowpasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Ative o Microsoft Edge para guardar as palavras-passe dos utilizadores.
  - Se ativar esta política, os utilizadores podem guardar as suas palavras-passe no Microsoft Edge. Da próxima vez que visitarem o site, o Microsoft Edge introduzirá automaticamente a palavra-passe.
  - Se desativar esta política, os utilizadores não podem guardar novas palavras-passe, mas ainda podem utilizar senhas previamente guardadas.
  
  Quando define esta política para *ativação* ou *desativação,* os utilizadores não podem alterar ou anular esta política no Microsoft Edge.
  
  Se configurar isto para *Não Configurado,* os utilizadores podem guardar senhas, bem como desligar esta funcionalidade.

- **Controlo quais extensões não podem ser instaladas**  
  **Predefinição**: Ativado  

  Enumere as extensões específicas que os utilizadores não podem instalar no Microsoft Edge. Quando implementa esta política, quaisquer extensões desta lista que foram previamente instaladas são desativadas, e o utilizador não poderá permitir. Se remover um item da lista de extensões bloqueadas, essa extensão é automaticamente reativada em qualquer lugar onde foi previamente instalada.
  
  Utilize **\*** para bloquear todas as extensões que não estão explicitamente listadas na lista de autorizações. Se esta política estiver definida para *não configurar,* os utilizadores podem instalar qualquer extensão no Microsoft Edge.
  
  Valor exemplo: extension_id1 extension_id2.  
  <br>
  - **IDs de extensão o utilizador deve ser impedido de instalar (ou * para todos)**  
    Selecione **Adicionar** e especificar extensões adicionais. **\*** é selecionado por defeito.

- **Configure Microsoft Defender SmartScreen**  
  **Predefinição**: Ativado  
  Microsoft Edge CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Esta definição de política permite configurar se deve ligar o Microsoft Defender SmartScreen. O Microsoft Defender SmartScreen fornece mensagens de aviso para ajudar a proteger os seus utilizadores de potenciais esquemas de phishing e software malicioso.
  
  - Por predefinição, o Microsoft Defender SmartScreen está ligado. Se ativar esta definição, o Microsoft Defender SmartScreen está ligado e os utilizadores não podem desligá-lo.
  - Se desativar esta definição, o Microsoft Defender SmartScreen está desligado e os utilizadores não podem ligá-lo.
  - Quando definido para *não configurado,* os utilizadores podem escolher se utilizam o Microsoft Defender SmartScreen.
  
  Esta política está disponível apenas em casos do Windows que se juntam a um domínio do Microsoft Ative Diretor, ou em casos do Windows 10 Pro ou Da Enterprise que estão inscritos para a gestão do dispositivo.

- **Permitir anfitriões de mensagens nativas ao nível do utilizador (instalados sem permissões de administração)**  
  **Predefinição**: Desativado

  Permite a instalação ao nível do utilizador de anfitriões de mensagens nativas. 
  - Se desativar esta política, o Microsoft Edge utilizará apenas anfitriões de mensagens nativas instalados a nível do sistema. Por padrão, se não configurar esta política, o Microsoft Edge permitirá a utilização de anfitriões de mensagens nativas ao nível do utilizador.

::: zone-end

## <a name="next-steps"></a>Passos seguintes

- [Conheça as linhas de base de segurança](security-baselines.md)
- [Evitar conflitos](security-baselines.md#avoid-conflicts)
- [Resolução de problemas de políticas e perfis no Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
