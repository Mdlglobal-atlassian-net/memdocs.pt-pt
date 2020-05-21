---
title: Definições personalizadas - Windows Holographic para dispositivos Empresariais - Microsoft Intune / Microsoft Docs
description: Adicione ou crie um perfil personalizado para utilizar as definições OMA-URI para dispositivos com o Windows Holographic for Business no Microsoft Intune, incluindo o Microsoft Hololens. Pode configurar definições de fornecedor de serviços de configuração da política (CSP) AllowFastReconnect, AllowVPN, AllowUpdateService, UpdateServiceURL, RequireUpdatesApproval, ApprovedUpdates e ApplicationLaunchRestrictions.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5eb1c69ed3a3a2b1671b6bec95a77cb627004ecf
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556086"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>Utilizar definições personalizadas para dispositivos com o Windows Holographic for Business no Intune

Ao utilizar o Microsoft Intune, pode adicionar ou criar definições personalizadas para os seus dispositivos com o Windows Holographic for Business, com "perfis personalizados". Os perfis personalizados são uma funcionalidade do Intune. Foram concebidos para adicionar definições e funcionalidades de dispositivos que não estão incorporadas Intune.

Os perfis personalizados do Windows Holographic for Business utilizam as definições Open Mobile Alliance Uniform Resource Identifier (OMA-URI) para configurar diferentes funcionalidades. Estas definições são normalmente utilizadas por fabricantes de dispositivos móveis para controlar as funcionalidades no dispositivo.

O Windows Holographic for Business disponibiliza várias definições de fornecedores de serviços de configuração (CSPs). Para obter uma descrição geral do CSP, veja [Introdução a fornecedores de serviços de configuração (CSPs) para profissionais de TI](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers). Para obter CSPs específicos suportados pelo Windows Holographic, veja [CSPs suportados no Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens).

Se estiver à procura de uma definição específica, lembre-se de que o [perfil de restrição de dispositivos com o Windows Holographic for Business](device-restrictions-windows-holographic.md) inclui várias definições incorporadas. Por isso, poderá não ter de introduzir valores personalizados.

Este artigo mostra-lhe como criar um perfil personalizado para dispositivos com o Windows Holographic for Business. Inclui também uma lista de definições OMA-URI recomendadas.

## <a name="before-you-begin"></a>Antes de começar

[Criar um perfil personalizado do Windows 10.](custom-settings-configure.md#create-the-profile)

## <a name="custom-oma-uri-settings"></a>Definições oma-URI personalizadas

**Adicionar**: Introduza as seguintes definições:

- **Nome** – introduza um nome exclusivo para a definição OMA-URI para o ajudar a identificá-la na lista de definições.
- **Descrição**: introduza uma descrição que lhe permita obter uma descrição geral da definição e outros detalhes importantes.
- **OMA-URI** (sensível a maiúsculas e minúsculas): introduza a definição OMA-URI que pretende utilizar.
- Tipo de **dados:** Selecione o tipo de dados que utilizará para esta definição OMA-URI. As opções são:

  - String
  - Cadeia (ficheiro XML)
  - Data e hora
  - Número inteiro
  - Vírgula flutuante
  - Booleano
  - Base64 (ficheiro)

- **Valor**: introduza o valor de dados que pretende associar à definição OMA-URI que introduziu. O valor depende do tipo de dados que selecionou. Por exemplo, se selecionar **Data e Hora,** selecione o valor de um apanhador de datas.

Depois de adicionar algumas definições, pode selecionar **Exportar**. A opção **Exportar** cria uma lista de todos os valores que adicionou num ficheiro de valores separados por vírgulas (.csv).

## <a name="recommended-custom-settings"></a>Definições personalizadas recomendadas

As seguintes definições são úteis para dispositivos com o Windows Holographic for Business:

### <a name="allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|Número inteiro<br/>0 – não permitido<br/>1 – permitido (predefinição)|

### <a name="allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|Número inteiro<br/>0 – o serviço de atualização não é permitido. <br/>1 – o serviço de atualização é permitido (predefinição).|

### <a name="allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|Número inteiro<br/>0 – não permitido<br/>1 – permitido (predefinição)|

### <a name="requireupdateapproval"></a>[Requerer ARedação](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|Esta definição está disponível em RS5 (construção 17763) e anteriormente. A partir do 19H1 (construção 18362), utilize o [Windows Update para o Negócios](../protect/windows-update-for-business-configure.md).<br/><br/>Número inteiro<br/>0 – não configurado. O dispositivo instala todas as atualizações aplicáveis.<br/>1 – o dispositivo instala apenas as atualizações que são aplicáveis e estão na lista de Atualizações Aprovadas. Defina esta política para 1 se a equipa de TI quiser controlar a implementação das atualizações nos dispositivos, como quando é pedido um teste antes da implementação.|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|Número inteiro entre 0 e 23, em que 0=00:00 e 23=23:00<br/>O valor predefinido é 3.|

### <a name="updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|Esta definição está disponível em RS5 (construção 17763) e anteriormente. A partir do 19H1 (construção 18362), utilize o [Windows Update para o Negócios](../protect/windows-update-for-business-configure.md).<br/><br/>String<br/>URL – o dispositivo procura atualizações do servidor WSUS no URL especificado.<br/>Não configurado – o dispositivo procura atualizações do Microsoft Update.|

### <a name="approvedupdates"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/*GUID*<br/><br/>**Importante**<br/>Tem de ler e aceitar os EULAs de atualização em nome dos seus utilizadores finais. Caso contrário, ocorrerá uma falha de segurança nas obrigações contratuais e legais.|O nó para as aprovações de atualizações e a aceitação do EULA em nome do utilizador final.<br/><br/>Para mais informações, veja [Atualizar CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp).|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Fornecedor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping* / *Grouping ApplicationType*/Policy<br/><br/>**Importante**<br/>O artigo AppLocker CSP utiliza exemplos de XML de escape. Para configurar as definições com os perfis personalizados do Intune, tem de utilizar XML simples.|String<br/>Para mais informações, veja [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp).|

### <a name="deletionpolicy"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|Número inteiro<br/>0 – eliminar imediatamente quando o dispositivo voltar a um estado sem utilizadores atualmente ativos<br/>1 – eliminar quanto for atingido o limiar de capacidade de armazenamento (predefinição)<br/>2 – eliminar quando for atingido o limiar de capacidade de armazenamento e o limiar de inatividade do perfil|

### <a name="enableprofilemanager"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|Booleano<br/>Verdadeiro – ativar<br/>Falso – desativar (predefinição)|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|Número inteiro<br/>O valor predefinido é 30.|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|Número inteiro<br/>O valor predefinido é 25.|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|Tipo de dados|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|Número inteiro<br/>O valor predefinido é 50.|

## <a name="find-the-policies-you-can-configure"></a>Encontrar as políticas que pode configurar

Pode consultar a lista completa de todos os fornecedores de serviços de configuração (CSPs) que o Windows Holographic suporta em [CSPs suportados no Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens). Nem todas as definições são compatíveis com todas as versões do Windows Holographic. A tabela em [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) (CSPs suportados no Windows Holographic) apresenta as versões suportadas para cada CSP.

Além disso, o Intune não suporta todas as definições apresentadas em [CSPs supported in Windows Holographic](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) (CSPs suportados no Windows Holographic). Para saber se o Intune suporta a definição que pretende, abra o artigo referente a essa definição. Cada página de definição mostra a respetiva operação suportada. Para trabalhar com o Intune, a definição tem de suportar as operações **Adicionar** ou **Substituir**.

## <a name="next-steps"></a>Próximos passos

[Atribuir o perfil,](device-profile-assign.md) [e monitorizar o seu estado](device-profile-monitor.md).

Criar um [perfil personalizado nos dispositivos windows 10](custom-settings-windows-10.md).

Saiba mais sobre [perfis personalizados](custom-settings-configure.md) em Intune.
