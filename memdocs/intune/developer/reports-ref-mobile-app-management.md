---
title: Gestão de Aplicações Móveis (MAM)
titleSuffix: Microsoft Intune
description: Tópico de referência para a categoria Mobile App Management das coleções de entidades na API do Armazém de Dados do Intune.
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
ms.assetid: 084F11AD-F7BA-45A4-8424-45E6E4564930
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 428ee1ce93b4f6fe21c4b0180a9df222f3e23e09
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331685"
---
# <a name="reference-for-mobile-app-management-mam-entities"></a>Referência para as entidades de gestão de aplicações móveis (MAM)

A categoria **Mobile App Management** contém entidades para aplicações móveis como:

- Aplicações
- Instâncias
- Estado de entrada
- Estado de funcionamento
- Estado de política
- Estado de inscrição
- Tipos de plataforma

## <a name="mamapplications"></a>mamAplicações

A entidade **mamApplication** lista aplicações Line-of-Business (LOB) que são geridas através da Mobile Application Management (MAM) sem inscrição na sua empresa.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| mamApplicationKey |Identificador único da aplicação MAM. | 432 |
| mamApplicationName |Nome da aplicação MAM. |Nome da exemplo da aplicação MAM |
| mamApplicationId |Identificação de aplicação do pedido MAM. | 123 |
| isDeleted |Indica se este registo da aplicação MAM foi atualizado. <br>True: a aplicação MAM tem um novo registo com campos atualizados nesta tabela. <br>False: o registo mais recente desta aplicação MAM. |True/False |
| startDateInclusiveUTC |Data e hora em UTC em que esta aplicação MAM foi criada no armazém de dados. |11/23/2016 12:00:00 AM |
| eliminadoDateUTC |Data e hora em UTC em que a propriedade IsDeleted foi alterada para True. |11/23/2016 12:00:00 AM |
| rowLastModificadoDateTimeUTC |Data e hora em UTC em que esta aplicação MAM foi modificada pela última vez no armazém de dados. |11/23/2016 12:00:00 AM |


## <a name="mamapplicationinstances"></a>mamApplicationCasos

A entidade **mamApplicationInstance** lista aplicações geridas pela Mobile Application Management (MAM) como instâncias singulares por utilizador por dispositivo. Todos os utilizadores e dispositivos listados na entidade estão protegidos, ou seja, têm pelo menos uma Política de MAM atribuída.


|          Propriedade          |                                                                                                  Descrição                                                                                                  |               Exemplo                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   aplicaçãoCasoChave   |                                                               Identificador exclusivo de instância da aplicação MAM no armazém de dados – chave de substituição.                                                                |                 123                  |
|           userId           |                                                                              Id do utilizador do utilizador que tem esta aplicação MAM instalada.                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   aplicaçãoInstanceId    |                                              Identificador exclusivo de instância da aplicação MAM, semelhante à propriedade ApplicationInstanceKey, apesar de o identificador ser uma chave natural.                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | Identificação de aplicação do pedido mam para o qual esta Instância de Aplicação Mam foi criada.   | 11/23/2016 12:00:00 AM   |
|     applicationVersion     |                                                                                     Versão desta aplicação MAM.                                                                                      |                  2                   |
|        criadoData         |                                                                 Data em que este registo da instância da aplicação MAM foi criado. O valor pode ser nulo.                                                                 |        11/23/2016 12:00:00 AM        |
|          Plataforma          |                                                                          Plataforma do dispositivo no qual esta aplicação MAM está instalada.                                                                           |                  2                   |
|      plataformaVersão       |                                                                      Versão de plataforma do dispositivo no qual esta aplicação MAM está instalada.                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            A versão de SDK MAM com a qual esta aplicação MAM foi encapsulada.                                                                            |                 3.2                  |
| mamDeviceId | Identificação do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
| mamDeviceType | Tipo de dispositivo do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
| mamDeviceName | Nome do dispositivo com o qual a MAM Application Instance está associada.   | 11/23/2016 12:00:00 AM   |
|         isDeleted          | Indica se este registo de instância da aplicação MAM foi atualizado. <br>True: esta instância de aplicação MAM tem um novo registo com campos atualizados nesta tabela. <br>False: o registo mais recente desta instância da aplicação MAM. |              True/False              |
|   startDateInclusiveUtc    |                                                              Data e hora em UTC em que esta instância da aplicação MAM foi criada no armazém de dados.                                                               |        11/23/2016 12:00:00 AM        |
|       eliminadoDateUtc       |                                                                             Data e hora em UTC em que a propriedade IsDeleted foi alterada para True.                                                                              |        11/23/2016 12:00:00 AM        |
| rowLastModificadoDateTimeUtc |                                                           Data e hora em UTC em que esta instância da aplicação MAM foi modificada pela última vez no armazém de dados.                                                            |        11/23/2016 12:00:00 AM        |


## <a name="mamcheckins"></a>MamCheckins

A entidade **mamCheckin** representa os dados recolhidos quando uma instância de aplicação de aplicação móvel (MAM) fez o check-in com o Serviço Intune. 

> [!Note]  
> Quando uma instância de aplicação dá entrada várias vezes por dia, o armazém de dados armazena-a como uma entrada única.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| dateKey |Chave da data quando a entrada da aplicação MAM foi registada no armazém de dados. | 20160703 |
| aplicaçãoCasoChave |Chave da instância da aplicação associada a esta entrada da aplicação MAM. | 123 |
| userKey |Chave do utilizador associado a esta entrada da aplicação MAM. | 4323 |
| mamApplicationKey |Chave de aplicação associada ao check-in da aplicação MAM. | 432 |
| dispositivoHealthKey |Chave de DeviceHealth associada a esta entrada da aplicação MAM. | 321 |
| plataformaChave |Representa a plataforma do dispositivo associado a esta entrada da aplicação MAM. |123 |
| eficazAppliedPolicyKey |Representa a política aplicada em vigor associada à aplicação MAM que deu entrada. Uma política aplicada em vigor resulta da união de todas as políticas relevantes para um utilizador e uma aplicação específicos. | 322 |
| pastCheckInDate |Data e hora em que esta aplicação MAM deu entrada pela última vez. O valor pode ser nulo. |11/23/2016 12:00:00 AM |


## <a name="mamdevicehealth"></a>mamDeviceHealth

A entidade **mamDeviceHealth** representa dispositivos que têm políticas de Gestão de Aplicações Móveis (MAM) implantadas para eles mesmo que sejam jailbrokens.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| dispositivoHealthKey |Identificador exclusivo do dispositivo e respetivo estado de funcionamento associado no armazém de dados – chave de substituição. |123 |
| deviceHealth |Identificador exclusivo do dispositivo e respetivo estado de funcionamento associado, semelhante a DeviceHealthKey, mas o identificador é uma chave natural. |b66bc706-ffff-7777-0340-032819502773 |
| dispositivoHealthName |Representa o estado do dispositivo. <br>Not available: não existem informações sobre este dispositivo. <br>Healthy: o dispositivo não foi desbloqueado por jailbreak. <br>Unhealthy: o dispositivo foi desbloqueado por jailbreak. |Not Available Healthy Unhealthy |
| rowLastModificadoDateTimeUtc |Data e hora em UTC em que o Estado de Funcionamento deste Dispositivo MAM específico foi modificado pela última vez no armazém de dados. |11/23/2016 12:00:00 AM |

## <a name="mameffectivepolicies"></a>mamEfetivações eficazes

A entidade **mamEffectivePolicy** lista todas as políticas eficazes de Gestão de Aplicações Móveis (MAM) aplicadas na sua organização. Uma política aplicada em vigor resulta da união de todas as políticas relevantes para um utilizador e uma aplicação específicos.

| Propriedade | Descrição | Exemplo |
|---------|------------|--------|
| eficazPolicyKey |Identificador exclusivo da política em vigor de MAM no armazém de dados. |2 |
| realPolicyKey |Identificador exclusivo da política de MAM criada pelo Profissional de TI. |1 |
| linhaCreatedDateTimeUtc |Data e hora em UTC em que esta política em vigor de MAM foi criada no armazém de dados. |11/23/2016 12:00:00 AM |

## <a name="mamplatforms"></a>MamPlatforms

A entidade **mamPlatform** lista os nomes e tipos da plataforma em que foi instalada uma aplicação de Gestão de Aplicações Móveis (MAM).


|          Propriedade          |                                    Descrição                                    |                         Exemplo                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        plataformaChave         |     Identificador exclusivo da plataforma no armazém de dados – chave de substituição.      |                           123                           |
|          Plataforma          | Identificador exclusivo da plataforma, semelhante a PlatformKey, mas é uma chave natural. |                           123                           |
|        plataformaNome        |                                   Nome da plataforma                                   | Não disponível <br>Nenhum <br>Portal do <br>iOS <br>Android. |
| rowLastModificadoDateTimeUtc | Data e hora em UTC em que esta plataforma foi modificada pela última vez no armazém de dados.  |                 11/23/2016 12:00:00 AM                  |

