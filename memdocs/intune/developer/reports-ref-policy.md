---
title: Referência para as entidades de políticas
titleSuffix: Microsoft Intune
description: Tópico de referência para a categoria Policy das coleções de entidades na API do Armazém de Dados do Intune.
keywords: Armazém de Dados do Intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/03/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a2f13bddb852b46459c9c79df39dda49ef9549d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325581"
---
# <a name="reference-for-policy-entities"></a>Referência para as entidades de políticas

A categoria **de políticas** contém entidades para dispositivos móveis que acompanham informações como:

- Inventário de perfis de configuração de dispositivos, perfis de configuração de aplicações e políticas de conformidade  
- Número de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia  
- Número de utilizadores no estado com êxito, pendente, com falhas ou com erros por dia  
- Número cumulativo de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia  

## <a name="policies"></a>políticas

A entidade **política** lista perfis de configuração do dispositivo, perfis de configuração de aplicações e políticas de conformidade. Pode atribuir as políticas com a Gestão de Dispositivos Móveis (MDM) a um grupo na sua empresa.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| políticaChave |Chave exclusiva para representar a política no armazém de dados. |123 |
| políticaId |Identificador exclusivo da Política no armazém de dados. |b66bc706-ffff-7437-0340-032819502773 |
| nome político |Nome da Política. |"Linha de Base do Windows 10" |
| políticaVersão |Versão da Política. Quando a política é editada ou alterada, é criada uma versão mais recente. |1, 2, 3 |
| isDeleted |Indica se o registo da Política foi atualizado.  <br>True – a política tem um novo registo com campos atualizados. <br>False – o registo mais recente da política. |True/False |
| startDateInclusiveUTC |Data e hora em UTC em que a política foi criada no armazém de dados. |11/23/2016 12:00:00 AM |
| eliminadoDateUTC |Data e hora em UTC em que a propriedade IsDeleted foi alterada para True. |11/23/2016 12:00:00 AM |
| rowLastModificadoDateTimeUTC |Data e hora em UTC em que a política foi modificada pela última vez no armazém de dados. |11/23/2016 12:00:00 AM |

## <a name="policytypes"></a>policyTypes

A entidade **policyType** lista tipos de perfis de configuração do dispositivo, perfis de configuração de aplicações e políticas de conformidade. Pode atribuir as políticas com a Gestão de Dispositivos Móveis (MDM) a um grupo na sua empresa.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| políticaTypeId |Identificador exclusivo da política no sistema de origem. |123 |
| políticaTypeKey |Identificador exclusivo da política no armazém de dados. |1 |
| políticaTypeName |Nome do tipo de política. |Política de Conformidade do Windows 10. |

## <a name="device-configuration"></a>Configuração do Dispositivo

A entidade **deviceConfigurationProfileDeviceActivity** lista o número de **dispositivos** no estado de erro bem sucedido, pendente, falhado ou erro por dia. O número reflete os Perfis de configuração de dispositivos atribuídos à entidade. Por exemplo, se um **dispositivo** estiver no estado de sucesso para todas as suas políticas atribuídas, ele incrementa o contador sucedido para esse dia. Se um dispositivo tiver dois perfis atribuídos, um no estado com êxito e outro num estado com erros, a entidade incrementa o contador do estado com êxito (Succeeded) e coloca o dispositivo no estado com erros. A entidade apresenta uma lista de quantos dispositivos estão em cada um dos estados num determinado dia nos últimos 30 dias.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| dateKey |Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. |20160703 |
| pendente |Número de Dispositivos exclusivos no estado pendente. |123 |
| com êxito |Número de Dispositivos exclusivos no estado com êxito. |12 |
| erro |Número de Dispositivos exclusivos no estado com erros. |10 |
| sem êxito |Número de Dispositivos exclusivos no estado com falhas. |2 |

A entidade **do dispositivoConfigurationProfileUserActivity** lista o número de **utilizadores** no estado de erro bem sucedido, pendente, falhado ou erro por dia. O número reflete os Perfis de configuração de dispositivos atribuídos à entidade. Por exemplo, se um **utilizador** estiver no estado de sucesso para todas as suas políticas atribuídas, ele sobe o contador sucedido por um para esse dia. Se um utilizador tiver dois perfis atribuídos, um no estado com êxito e outro no estado com erros, é contado o utilizador no estado com erros.  A entidade **do dispositivoConfigurationProfileUserActivity** lista quantos utilizadores estão em que o estado num determinado dia ao longo dos últimos 30 dias.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| dateKey |Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. |20160703 |
| pendente |Número de Utilizadores exclusivos no estado pendente. |123 |
| com êxito |Número de Utilizadores exclusivos no estado com êxito. |12 |
| erro |Número de Utilizadores exclusivos no estado com erros. |10 |
| sem êxito |Número de Utilizadores exclusivos no estado com falhas. |2 |

## <a name="policytypeactivities"></a>policyTypeActivities

A entidade **policyTypeActivity** lista o número acumulado de dispositivos no estado de erro, pendente, falhado ou errado. Apresenta uma lista destes estados relativamente a um perfil de configuração de dispositivo, perfil de configuração de aplicação ou política de conformidade por dia.

| Propriedade  | Descrição | Exemplo |
|---------|------------|--------|
| dateKey |dataChave quando o check-in de perfil de configuração do dispositivo foi registado no armazém de dados. |20160703 |
| políticaChave |policyKey, pode ser associado com a política para obter o nome de política. |Linha de base do Windows 10 |
| políticaTypeKey |O tipo de Chave de Política pode ser acompanhado do Tipo de Política para obter o nome do tipo de política. |Política de Compatibilidade do Windows 10 |
| pendente |Número de dispositivos exclusivos no estado pendente. |123 |
| com êxito |Número de dispositivos exclusivos no estado com êxito. |12 |
| erro |Número de dispositivos exclusivos no estado com erros. |10 |
| sem êxito |Número de dispositivos exclusivos no estado com falhas. |2 |

## <a name="compliance-policy"></a>Política de Conformidade

A Referência da API de Políticas de Conformidade contém entidades que fornecem informações de estado sobre as políticas de conformidade atribuídas a dispositivos.

### <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities

A tabela seguinte apresenta um resumo dos estados de atribuição de políticas de conformidade a dispositivos. Esta tabela indica a contagem de dispositivos detetados em cada estado de conformidade.


|Propriedade     |Descrição  |Exemplo  |
|---------|---------|---------|
|dateKey  |Chave da data em que o resumo da política de conformidade foi criado.|20161204 |
|desconhecido  |Número de dispositivos que estão offline ou que não conseguiram comunicar com o Intune ou o Azure AD por outros motivos. |5|
|não Aplicável      |Número de dispositivos em que as políticas de conformidade visadas pelo administrador não são aplicáveis.|201 |
|conforme      |Número de dispositivos que aplicaram com êxito uma ou mais políticas de conformidade do dispositivo visadas pelo administrador. |4083 |
|inGracePeriod      |Número de dispositivos que não estão em conformidade, embora se encontrem no período de tolerância definido pelo administrador. |57|
|não Conforme      |Número de dispositivos que não conseguiram aplicar uma ou mais definições de políticas de conformidade do dispositivo visadas pelo administrador ou nos quais o utilizador ainda não está a cumprir as políticas visadas pelo administrador.|43 |
|erro      |Número de dispositivos que não conseguiram comunicar com o Intune ou o Azure AD e devolveram uma mensagem de erro. |3|

### <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities 

A tabela seguinte apresenta um resumo dos estados de atribuição de políticas de conformidade a dispositivos por política e por tipo de política. Esta tabela indica a contagem de dispositivos detetados em cada estado de conformidade para todas as políticas de conformidade atribuídas.



|Propriedade  |Descrição  |Exemplo  |
|---------|---------|---------|
|dateKey  |Chave da data em que o resumo da política de conformidade foi criado.|20161219|
|políticaChave     |Chave da política de conformidade para a qual o resumo foi criado. |10178 |
|policyPlatformKey      |Chave do tipo de plataforma da política de conformidade para a qual o resumo foi criado.|5|
|desconhecido     |Número de dispositivos que estão offline ou que não conseguiram comunicar com o Intune ou o Azure AD por outros motivos.|13|
|não Aplicável     |Número de dispositivos em que as políticas de conformidade visadas pelo administrador não são aplicáveis.|3|
|conforme      |Número de dispositivos que aplicaram com êxito uma ou mais políticas de conformidade do dispositivo visadas pelo administrador. |45|
|inGracePeriod      |Número de dispositivos que não estão em conformidade, embora se encontrem no período de tolerância definido pelo administrador. |3|
|não Conforme      |Número de dispositivos que não conseguiram aplicar uma ou mais definições de políticas de conformidade do dispositivo visadas pelo administrador ou nos quais o utilizador ainda não está a cumprir as políticas visadas pelo administrador.|7|
|erro      |Número de dispositivos que não conseguiram comunicar com o Intune ou o Azure AD e devolveram uma mensagem de erro. |3|

### <a name="policyplatformtypes"></a>policyPlatformTypes

A tabela seguinte contém os tipos de plataforma de todas as políticas atribuídas. Os tipos de plataforma das políticas que nunca foram atribuídos a um dispositivo não são apresentados nesta tabela.


|Propriedade  |Descrição  |Exemplo  |
|---------|---------|---------|
|policyPlatformTypeKey      |A chave exclusiva do tipo de plataforma da política. |20170519 |
|policyPlatformTypeId      |O identificador exclusivo do tipo de plataforma da política.|1|
|policyPlatformTypeName      |O nome do tipo de plataforma da política.|AndroidForWork |

### <a name="policydeviceactivities"></a>policyDeviceActivities

A tabela seguinte mostra o número de dispositivos no estado com êxito, pendente, com falhas ou com erros por dia. O número apresentado reflete os perfis de dados por Tipo de Política. Por exemplo, se um dispositivo estiver no estado com êxito em todas as políticas atribuídas, o contador de casos com êxito tem um incremento de um para esse dia. Se um dispositivo tiver dois perfis atribuídos, um no estado com êxito e outro num estado com erros, a entidade incrementa o contador do estado com êxito (Succeeded) e coloca o dispositivo no estado com erros. A entidade policyDeviceActivity lista quantos dispositivos estão em que estado num determinado dia ao longo dos últimos 30 dias.

|Propriedade  |Descrição  |Exemplo  |
|---------|---------|---------|
|dateKey|Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados.|20160703|
|pendente|Número de Dispositivos exclusivos no estado pendente.|123|
|Succeeded|Número de Dispositivos exclusivos no estado com êxito.|12|
|políticaChave|policyKey, pode ser associado com a política para obter o nome de política.|Linha de base do Windows 10|
|erro|Número de Dispositivos exclusivos no estado com erros.|10|
|sem êxito|Número de Dispositivos exclusivos no estado com falhas.|2|

### <a name="policyuseractivities"></a>policyUserActivities

A tabela seguinte mostra o número de utilizadores no estado com êxito, pendente, com falhas ou com erros por dia. O número apresentado reflete os perfis de dados por Tipo de Política. Por exemplo, se um utilizador estiver no estado com êxito em todas as políticas atribuídas, sobe o contador com êxito em um para esse dia. Se um utilizador tiver dois perfis atribuídos, um no estado com êxito e outro no estado com erros, é contado o utilizador no estado com erros. A entidade PolicyUserActivity apresenta uma lista de quantos utilizadores estão em cada um dos estados num determinado dia nos últimos 30 dias.


| Propriedade  |                                         Descrição                                         |       Exemplo       |
|-----------|---------------------------------------------------------------------------------------------|---------------------|
|  dateKey  | Data-chave de quando a entrada do Perfil de Configuração do Dispositivo foi registada no armazém de dados. |      20160703       |
|  pendente  |                         Número de Dispositivos exclusivos no estado pendente.                          |         123         |
| com êxito |                         Número de Dispositivos exclusivos no estado com êxito.                          |         12          |
| políticaChave |                 policyKey, pode ser associado com a política para obter o nome de política.                 | Linha de base do Windows 10 |
|   erro   |                          Número de Dispositivos exclusivos no estado com erros.                           |         10          |

