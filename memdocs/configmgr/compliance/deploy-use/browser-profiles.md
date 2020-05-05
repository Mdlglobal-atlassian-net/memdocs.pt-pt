---
title: Configurar definições do Microsoft Edge
titleSuffix: Configuration Manager
description: Configure as definições para o navegador Web Microsoft Edge nos clientes do Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210099"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Configure as definições do Microsoft Edge no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!-- 1357310 -->
A partir da versão 1802, para os clientes que utilizam o navegador Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nos clientes do Windows 10, criar uma política de definições de conformidade do Gestor de Configuração para configurar várias definições do Microsoft Edge. 

Esta política aplica-se apenas aos clientes do Windows 10, versão 1703 ou posterior. <!--511552-->


## <a name="policy-settings"></a>Definições de política
Esta política inclui atualmente as seguintes definições:
- **Definir o navegador Microsoft Edge como padrão**: configura a definição de aplicação padrão do Windows 10 para o navegador web para o Microsoft Edge
- Permitir a **queda da barra de endereços**: Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política de [navegador AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir sincronizar os favoritos entre os navegadores**da Microsoft : Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política do [navegador SyncFavoritesBetweenIEEMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir dados de navegação claros na saída**: Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política de [navegador ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Não permita rastrear os cabeçalhos**: Para mais informações, consulte a política do [navegador AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir a preenchimento automática**: Para mais informações, consulte a política do [navegador AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para mais informações, consulte a política do [navegador AllowCookies.](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)
- Permita um **bloqueador pop-up**: Para mais informações, consulte a política do [navegador AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra**de endereços : Para mais informações, consulte a política do navegador [AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir enviar tráfego intranet para o Internet Explorer**: Para mais informações, consulte a política do navegador [SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir o gestor de passwords**: Para mais informações, consulte a política de [navegador AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir ferramentas de desenvolvimento**: Para mais informações, consulte a política do [navegador AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: Para mais informações, consulte a política do [navegador AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configure as definições do SmartScreen do Windows Defender para o Microsoft Edge
<!--1353701-->
A partir da versão 1806, esta política adiciona três definições para [o Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). A política inclui agora as seguintes definições adicionais na página de **Definições do SmartScreen:**

- **Permitir o SmartScreen**: Especifica se o Windows Defender SmartScreen é permitido. Para mais informações, consulte a política de [navegador AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- Os utilizadores podem substituir o **pedido do SmartScreen para sites**: Especifica se os utilizadores podem anular os avisos do Filtro SmartScreen do Windows Defender sobre websites potencialmente maliciosos. Para mais informações, consulte a política de [navegador PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- Os utilizadores podem substituir o **pedido do SmartScreen para ficheiros**: Especifica se os utilizadores podem anular os avisos do Filtro SmartScreen do Windows Defender sobre o descarregamento de ficheiros não verificados. Para mais informações, consulte a política de [navegador PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Criar o perfil do navegador Microsoft Edge

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Expandir **as Definições** de Conformidade e selecionar o nó de perfis de **navegador Microsoft Edge.** Clique na opção da fita para criar o **perfil Microsoft Edge**.
2. Especifique um **Nome** para a apólice, introduza opcionalmente uma **Descrição,** e clique **em Seguinte**.
3. Na página **Definições Gerais,** altere o valor para **Configurado** para as definições a incluir nesta política e clique em **Next**. A definição para **definir o Navegador Edge como padrão** deve ser configurada para continuar.
4. Na versão 1806 e posteriormente, configure as definições na página de **Definições do SmartScreen** e, em seguida, clique em **Next**. 
5. Na página **Plataformas Suportadas,** selecione as versões e arquiteturas S a que esta política se aplica, e clique em **Next**. 
6. Conclua o assistente.



## <a name="deploy-the-policy"></a>Implementar a política

1. Selecione a sua política e clique na opção de fita para **implementar**.
2. Clique em **Navegar** para selecionar a recolha do utilizador ou do dispositivo para implementar a política. 
3. Selecione opções adicionais se necessário.  
     a. Gere alertas quando a política não está em conformidade.  
     b. Detete o horário pelo qual o cliente avalia o cumprimento do dispositivo com esta política. 
4. Clique em **OK** para criar a implementação.



## <a name="next-steps"></a>Passos seguintes

Como qualquer política de definições de conformidade, o cliente remedia as definições na programação que especifica. [Monitore e informe sobre](monitor-compliance-settings.md) a conformidade do dispositivo na consola Do Gestor de Configuração.
