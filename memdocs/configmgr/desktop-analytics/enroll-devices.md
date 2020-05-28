---
title: Inscreva dispositivos em Desktop Analytics
titleSuffix: Configuration Manager
description: Saiba como inscrever dispositivos no Desktop Analytics.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 22b5461df3a560449316009471ea029967118f5d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864910"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Como inscrever dispositivos no Desktop Analytics

Quando ligar o Gestor de [Configuração](connect-configmgr.md) ao Desktop Analytics, configura as definições para inscrever dispositivos no Desktop Analytics. Pode alterar estas definições a qualquer momento. Certifique-se também de que os dispositivos estão atualizados.

## <a name="update-devices"></a>Atualizar dispositivos

Desktop Analytics utiliza dois componentes principais do Windows:

- **Componente**de compatibilidade : O componente de compatibilidade **(Appraiser)** executa diagnósticos no dispositivo Windows para avaliar o seu estado de compatibilidade com as versões mais recentes do Windows 10.

- **Serviço de Experiências de Utilizador Conectadoe Telemetria**: Com os dados de diagnóstico do Windows ativados, o serviço de experiência de utilizador conectado e telemetria **(DiagTrack)** recolhe sistema, aplicação e dados do condutor. A Microsoft analisa estes dados e partilha-os através do Desktop Analytics.

Instale a versão mais recente destes componentes para obter a melhor experiência com desktop Analytics.

A tabela seguinte lista as atualizações de cada componente nas versões de SO suportadas:

| Versão do SO | Avaliador | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | <sup> [Nota](#bkmk_note1) incluída 1</sup> | [Última atualização cumulativa](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | <sup> [Nota](#bkmk_note1) incluída 1</sup> | [Última atualização cumulativa](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | <sup> [Nota](#bkmk_note1) incluída 1</sup> | [Última atualização cumulativa](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | <sup> [Nota](#bkmk_note1) incluída 1</sup> | [Última atualização cumulativa](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | <sup> [Nota](#bkmk_note1) incluída 1</sup> | [Última atualização cumulativa](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup> [Nota 2](#bkmk_note2)</sup> | [Última rollup mensal](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup> [Nota 3](#bkmk_note3)</sup> | [Última rollup mensal](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Utilize o Gestor de Configuração para instalar automaticamente estas atualizações. Para mais informações, consulte [a implementação](../sum/deploy-use/deploy-software-updates.md)de atualizações de software .
>
> Reiniciar os dispositivos depois de instalar as atualizações de compatibilidade pela primeira vez.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a>Nota 1: Windows 10

Embora o Windows 10 inclua estes componentes por padrão, os dispositivos do Windows 10 requerem a mais recente atualização cumulativa para obter a funcionalidade completa do Desktop Analytics, como avaliar o dispositivo para compatibilidade com a versão mais recente do SISTEMA.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a>Nota 2: Windows 8.1

A Microsoft aumenta regularmente as atualizações para este componente, mas o número KB associado não muda. Certifique-se de que tem sempre a versão mais recente da atualização.

Este componente executa diagnósticos em sistemas Windows 8.1 que participam no Programa de Melhoria da Experiência do Cliente do Windows. Estes diagnósticos ajudam a determinar se pode ter problemas de compatibilidade ao atualizar para o Windows 10.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a>Nota 3: Windows 7

Se a sua organização não aplicar atualizações "Monthly Quality Rollup" aos dispositivos do Windows 7 e apenas aplicar atualizações "Security Only", encontrará algumas atualizações "Security Only" na [lista de atualizações que superam o KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). Pode instalar estas atualizações mais recentes em vez de KB 2952664.

> [!NOTE]
> Para o Windows 8.1, a Microsoft apenas revê o KB 2976978 como parte das atualizações "Monthly Quality Rollup".

## <a name="device-enrollment"></a>Inscrição de dispositivos

O serviço Desktop Analytics não tem agentes para instalar. A inscrição do dispositivo requer configurações de configuração nos dispositivos que pretende que possa monitorizar. Estas definições controlam a que se encontra o Desktop Analytics, o dispositivo deve enviar os seus dados e outras opções de configuração.

> [!Note]  
> Se utilizou previamente o Windows Analytics, utilize o mesmo espaço de trabalho para desktop Analytics. É necessário reinscrever dispositivos para desktop Analytics que já inscreveu no Windows Analytics.
>
> Você só pode ter um espaço de trabalho desktop Analytics por inquilino Azure AD. Os dispositivos só podem enviar dados de diagnóstico para um espaço de trabalho.  

O Gestor de Configuração proporciona uma experiência integrada para gerir e implementar estas configurações para os clientes. Para obter a melhor experiência, utilize o Gestor de Configuração.

Quando ligar o Gestor de Configuração ao Desktop Analytics, configura as definições para inscrever dispositivos. Para mais informações, consulte [Como ligar o Gestor de Configuração ao Desktop Analytics](connect-configmgr.md#bkmk_connect).

Para alterar estas definições, utilize o seguinte procedimento:

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó dos **Serviços Azure.** Selecione a ligação ao Desktop Analytics e escolha **propriedades** na fita.

2. Na página dados de **diagnóstico,** faça alterações conforme necessário para as seguintes definições:  

    - **ID Comercial**: este valor deve povoar automaticamente com o ID da sua organização. Se não o fizer, certifique-se de que o seu servidor proxy está configurado para permitir todos os [pontos finais necessários](enable-data-sharing.md#endpoints) antes de continuar. Também pode recuperar o seu ID Comercial manualmente a partir do [portal Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Nível de dados de diagnóstico do Windows 10**: Para mais informações, consulte [os níveis de dados de diagnóstico](enable-data-sharing.md#diagnostic-data-levels).  

    - **Permitir o nome do dispositivo nos dados de diagnóstico**: Para mais informações, consulte o nome do [dispositivo](#device-name).  

    Quando efaz alterações nesta página, a página **de funcionalidades Disponíveis** mostra uma pré-visualização da funcionalidade Desktop Analytics com as definições de dados de diagnóstico selecionadas.  

3. Na página de Ligação desktop **Analytics,** faça alterações conforme necessário para as seguintes definições:

    - **Nome do ecrã**: O portal Desktop Analytics apresenta esta ligação de Gestor de Configuração utilizando este nome.  

    - **Recolha do alvo**: Esta recolha inclui todos os dispositivos que o Gestor de Configuração configura com as definições de ID comerciais e dados de diagnóstico. É o conjunto completo de dispositivos que o Gestor de Configuração liga ao serviço Desktop Analytics.  

    - **Os dispositivos na recolha do alvo utilizam um proxy autenticado**pelo utilizador para comunicação de saída : Por defeito, este valor é **Nº**. Se necessário no seu ambiente, **deponha-se**a Sim. Para mais informações, consulte a [autenticação](enable-data-sharing.md#proxy-server-authentication)do servidor Proxy .

    - **Selecione coleções específicas para sincronizar com desktop Analytics**: Selecione **Adicionar** para incluir coleções adicionais da sua hierarquia de **recolha Target.** Estas coleções estão disponíveis no portal Desktop Analytics para agrupar com planos de implementação. Certifique-se de incluir coleções de exclusão de pilotos e pilotos.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Estas coleções continuam a sincronizar-se à medida que a sua adesão muda. Por exemplo, o seu plano de implementação utiliza uma coleção com uma regra de adesão ao Windows 7. À medida que estes dispositivos atualizam para o Windows 10, e o Gestor de Configuração avalia a adesão à recolha, esses dispositivos abandonam o plano de recolha e implementação.

### <a name="windows-settings"></a>Definições do Windows

Quando o Gestor de Configuração inscreve os dispositivos no Desktop Analytics, define as políticas do Windows para configurar o dispositivo para desktop Analytics. Na maioria das circunstâncias, utilize apenas o Configuro Diretor de Configuração para configurar estas definições. Não aplique também estas definições em objetos de política de grupo de domínio.

Para mais informações, consulte [as definições de política do Grupo para desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Nome do dispositivo

A partir do Windows 10, versão 1803, o nome do dispositivo deixou de ser recolhido por padrão. A recolha do nome do dispositivo com os dados de diagnóstico requer um opt-in separado. Sem o nome do dispositivo, é mais difícil para si identificar quais os dispositivos que requerem atenção enquanto avalia uma atualização para uma nova versão do Windows.

Se não enviar o nome do dispositivo, aparece no Desktop Analytics como "Desconhecido":

![Lista de dispositivos desktop Analytics mostrando nomes "desconhecidos"](media/unknown-device-name.png)

Existe uma opção nas definições do Gestor de Configuração para desktop Analytics para configurar esta opção: Permitir o **nome do dispositivo em dados de diagnóstico**. Esta definição do Gestor de Configuração controla a [definição](group-policy-settings.md)de política do Windows , **AllowDeviceNameInTelemettry**.

### <a name="conflict-resolution"></a>Resolução de conflitos

Em geral, utilize as coleções do Gestor de Configuração para direcionar as definições e inscrições do Desktop Analytics. Utilize adesão direta ou consultas para incluir ou excluir dispositivos da recolha. Para mais informações, consulte [Como criar coleções.](../core/clients/manage/collections/create-collections.md)

O Gestor de Configuração só configura as definições do Windows se um valor já não existir. Se precisar de configurar diferentes configurações para um grupo único de dispositivos, pode utilizar a política de [grupo](group-policy-settings.md). As definições direcionadas pela política do grupo têm precedência sobre as definições do Gestor de Configuração. Os dispositivos visados pela política do grupo podem não refletir com precisão o estado no painel de [saúde connection.](monitor-connection-health.md)

Quando configurar o nível de dados de diagnóstico, define o limite superior para o dispositivo. Por predefinição no Windows 10, na versão 1803 e posteriormente, os utilizadores podem optar por definir um nível mais baixo. Pode controlar este comportamento utilizando a definição de política de grupo, configurar a **definição de opt-in de definição de telemetria**. Para mais informações, consulte [as definições de política do Grupo para desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Definições de proxy

Se a sua organização utilizar a autenticação do servidor proxy para acesso à Internet, certifique-se de configurar corretamente ou os seus dispositivos. Para mais informações, consulte a [autenticação](enable-data-sharing.md#proxy-server-authentication)do servidor Proxy .

## <a name="next-steps"></a>Próximos passos

Avançar para o próximo artigo para criar planos de implementação no Desktop Analytics.
> [!div class="nextstepaction"]
> [Criar planos de implementação](create-deployment-plans.md)
