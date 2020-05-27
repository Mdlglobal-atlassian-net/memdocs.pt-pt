---
title: Utilize as linhas de base de segurança no Microsoft Intune - Azure [ Microsoft Docs
description: Utilize as definições de segurança recomendadas para proteger o utilizador e os dados em dispositivos com a Microsoft Intune para a gestão de dispositivos móveis. Ativar encriptação, configurar a Proteção avançada de ameaças do Microsoft Defender, controlar o Internet Explorer, definir políticas de segurança locais, exigir uma palavra-passe, bloquear transferências de internet e muito mais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d533acfa60672bed3d6919116f11f43d525b6551
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988321"
---
# <a name="use-security-baselines-to-configure-windows-10-devices-in-intune"></a>Utilize linhas de base de segurança para configurar dispositivos Windows 10 em Intune

Utilize as linhas de segurança da Intune para o ajudar a proteger e proteger os seus utilizadores e dispositivos. As linhas de base de segurança são grupos pré-configurados de definições do Windows que o ajudam a aplicar um grupo conhecido de configurações e valores predefinidos que são recomendados pelas equipas de segurança relevantes. Quando cria um perfil de base de segurança no Intune, está a criar um modelo que consiste em múltiplos perfis de configuração do *dispositivo.*

Esta funcionalidade aplica-se a:

- Windows 10 versão 1809 e mais tarde

Implementa linhas de base de segurança para grupos de utilizadores ou dispositivos em Intune, e as definições aplicam-se a dispositivos que executam o Windows 10 ou posteriormente. Por exemplo, a Base de Segurança do *MDM* ativa automaticamente o BitLocker para unidades amovíveis, necessita automaticamente de uma palavra-passe para desbloquear um dispositivo, desativa automaticamente a autenticação básica e muito mais. Quando um valor predefinido não funciona para o seu ambiente, personalize a linha de base para aplicar as definições de que necessita.

Os tipos de base separados podem incluir as mesmas definições, mas utilizam diferentes valores predefinidos para essas definições. É importante compreender os incumprimentos nas linhas de base que escolhe utilizar e, em seguida, modificar cada linha de base para se adaptar às suas necessidades organizacionais.

> [!NOTE]
> A Microsoft não recomenda a utilização de versões de pré-visualização de linhas de base de segurança num ambiente de produção. As definições numa linha de pré-visualização podem mudar ao longo da pré-visualização.

As linhas de base de segurança podem ajudá-lo a ter um fluxo de trabalho seguro de ponta a ponta ao trabalhar com o Microsoft 365. Alguns dos benefícios são:

- Uma linha de base de segurança inclui as melhores práticas e recomendações sobre configurações que impactam a segurança. Intune parceiros com a mesma equipa de segurança do Windows que cria linhas de base de segurança de política de grupo. Estas recomendações baseiam-se em orientação e experiência extensiva.
- Se é novo em Intune, e não sabe por onde começar, então as linhas de segurança dão-lhe uma vantagem. Pode criar e implementar rapidamente um perfil seguro, sabendo que está a ajudar a proteger os recursos e dados da sua organização.
- Se atualmente utilizar a política de grupo, migrar para Intune para gestão é muito mais fácil com estas linhas de base. Estas linhas de base são nativamente construídas em Intune, e incluem uma experiência de gestão moderna.

[As linhas de base](https://docs.microsoft.com/windows/security/threat-protection/windows-security-baselines) de segurança do Windows são um ótimo recurso para saber mais sobre esta funcionalidade. [A gestão de dispositivos móveis](https://docs.microsoft.com/windows/client-management/mdm/) (MDM) é um grande recurso sobre o MDM, e o que pode fazer em dispositivos Windows.

## <a name="available-security-baselines"></a>Linhas de base de segurança disponíveis

As seguintes instâncias de base de segurança estão disponíveis para utilização com o Intune. Utilize os links para visualizar as definições para a instância mais recente de cada linha de base.

- **Linha de Base de Segurança do MDM**
  - [Base de Segurança do MDM para maio de 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Pré-visualização: Base de Segurança do MDM para outubro de 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)

- **Linha de base** 
   ATP do Microsoft Defender *(Para utilizar esta linha de base, o seu ambiente deve satisfazer os pré-requisitos para a utilização da [Proteção avançada de ameaças do Microsoft Defender)](advanced-threat-protection.md#prerequisites)*.
  - [Linha de base ATP microsoft Defender para abril de 2020 - versão 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Linha de base ATP microsoft Defender para março de 2020 - versão 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > A linha de segurança ATP do Microsoft Defender foi otimizada para dispositivos físicos e não é atualmente recomendada para utilização em máquinas virtuais (VMs) ou pontos finais VDI. Certas definições de base podem ter impacto em sessões interativas remotas em ambientes virtualizados.  Para mais informações, consulte Aumentar a conformidade com a linha de [segurança ATP do Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) na documentação do Windows.

- **Linha de Base do Microsoft Edge**
  - [Linha de base do Microsoft Edge para abril de 2020 (versão Edge 80 e mais tarde)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Pré-visualização: Linha de base do Microsoft Edge para outubro de 2019 (versão Edge 77 e mais tarde)](security-baseline-settings-edge.md?pivots=edge-october-2019)

Pode continuar a utilizar e editar perfis que criou anteriormente com base num modelo de pré-visualização, mesmo quando esse modelo de pré-visualização já não está disponível para criar novos perfis.

Quando estiver pronto para avançar para uma versão mais recente de uma linha de base que utiliza, consulte [alterar a versão base para um perfil](#change-the-baseline-version-for-a-profile) neste artigo. 

## <a name="about-baseline-versions-and-instances"></a>Sobre versões e instâncias de base

Cada nova versão de uma linha de base pode adicionar ou remover definições ou introduzir outras alterações. Por exemplo, à medida que as novas definições do Windows 10 ficam disponíveis com novas versões do Windows 10, o MDM Security Baseline poderá receber uma nova versão que inclui as definições mais recentes.

No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)sob as linhas de **segurança endpoint,** verá uma lista das linhas de base  >  **Security baselines** disponíveis. A lista inclui:
- o nome do modelo de linha de base
- quantos perfis você tem que usar que tipo de linha de base
- quantas instâncias separadas (versões) do tipo de linha de base estão disponíveis
- uma última data *publicada* que identifica quando a versão mais recente do modelo de base ficou disponível

Para ver mais informações sobre as versões de base que utiliza, selecione uma linha de base para abrir o seu painel de *visão geral* e, em seguida, selecione **Versões**. Intune apresenta detalhes sobre as versões dessa linha de base que estão a ser utilizadas pelos seus perfis. Os detalhes incluem a versão base mais recente e atual. Pode selecionar uma única versão para visualizar detalhes mais profundos sobre os perfis que utilizam essa versão.

Pode optar por [alterar a versão](#change-the-baseline-version-for-a-profile) de uma linha de base que está em uso com um determinado perfil. Quando muda a versão, não precisa de criar um novo perfil de base para tirar partido das versões atualizadas. Em vez disso, pode selecionar um perfil de base e utilizar a opção incorporada para alterar a versão por exemplo desse perfil para um novo.

### <a name="compare-baseline-versions"></a>Comparar versões de base

No painel **versões** para uma linha de base de segurança está uma lista de cada versão desta linha de base que implementou. Esta lista também inclui a versão mais recente e ativa da linha de base. Quando cria um novo *perfil*de base de segurança, o perfil utiliza a versão mais recente da linha de base de segurança.  Pode continuar a utilizar e editar perfis que criou anteriormente que utilizam uma versão de base anterior, incluindo linhas de base criadas utilizando uma versão Preview.

Para entender o que mudou entre versões, selecione as caixas de verificação para duas versões diferentes e, em seguida, selecione **Compare as linhas**de base . Em seguida, é-lhe pedido que descarregue um ficheiro CSV que detalha essas diferenças.

O download identifica cada definição nas duas versões de base, e observa se esta definição mudou (*não igual*) ou se permaneceu a mesma *(igual).* Os detalhes também incluem o valor padrão para a definição por versão, e se a definição foi *adicionada* à versão mais recente, ou *removida* da versão mais recente.

![Comparar linhas de base](./media/security-baselines/compare-baselines.png)

## <a name="avoid-conflicts"></a>Evitar conflitos

Pode utilizar uma ou mais das linhas de base disponíveis no seu ambiente Intune ao mesmo tempo. Também pode usar várias instâncias das mesmas linhas de base de segurança que têm diferentes personalizações.

Quando utilizar várias linhas de base de segurança, reveja as definições em cada uma para identificar quando as suas diferentes configurações de base introduzem valores contraditórios para a mesma configuração. Uma vez que pode implementar linhas de base de segurança concebidas para diferentes intenções e implementar múltiplas instâncias da mesma linha de base que incluem configurações personalizadas, pode criar conflitos de configuração para dispositivos que devem ser investigados e resolvidos.

Além disso, as linhas de base de segurança gerem frequentemente as mesmas definições que pode definir com perfis de [configuração](../configuration/device-profiles.md) do dispositivo ou outros tipos de política. Por isso, mantenha-se atento e considere as suas políticas e perfis adicionais para configurações quando procurar evitar ou resolver conflitos.

Utilize as informações nos seguintes links para ajudar a identificar e resolver conflitos:

- [Resolução de problemas de políticas e perfis no Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorize as suas linhas de base de segurança](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="manage-baselines"></a>Gerir linhas de base

As tarefas comuns quando trabalha com linhas de base de segurança incluem:

- [Criar um perfil](#create-the-profile) – Configure as definições que pretende utilizar e atribua a linha de base a grupos.
- [Alterar a versão](#change-the-baseline-version-for-a-profile) – Alterar a versão de base em uso por um perfil.
- [Remova uma tarefa de base](#remove-a-security-baseline-assignment) - Saiba o que acontece quando deixar de gerir as definições com uma linha de base de segurança.


### <a name="prerequisites"></a>Pré-requisitos

- Para gerir as linhas de base em Intune, a sua conta deve ter o papel de [Policy and Profile Manager](../fundamentals/role-based-access-control.md#built-in-roles) incorporado.

- A utilização de algumas linhas de base pode exigir que tenha uma subscrição ativa de serviços adicionais, como o Microsoft Defender ATP.

### <a name="create-the-profile"></a>Criar o perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione bases de segurança de **endpoint**  >  **Security baselines** para ver a lista de linhas de base disponíveis.

   ![Selecione uma linha de base de segurança para configurar](./media/security-baselines/available-baselines.png)

3. Selecione a linha de base que deseja utilizar e, em seguida, selecione **criar o perfil**.

4. No separador **Basics,** especifique as seguintes propriedades:

   - **Nome**: Introduza um nome para o perfil de base de segurança. Por exemplo, introduza *o perfil Standard para O ATP defender*.

   - **Descrição**: Introduza algum texto que descreva o que esta linha de base faz. A descrição é para que insira qualquer texto que queira. É opcional, mas recomendado.

   Selecione **Next** para ir ao separador seguinte. Depois de ter avançado para um novo separador, pode selecionar o nome do separador para voltar a um separador previamente visto.

5. No separador de definições de Configuração, veja os grupos de **Definições** disponíveis na linha de base selecionada. Pode expandir um grupo para visualizar as definições desse grupo e os valores predefinidos para essas definições na linha de base. Para encontrar configurações específicas:
   - Selecione um grupo para expandir e rever as definições disponíveis.
   - Utilize a barra *de pesquisa* e especifique as palavras-chave que filtram a vista para exibir apenas os grupos que contêm os seus critérios de pesquisa.

   Cada definição numa linha de base tem uma configuração predefinida para essa versão de base. Reconfigure as definições predefinidas para atender às necessidades do seu negócio. As linhas de base diferentes podem conter a mesma definição e utilizar diferentes valores predefinidos para a definição, dependendo da intenção da linha de base.

   ![Expanda um grupo para ver as configurações para esse grupo](./media/security-baselines/sample-list-of-settings.png)

6. No separador **'Etiquetas Scope',** selecione **Selecione etiquetas** de âmbito para abrir o painel *de etiquetas Select para* atribuir etiquetas de âmbito ao perfil.

7. No separador **De atribuição,** selecione **Select grupos para incluir** e, em seguida, atribuir a linha de base a um ou mais grupos. Utilize **grupos Select para excluir** para afinar a atribuição.

   ![Atribuir um perfil](./media/security-baselines/assignments.png)

8. Quando estiver pronto para implementar a linha de base, avance para o **Review + crie** o separador e reveja os detalhes para a linha de base. Selecione **Criar** para guardar e implementar o perfil.

   Assim que criar o perfil, é empurrado para o grupo designado e pode aplicar-se imediatamente.

   > [!TIP]
   > Se guardar um perfil sem primeiro atribuir a grupos, poderá depois editar o perfil para o fazer.

   ![Rever a linha de base](./media/security-baselines/review.png)

9. Depois de criar um perfil, edite-o indo para as linhas de segurança de **segurança endpoint,**  >  **Security baselines**selecione o tipo de linha de base que configurae e, em seguida, selecione **Perfis**. Selecione o perfil na lista de perfis disponíveis e, em seguida, selecione **Propriedades**. Pode editar as definições de todos os separadores de configuração disponíveis e selecionar **Rever + guardar** para comprometer as suas alterações.

### <a name="change-the-baseline-version-for-a-profile"></a>Alterar a versão de base para um perfil

Pode alterar a versão da instância de base que em uso com um perfil.  Quando muda a versão, seleciona uma instância disponível da mesma linha de base. Não é possível alterar entre dois tipos de base diferentes, tais como alterar um perfil de usar uma linha de base para o Defender ATP para usar a linha de base de segurança do MDM.

Ao configurar uma alteração da versão de base, pode descarregar um ficheiro CSV que lista as alterações entre as duas versões de base envolvidas. Também tem a opção de manter todas as suas personalizações a partir da versão base original, ou implementar a nova versão usando todos os seus valores padrão. Não tem a opção de fazer alterações nas definições individuais quando muda a versão de uma linha de base para um perfil.

Após a poupança, após a conversão estar concluída, a linha de base é imediatamente reimplantada para grupos designados.

**Durante a conversão:**

- Novas definições que não estavam na versão original que estava a usar são adicionadas e definidas para usar os valores predefinidos.

- As definições que não estão na nova versão de base selecionada são removidas e já não são aplicadas por este perfil de base de segurança.

  Quando uma definição já não é gerida por um perfil de base, essa definição não é redefinida no dispositivo. Em vez disso, a regulação do dispositivo permanece definida até à sua última configuração até que algum outro processo gere a definição para o alterar. Exemplos de processos que podem alterar uma definição depois de deixar de geri-lo incluem um perfil de base diferente, uma definição de política de grupo ou configuração manual que é feita no dispositivo.

#### <a name="to-change-the-baseline-version-for-a-profile"></a>Para alterar a versão de base para um perfil

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). 

2. Selecione as linhas de segurança de **endpoint**e, em  >  **Security baselines**seguida, selecione o azulejo para o tipo de linha de base que tem o perfil que pretende alterar.

3. Em seguida, selecione **Perfis**, e, em seguida, selecione a caixa de verificação para o perfil que pretende editar e, em seguida, selecione **Versão Change**.

   ![selecionar uma linha de base](./media/security-baselines/select-baseline.png)

4. No painel **'Versão alteração',** utilize a linha de **base de segurança Select para atualizar para** dropdown e selecione a instância de versão que pretende utilizar.

   ![selecionar uma versão](./media/security-baselines/select-instance.png)

5. Selecione **a atualização do Review** para descarregar um ficheiro CSV que apresenta a diferença entre a versão atual dos perfis e a nova versão que selecionou. Reveja este ficheiro de modo a que compreenda quais as definições novas ou removidas e quais os valores predefinidos para estas definições no perfil atualizado.

   Quando estiver pronto, continue para o próximo passo.

6. Escolha uma das duas opções para **Selecionar um método para atualizar o perfil:**
   - **Aceite alterações de base mas mantenha as minhas personalizações de configuração existentes** - Esta opção mantém as personalizações que fez para o perfil de base e aplica-as à nova versão que selecionou para usar.
   - **Aceite alterações de base e elimine as personalizações de definição existentes** - Esta opção substitui completamente o seu perfil original. O perfil atualizado utilizará os valores predefinidos para todas as definições.

7. Selecione **Submeter**. As atualizações do perfil para a versão de base selecionada e após a conversão estar concluída, a linha de base reimplanta-se imediatamente para os grupos designados.

### <a name="remove-a-security-baseline-assignment"></a>Remover uma atribuição de base de segurança

Quando uma definição de base de segurança já não se aplica a um dispositivo, ou as definições numa linha de base são definidas para *Não configuradas,* essas definições num dispositivo não revertem para uma configuração pré-gerida. Em vez disso, as configurações anteriormente geridas no dispositivo mantêm as suas últimas configurações recebidas da linha de base até que algum outro processo atualize essas definições no dispositivo.

Outros processos que poderão alterar posteriormente as definições no dispositivo incluem uma linha de base de segurança diferente ou nova, perfil de configuração do dispositivo, configurações de Política de Grupo ou edição manual da definição no dispositivo.

### <a name="duplicate-a-security-baseline"></a>Duplicar uma linha de base de segurança

Pode criar duplicados das suas linhas de base de segurança. Um cenário quando duplicar uma linha de base é útil é quando se pretende atribuir uma linha de base semelhante, mas distinta, a um subconjunto de dispositivos. Ao criar um duplicado, não precisará recriar manualmente toda a linha de base. Em vez disso, pode duplicar qualquer uma das suas linhas de base atuais e, em seguida, introduzir apenas as alterações que a nova instância requer. Só pode alterar uma definição específica e o grupo a que a linha de base é atribuída.

Quando criar um duplicado, dará à cópia um novo nome. A cópia é feita com as mesmas configurações de definição e etiquetas de âmbito que a original, mas não terá nenhuma atribuição. Terá de editar a nova linha de base para adicionar atribuições.

Todas as bases de segurança suportam a criação de uma duplicação.

Depois de duplicar uma linha de base, reveja e edite a nova instância para fazer alterações na sua configuração.

#### <a name="to-duplicate-a-baseline"></a>Para duplicar uma linha de base

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vá para as linhas de segurança de **endpoint,**  >  **Security baselines**selecione o tipo de linha de base que pretende duplicar e, em seguida, selecione **Perfis**.
3. Clique à direita no perfil que pretende duplicar e selecionar **Duplicate,** ou selecione a elipse **(...**) à direita da linha de base e selecione **Duplicato**.
4. Forneça um **novo nome** para a linha de base e, em seguida, selecione **Guardar**.

Depois de um *Refresh,* o novo perfil de base aparece no centro de administração.

#### <a name="to-edit-a-baseline"></a>Para editar uma linha de base

1. Selecione a linha de base e, em seguida, selecione **Propriedades**.
2. Selecione **Definições** para expandir a lista de categorias de definições na linha de base. Não é possível modificar as definições desta vista, mas pode rever a forma como estão configuradas.
3. Para modificar as definições, selecione **Editar** para cada categoria onde pretende fazer uma alteração:
   - Noções básicas
   - Atribuições
   - Scope tags (Etiquetas de âmbito)
   - Definições de configuração
4. Depois de ter feito alterações, selecione **Guardar** para guardar as suas edições.  Tem de guardar edites para uma categoria antes de poder introduzir edites em categorias adicionais.

### <a name="older-baseline-versions"></a>Versões de base mais antigas

O Microsoft Endpoint Manager atualiza as versões de Bases de Segurança incorporadas, dependendo das necessidades em mudança de uma organização típica. Cada novo lançamento resulta numa atualização de versão para uma linha de base específica. A expectativa é que os clientes utilizem a versão base mais recente como ponto de partida para os seus perfis de Configuração de Dispositivos.

Quando já não existem perfis que utilizem uma linha de base mais antiga listada no seu inquilino, o Microsoft Endpoint Manager apenas listará a versão base mais recente disponível.

Se tiver um perfil associado a uma linha de base mais antiga, essa linha de base mais antiga continuará a ser listada.

## <a name="co-managed-devices"></a>Dispositivos cogeridos

As linhas de base de segurança em dispositivos geridos por Intune são semelhantes a dispositivos cogeridos com O Gestor de Configuração. Os dispositivos cogeridos utilizam o Configurador de Configuração e o Microsoft Intune para gerir os dispositivos Do Windows 10 simultaneamente. Permite anexar o investimento do Gestor de Configuração existente aos benefícios do Intune. [A visão geral da cogestão](https://docs.microsoft.com/configmgr/comanage/overview) é um ótimo recurso se utilizar o Gestor de Configuração, e também quer os benefícios da nuvem.

Quando utilizar dispositivos cogeridos, tem de mudar a carga de trabalho de **configuração** do Dispositivo (as suas definições) para Intune. [A carga de trabalho de configuração](https://docs.microsoft.com/configmgr/comanage/workloads#device-configuration) do dispositivo fornece mais informações.

## <a name="q--a"></a>Perguntas e Respostas

### <a name="why-these-settings"></a>Por que estas configurações?

A equipa de segurança da Microsoft tem anos de experiência a trabalhar diretamente com os desenvolvedores do Windows e a comunidade de segurança para criar estas recomendações. As definições nesta linha de base são consideradas as opções de configuração mais relevantes relacionadas com a segurança. Em cada nova construção do Windows, a equipa ajusta as suas recomendações com base em funcionalidades recém-lançadas.

### <a name="is-there-a-difference-in-the-recommendations-for-windows-security-baselines-for-group-policy-vs-intune"></a>Existe alguma diferença nas recomendações para as linhas de segurança do Windows para a política de grupo vs. Intune?

A mesma equipa de segurança da Microsoft escolheu e organizou as definições para cada linha de base. Intune inclui todas as configurações relevantes na linha de base de segurança Intune. Existem algumas definições na linha de base da política do grupo que são específicas para um controlador de domínio no local. Estas definições estão excluídas das recomendações da Intune. Todas as outras definições são as mesmas.

### <a name="are-the-intune-security-baselines-cis-or-nsit-compliant"></a>As linhas de segurança Intune CIS ou NSIT são conformes?

Em rigor, não. A equipa de segurança da Microsoft consulta organizações, como o CIS, para compilar as suas recomendações. Mas não há um mapeamento um-para-um entre as linhas de base "cis-compliant" e microsoft.

### <a name="what-certifications-does-microsofts-security-baselines-have"></a>Que certificações têm as linhas de segurança da Microsoft? 

- A Microsoft continua a publicar linhas de base de segurança para as políticas do grupo (GPOs) e o Kit de Ferramentas de Conformidade de [Segurança,](https://docs.microsoft.com/windows/security/threat-protection/security-compliance-toolkit-10)como tem vindo a fazer há muitos anos. Estas linhas de base são usadas por muitas organizações. As recomendações nestas linhas de base são do envolvimento da equipa de segurança da Microsoft com clientes empresariais e agências externas, incluindo o Departamento de Defesa (DoD), Instituto Nacional de Normalização e Tecnologia (NIST), e muito mais. Partilhamos as nossas recomendações e linhas de base com estas organizações. Estas organizações também têm as suas próprias recomendações que espelham de perto as recomendações da Microsoft. À medida que a gestão de dispositivos móveis (MDM) continua a crescer na nuvem, a Microsoft criou recomendações equivalentes de MDM destas linhas de base políticas do grupo. Estas linhas de base adicionais são incorporadas no Microsoft Intune, e incluem relatórios de conformidade sobre utilizadores, grupos e dispositivos que seguem (ou não seguem) a linha de base.

- Muitos clientes estão a usar as recomendações de base intune como ponto de partida, e depois personalizam-nas para satisfazer as suas exigências de TI e segurança. A **Linha de Base** de Segurança do MDM do Windows 10 RS5 da Microsoft é a primeira linha de base a ser lançada. Esta linha de base é construída como uma infraestrutura genérica que permite aos clientes eventualmente importar outras linhas de base de segurança com base em Normas CIS, NIST e outras normas. Atualmente, está disponível para Windows e acabará por incluir iOS/iPadOS e Android.

- Migrar das políticas do grupo Ative Directory para uma solução pura em nuvem usando o Azure Ative Directory (AD) com a Microsoft Intune é uma viagem. Para ajudar, existem modelos de política de grupo incluídos no Kit de [Ferramentas](https://docs.microsoft.com/windows/security/threat-protection/security-compliance-toolkit-10) de Conformidade de Segurança que podem ajudar a gerir dispositivos híbridos ad e azure ad-joined. Estes dispositivos podem obter configurações de MDM a partir da nuvem (Intune) e definições de política de grupo a partir de controladores de domínio no local, conforme necessário.

## <a name="next-steps"></a>Passos seguintes

- Ver as definições nas versões mais recentes das linhas de base disponíveis:
  - [Linha de base de segurança do MDM](security-baseline-settings-mdm-all.md)
  - [Linha de base ATP do Microsoft Defender](security-baseline-settings-defender-atp.md)

- Verifique o estado e monitorize a [linha de base e](security-baselines-monitor.md) o perfil
