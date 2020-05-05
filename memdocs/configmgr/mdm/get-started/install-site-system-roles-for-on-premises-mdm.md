---
title: Instalar funções para o MDM no local
titleSuffix: Configuration Manager
description: Instale as funções necessárias do sistema de site para a gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721858"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Instale funções do sistema do site para o MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração no local de gestão de dispositivos móveis (MDM) requer as seguintes funções do sistema do site no site do Gestor de Configuração:

- Ponto de inscrição

- Ponto proxy de registo

- Ponto de distribuição

- Ponto de gestão de dispositivos, que é um ponto de gestão que permite para dispositivos móveis

## <a name="requirements-and-limitations"></a>Requisitos e limitações

- No local, o MDM requer que ative as funções do sistema do site para comunicações HTTPS. Para obter mais informações, consulte [A configuração de certificados para comunicações fidedignas no MDM](set-up-certificates-on-premises-mdm.md)no local .

- O atual ramo do Gestor de Configuração apenas suporta ligações *intranet* de dispositivos aos pontos de distribuição e pontos de gestão de dispositivos para o MDM no local. No entanto, se também gere computadores macOS, esses clientes necessitam de ligações à *Internet* para essas mesmas funções. Quando configurar o ponto de distribuição e o ponto de gestão do dispositivo, utilize a opção de **permitir ligações intranet e internet.**

- Os pontos de distribuição que configura para ligações intranet exigem que configure os limites do site para eles. O Gestor de Configuração apenas suporta os limites de gama IPv4 para o MDM no local. Para mais informações, consulte Definir os limites do [site e os grupos de fronteira.](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)

- Se utilizar [réplicas](../../core/servers/deploy/configure/database-replicas-for-management-points.md) de base de dados com o ponto de gestão do dispositivo, os dispositivos recém-inscritos não conseguirão inicialmente ligar-se. Esta falha de ligação ocorre porque a réplica da base de dados não tem a informação sobre o dispositivo recém-matriculado necessário para uma ligação bem sucedida. As réplicas sincronizam a cada cinco minutos. Os dispositivos não se ligarão durante os primeiros cinco minutos após a inscrição, que normalmente são duas tentativas de ligação. Em seguida, os dispositivos ligar-se-ão com sucesso.

## <a name="add-roles"></a>Adicionar funções

Se estiver a adicionar MDM no local a um site que tem a maioria dos dispositivos geridos com o cliente do Gestor de Configuração, pode já ter algumas destas funções instaladas no site. Por exemplo, o ponto de distribuição é uma função comum, e o ponto de gestão do dispositivo é necessário para gerir dispositivos macOS.

Para obter mais informações sobre como adicionar funções ao seu site, consulte [adicionar funções](../../core/servers/deploy/configure/install-site-system-roles.md)do sistema do site .

## <a name="configure-roles"></a>Configurar funções

Configure funções novas ou existentes para gerir dispositivos móveis. Siga os passos abaixo para configurar o ponto de distribuição e o ponto de gestão do dispositivo para funcionar corretamente para o MDM no local:

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione o nó de Funções de **Servidores e Derôs.**

1. Selecione o servidor do sistema do site com o ponto de distribuição ou ponto de gestão do dispositivo que pretende configurar. Selecione o servidor na lista e, em seguida, selecione a função do **sistema do Site** no painel de detalhes do Sistema do Site. Na fita, no separador **Role site,** selecione **Propriedades**.

    > [!TIP]
    > Num grande site, pode consultar a vista apenas para mostrar servidores com funções específicas. Quando selecionar o nó de Funções de **Servidores e Derpor funções,** na fita, na etiqueta Home, selecione **Servidores com Função**. Em seguida, selecione o papel que deseja da lista de funções atualmente disponíveis no site.

    No separador **Geral** das propriedades do **sistema do Site,** certifique-se de que o **Nome** é um nome de domínio totalmente qualificado (FQDN). Feche as propriedades.

1. Na lista de consolas, selecione um servidor com uma função de ponto de distribuição no local. Selecione a função do **ponto de distribuição** no painel de detalhes do sistema do site. Na fita, no separador **Role site,** selecione **Propriedades**. No separador de **comunicação** do ponto de **distribuição Propriedades:**

    1. Selecione **HTTPS**, e selecione **Permitir ligações apenas intranet**.

        > [!IMPORTANT]
        > Se também estiver a gerir computadores macOS com o cliente Do Gestor de Configuração, utilize **ligações intranet e internet.**

    1. Ative a opção de **permitir que os dispositivos móveis se conectem a este ponto**de distribuição e, em seguida, fechem as propriedades.

1. Propriedades abertas para a função do sistema de site de **ponto de gestão.**

    1. No separador **Geral,** selecione **HTTPS**, e selecione **Permitir ligações apenas intranet**.

        > [!IMPORTANT]
        > Se também estiver a gerir computadores macOS com o cliente Do Gestor de Configuração, utilize **ligações intranet e internet.**

    1. Ative a opção de **permitir que dispositivos móveis e Computador Mac utilizem este ponto de gestão**e, em seguida, feche minhá-lo.

        > [!NOTE]
        > Esta opção transforma efetivamente o ponto de gestão num ponto de gestão de *dispositivos.*  

## <a name="next-step"></a>Passo seguinte

Depois de adicionar e configurar as funções para a gestão de dispositivos móveis, configure os servidores como pontos finais fidedignos. Esta confiança permite que as funções comuniquem e matriculem dispositivos geridos.

> [!div class="nextstepaction"]
> [Configurar certificados para comunicações fidedignas](set-up-certificates-on-premises-mdm.md)
