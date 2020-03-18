---
title: Definições de quiosque para Windows 10 no Microsoft Intune – Azure | Microsoft Docs
description: Configure os seus dispositivos Windows 10 (e mais tarde) como quiosques de aplicação única e multi-aplicações, personalize o menu inicial, adicione aplicações, mostre a barra de tarefas e configure um navegador web no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/02/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1750ff93f0896e620af243d96914caa428e37a4a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332009"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Windows 10 e posteriores configurações do dispositivo para funcionar como um quiosque em Intune

No Windows 10 e em dispositivos posteriores, pode configurar estes dispositivos para funcionar em modo quiosque de aplicações únicas ou no modo quiosque de várias aplicações.

Este artigo lista e descreve as diferentes definições que pode controlar no Windows 10 e dispositivos posteriores. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para configurar o windows 10 e dispositivos posteriores para funcionar no modo quiosque.

Como administrador intune, pode criar e atribuir estas definições aos seus dispositivos.

Para saber mais sobre a funcionalidade do quiosque Windows em Intune, consulte as definições do [quiosque configurar](kiosk-settings.md).

## <a name="before-you-begin"></a>Antes de começar

- [Criar o perfil.](kiosk-settings.md#create-the-profile)

- Este perfil de quiosque está diretamente relacionado com o perfil de restrições do dispositivo que cria utilizando as [definições](device-restrictions-windows-10.md#microsoft-edge-browser)do quiosque do Microsoft Edge . Resumindo:

  1. Crie este perfil de quiosque para executar o dispositivo no modo quiosque.
  2. Crie o perfil de restrições do dispositivo e configure [funcionalidades](device-restrictions-windows-10.md#microsoft-edge-browser)e definições específicas permitidas no Microsoft Edge.

- Certifique-se de que quaisquer ficheiros, scripts e atalhos estão no sistema local. Para mais informações, incluindo outros requisitos do Windows, consulte [Personalizar e exportar layout Iniciar](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Certifique-se de atribuir este perfil de quiosque aos mesmos dispositivos que o seu [perfil Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser).

## <a name="single-full-screen-app-kiosks"></a>Quiosques de uma aplicação em ecrã inteiro

Executa apenas uma aplicação no dispositivo.

- **Selecione um modo de quiosque**: Escolha uma única **aplicação, quiosque de ecrã completo**.

- **Tipo de início de sessão do utilizador**: as aplicações que adicionar são executadas como a conta de utilizador que introduzir. As opções são:

  - **Auto logon (Windows 10 versão 1803 e mais tarde)** : Utilização em quiosques em ambientes virados para o público que não exijam que o utilizador inicie sessão, semelhante a uma conta de hóspedes. Esta definição utiliza o [CSP AssignedAccess](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Conta de utilizador local**: introduza a conta de utilizador local (para o dispositivo). A conta que introduz entra entra no quiosque.

- Tipo de **aplicação:** Selecione o tipo de aplicação. As opções são:

  - **Adicione**o navegador Microsoft Edge : Selecione o **navegador Microsoft Edge**e escolha o tipo de modo de quiosque **Edge:**

    - **Sinalização digital/interativa**: Abre um ecrã completo URL e só mostra o conteúdo nesse website. [Configurar sinais digitais](https://docs.microsoft.com/windows/configuration/setup-digital-signage) fornece mais informações sobre esta funcionalidade.
    - **Navegação pública (InPrivate)** : Executa uma versão limitada de vários separadores do Microsoft Edge. Os utilizadores podem navegar publicamente ou terminar a sua sessão de navegação.

    Para obter mais informações sobre estas opções, consulte [o modo de quiosque do Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Esta definição permite o navegador Microsoft Edge no dispositivo. Para configurar as definições específicas do Microsoft Edge, crie um perfil de configuração do dispositivo (**Configuração** do dispositivo > **Perfis** > **Criar perfil** > **Windows 10** para restrições de plataforma e **dispositivos** >  **Microsoft Edge Browser).** [O Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) lista os navegadores e descreve as definições disponíveis.

  - **Adicionar navegador quiosque**: Selecione **as definições do navegador kiosk**. Estas definições controlam uma aplicação de browser no quiosque. Certifique-se de obter a [aplicação](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) do navegador Kiosk da Loja, adicione-a ao Intune como uma [App de Clientes](../apps/apps-add.md). Em seguida, atribua a aplicação aos dispositivos do quiosque.

    Introduza as seguintes definições:

    - **URL da home page predefinido**: introduza o URL predefinido mostrado quando o browser do quiosque abre ou quando o browser é reiniciado. Por exemplo, introduza: `http://bing.com` ou `http://www.contoso.com`.

    - **Botão de início**: **mostre** ou **oculte** o botão de início do browser do quiosque. Por predefinição, o botão não é mostrado.

    - **Botões de navegação**: **mostre** ou **oculte** os botões voltar e avançar. Por predefinição, os botões de navegação não são mostrados.

    - **Botão de terminar sessão**: **mostre** ou **oculte** o botão de terminar sessão. Quando o botão é apresentado, o utilizador seleciona-o e a aplicação pede para terminar a sessão. Ao confirmar, o browser limpa todos os dados de navegação (cookies, cache, etc.) e abre o URL predefinido. Por predefinição, o botão não é mostrado.

    - **Atualizar o browser após um tempo de inatividade**: introduza o período de tempo de inatividade (1-1440 minutos) necessário antes de o browser do quiosque reiniciar num estado novo. O tempo inativo é o número de minutos desde a última interação do utilizador. Por predefinição, o valor está vazio ou em branco, o que significa que não existe nenhum tempo limite de inatividade.

    - **Sites permitidos**: utilize esta definição para permitir que determinados sites sejam abertos. Por outras palavras, utilize esta funcionalidade para restringir ou impedir determinados sites no dispositivo. Por exemplo, pode permitir que todos os sites em `http://contoso.com` sejam abertos. Por predefinição, todos os sites são permitidos.

      Para permitir sites específicos, carregue um ficheiro que inclua uma lista dos sites permitidos em linhas separadas. Se não adicionar um ficheiro, todos os sites serão permitidos. Por defeito, Intune suporta wild card. Assim, quando entrar no domínio, como `sharepoint.com`, permita que subdomínios sejam automaticamente permitidos, como `contoso.sharepoint.com`, `my.sharepoint.com`, e assim por diante.

      O seu ficheiro de exemplo deve ser semelhante à seguinte lista:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Os quiosques do Windows 10 com Autologon ativados através do Microsoft Kiosk Browser devem utilizar uma licença offline da Microsoft Store for Business. Este requisito deve-se ao modo de utilização da Autologon, uma conta de utilizador local sem credenciais de Diretório Ativo Azure (AD). Então, as licenças online não podem ser avaliadas. Para mais informações, consulte [Distribute aplicativos offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Adicionar aplicativo Store**: Selecione **Adicionar uma aplicação**de loja , e escolha uma aplicação da lista.

    Não tem aplicações listadas? Adicione algumas através dos passos indicados em [Aplicações de Cliente](../apps/apps-add.md).
    
 - **Especificar Janela de Manutenção para Reiniciações**de aplicações : O predefinido é "Não Configurado", selecione "Require" para verificar se existem aplicações que exijam um reinício para a instalação completa.
 
     Se utilizar o navegador Kiosk ou outra microsoft store para aplicação de negócios, decida com que frequência verificar se existem atualizações de aplicações que necessitem de reiniciar para completar a instalação da aplicação. Caso não esteja configurado, as aplicações da Microsoft Store for Business recomeçarão a uma hora não programada 3 dias após a instalação de uma atualização da aplicação.
     
     - **Hora de início**da janela de manutenção : Selecione a data e a hora do dia para começar a verificar os clientes para quaisquer atualizações de aplicações que exijam o reinício. A hora de início é meia-noite, ou zero minutos.
     
     - **Recorrência da janela de manutenção**: O predefinido é diário.
         Detete a frequência com que as janelas de manutenção para atualizações de aplicações terão lugar. A recomendação é diária para evitar o reinício da aplicação não programada.

  [Gestão de Aplicações/AgendaForceRestartForUpdateFailures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosks"></a>Quiosques de várias aplicações

As aplicações neste modo estão disponíveis no menu Iniciar. Estas aplicações são as únicas aplicações que o utilizador pode abrir. Se uma aplicação tem uma dependência de outra aplicação, ambas devem ser incluídas na lista de aplicações permitidas. Por exemplo, o Internet Explorer 64-bit tem uma dependência do Internet Explorer 32 bits, por isso deve permitir tanto "C:\Program Files\internet explorer\iexplore.exe" e "C:\Program Files (x86)\Internet Explorer\iexplore.exe". 

- **Selecione um modo de quiosque**: Escolha o quiosque de **aplicações Multi**.

- **Target Windows 10 em dispositivos de modo S:**
  - **Sim:** Permite armazenar aplicações e aplicações AUMID (exclui aplicações Win32) no perfil do quiosque.
  - **Não**: Permite aplicações de loja, aplicações Win32 e aplicações AUMID no perfil do quiosque. Este perfil de quiosque não está implantado em dispositivos em modo S.

- **Tipo de início de sessão do utilizador**: as aplicações que adicionar são executadas como a conta de utilizador que introduzir. As opções são:

  - **Auto logon (Windows 10 versão 1803 e mais tarde)** : Utilização em quiosques em ambientes virados para o público que não exijam que o utilizador inicie sessão, semelhante a uma conta de hóspedes. Esta definição utiliza o [CSP AssignedAccess](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Conta de utilizador local**: **adicione** a conta de utilizador local (para o dispositivo). A conta que introduz entra entra no quiosque.
  - Utilizador ou grupo da **AD Azure (versão 1803 do Windows 10 e posterior)** : Selecione **Adicionar**, e escolha utilizadores ou grupos De AD Azure da lista. Pode selecionar vários utilizadores e grupos. Escolha **Selecionar** para guardar as alterações.
  - **Visitante do HoloLens**: A conta de visitante é uma conta de convidado que não necessita de credenciais ou de autenticação do utilizador, como está descrito em [Shared PC mode concepts (Conceitos de modo de PC partilhado)](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Navegador e Aplicações**: Adicione as aplicações para executar no dispositivo do quiosque. Lembre-se de que pode adicionar várias aplicações.

  - **Navegadores**

    - **Adicione o Microsoft Edge**: O Microsoft Edge é adicionado à grelha de aplicações e todas as aplicações podem ser executadas neste quiosque. Escolha o tipo de **modo de quiosque Microsoft Edge:**

      - **Modo normal (versão completa do Microsoft Edge)** : Executa uma versão completa do Microsoft Edge com todas as funcionalidades de navegação. Os dados e o estado do utilizador são guardados entre sessões.
      - **Navegação pública (InPrivate)** : Executa uma versão multi-tab do Microsoft Edge InPrivate com uma experiência personalizada para quiosques que funcionam em modo de ecrã completo.

      Para obter mais informações sobre estas opções, consulte [o modo de quiosque do Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Esta definição permite o navegador Microsoft Edge no dispositivo. Para configurar as definições específicas do Microsoft Edge, crie um perfil de configuração do dispositivo (**Configuração** do dispositivo > **Perfis** > **Criar perfil** > **Windows 10** para restrições de plataforma e **dispositivos** >  **Microsoft Edge Browser).** [O Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) lista os navegadores e descreve as definições disponíveis.

    - **Adicionar navegador quiosque**: Estas configurações controlam uma aplicação de navegador web no quiosque. Garanta que implementa uma aplicação de browser para os dispositivos de quiosque com as [Aplicações de Cliente](../apps/apps-add.md).

      Introduza as seguintes definições:

      - **URL da home page predefinido**: introduza o URL predefinido mostrado quando o browser do quiosque abre ou quando o browser é reiniciado. Por exemplo, introduza: `http://bing.com` ou `http://www.contoso.com`.

      - **Botão de início**: **mostre** ou **oculte** o botão de início do browser do quiosque. Por predefinição, o botão não é mostrado.

      - **Botões de navegação**: **mostre** ou **oculte** os botões voltar e avançar. Por predefinição, os botões de navegação não são mostrados.

      - **Botão de terminar sessão**: **mostre** ou **oculte** o botão de terminar sessão. Quando o botão é apresentado, o utilizador seleciona-o e a aplicação pede para terminar a sessão. Ao confirmar, o browser limpa todos os dados de navegação (cookies, cache, etc.) e abre o URL predefinido. Por predefinição, o botão não é mostrado.

      - **Atualizar o browser após um tempo de inatividade**: introduza o período de tempo de inatividade (1-1440 minutos) necessário antes de o browser do quiosque reiniciar num estado novo. O tempo inativo é o número de minutos desde a última interação do utilizador. Por predefinição, o valor está vazio ou em branco, o que significa que não existe nenhum tempo limite de inatividade.

      - **Sites permitidos**: utilize esta definição para permitir que determinados sites sejam abertos. Por outras palavras, utilize esta funcionalidade para restringir ou impedir determinados sites no dispositivo. Por exemplo, pode permitir que todos os sites em `contoso.com*` sejam abertos. Por predefinição, todos os sites são permitidos.

        Para permitir sites específicos, carregue um ficheiro .csv que inclua uma lista dos sites permitidos. Se não adicionar um ficheiro .csv, todos os sites serão permitidos.

      > [!NOTE]
      > Os quiosques do Windows 10 com Autologon ativados através do Microsoft Kiosk Browser devem utilizar uma licença offline da Microsoft Store for Business. Este requisito deve-se ao modo de utilização da Autologon, uma conta de utilizador local sem credenciais de Diretório Ativo Azure (AD). Então, as licenças online não podem ser avaliadas. Para mais informações, consulte [Distribute aplicativos offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Aplicações**

    - **Adicionar aplicação da loja**: adicione uma aplicação na Microsoft Store para Empresas. Se não tiver aplicações listadas, poderá obter aplicações e [adicioná-las ao Intune](../apps/store-apps-windows.md). Por exemplo, pode adicionar o Browser do Quiosque, Excel, OneNote e muito mais.

    - **Adicionar Aplicação Win32**: uma aplicação Win32 é uma aplicação de ambiente de trabalho tradicional, como o Visual Studio Code ou o Google Chrome. Introduza as seguintes propriedades:

      - **Nome da aplicação**: obrigatório. Introduza um nome para a aplicação.
      - **Caminho local**: obrigatório. Introduza o caminho para o executável, tal como `C:\Program Files (x86)\Microsoft VS Code\Code.exe` ou `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **ID do modelo de utilizador da aplicação (AUMID)** : introduza o ID do modelo de utilizador da aplicação (AUMID) da aplicação Win32. Esta definição determina o esquema de início do mosaico na área de trabalho. Para obter este ID, consulte [Get-StartApps](https://docs.microsoft.com/powershell/module/startlayout/get-startapps?view=win10-ps).

    - **Adicionar por AUMID**: utilize esta opção para adicionar aplicações do Windows de caixa de entrada, como o Bloco de notas ou a Calculadora. Introduza as seguintes propriedades:

      - **Nome da aplicação**: obrigatório. Introduza um nome para a aplicação.
      - **ID do modelo de utilizador da aplicação (AUMID)** : obrigatório. Introduza o ID do modelo de utilizador da aplicação (AUMID) da aplicação Windows. Para obter este ID, veja [Find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) (Localizar o ID do Modelo de Utilizador da Aplicação de uma aplicação instalada).

    - **Lançamento automático**: Opcional. Escolha uma aplicação para AutoLaunch quando o utilizador iniciar sintetiza. Apenas uma única aplicação pode ser AutoLançada.
    - **Tamanho do mosaico**: obrigatório. Escolha um tamanho de mosaico da aplicação: Pequeno, Médio, Largo ou Grande.

  > [!TIP]
  > Depois de adicionar todas as aplicações, pode alterar a ordem de apresentação ao clicar e arrastar as aplicações na lista.  

- **Utilizar o esquema do menu Iniciar alternativo**: escolha **Sim** para introduzir um ficheiro XML que descreva como as aplicações são apresentadas no menu Iniciar, incluindo a ordem das aplicações. Utilize esta opção se precisar de uma personalização adicional no menu Iniciar. O artigo [Customize and export Start layout (Personalizar e exportar o esquema do menu Iniciar)](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout) fornece algumas orientações e um ficheiro XML de exemplo.

- **Barra de tarefas do Windows**: escolha **Mostrar** ou **Ocultar** a barra de tarefas. Por predefinição, a barra de tarefas não é mostrada. Os ícones, como o ícone Wi-Fi, são mostrados, mas as definições não podem ser alteradas pelos utilizadores finais.

- **Permitir o acesso à pasta de downloads**: Escolha **Sim** para permitir que os utilizadores acedam à pasta Downloads no Windows Explorer. Por predefinição, o acesso à pasta Downloads é desativado. Esta funcionalidade é comumente utilizada para os utilizadores finais acederem a itens descarregados a partir de um navegador.

## <a name="next-steps"></a>Próximos passos

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).

Também pode criar perfis de quiosque para [Android,](device-restrictions-android.md#kiosk) [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)e Windows Holographic para dispositivos [Business.](kiosk-settings-holographic.md)

Consulte também a criação de [um quiosque de aplicações únicas](https://docs.microsoft.com/windows/configuration/kiosk-single-app) ou [instale um quiosque multi-aplicativos](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps) na orientação do Windows.
