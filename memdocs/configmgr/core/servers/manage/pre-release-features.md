---
title: Funcionalidades de pré-lançamento
titleSuffix: Configuration Manager
description: As funcionalidades de pré-lançamento são características que estão no ramo atual para testes precoces em ambiente de produção.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720157"
---
# <a name="pre-release-features-in-configuration-manager"></a>Funcionalidades de pré-lançamento no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

As funcionalidades de pré-lançamento são características que estão no ramo atual para testes precoces em ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda em desenvolvimento ativo. Podem receber alterações até saírem da categoria de pré-lançamento.

## <a name="give-consent"></a>Dar consentimento  

Antes de utilizar as funcionalidades de pré-lançamento, dê o seu consentimento para utilizar as funcionalidades de pré-lançamento. Dar consentimento é uma ação única por hierarquia que não se pode desfazer. Até que dê o seu consentimento, não pode ativar novas funcionalidades de pré-lançamento incluídas em atualizações. Depois de ligar um recurso de pré-lançamento, não pode desligá-lo.

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Clique em **Definições de Hierarquia** na fita.  

3. No separador **Geral** das Definições da Hierarquia Propriedades, ative a opção de **Consentimento para utilizar as funcionalidades de pré-lançamento**. Clique em **OK**.  

## <a name="enable-pre-release-features"></a>Ativar funcionalidades de pré-lançamento

Quando instala uma atualização que inclui funcionalidades de pré-lançamento, estas funcionalidades são visíveis nas Atualizações e no Assistente de Manutenção com as funcionalidades regulares incluídas na atualização.

### <a name="if-you-have-given-consent"></a>Se tiver dado consentimento

Nas atualizações e no Assistente de Manutenção, ative as funcionalidades de pré-lançamento. Selecione as funcionalidades de pré-lançamento como qualquer outra funcionalidade.

Opcionalmente, aguarde para ativar as funcionalidades de pré-lançamento mais tarde a partir do nó **De características** em **Atualizações e Manutenção** no espaço de trabalho da **Administração.** Selecione uma funcionalidade e, em seguida, clique **em ligar** na fita. Até que dê o seu consentimento, esta opção não está disponível para uso.

### <a name="if-you-havent-given-consent"></a>Se não deu consentimento

Nas Atualizações e assistentes de manutenção, as funcionalidades de pré-lançamento são visíveis, mas não é possível permitir. Após a instalação da atualização, estas funcionalidades são visíveis no nó **De Características.** No entanto, não pode permitir até que dê o seu consentimento.

> [!IMPORTANT]  
> Numa hierarquia multi-site, só é possível ativar funcionalidades opcionais ou pré-lançamento a partir do site da administração central. Este comportamento garante que não há conflitos em toda a hierarquia. <!--507197-->  
>
> Se deu consentimento num local primário autónomo e, em seguida, expandir a hierarquia instalando um novo site de administração central, deve dar o seu consentimento novamente no site da administração central.  

Quando ativa uma funcionalidade de pré-lançamento, o gestor de hierarquia do Gestor de Configuração (HMAN) deve processar a alteração antes que essa funcionalidade fique disponível. O processamento da mudança é muitas vezes imediato. Dependendo do ciclo de processamento de HMAN, pode levar até 30 minutos para ser concluído. Depois de processada a alteração, reinicie a consola antes de utilizar a funcionalidade.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Lista de funcionalidades de pré-lançamento

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Funcionalidade          | Adicionado como pré-lançamento | Adicionado como uma característica completa |
|------------------|----------------------|-------------------------|
| [Grupos de orquestração](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Versão 2002 | ![Ainda não](media/red_x.png) |
| [Tipo de implantação da sequência de tarefas](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Versão 2002 | ![Ainda não](media/red_x.png) |
| [Remova o site da administração central](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Versão 2002 | ![Ainda não](media/red_x.png) |
| [Debugger de sequência de tarefas](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Versão 1906 | ![Ainda não](media/red_x.png) |
| [Grupos de candidatura](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Versão 1906 | ![Ainda não](media/red_x.png) |
| [Descoberta do grupo de utilizadores do Diretório Ativo Azure](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Versão 1906 | Versão 2002 |
| [Sincronizar os resultados da adesão à coleção para o Azure Ative Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Versão 1906| Versão 2002 |
| [CMPivot autónomo](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Versão 1906 | Versão 2002 |
| [Serviço de administração do SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Versão 1810 | Versão 1906 |
| [Sistema de site HTTP melhorado](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Versão 1806 | Versão 1810 |
| [Aplicativos de clientes para dispositivos cogeridos](../../../comanage/workloads.md#client-apps) <br/> (anteriormente conhecidas como *aplicativos Móveis para dispositivos cogeridos)* <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Versão 1806 | Versão 2002 |
| [Gestor de conversão de pacotes](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Versão 1806 | Versão 1810 |
| [Implementações faseadas](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Versão 1802 | Versão 1806 |
| [Gestão do Controlo de Aplicações do Windows Defender](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Versão 1702 | Versão 1906 |
| [Manutenção de uma coleção consciente do cluster (grupos servidor)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Versão 1602 | ![Ainda não](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Para obter mais informações sobre as funcionalidades não pré-lançamento que deve ativar primeiro, consulte [as funcionalidades opcionais enable a partir de atualizações](install-in-console-updates.md#bkmk_options).  
>
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo técnico de pré-visualização, consulte [A Pré-visualização Técnica](../../get-started/technical-preview.md).  
