---
title: Lançamentos de pré-visualização técnica
titleSuffix: Configuration Manager
description: Conheça o ramo de pré-visualização técnica para testar novas funcionalidades e capacidades no Gestor de Configuração.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bfcdd74b7b5c31e3f3ab6bb38a7ea96de9d05eec
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905148"
---
# <a name="technical-preview-for-configuration-manager"></a>Pré-visualização técnica para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo fornece detalhes sobre o ramo de pré-visualização técnica mensal do Gestor de Configuração. A pré-visualização técnica introduz uma nova funcionalidade em que a Microsoft está a trabalhar. Introduz novas funcionalidades que ainda não estão incluídas no atual ramo do Gestor de Configuração. Estas funcionalidades poderão eventualmente ser incluídas numa atualização ao ramo atual. Antes de finalizarmos as funcionalidades, queremos que experimente e nos dê feedback.

Como esta versão é uma pré-visualização técnica, os detalhes e funcionalidades estão sujeitos a alterações.

Esta informação aplica-se a todas as versões do ramo de pré-visualização técnica do Gestor de Configuração. Este artigo lista cada nova funcionalidade juntamente com a versão técnica de pré-visualização na qual aparece pela primeira vez. Por exemplo, versão **2001** para janeiro `01` ( ) de 2020 ( `20` ). Artigos separados dedicados a cada versão de pré-visualização detalham as características individuais.

Para obter informações sobre as novidades no *atual ramo* do Gestor de Configuração, consulte [as novidades nas versões incrementais do Gestor de Configuração.](../plan-design/changes/whats-new-incremental-versions.md)

> [!Tip]
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>Requisitos e limitações

> [!IMPORTANT]
> A pré-visualização técnica é licenciada para uso apenas em ambiente de laboratório. A Microsoft pode não fornecer serviços de suporte e certas funcionalidades podem não estar disponíveis em pré-visualizações técnicas. Além disso, o software de pré-visualização técnica pode ter reduzido ou diferentes padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade em relação ao software fornecido comercialmente.

Para a maioria dos pré-requisitos do produto, utilize a informação nas [configurações suportadas](../plan-design/configs/supported-configurations.md). As seguintes exceções aplicam-se ao serviço técnico de pré-visualização:

- Cada instalação está ativa durante 90 dias antes de ficar inativa.

- O inglês é o único idioma suportado.

- Apenas suporta os seguintes parâmetros de linha de comando de configuração:

  - `/silent`
  - `/testdbupgrade`

- O ponto de ligação de serviço instala-se no modo online. Não suporta o modo offline.

- Os artigos separados para cada versão específica da pré-visualização técnica incluem limitações ou requisitos adicionais, conforme aplicável.

- As seguintes funcionalidades não são suportadas com o ramo de pré-visualização técnica:

  - [Migração](../migration/migrate-data-between-hierarchies.md) para ou a partir deste ramo de pré-visualização.

  - [Atualize](../servers/deploy/install/upgrade-to-configuration-manager.md) para este ramo de pré-visualização.

  - [Recuperação](../servers/manage/recover-sites.md) do site da última pasta do CD..<!--507106-->

- Não há suporte para atualizar para a filial atual a partir deste ramo de pré-visualização.

    > [!Note]
    > Quando as atualizações estiverem disponíveis para uma versão de pré-visualização, ainda as encontra e instala a partir do nó de **Atualizações e Manutenção** da consola 'Gestor de Configuração'. Para obter um vídeo do processo de atualização na consola, consulte os pacotes de atualização do [Gestor de Configuração](https://www.youtube.com/embed/KBd_EGFbUT8) de Instalação na youtube.com.

- Só suporta um local primário autónomo. Não há apoio para um site de administração central, vários locais primários ou locais secundários.

O ramo técnico de pré-visualização do Gestor de Configuração suporta os seguintes produtos e tecnologias:

- Salvo indicação em contrário, o ramo de pré-visualização técnica suporta as mesmas versões do SQL Server que o ramo atual. Para mais informações, consulte [as versões Suportadas Do Servidor SQL](../plan-design/configs/support-for-sql-server-versions.md).

- O site suporta até 10 clientes, que podem executar qualquer versão de OS do [cliente suportada.](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)<!-- SCCMDocs#1656 -->

> [!Note]
> A inclusão destes produtos neste conteúdo não implica uma extensão do suporte para uma versão que está para além do seu ciclo de vida de suporte. O Gestor de Configuração não suporta produtos que estão para além do seu ciclo de vida de suporte. Para mais informações, consulte [a Política de Ciclo de Vida](https://support.microsoft.com/lifecycle)da Microsoft .

## <a name="install-and-update"></a><a name="bkmk_install"></a>Instalar e atualizar

O ramo de pré-visualização técnica do Gestor de Configuração para utilização laboratorial é distinto do ramo atual do Gestor de Configuração para utilização da produção.

Primeiro instale uma versão de base do ramo de pré-visualização técnica. Depois de instalar uma versão de base, utilize atualizações na consola para atualizar a sua instalação com a versão de pré-visualização mais recente. Normalmente, estão disponíveis novas versões da pré-visualização técnica todos os meses.

A Microsoft suporta cada versão de pré-visualização técnica até estarem disponíveis três versões sucessivas. Por exemplo, quando a versão 1908 foi lançada, a versão 1904 já não estava em suporte. As versões 1905, 1906 e 1907 permaneceram em apoio. Quando uma linha de base cai fora do suporte, ainda é suportado para instalar um novo site de pré-visualização técnica, assumindo que você atualiza imediatamente para uma versão suportada. A linha de base mais antiga é suportada até que uma nova versão de base esteja disponível. Atualize a versão mais recente disponível a partir da linha de base e, em seguida, repita o processo de atualização até instalar a versão de pré-visualização técnica mais recente.

> [!TIP]
> Quando instalar uma atualização para a pré-visualização técnica, atualiza a sua instalação de pré-visualização para a nova versão técnica de pré-visualização. Uma instalação técnica de pré-visualização nunca tem a opção de fazer upgrade para uma instalação de filial atual. Também nunca recebe atualizações da versão atual do ramo.
>
> Várias vezes ao longo do ano, existem as versões técnicas de pré-visualização e as versões atuais do ramo com o mesmo número de versão. Por exemplo, existe uma versão de pré-visualização técnica de 1910 e uma versão atual da sucursal de 1910.

### <a name="active-baseline-versions"></a>Versões de base ativas

Instale uma versão de base até um ano após o seu lançamento. Quando instalar um novo site de pré-visualização técnica, utilize a versão base mais recente.

- Versão técnica de **pré-visualização 2002**: A versão de pré-visualização técnica do Diretor de Configuração 2002 está disponível como uma atualização na consola e como uma nova versão de base.

Faça o download de uma versão de base do Centro de [Avaliação.](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a>Fornecendo feedback

Adoramos ouvir o seu feedback sobre as novas funcionalidades na pré-visualização técnica. Para mais informações, consulte o [feedback do Produto.](../understand/find-help.md#product-feedback)

Se tiver ideias sobre novas funcionalidades que gostaria de ver, avise-nos! Envie novas ideias e vote nas ideias por outros: [Gestor de Configuração UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a>Funcionalidades na versão mais recente

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2003.md) <!--ID-->

As seguintes funcionalidades estão disponíveis com a mais recente versão de pré-visualização técnica do Gestor de Configuração:

### <a name="technical-preview-version-2004"></a>Versão de pré-visualização técnica 2004

- [Anexo de inquilino do Microsoft Endpoint Manager: Detalhes do cliente configMgr](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Notificações da Microsoft](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Copiar dados de descoberta da consola](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Melhorias à CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Suporte para a versão 7 da PowerShell](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Passo de sequência de tarefas de formato e de divisão](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Regras de informação de gestão para a implantação do OS](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [Cmdlets PowerShell para tipos de implementação de sequência de tarefas](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

> [!NOTE]
> As funcionalidades que estavam disponíveis numa versão anterior da pré-visualização técnica permanecem disponíveis em versões posteriores. Da mesma forma, as funcionalidades adicionadas ao ramo atual do Gestor de Configuração permanecem disponíveis no ramo técnico de pré-visualização.

## <a name="features-in-recent-technical-previews"></a>Funcionalidades em pré-visualizações técnicas recentes

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Diretor de Configuração desde a versão atual do ramo 2002:

> [!TIP]
> Quando uma nova versão atual da sucursal está disponível, as funcionalidades que estão disponíveis nessa versão estão listadas no mais recente *What's new* article. Para mais informações, consulte [o que há de novo em versões incrementais.](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)

### <a name="technical-preview-version-2003"></a>Versão de pré-visualização técnica 2003

- [Clientes do Gestor de Configuração a bordo do Microsoft Defender ATP através da consola Microsoft Endpoint Manager](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Reparações de itens de configuração de rastreio](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Mostrar grupos de fronteira para dispositivos](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Novo assistente de feedback](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Melhorias no painel de instrumentos da Microsoft Edge Management](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Melhorias à CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Consulta de feedback enviado à Microsoft](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Novo método SDK para o progresso da sequência de tarefas](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Melhorias na implantação do OS](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Funcionalidades em pré-visualizações técnicas anteriores

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Gestor de Configuração. Estas funcionalidades permanecem disponíveis em versões posteriores, mas ainda não estão disponíveis no ramo atual.

| Funcionalidade        | Versão de pré-visualização técnica |
|----------------|---------------------------|
| Anexar ficheiros ao feedback <!--3556011--> | [Pré-visualização tecnológica de 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Melhorias nos pontos de distribuição multicast-habilitados <!--3785535--> | [Antevisão da tecnologia 1908.2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Modelos de implementação faseados <!--4961086--> | [Pré-visualização tecnológica de 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Controlo remoto em qualquer lugar usando gateway de gestão de nuvem <!--4575930--> | [Antevisão tecnológica 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Melhorias no Centro Comunitário <!--3555935--> | [Antevisão tecnológica 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Melhorias no Centro Comunitário <!--4224401--> | [Antevisão tecnológica 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Centro Comunitário e GitHub <!--3555935--> | [Antevisão tecnológica 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Estimativa de custos de serviços na nuvem <!--3555774--> | [Antevisão tecnológica 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Relatórios de descarregamento do Centro Comunitário <!--3555936--> | [Antevisão tecnológica 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Centro Comunitário <!--3556020, fka 1357766--> | [Antevisão tecnológica 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Serviço de resposta PXE baseado no cliente <!--3556018, fka 1357148--> | [Antevisão tecnológica 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Suporte de arranque de rede PXE para IPv6 <!--3601254, fka 1269793--> |[Antevisão tecnológica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Utilizar o Azure Active Directory <!--3607315, fka 1322145--> | [Antevisão tecnológica 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Melhorias na Inteligência de Ativos <!--3601024, fka 1307390--> | [Antevisão tecnológica 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Consulte também

Para obter mais informações, veja os seguintes artigos:

- [Avaliar o Configuration Manager num laboratório](evaluate-with-lab-environment.md)
- [Novidades das versões incrementais do Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Introdução ao Configuration Manager](../understand/introduction.md)

> [!Tip]
> Para obter mais informações sobre as funcionalidades atuais do ramo que requerem consentimento para ativar, consulte [as funcionalidades de pré-lançamento](../servers/manage/pre-release-features.md).
>
> Para obter mais informações sobre as funcionalidades atuais do ramo que deve ativar primeiro, consulte [as funcionalidades opcionais enable a partir de atualizações](../servers/manage/install-in-console-updates.md#bkmk_options).
