---
title: Pré-visualização de análise endpoint
titleSuffix: Configuration Manager
description: Instruções para pré-visualização de análise de Endpoint.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e7dbb53833c29aae442eec4ca3c8402b99cde237
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693239"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>Pré-visualização de análise endpoint

> [!Note]  
> Esta informação diz respeito a uma funcionalidade de pré-visualização que pode ser substancialmente modificada antes de ser lançada comercialmente. A Microsoft não faz garantias, de forma expressa ou implícita, em relação à informação aqui apresentada. 
>
> Para mais informações sobre alterações à análise de Endpoint, consulte [o que há de novo na análise de Endpoint](whats-new-endpoint-analytics.md). 

## <a name="endpoint-analytics-overview"></a>Visão geral da análise do ponto final

Não é incomum para os utilizadores finais experimentar longos tempos de arranque ou outras perturbações. Estas perturbações podem dever-se a uma combinação de:

- Hardware legado
- Configurações de software que não são otimizadas para a experiência do utilizador final
- Problemas causados por alterações de configuração e atualizações

Estes problemas e outros problemas de experiência do utilizador final persistem porque a TI não tem muita visibilidade na experiência do utilizador final. Geralmente, a única visibilidade nestas questões provém de um canal de suporte lento e dispendioso que normalmente não fornece informações claras sobre o que precisa de ser otimizado. Não é só o suporte de TI que suporta o custo destes problemas. O tempo que os trabalhadores gastam a tratar de questões também é dispendioso. Problemas de desempenho, fiabilidade e suporte que reduzam a produtividade dos utilizadores podem ter um grande impacto também na linha de fundo de uma organização.

**A análise do Endpoint** visa melhorar a produtividade dos utilizadores e reduzir os custos de suporte de TI, fornecendo informações sobre a experiência do utilizador. Os insights permitem que o TI otimize a experiência do utilizador final com suporte proactivo e detete regressões à experiência do utilizador, avaliando o impacto do utilizador nas alterações de configuração.

Esta versão inicial, centra-se em três coisas:

- [**Software recomendado**](#bkmk_uea_rs): Recomendações para proporcionar a melhor experiência do utilizador
- [**Scripts de remediação proactiva**](#bkmk_uea_prs): Corrigir problemas de suporte comuns antes de os utilizadores finais notarem problemas
- [**Desempenho de arranque**](#bkmk_uea_bp): Ajuda a levar os utilizadores da power-on para a produtividade rapidamente sem uma bota longa e assinar em atrasos

Esta libertação é apenas o começo. Vamos lançar rapidamente novas informações para outras experiências-utilizador chave logo após o lançamento inicial. Para mais informações sobre alterações à análise de Endpoint, consulte [o que há de novo na análise de Endpoint](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a>Começar

Para começar a utilizar a análise do Endpoint, verifique os pré-requisitos e, em seguida, comece a recolher dados. 

### <a name="technical-prerequisites"></a>Pré-requisitos técnicos

Para esta pré-visualização, pode inscrever dispositivos através do 'Configuração Manager' ou do Microsoft Intune. 

Para inscrever os dispositivos via Intune, esta pré-visualização requer:
- Intune dispositivos matriculados com o Windows 10
- Os insights de desempenho do startup só estão disponíveis para dispositivos que executam a versão 1903 ou posteriormente do Windows 10 Enterprise (as edições Home e Pro não são suportadas atualmente), e os dispositivos devem ser Azure AD adesão ou Híbrido Azure AD juntou-se. As máquinas de trabalho unidas não são atualmente suportadas.
- Conectividade de rede de dispositivos para a nuvem pública da Microsoft. Para mais informações, consulte [pontos finais.](#bkmk_uea_endpoints)
- A função de Administrador de [Serviço Intune](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) é necessária para começar a [recolher dados](#bkmk_uea_start).
   - Ao clicar em **Iniciar,** concorda e reconhece que os dados dos seus clientes podem ser armazenados fora do local selecionado quando fornetiu o seu inquilino Microsoft Intune.
   - Depois de clicar **Iniciar** para recolher dados, outras funções apenas para leitura podem ver os dados.

Para inscrever dispositivos via Configuração Manager, esta pré-visualização requer:
- Versão de Gestor de Configuração 2002 ou mais recente
- Clientes atualizados para versão 2002 ou mais recente
- Anexo de inquilino do [Microsoft Endpoint Manager](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) habilitado com uma localização de inquilino Azure da América do Norte (em breve iremos expandir-nos para outras regiões)

Quer os dispositivos de inscrição através de Intune ou De Configuration Manager, [**a escrita de reparação proactiva**](#bkmk_uea_prs) tem os seguintes requisitos:
- Os dispositivos devem ser a AD Azure ou a Azure AD híbrida unida e satisfazer uma das seguintes condições:
- Um dispositivo Windows 10 Enterprise, Professional ou Education que é gerido pela Intune
- Um dispositivo [cogerido](../../comanage/overview.md) com o Windows 10 Enterprise, versão 1607 ou mais tarde com as [aplicações cliente,](../../comanage/workloads.md#client-apps) a carga de trabalho apontada para intune.
- Um dispositivo [cogerido](../../comanage/overview.md) com o Windows 10 Enterprise, versão 1903 ou mais tarde com as [aplicações cliente,](../../comanage/workloads.md#client-apps) a carga de trabalho apontada para o Gestor de Configuração.

### <a name="licensing-prerequisites"></a>Pré-requisitos de licenciamento

A análise do endpoint está incluída nos seguintes planos: 

- [Mobilidade Empresarial + Segurança E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) ou superior
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) ou superior.

As reparações proactivas também requerem uma das seguintes licenças para os dispositivos geridos:
- Windows 10 Enterprise E3 ou E5 (incluído na Microsoft 365 F3, E3 ou E5)
- Educação Windows 10 A3 ou A5 (incluído na Microsoft 365 A3 ou A5)
- Windows Virtual Desktop Access E3 ou E5

### <a name="permissions"></a>Permissões

#### <a name="endpoint-analytics-permissions"></a>Permissões de análise endpoint

As seguintes permissões são utilizadas para análise de Endpoint:
- **Leia** na categoria de configurações do **Dispositivo.**
- **Leia** na categoria **Organização.** <!--temporary for pp-->
- Permissões adequadas ao papel do utilizador na categoria **Endpoint Analytics.**

Um utilizador só para leitura só necessitaria da permissão **De Leitura** nas **configurações** do Dispositivo e nas categorias **Endpoint Analytics.** Um administrador intune normalmente precisaria de todas as permissões.

#### <a name="proactive-remediations-permissions"></a>Autorizações proactivas de reparação

Para remediações proactivas, o utilizador necessita de permissões adequadas ao seu papel na categoria de configurações do **Dispositivo.**  Não são necessárias permissões na categoria **Endpoint Analytics** se o utilizador utilizar apenas reparações proactivas.


## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a>Comece a recolher dados

1. Ir para `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Clique em **Iniciar**. Isto atribuirá automaticamente um perfil de configuração para recolher dados de desempenho de arranque de todos os dispositivos elegíveis. Pode [alterar os dispositivos atribuídos](#bkmk_uea_profile) mais tarde. Pode levar até 24 horas para que os dados de desempenho do arranque possam ser preenchidos a partir dos seus dispositivos matriculados no Intune após o seu reboot.
   - Para obter mais informações sobre questões comuns, consulte a inscrição do dispositivo de desempenho de [startups troubleshooting.](#bkmk_uea_enrollment_tshooter)

## <a name="overview-page"></a>Página de visão geral

Assim que os seus dados estiverem prontos, irá notar algumas informações na página **de visão geral,** explicadas com mais detalhes abaixo:

- A **pontuação** da experiência do Utilizador é uma média ponderada de 50/50 das pontuações de **desempenho** recomendadas do software e **do Arranque.** Vamos expandir o conjunto de subpontuações ao longo do tempo.

- Pode comparar a sua pontuação atual com outras pontuações, definindo uma linha de base.
  - Como descrito na secção [de base,](#bkmk_uea_baselines) há uma linha de base incorporada para a *mediana comercial* para ver como se compara a uma empresa típica. Pode criar novas linhas de base com base nas suas métricas atuais para que possa acompanhar o progresso ou ver regressões ao longo do tempo.
   - Os marcadores de base são mostrados para a sua pontuação geral e subpontuações. Se alguma das pontuações tiver regredido em mais do que o limiar configurável da linha de base selecionada, a pontuação é exibida a vermelho e a pontuação de nível superior é sinalizada como necessitando de atenção.
  - Um estado de **dados insuficientes** significa que não tem dispositivos suficientes a reportar para fornecer uma pontuação significativa. Atualmente, precisamos de pelo menos cinco dispositivos.

- **Os filtros** permitir-lhe-ão visualizar a sua pontuação num subconjunto de dispositivos ou utilizadores. No entanto, a funcionalidade do filtro não está ativada nesta pré-visualização.

- **Insights e recomendações** é uma lista prioritária para melhorar a sua pontuação. Esta lista é filtrada para o contexto do subnódoto quando navega para **as melhores práticas** ou **software Recomendado**.

[![Página geral de análise de endpoint](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a>Software recomendado

> [!Important]  
> Endpoint Analytics calcula a pontuação de **adoção** do Software para todos os seus dispositivos geridos intune, independentemente de terem sido matriculados no Endpoint Analytics ou não.

É sabido que determinado software melhora a experiência do utilizador final, independentemente das métricas de saúde de nível inferior. Por exemplo, o Windows 10 tem uma pontuação de Net Promoter muito mais alta do que o Windows 7. A pontuação de **adoção** do Software é um número entre 0 e 100 que representa uma média ponderada da percentagem de dispositivos que implementaram vários softwarerecomendados. A ponderação atual é maior para o Windows do que para as outras métricas, uma vez que os utilizadores interagem com eles com mais frequência. As métricas são descritas abaixo: 

[![Página de software recomendada de análise endpoint](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a>Windows 10

O Windows 10 oferece uma melhor experiência de utilizador do que as versões mais antigas do Windows. Consulte o [livro branco TEI](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) para obter mais informações.

Esta métrica mede a percentagem de dispositivos no Windows 10 contra uma versão mais antiga do Windows.

A ação de reparação recomendada para dispositivos móveis a partir de versões mais antigas do Windows é criar um plano de implementação utilizando [desktop Analytics](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a>Piloto automático

O Microsoft Autopilot fornece uma experiência inicial de provisionamento mais simples para pCs do Windows 10 do que a experiência nativa, reduzindo o número de ecrãs no out Of Box Experience (OOBE) e fornecendo predefinições, para garantir que o dispositivo dos funcionários está a fornecer corretamente a partir da fábrica ou em reset.

Esta métrica mede a percentagem de dispositivos windows 10 que estão registados para o Autopilot.

A ação de reparação recomendada é registar os dispositivos existentes no Autopilot utilizando o [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a>Diretório Ativo Azure

O Azure Ative Directory (Azure AD) oferece aos utilizadores inúmeros benefícios de produtividade, incluindo um único registo em todo o dispositivo para apps e serviços, sign-in do Windows Hello, recuperação de BitLocker self-service e roaming de dados corporativos.

Esta métrica mede a percentagem de dispositivos matriculados em Azure AD.

Os seus dispositivos geridos microsoft-Intune já estão matriculados no Azure AD. A ação de reparação recomendada para dispositivos geridos pelo Gestor de Configuração é [matriculá-los em Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) ou [cogeri-los](../../comanage/overview.md). Os dispositivos de cogestão também melhoram a sua pontuação de gestão de nuvem.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a>Gestão de nuvens

O Microsoft Intune fornece aos utilizadores vários benefícios de produtividade, incluindo permitir o acesso aos recursos corporativos mesmo quando estão fora da rede corporativa, e elimina a necessidade e desempenho da Política de Grupo, resultando numa melhor experiência de utilizador final. Esta métrica mede a percentagem de computadores matriculados no Microsoft Intune. Veja como [a Microsoft está a permitir isto para os nossos colaboradores.](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune)

A ação de reparação recomendada para dispositivos geridos pelo Gestor de Configuração que ainda não estão matriculados em Intune é [cogeri-los](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a>Sem mediana comercial

A linha de base incorporada da **mediana comercial** não tem atualmente métricas para as subpontuações listadas nas secções acima.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a>Desempenho da startup

> [!NOTE]
> Se não estiver a ver dados de desempenho de startups de todos os seus dispositivos, consulte a inscrição do dispositivo de desempenho do [startup Troubleshooting](#bkmk_uea_enrollment_tshooter).

A pontuação de desempenho do startup ajuda a levar os utilizadores da power-on à produtividade rapidamente, sem longas boot e atrasos de entrada. A **pontuação do Arranque** é um número entre 0 e 100. Esta pontuação é uma média ponderada da **pontuação boot** e da pontuação **sign-in,** que são calculadas da seguinte forma:

- **Pontuação da bota**: Com base no tempo de entrada de energia para iniciar sessão. Olhamos para o último tempo de arranque de cada dispositivo, excluindo a fase de atualização, e depois marcamos de 0 (pobre) a 100 (excecional). Estas pontuações são médias para fornecer uma pontuação total de botas de inquilino.
- **Pontuação de entrada**: Com base no tempo a partir do momento em que as credenciais foram introduzidas até que o utilizador possa aceder a um ambiente de trabalho responsivo (o que significa que o ambiente de trabalho foi renderizado e o uso do CPU caiu abaixo de 50% durante pelo menos 2 segundos). Olhamos para o último tempo de início de hora de entrada para cada dispositivo, excluindo os primeiros sign-ins ou inscrições imediatamente após uma atualização de funcionalidades, e depois marcamos de 0 (pobre) a 100 (excecional). Estas pontuações são médias para fornecer uma pontuação total de botas de inquilino.

[![Página de desempenho de startup de análise endpoint](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Informações

A página de desempenho do **Startup** também fornece uma lista prioritária de **Insights e recomendações,** descritas nas seguintes secções:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a>Discos rígidos

O desempenho do arranque fornece uma visão do número de dispositivos em que o boot drive é um disco rígido. As unidades de disco rígido normalmente resultam em boot vezes três a quatro vezes mais do que as unidades de estado sólido. Também relatamos a melhoria esperada para iniciar o desempenho que obteria ao mudar-se para unidades de estado sólido.

Clique no entanto para ver a lista de dispositivos que têm discos rígidos. A ação recomendada é atualizar estes dispositivos para unidades de estado sólido.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a>Política de Grupo

O desempenho do arranque fornece uma visão sobre o número de dispositivos que têm atrasos no arranque e tempos de iniciação causados pela Política de Grupo. Clicar leva-o à vista dos dispositivos. A vista é classificada pelo tempo de Política de Grupo, para que possa ver dispositivos afetados para mais resolução de problemas.

Se clicar num determinado dispositivo, pode ver a sua bota e a sua história de registo. A história ajuda-o a determinar se o problema é uma regressão e quando pode ter ocorrido.

Embora existam muitos artigos sobre como otimizar o desempenho das Políticas de Grupo, pode optar por migrar para a gestão de nuvens. Migrar para a gestão de nuvem permite-lhe usar as linhas de base de [segurança Intune](https://docs.microsoft.com/intune/protect/security-baselines) e a ferramenta Policy Analytics em breve lançada.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a>Bota lenta e tempos de inscrição

O desempenho do arranque fornece uma visão sobre o número de dispositivos com boot lenta ou tempos de início de sessão. Uma pontuação de arranque ou uma pontuação de "0" significa que é lento. Clicar leva-o à vista dos dispositivos. Os dispositivos são classificados por tempo de arranque do núcleo ou tempo de sinalização do núcleo, respectivamente, para que possa ver os dispositivos afetados para mais resolução de problemas.

Se clicar num determinado dispositivo, pode ver a sua bota e a sua história de registo. A história ajuda-o a determinar se o assunto foi uma regressão e quando poderia ter ocorrido.

### <a name="reporting-tabs"></a>Separadores de relatórios

A página de desempenho do **Startup** tem separadores de relatórios que fornecem suporte para os insights, incluindo:
1. **Desempenho do modelo.** Este separador permite-lhe ver o desempenho do boot e do sign-in por modelo do dispositivo, o que pode ajudá-lo a identificar se os problemas de desempenho estão isolados em determinados modelos.
1. **Desempenho do dispositivo**. Este separador fornece métricas de boot e de iniciação para todos os seus dispositivos. Você pode classificar por uma métrica particular (por exemplo, tempo de inscrição GP) para ver quais os dispositivos que têm as piores pontuações para essa métrica para ajudar na resolução de problemas. Pode também pesquisar um dispositivo pelo nome. Se clicar num dispositivo, pode ver o seu histórico de boot e sign-in, o que pode ajudá-lo a identificar se houve uma regressão recente
1. **Processos de arranque.** Este separador (se visível; só voámos isto para alguns de vocês, uma vez que ainda estamos a desenvolver esta funcionalidade) mostrar-lhe-á quais os processos que estão a impactar a fase de "tempo para desktop responsivo"; isto é - manter o CPU acima de 50% após a prestação do ambiente de trabalho.

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a>Reparações proactivas

As reparações proativas são pacotes de scripts que podem detetar e corrigir problemas de suporte comuns no dispositivo de um utilizador antes mesmo de perceberem que há um problema. Estas reparações podem ajudar a reduzir as chamadas de apoio. Você pode criar seu próprio pacote de script, ou implementar um dos pacotes de script que escrevemos e usamos no nosso ambiente para reduzir os bilhetes de suporte.

Cada pacote de script supor um script de deteção, um script de reparação e metadados. Através do Intune, poderás implementar estes pacotes de scripts e ver relatórios sobre a sua eficácia. Estamos a desenvolver ativamente novos pacotes de guiões e gostaríamos de saber as suas experiências usando-os. Contacte o seu contacto de pré-visualização de análise endpoint se tiver algum feedback sobre os pacotes de script.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a>Obtenha os scripts de deteção e reparação

1. Copie os scripts da parte inferior deste artigo na secção de [scripts PowerShell.](#bkmk_uea_ps_scripts)
    - Os ficheiros script `det` cujos nomes começam são scripts de deteção. Os scripts de `rem`reparação começam com .
    - Para obter uma descrição dos scripts, consulte as [descrições](#bkmk_uea_scripts)do Script .
1. Guarde cada script usando o nome fornecido. O nome também está nos comentários no topo de cada script.
    - Pode usar um nome de script diferente, mas não corresponderá ao nome listado na secção descrições do [Script.](#bkmk_uea_scripts)


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a>Implementação e monitorização de scripts
O serviço de extensão de **gestão intune** da Microsoft obtém os scripts de Intune e executa-os. Os guiões são reexecutados a cada 24 horas. Para implantar e monitorizar as scripts, siga as instruções abaixo:

1. Vá ao nó de **reparações proactivana** na consola.
1. Clique no botão **de pacote de script Criar** um pacote de script.
     [![Página de reparações proactivas de endpoint. Selecione o link de criação.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. Na etapa **basics,** dê ao pacote de script um **nome** e opcionalmente, uma **descrição**. O campo **Publisher** pode ser editado, mas não tem o nome do seu inquilino. **A versão** não pode ser editada. 
1. Na etapa **definições,** copie o texto dos scripts que descarregou para os scripts **de Deteção** e **remediação.** 
   - Precisa do script de deteção e remediação correspondente para estar no mesmo pacote. Por exemplo, `Detect_stale_Group_Policies.ps1` o script de `Remediate_stale_GroupPolicies.ps1` deteção corresponde ao script de reparação.
       [![Análise final analítica Proactive remedia a página de definições de script.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Termine as opções na página **Definições** com as seguintes configurações recomendadas:
   - **Execute este script usando as credenciais de login**: Isto depende do script. Para mais informações, consulte as [descrições](#bkmk_uea_scripts)do Script .
   - **Impor a verificação**de assinatura do script : Não
   - **Executar script em PowerShell de 64 bits**: Não
1. Clique **em Seguinte** e, em seguida, atribua todas as **etiquetas de Âmbito** que precisar.
1. Na etapa de **Atribuiçãos,** selecione os grupos de dispositivos para os quais pretende implementar o pacote de scripts.
1. Complete o **passo Review + Criar** passo para a sua implementação.
1. Em **análise de Endpoint reporting** > **- Reparações proactivas,** pode ver uma visão geral do seu estado de deteção e reparação.
       [![Análise final aanálise Relatório de reparações proactivas, página geral.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Clique no **estado do Dispositivo** para obter detalhes de estado para cada dispositivo na sua implementação.
       [![Análise endpoint Proactiva remedia o estado do dispositivo.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a>Definições de análise de endpoint

A partir da página de definições, pode selecionar **General** ou **Baseline**. Cada uma destas definições é descrita abaixo:

### <a name="general"></a><a name="bkmk_uea_gen"></a>Geral

A página **geral** em **Definições** permite-lhe ver se a recolha de dados de desempenho do arranque intune foi ativada. É ativado automaticamente para todos os seus dispositivos por padrão quando clica **em Iniciar** para ativar a análise da experiência do utilizador. Tem a opção de ir ao nó da política de recolha de dados Intune para alterar o conjunto de dispositivos em que os registos de arranque e de entrada são recolhidos.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a>Política de recolha de dados insintonizada

Para atribuir esta definição a um subconjunto de dispositivos, [Crie um perfil](/intune/configuration/device-profile-create#create-the-profile) com as seguintes informações: 

  - **Nome**: Introduza um nome descritivo para o perfil, como a política de recolha de **dados Intune**
   
  - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    
  - **Plataforma**: selecione **Windows 10 e posterior**
   
  - **Tipo de perfil**: Selecione **monitorização da Saúde do Windows**
   
  - Configurar as **Definições:**
   
       - **Monitorização da Saúde**: Selecione **Ativar** para recolher informações de eventos a partir de dispositivos Windows 10
    
    - **Âmbito**: Selecione **desempenho da bota** 

  - Utilize as [etiquetas de âmbito](/intune/configuration/device-profile-create#scope-tags) e [as regras de aplicabilidade](/intune/configuration/device-profile-create#applicability-rules) para filtrar o perfil para grupos ou dispositivos específicos de TI num grupo que satisfaça critérios específicos.

> [!NOTE]
> Existe um espaço reservado para instruções para configurar o conector de dados do Gestor de Configuração. No entanto, esta funcionalidade não foi implementada nesta pré-visualização privada inicial.

  [![Página de definições gerais de análise de ponto final](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a>Gestão de base

Pode comparar as suas pontuações e subpontuações atuais com outras, definindo uma linha de base.

1. Há uma linha de base incorporada para a **mediana comercial,** que permite comparar as suas pontuações com uma empresa típica.
1. Pode criar novas linhas de base com base nas suas métricas atuais para acompanhar o progresso ou ver regressões ao longo do tempo. Clique no novo botão **Criar** e dê um nome à sua nova linha de base. Recomendamos um nome que inclua a data, por isso é mais fácil selecionar a partir da entrega nas páginas de relatórios.
1. Há um limite de 100 linhas de base por inquilino. Pode eliminar antigas linhas de base que já não são necessárias.
1. As suas métricas atuais serão sinalizadas de vermelho e mostrar-se-ão como regredidas se ficarem abaixo da linha de base atual nos seus relatórios. Como é perfeitamente normal que as métricas oscilem de dia para dia, pode-se estabelecer um limiar de regressão, que não chega a 10%. Com este limiar, as métricas só são sinalizadas como regredidas se tiverem regredido em mais de 10%.

   [![Página de definições de linha de base de análise de ponto final](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a>Resolução de problemas

As secções abaixo podem ser usadas para ajudar em problemas de resolução de problemas que você pode encontrar.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a>Inscrição de dispositivo de desempenho de startup de resolução de problemas

Se a página geral mostrar uma pontuação de desempenho de arranque de zero acompanhada por um banner que mostra que está à espera de dados, ou se o separador de desempenho do dispositivo do startup mostrar menos dispositivos do que espera, existem alguns passos que pode tomar para resolver o problema.

Primeiro, aqui está um resumo rápido das limitações para a recolha de dados de desempenho de startups:
1. Os dispositivos devem ser da versão 1903 do Windows 10 ou posterior.
2. Os dispositivos devem ser adssidos azure. Atualmente não suportamos dispositivos Remetos no Local de Trabalho, embora estejamos a investigar ativamente a viabilidade de adicionar esta funcionalidade ao Windows.
3. Os dispositivos devem ser a edição do Windows 10 Enterprise. O Windows 10 Home and Professional não está atualmente suportado, embora estejam a investigar ativamente a viabilidade de adicionar esta funcionalidade ao Windows.

Note que estes problemas não se aplicarão aos dados provenientes do próximo conector do Gestor de Configuração; será capaz de recolher dados de qualquer PC cliente do Gestor de Configuração, independentemente da versão, edição ou configuração de diretório.

Segundo, aqui está uma lista rápida de verificação para resolver problemas:
1. Certifique-se de que tem o perfil de Monitorização de Saúde do Windows direcionado para todos os dispositivos para os quais pretende obter dados de desempenho. Pode encontrar um link para este perfil a partir da página de definição de análise de ponto final, ou navegar para ele como faria qualquer outro perfil Intune. Veja o separador de atribuição para se certificar de que é atribuído ao conjunto de dispositivos esperado. 
1. Veja quais os dispositivos que foram configurados com sucesso para a recolha de dados. Pode também ver esta informação na página de visão geral dos perfis.  
   - Existe um problema conhecido em que os clientes podem ver erros `-2016281112 (Remediation failed)`de atribuição de perfis, onde os dispositivos afetados mostram um código de erro de . Estamos a investigar ativamente este assunto.
1. Os dispositivos que foram configurados com sucesso para recolha de dados devem ser reiniciados após a recolha de dados, e deve esperar até 24 horas depois para que o dispositivo apareça no separador de desempenho do dispositivo.
1. Se o seu dispositivo foi configurado com sucesso para recolha de dados, foi posteriormente reiniciado e, após 24 horas, ainda não o vê, então pode ser que o dispositivo não consiga chegar aos nossos pontos finais de recolha. Este problema pode acontecer se a sua empresa utilizar um servidor proxy e os pontos finais não tiverem sido ativados no proxy. Para mais informações, consulte [pontos finais de resolução de problemas](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a>Pontos finais

Para inscrever dispositivos para análise de Endpoint, eles precisam enviar dados funcionais necessários para a Microsoft. Se o seu ambiente utilizar um servidor proxy, use estas informações para ajudar a configurar o proxy.

Para permitir a partilha de dados funcionais, configure o seu servidor proxy para permitir os seguintes pontos finais:

> [!Important]  
> Para a privacidade e integridade dos dados, o Windows verifica um certificado Microsoft SSL (fixação de certificado) ao comunicar com os pontos finais de partilha de dados funcionais necessários. Interceção e inspeção ssl não são possíveis. Para utilizar a análise de Endpoint, exclua estes pontos finais da inspeção SSL.<!-- BUG 4647542 -->

| Ponto Final  | Função  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Utilizado para enviar [dados funcionais necessários](#bkmk_uea_datacollection) para o ponto final de recolha de dados Intune. |
| `https://graph.windows.net` | Usado para recuperar automaticamente as definições ao fixar a sua hierarquia à análise de Endpoint (na função De Servidor de Gestor de Configuração). Para mais informações, consulte [Configure o proxy para um servidor](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)de sistema de site . |
| `https://*.manage.microsoft.com` | Usado para sincronizar a recolha e dispositivos do dispositivo com análise de Endpoint (apenas na função de Servidor de Gestor de Configuração). Para mais informações, consulte [Configure o proxy para um servidor](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)de sistema de site . |


### <a name="proxy-server-authentication"></a>Autenticação do servidor proxy

Se a sua organização utilizar a autenticação do servidor proxy para acesso à Internet, certifique-se de que não bloqueia os dados por causa da autenticação. Se o seu representante não permitir que os dispositivos enviem estes dados, não aparecerão no Desktop Analytics.

#### <a name="bypass-recommended"></a>Bypass (recomendado)

Configure os seus servidores proxy para não exigir a autenticação por procuração para o tráfego para os pontos finais de partilha de dados. Esta opção é a solução mais abrangente. Funciona para todas as versões do Windows 10.  

#### <a name="user-proxy-authentication"></a>Autenticação por procuração do utilizador

Configure os dispositivos para utilizar o contexto do utilizador inscrito para autenticação por procuração. Este método requer as seguintes configurações:

- Os dispositivos têm a atual atualização de qualidade para uma versão suportada do Windows

- Configure o proxy de nível de utilizador (proxy WinINET) nas **definições proxy** na Rede & grupo de Definições do Windows. Também pode utilizar o painel de controlo de opções de Internet legado.

- Certifique-se de que os utilizadores têm permissão de procuração para chegar aos pontos finais de partilha de dados. Esta opção requer que os dispositivos possuam utilizadores de consolas com permissões por procuração, pelo que não pode utilizar este método com dispositivos sem cabeça.

> [!IMPORTANT]
> A abordagem de autenticação por procuração do utilizador é incompatível com a utilização da Proteção avançada de ameaças do Microsoft Defender. Este comportamento deve-se ao facto de esta autenticação se basear `0`na chave de registo **DisableEnterpriseAuthProxy** definida para , enquanto o Microsoft Defender ATP exige que seja definido para `1`. Para mais informações, consulte configurações de [proxy de máquina seleção e conectividade](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)de internet no MICROSOFT Defender ATP .

#### <a name="device-proxy-authentication"></a>Autenticação por procuração de dispositivo

Esta abordagem apoia os seguintes cenários:

- Dispositivos sem cabeça, onde nenhum utilizador entra ou utilizadores do dispositivo não têm acesso à Internet

- Proxies autenticados que não usam autenticação integrada do Windows

- Se também utilizar a Proteção avançada de ameaças do Microsoft Defender

Esta abordagem é a mais complexa porque requer as seguintes configurações:

- Certifique-se de que os dispositivos podem chegar ao servidor proxy através do WinHTTP no contexto do sistema local. Utilize uma das seguintes opções para configurar este comportamento:

  - A linha de comando`netsh winhttp set proxy`

  - Protocolo de auto-descoberta de procuração web (WPAD)

  - Procuração transparente

  - Configure o proxy WinINET em todo o dispositivo utilizando a seguinte definição de política de grupo: Faça definições de **procuração por máquina (em vez de por utilizador)** (ProxySettingsPerUser = `1`)

  - Ligação direcionada ou que utiliza tradução de endereços de rede (NAT)

- Configure servidores proxy para permitir que as contas de computador no Ative Directory acedam aos pontos finais dos dados. Esta configuração requer servidores proxy para suportar a Autenticação Integrada do Windows.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>Perguntas frequentes

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Porque é que os guiões estão a sair com um código de 1?

Os scripts saem com um código de 1 para sinalizar para Insinserir que deve ocorrer a reparação. Neste caso, sair de um roteiro de deteção com 1 significa que é verdade que é necessária uma reparação. Muitos pacotes de scriptque funcionam exclusivamente em CM podem mostrar-se conformes, mas sair com um código de 1. Para estes scripts, sair com um código de 1 não é algo alarmante, mas pode querer verificar se o dispositivo repara corretamente.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Porque é que o script update Stale Group Policies regressou com o erro 0x87D00321?

0x87D00321 é um erro de execução do script. Este erro ocorre tipicamente com máquinas que estão ligadas remotamente. Uma potencial mitigação pode ser apenas implantar para uma coleção dinâmica de máquinas que têm conectividade interna da rede.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a>Descrições do guião

Esta tabela mostra os nomes do guião, descrições, deteções, reparações e itens configuráveis. Os ficheiros script `Detect` cujos nomes começam são scripts de deteção. Os scripts de `Remediate`reparação começam com . Estes scripts podem ser copiados a partir da próxima secção deste artigo.

|Nome do script|Descrição|
|---|---|
|**Atualizar políticas de grupo stale** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Deteta se a última atualização da Política de Grupo for maior do que `7 days` há pouco.  </br>Personalize o limiar de 7 `$numDays` dias alterando o valor para o script de deteção. </br></br>Repara-se correndo `gpupdate /target:computer /force` e`gpupdate /target:user /force`  </br> </br>Pode ajudar a reduzir as chamadas de suporte relacionadas com a conectividade da rede quando os certificados e configurações são entregues através da Política de Grupo. </br> </br> **Executar o script usando as credenciais logge-on**: Sim|
|**Reiniciar o serviço Click-to-Run do Office** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Deteta se o serviço Click-to-Run está programado para iniciar automaticamente e se o serviço for interrompido. </br> </br> Repara-se, definindo o serviço para iniciar automaticamente e iniciar o serviço se este for interrompido. </br></br> Ajuda a corrigir problemas em que as Aplicações Win32 Microsoft 365 para empresa não serão lançadas porque o serviço Click-to-Run está parado. </br> </br> **Executar o script usando as credenciais logge-on**: Não|
|**Verificar certificados de rede** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Deteta certificados emitidos por um CA na loja pessoal da Máquina ou do Utilizador que estejam caducadas ou perto de expirar. </br> Especifique o CA `$strMatch` alterando o valor para no script de deteção. Especifique 0 para `$expiringDays` encontrar certificados caducados, ou especifique outro número de dias para encontrar certificados perto de expirar.  </br></br>Repara-se levantando uma notificação de torrada ao utilizador. </br> Especifique os `$Title` valores e `$msgText` valores com o título de mensagem e texto que pretende que os utilizadores vejam. </br> </br> Anota os utilizadores de certificados caducados que possam ter de ser renovados. </br> </br> **Executar o script usando as credenciais logge-on**: Não|
|**Certificados claros** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Deteta certificados caducados emitidos por uma AC na loja pessoal do utilizador atual. </br> Especifique o CA `$certCN` alterando o valor para no script de deteção. </br> </br> Repara-se ao apagar certificados expirados emitidos por uma AC da loja pessoal do utilizador atual. </br> Especifique o CA `$certCN` alterando o valor para o script de reparação. </br> </br> Encontra e elimina os certificados expirados emitidos por uma AC a partir da loja pessoal do utilizador atual. </br> </br> **Executar o script usando as credenciais logge-on**: Sim|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a>PowerShell Scripts

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>Privacidade de dados de análise endpoint

### <a name="data-flow"></a>Fluxo de dados

A ilustração que se segue mostra como os dados funcionais necessários fluem de dispositivos individuais através dos nossos serviços de dados, armazenamento transitório e para o seu inquilino. Os dados fluem através dos nossos oleodutos empresariais existentes sem depender de dados de diagnóstico do Windows.

[![Diagrama de fluxo de dados de experiência do utilizador](media/dataflow.png)](media/dataflow.png#lightbox)

1. Configure a política de recolha de **dados intune** para dispositivos matriculados. Por predefinição, esta política é atribuída a "Todos os Dispositivos" quando **iniciar** a análise do Endpoint. No entanto, pode [alterar a atribuição a](#bkmk_uea_set) qualquer momento para um subconjunto de dispositivos ou nenhum dispositivo.

2. Os dispositivos enviam dados funcionais necessários.

    - Para dispositivos Intune com a política atribuída, os dados são enviados a partir da extensão de gestão Intune. Para mais informações, consulte [os requisitos.](#bkmk_uea_prereq)
    - Para dispositivos geridos pelo Gestor de Configuração, os dados também podem fluir para a Microsoft Endpoint Management através do conector ConfigMgr. O conector ConfigMgr está ligado à nuvem. Só requer ligação a um inquilino intune, não ligando a cogestão.

> [!Note]  
> Os dados necessários para calcular a pontuação de arranque de um dispositivo são gerados durante o tempo de arranque. Dependendo das definições de potência e do comportamento do utilizador, pode demorar semanas após o dispositivo ter sido corretamente atribuído a política para mostrar a pontuação de arranque na consola de administração.  

3. O serviço microsoft Endpoint Management processa dados para cada dispositivo e publica os resultados tanto para dispositivos individuais como para agregados organizacionais na consola de administração utilizando APIs de Gráfico MS.

A latência média de ponta a ponta é de cerca de 12 horas e é fechada pelo tempo que leva para fazer o processamento diário. Todas as outras partes do fluxo de dados estão quase em tempo real.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Recolha de dados

Atualmente, a funcionalidade básica da Endpoint analytics recolhe informações associadas aos registos de desempenho do arranque que se enquadram nas categorias [identificadas](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) e [pseudónimos.](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data) À medida que adicionamos funcionalidadeadicional ao longo do tempo, os dados recolhidos variarão conforme necessário. Os principais pontos de dados atualmente a ser recolhidos:

#### <a name="identified-data"></a>Dados identificados

- Informações do inventário de hardware
  - **Fazer:** Fabricante de dispositivos
  - **modelo:** Modelo de dispositivo
  - **dispositivoClasse:** A classificação do dispositivo. Por exemplo, Desktop, Server ou Mobile.
  - **País:** A definição da região do dispositivo
- Inventário da aplicação, como
  - **nome:** Janelas
  - **ver:** A versão do sistema operativo atual.
  
#### <a name="pseudonymized-data"></a>Dados com pseudónimo

- Dados de diagnóstico, desempenho e utilização associados a um utilizador e/ou dispositivo
  - **logOnId**
  - **bootId:** O ID do arranque do sistema
  - **coreBootTimeInMillisegundos:** Hora da bota do núcleo
  - **totalBootTimeInMillisegundos:** Tempo total de arranque
  - **atualizarTimeInMilliseconds:** Hora de as atualizações do OS completarem
  - **gpLogonDurationInMilliseconds**: Tempo para as políticas do grupo processarem
  - **desktopShownDurationInMillisegundos:** Hora de trabalhar (explorer.exe) para ser carregado
  - **desktopUsdurationInMillisegundos:** Hora de desktop (explorer.exe) ser utilizável
  - **topProcesses:** Lista de processos carregados durante o arranque com nome, com estatísticas de utilização do CPU e detalhes da aplicação (Nome, editor, versão). Por *exemplo\"{\"Nome de\"processo :\"\"\"\"\\\\\\\\\\\\\"\"\"\"&reg; &reg; \"\"\"\"\"\"\"\"\"svchost\", CpuUsage :43, ProcessFullPath : C: Windows System32 svchost.exe , ProductName : Microsoft Windows Operating System , Publisher : Microsoft Corporation , ProductVersion : 10.0.18362.1 }\"*
- Dados de dispositivo que não estão associados a um dispositivo ou utilizador (se estes dados estiverem associados a um dispositivo ou utilizador, o Intune trata-os como se fossem dados identificados)
  - **ID:** ID de dispositivo único usado pelo Windows Update
  - **localId:** Um ID único definido localmente para o dispositivo. Este não é o nome do dispositivo legível pelo homem. Muito provavelmente igual ao valor armazenado na HKLM\Software\Microsoft\SQMClient\MachineId.
  - **addispositivo:** Id do dispositivo de diretório ativo Azure
  - **orgId:** GUID único representando o Microsoft O365 Tenant
  
> [!Important]  
> As nossas políticas de tratamento de dados são descritas na Declaração de [Privacidade Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)da Microsoft . Apenas utilizamos os dados do seu cliente para lhe fornecer os serviços que se inscreveu. Como descrito durante o processo de embarque, anonimizamos e agregamos as pontuações de todas as organizações inscritas para manter as linhas de base atualizadas.


### <a name="resources"></a>Recursos

Para obter mais informações sobre aspetos de privacidade relacionados, consulte os seguintes artigos:

- [Declaração de Privacidade do Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 e conformidade com a privacidade](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Termos de licenciamento e documentação](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Segurança e privacidade nos centros de dados do Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  
- [Confiança na nuvem de confiança](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centro de Fidedignidade](https://www.microsoft.com/trustcenter)  
