---
title: Registo de Alterações do Armazém de Dados do Intune
titleSuffix: Microsoft Intune
description: Este tópico fornece uma lista de alterações para a API do Microsoft Intune Data Warehouse.
keywords: Armazém de Dados do Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: E85DBB2D-67BB-4E10-82D6-E43046B9C43C
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 632f3bf16fd062acf05c7bd4e269069468df42a3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331825"
---
# <a name="change-log-for-the-intune-data-warehouse-api"></a>Registo de alterações da API do Armazém de Dados do Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Mantenha-se a par das atualizações do Armazém de Dados do Intune.

## <a name="1903-part-2"></a>1903 (Parte 2)
_Lançado abril de 2019_

### <a name="beta-changes"></a>Alterações beta

A tabela seguinte lista as recentes recolhas removidas e as coleções de substituições no Intune Data Warehouse.

|    Recolha                          |    Alteração     |    Informações adicionais                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    mobileAppDeviceUserInstallStatus    |    Removidas    |    Utilize [mobileAppInstallStatusCounts](intune-data-warehouse-collections.md#mobileappinstallstatuscounts) em vez disso.                                                                                                                                                                                                                                                                     |
|    inscriçõesTipos                     |    Removidas    |    Utilize o [dispositivoNúmeros de inscrição.](intune-data-warehouse-collections.md#deviceenrollmenttypes)                                                                                                                                                                                                                                                                                      |
|    mdmStatuses                         |    Removidas    |    Use [complianceStates](intune-data-warehouse-collections.md#compliancestates) em vez disso.                                                                                                                                                                                                                                                                                               |
|    workPlaceJoinStateTypes             |    Removidas    |    Utilize a propriedade `azureAdRegistered` nos [dispositivos](intune-data-warehouse-collections.md#devices) e [coleções de dispositivosPropertyHistories.](intune-data-warehouse-collections.md#devicepropertyhistories)                                                                                                                                                                                                             |
|    clientRegistrationStateTypes        |    Removidas    |    Utilize o [dispositivoRegistrationStates.](intune-data-warehouse-collections.md#deviceregistrationstates)                                                                                                                                                                                                                                                                             |
|    currentUser                         |    Removidas    |    Utilize a coleção de [utilizadores](intune-data-warehouse-collections.md#users) em vez disso.                                                                                                                                                                                                                                                                                                      |
|    mdmDeviceInventoryHistories         |    Removidas    |    Muitas das propriedades foram redundantes ou podem agora ser encontradas no [dispositivoPropertyHistories](intune-data-warehouse-collections.md#devicepropertyhistories) ou coleções de [dispositivos.](intune-data-warehouse-collections.md#devices) Quaisquer propriedades **do mdmDeviceInventoryHistories** que ainda não estão listadas com estas duas coleções já não estão disponíveis. Veja os detalhes abaixo.    |

A tabela seguinte lista as propriedades antigas anteriormente encontradas na coleção **mdmDeviceInventoryHistories** e a alteração/substituição. Quaisquer propriedades que estivessem em **mdmDeviceInventoryHistories,** mas não listadas abaixo, foram removidas.

|    Propriedade antiga                |    Alteração/substituição                                                           |
|--------------------------------|---------------------------------------------------------------------------------|
|    tecnologia celular          |    tecnologia celular na coleção de dispositivos                                     |
|    deviceClientId              |    dispositivoId na recolha de dispositivos                                               |
|    dispositivoFabricante          |    fabricante na coleção de dispositivos                                           |
|    deviceModel                 |    modelo na coleção de dispositivos                                                  |
|    deviceName                  |    dispositivoNome na coleção de dispositivos                                             |
|    deviceOsPlatform            |    dispositivoTypeKey na recolha de dispositivos                                          |
|    deviceOsVersion             |    osVersão na coleção devicePropertyHistories                              |
|    deviceType                  |    dispositivoTypeKey na recolha de dispositivos, referenciando a recolha de tipos de dispositivos    |
|    encryptionState             |    propriedade encriptaçãoEstado na coleção de dispositivos                           |
|    exchangeActiveSyncId        |    propriedade easDeviceId na coleção de dispositivos                               |
|    exchangeDeviceId            |    easDeviceId na coleção de dispositivos                                            |
|    imei                        |    imei na coleção de dispositivos                                                   |
|    isSupervised                |    propriedade isSupervisionada na coleção de dispositivos                              |
|    prisãoQuebrado                  |    prisãoQuebrada na coleção devicePropertyHistories                             |
|    meid                        |    propriedade meid na coleção de dispositivos                                      |
|    oem                         |    fabricante na coleção de dispositivos                                           |
|    osName                      |    dispositivoTypeKey na recolha de dispositivos, referenciando a recolha de tipos de dispositivos    |
|    phoneNumber                 |    telefoneNúmero na coleção de dispositivos                                            |
|    plataformaType                |    modelo na coleção de dispositivos                                                  |
|    produto                     |    dispositivoTypeKey na recolha de dispositivos                                          |
|    produtoVersão              |    osVersão na coleção devicePropertyHistories                              |
|    serialNumber                |    sérieNúmero na coleção de dispositivos                                           |
|    storageFree                 |    propriedade freeStorageSpaceInBytes na coleção de dispositivos                   |
|    storageTotal                |    propriedade totalStorageSpaceInBytes na coleção de dispositivos                |
|    subscritorCarrierNetwork    |    propriedade subscritorCarrier na coleção de dispositivos                         |
|    wifimac                     |    wiFiMacAddress na coleção de dispositivos                                         |

A tabela a seguir enumera alterações às propriedades encontradas na coleção [propertyHistories:](intune-data-warehouse-collections.md#devicepropertyhistories) 

|    Propriedade antiga                  |    Alteração/substituição                                               |
|----------------------------------|---------------------------------------------------------------------|
|    categoryId                    |    dispositivoCategoriaChave, referenciação de dispositivosColeçãocategorias       |
|    certExpirationDate            |    Removidas                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    criadoData                   |    DataTime inscrito na recolha de dispositivos                           |
|    deviceTypeKey                 |    dispositivoTypeKey na recolha de dispositivos                              |
|    easID                         |    easDeviceId na coleção de dispositivos                                |
|    enrolledByUser                |    userId na recolha de dispositivos                                     |
|    enrollmentTypeKey             |    dispositivoInscriçTypeKey na recolha de dispositivos                    |
|    graphDeviceIsCompliant        |    Removidas                                                          |
|    graphDeviceIsManaged          |    Removidas                                                          |
|    lastContact                   |    últimoSyncDateTime na coleção de dispositivos                           |
|    lastContactNotification       |    Removidas                                                          |
|    lastContactWorkplaceJoin      |    Removidas                                                          |
|    lastExchangeStatusUtc         |    Removidas                                                          |
|    lastModifiedDateTimeUTC       |    Removidas                                                          |
|    lastPolicyUpdateUtc           |    Removidas                                                          |
|    managementAgentKey            |    managementStateKey                                               |
|    fabricante                  |    fabricante na coleção de dispositivos                               |
|    mdmStatusKey                  |    complianceStateKey, referenciando complianceRecolha de estados    |
|    modelo                         |    modelo na coleção de dispositivos                                      |
|    osFamily                      |    sistema operativo na recolha de dispositivos                            |
|    osRevisionNumber              |    osVersão na coleção de dispositivos                                  |
|    processadorArquitetura         |    Removidas                                                          |
|    referenceId                   |    azureAdDeviceId na coleção de dispositivos                            |
|    serialNumber                  |    sérieNúmero na coleção de dispositivos                               |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

A tabela a seguir enumera alterações às propriedades encontradas na recolha de [dispositivos:](intune-data-warehouse-collections.md#devices) 

|    Propriedade antiga                  |    Alteração/substituição                                               |
|----------------------------------|---------------------------------------------------------------------|
|    categoryId                    |    dispositivoCategoriaChave, referenciação de dispositivosColeçãocategorias       |
|    certExpirationDate            |    Removidas                                                          |
|    clientRegistrationStateKey    |    deviceRegistrationStateKey                                       |
|    criadoData                   |    enrolledDateTime                                                 |
|    easId                         |    easDeviceId                                                      |
|    enrolledByUser                |    userId                                                           |
|    enrollmentTypeKey             |    deviceEnrollmentTypeKey                                          |
|    graphDeviceIsCompliant        |    Removidas                                                          |
|    graphDeviceIsManaged          |    Removidas                                                          |
|    lastContact                   |    lastSyncDateTime                                                 |
|    lastContactNotification       |    Removidas                                                          |
|    lastContactWorkplaceJoin      |    Removidas                                                          |
|    lastExchangeStatusUtc         |    Removidas                                                          |
|    lastPolicyUpdateUtc           |    Removidas                                                          |
|    mdmStatusKey                  |    complianceStateKey, referenciando complianceRecolha de estados    |
|    osFamily                      |    operatingSystem                                                  |
|    processadorArquitetura         |    Removidas                                                          |
|    referenceId                   |    azureAdDeviceId                                                  |
|    workplaceJoinStateKey         |    azureAdRegistered                                                |

A tabela a seguir enumera alterações aos imóveis encontrados na recolha de [inscriçõesAtividades:](intune-data-warehouse-collections.md#enrollmentactivities) 

|    Propriedade antiga         |    Alteração/substituição         |
|-------------------------|-------------------------------|
|    enrollmentTypeKey    |    deviceEnrollmentTypeKey    |

A tabela a seguir enumera alterações às propriedades encontradas na coleção [mamApplications:](intune-data-warehouse-collections.md#mamapplications) 

|    Propriedade antiga       |    Alteração/substituição    |
|-----------------------|--------------------------|
|    aplicaçãoChave     |    mamApplicationKey     |
|    applicationName    |    mamApplicationName    |
|    applicationId      |    mamApplicationId      |

A tabela a seguir enumera alterações às propriedades encontradas na coleção [mamApplicationInstances:](intune-data-warehouse-collections.md#mamapplicationinstances) 

|    Propriedade antiga     |    Alteração/substituição    |
|---------------------|--------------------------|
|    applicationId    |    mamApplicationId      |
|    deviceId         |    mamDeviceId           |
|    deviceType       |    mamDeviceType         |
|    deviceName       |    mamDeviceName         |

A tabela a seguir enumera alterações às propriedades encontradas na coleção [mamCheckins:](intune-data-warehouse-collections.md#mamcheckins) 

|    Propriedade antiga      |    Alteração/substituição    |
|----------------------|--------------------------|
|    aplicaçãoChave    |    mamApplicationKey     |

A tabela a seguir enumera alterações às propriedades encontradas na recolha dos [utilizadores:](intune-data-warehouse-collections.md#users) 

|    Propriedade antiga             |    Alteração/substituição    |
|-----------------------------|--------------------------|
|    startDateInclusiveUtc    |    Removidas               |
|    endDateInclusiveUtc      |    Removidas               |
|    isCurrent                |    Removidas               |

## <a name="1903"></a>1903
_Lançado março de 2019_

### <a name="v10-changes-reflecting-back-to-beta"></a>V1.0 alterações refletindo de volta à beta
Quando o V1.0 foi introduzido pela primeira vez em 1808, diferia de algumas formas significativas da Beta API. Em 1903 essas alterações serão refletidas de volta na versão Beta API. Se tiver relatórios importantes que utilizem a versão Beta API, recomendamos vivamente a troca desses relatórios para V1.0 para evitar alterações de rutura. Consulte as informações da [versão API](reports-api-url.md) para obter mais informações sobre as versões API do Data Warehouse e a compatibilidade para trás.

## <a name="1902"></a>1902 
_Lançado fevereiro de 2019_

### <a name="power-bi-compliance-app"></a>Aplicação power bi compliance

Aceda ao seu Intune Data Warehouse em Power BI Online utilizando a aplicação [Intune Compliance (Data Warehouse).](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) Com esta aplicação Power BI, já pode aceder e partilhar relatórios pré-criados sem qualquer configuração e sem sair do seu navegador web.

> [!NOTE]
> Existem dois filtros adicionais que pode aplicar na aplicação Intune Compliance.

#### <a name="add-additional-filters-to-the-intune-compliance-app"></a>Adicione filtros adicionais à app Intune Compliance
1. Abra a aplicação [Intune Compliance (Data Warehouse)](https://aka.ms/intune/datawarehouseapi/getpowerbiapp) nos seus navegadores web.
2. Clique em **Dispositivos Não Conformes** e selecione **Non-Compliant** no filtro **complianceStatus.**
3. Clique em **Dispositivos Desconhecidos** e selecione **Ainda não disponível** no filtro **complianceStatus.**

## <a name="1812"></a>1812 
_Lançado dezembro de 2018_

### <a name="enrollment-activities-collection-released-to-v10"></a>Coleção de Atividades de Inscrição Lançada para v1.0 

A coleção de Atividades de Inscrição já está disponível em v1.0. Pode utilizar esta coleção para compreender o volume de falhas de matrícula e as tendências do seu ambiente. Para mais informações, consulte [inscriçõesActividades,](intune-data-warehouse-collections.md#enrollmentactivities) [inscriçõesEventStatuses,](intune-data-warehouse-collections.md#enrollmenteventstatuses) [inscriçõesFailureCategories,](intune-data-warehouse-collections.md#enrollmentfailurecategories)e [inscriçõesFailureReasons](intune-data-warehouse-collections.md#enrollmentfailurereasons).

## <a name="1808"></a>1808
_Lançada em agosto de 2018_

### <a name="v10-collections"></a>Coleções v1.0  

Agora, pode utilizar a versão v1.0 do Armazém de Dados do Intune, ao definir o parâmetro de consulta `api-version=v1.0`. As atualizações para coleções no Armazém de Dados são acumulativas por natureza e não interrompem cenários existentes.

### <a name="enrollment-activities-collection-released-to-beta"></a>Coleção de atividades de inscrição lançada para Beta

A nova coleção `Enrollment Activities` é lançada para beta. Pode utilizar esta coleção para entender como a inscrição está a decorrer ao visualizar as falhas mais comuns. 


## <a name="1805"></a>1805
_Lançado em maio de 2018_

### <a name="correction-to-device-count-in-devices-collection"></a>Correção na contagem de dispositivos na coleção **Dispositivos** 

Foi feita uma correção à coleção **Dispositivos** que pode diminuir o número total de dispositivos que filtram pelo atributo `isDeleted`. Esta lista é um resultado da correção e não é um erro. Para mais informações sobre a coleção **Dispositivos**, veja [Referência para entidades de dispositivos](reports-ref-devices.md). 


## <a name="1801"></a>1801
_Lançada em janeiro de 2018_

### <a name="intune-data-warehouse-application-only-authentication----1867540---"></a>Autenticação apenas com a aplicação do Armazém de Dados do Intune <!-- 1867540 -->

Pode configurar uma aplicação com o Azure Active Directory (Azure AD) e autenticar para o Armazém de Dados do Intune. Para obter mais informações, veja [Autenticação apenas com a aplicação do Armazém de Dados do Intune](data-warehouse-app-only-auth.md).

### <a name="azure-ad-and-intune-credential-requirements----2077525---"></a>Requisitos de credenciais do Azure AD e do Intune <!-- 2077525 -->

- Já não é necessário atribuir uma licença do Intune ao utilizador ao aceder ao Armazém de Dados do Intune (incluindo a API).
- O nome da função do Intune foi alterado de **Relatórios** para **Armazém de dados do Intune**. 

    Para obter mais informações, veja [Requisitos de credenciais do Azure AD e do Intune](reports-api-url.md#azure-ad-and-intune-credential-requirements).

### <a name="odata-query-options----2077711---"></a>Opções de consulta de OData <!-- 2077711 -->

Pode utilizar <code>$select</code> como um parâmetro de consulta de OData. A versão atual suporta os seguintes parâmetros de consulta de OData: <code>$filter</code>, <code>$orderby</code>, <code>$select</code>, <code>$skip</code> e <code>$top</code>. Para obter mais informações, veja [Opções de consulta de OData](reports-api-url.md#odata-query-options).

### <a name="new-entities-in-the-in-data-warehouse-data-model----2077804---"></a>Novas entidades no modelo de dados data Warehouse <!-- 2077804 -->

- A entidade [**MobileAppDeviceuserInstallStatus**](reports-ref-application.md) foi adicionada. A entidade **MobileAppDeviceUserInstallStatus** representa um estado de instalação da aplicação móvel de um determinado dispositivo e utilizador.
- A entidade, [**MobileAppInstallStates,** ](reports-ref-application.md#mobileappinstallstates)foi adicionada. A entidade **MobileAppInstallState** representa o estado de instalação de uma aplicação móvel depois de ser atribuída a um grupo que contém dispositivos, utilizadores ou ambos. 

## <a name="1710"></a>1710
_Lançado em novembro de 2017_

### <a name="a-new-entity-collection-named-current-user-is-limited-to-currently-active-user-data----1544273---"></a>A nova coleção de entidades denominada Utilizador Atual está limitada aos dados dos utilizadores atualmente ativos <!-- 1544273 -->

A coleção de entidades **Utilizadores** contém todos os utilizadores do Azure Active Directory (Azure AD) com licenças atribuídas na empresa. Estes registos incluem estados do utilizador durante o período de recolha dos dados, mesmo que o utilizador tenha sido removido. Por exemplo, um utilizador pode ser adicionado ao Intune e, em seguida, removido no decorrer do mês anterior. Apesar de este utilizador não estar presente no momento do relatório, o utilizador e o estado estão presentes nos dados. Pode criar um relatório que mostrará a duração da presença no histórico do utilizador nos seus dados.

Em contrapartida, a nova coleção de entidades **Utilizador Atual** contém apenas os utilizadores que não foram removidos. A coleção de entidades **Utilizador Atual** contém apenas os utilizadores atualmente ativos. Para obter informações sobre a coleção de entidades **Utilizador Atual**, veja [Reference for current user entity (Referência para a entidade utilizador atual)](reports-ref-data-model.md).

## <a name="1709"></a>1709
_Lançamento em outubro de 2017_

### <a name="user-device-association-entity-collection-added-to-intune-data-warehouse-data-model----1187917---"></a>Recolha de entidades de associação de dispositivos de utilizador adicionada ao modelo de dados intune Data Warehouse <!-- 1187917 -->

Agora pode criar relatórios e visualizações de dados com as informações de associação de dispositivos do utilizador que associam o utilizador às coleções de dispositivos de entidades. Pode aceder ao modelo de dados através do ficheiro do Power BI (PBIX) obtido na página do Intune do Armazém de Dados, através do ponto final do OData ou ao desenvolver um cliente personalizado. Para obter mais informações, veja a [Associação de Dispositivos do Utilizador](reports-ref-user-device.md).

### <a name="new-entities-in-the-in-data-warehouse-data-model----1479526--------"></a>Novas entidades no modelo de dados data Warehouse <!-- 1479526 --><!-- -->

- A entidade [**UserDeviceAssociation**](reports-ref-user-device.md) foi adicionada. A entidade **UserDeviceAssociation** contém associações de dispositivos do utilizador na sua organização. Agora pode criar relatórios e visualizações de dados com as informações de associação de dispositivos do utilizador que associam o utilizador às coleções de dispositivos de entidades.  
- A entidade [**IntuneManagementExtension**](reports-ref-intunemanagementextension.md) foi adicionada. **IntuneManagementExtension** contém entidades para dispositivos móveis que controlam informações como o estado da versão e da instalação.

## <a name="next-steps"></a>Próximos passos
- Saiba [o que há de novo a cada semana em Intune.](../fundamentals/whats-new.md) Também pode descobrir quais são as alterações futuras, os avisos importantes sobre o serviço e as informações sobre versões anteriores.
- Leia o [Blogue do Microsoft Intune](https://go.microsoft.com/fwlink/?LinkID=273882).
