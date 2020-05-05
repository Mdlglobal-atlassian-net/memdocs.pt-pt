---
title: Painel de gestão de clientes do Office 365
titleSuffix: Configuration Manager
description: Gabinete de Revisão 365 informações de clientes do Painel de Gestão de Clientes do Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110394"
---
# <a name="office-365-client-management-dashboard"></a>Painel de gestão de clientes do Office 365

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Note]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

Começando na versão 1802 do Gestor de Configuração, pode rever as informações do Office 365 do cliente do painel de gestão de clientes do Office 365. O painel de gestão de clientes do Office 365 apresenta uma lista de dispositivos relevantes quando são selecionadas secções de gráficos. <!--1357281 -->

## <a name="prerequisites"></a>Pré-requisitos

### <a name="enable-hardware-inventory"></a>Ativar o inventário de hardware

Os dados apresentados no painel de instrumentos de Gestão de Clientes do Office 365 provêm do inventário de hardware. Ative o inventário de hardware e selecione a classe de inventário de hardware do **Office 365 ProPlus Configurações** para obter dados para exibir no painel de instrumentos.
 
1. Ativar o inventário de hardware, se ainda não estiver ativado. Para mais detalhes, consulte o inventário de [hardware da Configuração](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. Na consola 'Gestor de Configuração', navegue para as**definições** > padrão do**cliente**de **Administração** > .  
3. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  
4. Na caixa de diálogo **Predefinições de Cliente** , clique em **Inventário de Hardware**.  
5. Na lista **Definições do Dispositivo** , clique em **Definir Classes**.  
6. Na caixa de diálogo de classes de inventário de **hardware,** selecione **Configurações ProPlus do Office 365**.  
7. Clique em **OK** para guardar as suas alterações e fechar a caixa de diálogo **Classes de Inventário de Hardware** .

O painel de instrumentos de Gestão de Clientes do Office 365 começa a apresentar dados à medida que o inventário de hardware é reportado.

### <a name="connectivity-for-top-level-site-server"></a>Conectividade para servidor de site de nível superior

*(Introduzido na versão 1906 como pré-requisito)*

O servidor do site de nível superior precisa de ter acesso ao seguinte ponto final para descarregar o ficheiro de prontidão:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> A conectividade da Internet não é necessária para os dispositivos do cliente para nenhum destes cenários.

### <a name="enable-data-collection-for-office-365-proplus"></a>Ativar a recolha de dados para o Office 365 ProPlus

*(Introduzido na versão 1910 como pré-requisito)*

A partir da versão 1910, terá de permitir a recolha de dados para o Office 365 ProPlus para preencher informações no **Office 365 ProPlus Pilot and Health Dashboard**. Os dados são armazenados na base de dados do Site Do Gestor de Configuração e não enviados para a Microsoft.

Estes dados são diferentes dos dados de diagnóstico, que são descritos nos dados de [Diagnóstico enviados do Office 365 ProPlus para a Microsoft](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

Pode ativar a recolha de dados utilizando a Política de Grupo ou editando o registo.

#### <a name="enable-data-collection-from-group-policy"></a>Ativar a recolha de dados da Política de Grupo

1. Descarregue os mais recentes [ficheiros do Modelo Administrativo do Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49030).
2. Ativar a definição da política `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`de recolha de dados de **telemetria** em baixo .
    - Em alternativa, aplique a definição de política com o serviço de [política de nuvem do Office](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service).
    - A definição de política também é usada pelo Office Telemettry Dashboard, que não precisa de implementar para esta recolha de dados.

#### <a name="enable-data-collection-from-the-registry"></a>Ativar a recolha de dados a partir do registo

O comando abaixo é um exemplo de como ativar a recolha de dados a partir do registo:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualização do painel de gestão de clientes do Office 365

Para ver o painel de gestão de clientes do Office 365 na consola do Gestor de Configuração, vá ao Gabinete de**Visão Geral** > da **Biblioteca** > de Software**365 Gestão**de Clientes. Na parte superior do painel de instrumentos, utilize a definição de drop-down **da Recolha** para filtrar os dados do painel de instrumentos pelos membros de uma recolha específica. Começando na versão 1802 do Gestor de Configuração, o painel de gestão de clientes do Office 365 apresenta uma lista de dispositivos relevantes quando são selecionadas secções de gráficos.

O painel de instrumentos de Gestão de Clientes do Office 365 fornece gráficos para as seguintes informações:

- Número de clientes do Office 365
- Versões de clientes do Office 365
- Escritório 365 línguas de cliente
- Office 365 canais de clientes Para mais informações, consulte [a visão geral dos canais de atualização para o Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a>Integração para prontidão do Office 365 ProPlus
<!--3735402-->
A partir da versão 1902 do Gestor de Configuração, pode utilizar o dashboard para identificar dispositivos com alta confiança que estão prontos a fazer upgrade para o Office 365 ProPlus. Esta integração fornece informações sobre potenciais problemas de compatibilidade com add-ins e macros do Office no seu ambiente. Em seguida, utilize o Gestor de Configuração para implementar o Office em dispositivos prontos.

O painel de gestão de clientes do Office 365 inclui um novo azulejo, **Office 365 ProPlus Upgrade Readiness**. Este azulejo é um gráfico de barras de dispositivos nos seguintes estados:
- Não avaliado
- Pronto para atualizar
- Necessidades de revisão

Selecione um estado para perfurar uma lista de dispositivos. Este relatório de prontidão mostra mais detalhes sobre os dispositivos. Inclui colunas para o estado de compatibilidade de ambos os add-ins e macros do Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Pré-requisitos para integração de prontidão do Office 365 ProPlus

- Ativar o inventário de hardware nas definições do cliente. Para mais informações, consulte a secção [Pré-Requisitos.](#prerequisites)  

- O dispositivo necessita de conectividade com a rede de entrega de conteúdos do Office (CDN) para descarregar um ficheiro de prontidão adicionais. Para mais informações, consulte as redes de entrega de [conteúdos.](https://docs.microsoft.com/office365/enterprise/content-delivery-networks) Se o dispositivo não conseguir descarregar este ficheiro, o estado de adição é *need review*.  

    > [!Note]  
    > Não são enviados dados para a Microsoft para esta funcionalidade.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a>Prontidão macro detalhada

Por padrão, o agente de digitalização olha para a lista de ficheiros mais recentemente utilizada (MRU) em cada dispositivo. Conta os ficheiros desta lista que suportam macros. Estes ficheiros incluem os seguintes tipos:
- Formatos de ficheiros do Office macroactivados, tais como livros de trabalho macroactivados excel (.xlsm) ou documento macro-habilitado word (.docm)  
- Formatos de Escritório mais antigos que não indicam se há conteúdo macro. Por exemplo, um livro Excel 97-2003 (.xls).

Se precisar de informações mais detalhadas sobre a compatibilidade macro, implemente o **Kit de Ferramentas de Prontidão para** o Office analisar o código dentro dos ficheiros macro. Verifica se existem potenciais preocupações de compatibilidade. Por exemplo, o ficheiro utiliza uma função que mudou numa versão mais recente do Office. Depois de executar o Kit de Ferramentas de Prontidão para O Office e selecionar a opção `-mru` para documentos do Office mais **recentemente utilizados e add-ins instalados neste computador,** ou usar a bandeira na linha de comando, os resultados podem ser captados pelo agente de inventário de hardware do Gestor de Configuração. Estes dados adicionais aumentam o cálculo de prontidão do dispositivo. Para mais informações, consulte Utilize o Kit de [Ferramentas de Prontidão para o Office para avaliar a compatibilidade da aplicação para o Office 365 ProPlus](https://aka.ms/readinesstoolkit).

Note que o Kit de Ferramentas de Prontidão não precisa de ser instalado em todos os dispositivos-alvo para efetuar a varredura. Pode utilizar a opção de linha de comando da amostra abaixo para digitalizar cada dispositivo desejado.  A bandeira de saída é necessária, mas os ficheiros não serão utilizados para gerar os resultados no painel de instrumentos, pelo que qualquer localização válida pode ser selecionada.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Para mais informações, consulte Obter informações de [prontidão para vários utilizadores numa empresa](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a>Painel de prontidão de upgrade do Office 365 ProPlus

*(Introduzido na versão 1906)*

<!--4021125-->
Para o ajudar a determinar quais os dispositivos que estão prontos para fazer o upgrade para o Office 365 ProPlus, existe um dashboard de prontidão a partir da versão 1906. Inclui o azulejo de prontidão de **atualização do Office 365 ProPlus** que foi lançado na versão atual do Office Manager de Configuração 1902. Os seguintes azulejos novos neste dashboard ajudam-no a avaliar o complemento do Office e a prontidão macro:

- Implementação
- Prontidão do dispositivo
- Prontidão de adição
- Declarações de suporte adicionais
- Melhores add-ins por contagem de versão
- Número de dispositivos que têm macros
- Macro prontidão
- Macro advisories

O vídeo seguinte é uma sessão da Ignite 2019, que inclui mais informações:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Boas práticas para avaliação de compatibilidade e atualizações proPlus do Microsoft Office 365 usando a prontidão do Office em Gestor de Configuração](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Utilização do painel de prontidão de upgrade do Office 365 ProPlus

Depois de verificar se tem os [pré-requisitos,](#prerequisites)utilize as seguintes instruções para utilizar o painel de instrumentos:
 
1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o **Office 365 Client Management.**
1. Selecione o nó de prontidão de **atualização do Office 365 ProPlus.**
1. Altere a Arquitetura de **Coleção** e **Target Office** para alterar a informação transmitida no painel de instrumentos.

![Painel de prontidão de upgrade do Office 365 ProPlus](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Painel de prontidão de upgrade do Office 365 ProPlus](./media/4021125-office-365-to-add-ins.png)

![Painel de prontidão de upgrade do Office 365 ProPlus](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>Informações de prontidão do dispositivo

Uma vez avaliado o inventário de complemento e macro em cada dispositivo, os dispositivos são então agrupados de acordo com a informação. Os dispositivos cujo estatuto estão listados como **Ready to upgrade** não são suscetíveis de ter quaisquer problemas de compatibilidade.

A seleção da categoria **Ready to upgrade** no gráfico mostra mais detalhes sobre os dispositivos na coleção limitativa. Pode rever a lista de dispositivos, fazer seleções de acordo com os seus requisitos de negócio e criar uma nova recolha de dispositivos a partir da sua seleção. Utilize a sua nova coleção para implementar o Office 365 ProPlus com o Gestor de Configuração.

Os dispositivos que podem estar em risco por problemas de compatibilidade são marcados como **revisão de necessidades**. Estes dispositivos podem necessitar de medidas a tomar antes de os atualizar para o Office 365 ProPlus. Por exemplo, pode atualizar add-ins críticos para uma versão mais recente.

### <a name="add-in-information"></a>Informação de adição

 Em cada dispositivo, é recolhido um inventário de todos os addins instalados. O inventário é então comparado com as informações que a Microsoft tem sobre o desempenho do add-in no Office 365 ProPlus. Se for encontrado um add-in que poderá causar problemas após a atualização, todos os dispositivos com o add-in são sinalizados para revisão.

### <a name="macro-information"></a>Informação macro

O Gestor de Configuração analisa os ficheiros mais recentemente utilizados em cada dispositivo. Conta os ficheiros desta lista que suportam macros, incluindo os seguintes tipos:

- Formatos de ficheiros do Office macro-habilitados.
- Formatos de Escritório mais antigos, que não indicam se há conteúdo macro.

Este relatório pode ser utilizado para identificar quais os dispositivos que utilizaram recentemente ficheiros que podem conter macros. O Kit de **Ferramentas de Prontidão para O Office** pode então ser implementado utilizando o Gestor de Configuração para digitalizar quaisquer dispositivos onde sejam necessárias informações mais detalhadas, e verificar se existem potenciais preocupações de compatibilidade. Por exemplo, se o ficheiro utilizar uma função que mudou numa versão mais recente do Office.

Para obter mais informações sobre como realizar a varredura, consulte a [prontidão de macro detalhada](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a>Painel piloto e painel de saúde do Office 365 ProPlus
<!--4488272, 4488301-->
*(Introduzido na versão 1910)*

A partir da versão 1910, o **Office 365 ProPlus Pilot and Health Dashboard** ajuda-o a planear, pilotar e executar a sua implementação do Office 365 ProPlus. O dashboard fornece informações de saúde para dispositivos com o Office 365 ProPlus para ajudar a identificar possíveis problemas que possam afetar os seus planos de implementação. O **Office 365 ProPlus Pilot and Health Dashboard** fornece uma recomendação para dispositivos piloto baseados em inventário de adição. Os seguintes azulejos estão no painel de instrumentos:

- Gerar piloto
- Dispositivos-piloto recomendados
- Implementar piloto
- Dispositivos que enviam dados de saúde
- Dispositivos que não cumprem objetivos de saúde
- Add-ins não cumprem objetivos de saúde
- Macros não cumprem objetivos de saúde

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Utilização do painel piloto e de saúde do Office 365 ProPlus

Depois de verificar se tem os [pré-requisitos,](#prerequisites)utilize as seguintes instruções para utilizar o painel de instrumentos:

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software,** expanda o **Office 365 Client Management.**
1. Selecione o nó de **Piloto e Saúde do Office 365.**

![Painel piloto e painel de saúde do Office 365 ProPlus](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Gerar piloto

Gere uma recomendação piloto a partir de uma coleção limitativa ao clique de um botão. Assim que a ação é lançada, uma tarefa de fundo começa a calcular a sua coleção piloto. A sua coleção limitativa deve conter pelo menos um dispositivo com uma versão do Office que não seja proPlus.

### <a name="recommended-pilot-devices"></a>Dispositivos-piloto recomendados

**Os dispositivos-piloto recomendados** são um conjunto mínimo de dispositivos que representam todos os add-ins instalados em toda a recolha limitativa que utilizou ao gerar o piloto. Faça uma aperte para obter uma lista destes dispositivos. Em seguida, utilize os detalhes para excluir quaisquer dispositivos do piloto, se necessário. Se todos os seus add-ins já estiverem nos dispositivos Do Office 365 ProPlus, então os dispositivos com esses add-ins não serão incluídos no cálculo. Isto também significa que é possível que não obtenha quaisquer resultados na sua recolha de pilotos, uma vez que todos os seus add-ins foram vistos em dispositivos onde o Office 365 ProPlus está instalado.

### <a name="deploy-pilot"></a>Implementar piloto

Assim que aceitar os seus dispositivos piloto, desloque o Office 365 Proplus para a recolha de pilotos utilizando o assistente de implantação faseado. Os administradores podem definir o piloto e limitar a recolha no assistente para gerir as implementações.

### <a name="health-data"></a>Dados de saúde

Assim que o Office 365 Proplus estiver instalado, ative dados de saúde nos seus dispositivos piloto. Os dados de saúde dão-lhe uma visão sobre quais os add-ins e macros que não cumprem os objetivos de saúde. Os **Dispositivos prontos a implementar** o gráfico identificam dispositivos não pilotoque estão prontos para serem implantados utilizando os conhecimentos sanitários. Obtenha uma contagem de dispositivos que estão enviando dados de saúde dos **Dispositivos enviando** gráfico de dados de saúde.

### <a name="devices-not-meeting-health-goals"></a>Dispositivos que não cumprem objetivos de saúde

Este azulejo resume dispositivos que têm problemas com add-ins, macros ou ambos.

### <a name="add-ins-not-meeting-health-goals"></a>Add-ins não cumprem objetivos de saúde

- Falhas de carga: O add-in não começou.
- Crashs: O add-in falhou enquanto corria.
- Erro: O add-in reportou um erro.
- Múltiplas questões: O add-in tem mais do que uma das questões acima referidas.

### <a name="macros-not-meeting-health-goals"></a>Macros não cumprem objetivos de saúde

- Falhas de carga: O documento não foi carregado.
- Erros de tempo de execução: Ocorreu um erro enquanto a macro estava a funcionar. Estes erros podem depender das inputs, pelo que nem sempre pode ocorrer.
- Compile erros: a macro não compilou corretamente para não tentar correr.
- Múltiplas questões: A macro tem mais do que uma das questões acima.

> [!NOTE]
> O inventário macro é povoado por dados do Kit de Ferramentas de Prontidão para O Escritório e ficheiros de dados recentemente utilizados. A saúde macro é povoada por dados de saúde. Devido às diferentes fontes de dados, é possível que o estado de saúde macro seja **revisão de necessidades** quando o inventário macro não é **digitalizado**. <!--5922845-->

### <a name="known-issues"></a>Problemas conhecidos

Há um problema conhecido com o azulejo **piloto de implantação.** Neste momento não pode ser usado para ser usado para um piloto. A suver é o fluxo de trabalho existente para a implementação de uma aplicação utilizando o Assistente de Implantação Faseada. <!--5525871-->

## <a name="next-steps"></a>Passos seguintes

[Gerir o Office 365 ProPlus com o Configuration Manager](manage-office-365-proplus-updates.md)
