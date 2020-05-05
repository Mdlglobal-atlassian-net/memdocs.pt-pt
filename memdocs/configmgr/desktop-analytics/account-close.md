---
title: Como fechar a sua conta
titleSuffix: Configuration Manager
description: Como remover desktop Analytics da sua conta Azure
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722523"
---
# <a name="how-to-close-your-account"></a>Como fechar a sua conta

Se configurar o Desktop Analytics no seu ambiente e, em seguida, decidir que precisa removê-lo, use este processo para fechar a sua conta.

## <a name="prerequisites"></a>Pré-requisitos

Apenas um **Administrador Global** pode fechar ou reativar a conta no portal Azure.

## <a name="process-to-offboard"></a>Processo para offboard

1. Abra o [portal Desktop Analytics](https://aka.ms/desktopanalytics) na Microsoft 365 Device Management como utilizador com a função de Administrador **Global.**

1. No menu **Definições Globais,** selecione **Serviços Conectados**. Na secção de dispositivos de inscrição, selecione a opção **offboard**.

1. Se decidir continuar, a sua conta está fechada.

> [!Important]
> Continue com o resto deste artigo após 90 dias, ou se não reativar.
>
> Se quiser fechar completamente a sua conta sem esperar 90 dias, [reponha](account-reset.md) primeiro a sua conta.

## <a name="reactivate"></a>Reativar

Durante os próximos 90 dias, qualquer administrador da sua organização que aceda ao portal Desktop Analytics verá um aviso de que optou por offboard.

Um administrador global pode reativar a conta dentro de 90 dias. Para restaurar o Desktop Analytics para a sua organização, selecione a opção de **me levar**de volta .

## <a name="delete-the-solution"></a>Eliminar a solução

> [!Warning]
> Continue com o resto deste artigo após 90 dias, ou se não reativar. Se apagar e desligar estes outros componentes, não tente reativar.

1. Inscreva-se no [portal Azure](https://portal.azure.com) como utilizador com o papel de **administrador global.**

1. Procure em **Todos os recursos** o nome do seu espaço de trabalho Desktop Analytics. Este nome é o que criou ao inscrever-se para o serviço.

1. Eliminar `Microsoft365Analytics(YourWorkspaceName)` do tipo **Solução**.

Os dados do Desktop Analytics envelhecem com base na sua política de retenção de dados para o espaço de trabalho. Pode continuar a utilizar quaisquer outras soluções no mesmo espaço de trabalho.

> [!Important]  
> Se estiver a utilizar o espaço de trabalho log Analytics com outras soluções, não elimine o espaço de trabalho.

## <a name="remove-user-and-app-access"></a>Remover o acesso ao utilizador e à aplicação

1. Inscreva-se no [portal Azure](https://portal.azure.com) como utilizador com o papel de **administrador global.** Vá ao **Diretório Ativo Azure.**

1. Em **Funções e administradores,** procure o papel de administrador do **Desktop Analytics.** Retire os seus membros.

1. Em **Grupos,** remova os membros dos seguintes grupos:

    - **Administradores de clientes de Análise M365 (Proprietários de Log Analytics)**
    - **M365 Analytics Client Admins (Log Analytics Contributors)**

1. Nas **aplicações da Enterprise,** elimine ou revogue as permissões de acesso para as seguintes aplicações:

    - `MaLogAnalyticsReader`

    - A aplicação ConfigMgr. Para encontrar o nome desta aplicação, vá à consola Do Gestor de Configuração. No espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** Abra as propriedades do serviço **Desktop Analytics** e mude para o separador **Aplicações.** A **aplicação Web** é esta aplicação Azure.

        > [!Important]  
        > Antes de efazer alterações nesta aplicação em Azure AD, certifique-se de que não a está a reutilizar com outro serviço no Gestor de Configuração.

## <a name="disconnect-configuration-manager"></a>Gestor de configuração de desconexão

1. Abra a consola 'Gestor de Configuração' como utilizador com a função **de administrador completo.**

1. Vá ao espaço de trabalho da **Administração,** expanda os **Serviços cloud,** e selecione o nó dos **Serviços Azure.**

1. Elimine o serviço Desktop Analytics.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Eliminar coleções para as implantações piloto e de produção

1. Na consola 'Gestor de Configuração', selecione **Coleções de Dispositivos** no espaço de trabalho **De Ativos e Conformidade.**

1. Elimine todas as coleções que já não estiver a utilizar. Por predefinição, as coleções estão localizadas sob a pasta Planos de **Implantação.**  

## <a name="reconfigure-clients"></a>Reconfigurar clientes

### <a name="unenroll-devices"></a>Dispositivos de desinscrição

Nos dispositivos matriculados, remova o valor CommercialID das seguintes teclas do Registo windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuração de dados de diagnóstico do Windows

Se não quiser que os seus dispositivos continuem a enviar dados de diagnóstico:

- Windows 10: definir o nível de dados de diagnóstico para **A Segurança**
- Windows 7 SP1 ou 8.1: desativar a **chave de opt-in de dados comerciais**

Desdefinir estes valores utilizando um dos seguintes métodos:

- Política de grupo, na **configuração de computador modelos** > **administrativos** > De recolha de dados de componentes > **windows**e**visualizações**
- Gestão de dispositivos móveis (MDM), como [o Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para mais informações, consulte [configure dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Quando aplica estas alterações, os dispositivos deixam imediatamente de enviar dados de diagnóstico. Pode levar 24 a 48 horas para a Microsoft parar de processar insights para o seu espaço de trabalho. A Microsoft elimina estes dados dos seus serviços na nuvem dentro de 30 dias ou menos.
