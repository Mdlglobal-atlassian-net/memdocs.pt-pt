---
title: Antevisão Técnica 1710 / Microsoft Docs
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão 1710 de Pré-visualização Técnica para O Gestor de Configuração.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 503bb6d2293b4b5efb1d84980225a9d7052e1656
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721298"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1710 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1710. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja a [Pré-visualização Técnica para o Gestor](../../core/get-started/technical-preview.md) de Configuração para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **Suporte para Windows 10, versão 1709 (também conhecida como Atualização**de Criadores de outono) .  A partir deste lançamento do Windows, os meios de comunicação windows incluem várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou imagem do sistema operativo, certifique-se de selecionar uma [edição que seja suportada para utilização pelo Select Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **A atualização para uma nova versão de pré-visualização falha quando tiver um servidor de site em modo passivo**. Quando executar uma versão de pré-visualização que tenha um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)tem de desinstalar o servidor do site do modo passivo antes de poder atualizar com sucesso o seu site de pré-visualização para esta nova versão de pré-visualização. Pode reinstalar o servidor do site do modo passivo depois de o site completar a atualização.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola, vá para **a Administração** > **Resumo** > servidores de**configuração** > do site**e funções**do sistema do site, e, em seguida, selecione o servidor de site de modo passivo.
  2. No painel de funções do **Sistema do Site,** clique à direita na função **do servidor do Site** e, em seguida, escolha remover **a função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Melhorias para a implementação de scripts PowerShell do Gestor de Configuração
Com esta versão, os scripts PowerShell que implementa agora suportam a utilização das seguintes melhorias: 
- **Âmbitos de segurança.**  Os scripts agora usam âmbitos de segurança para controlar scripts de autoria e execução. Isto é feito através da atribuição de tags que representam grupos de utilizadores. Para obter mais informações sobre a utilização de âmbitos de segurança, consulte a [configuração da administração baseada em funções para o Gestor de Configuração](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Monitorização em tempo real.** Quando monitorizas a execução de um guião, é agora em tempo real à medida que o guião corre.
- **Validação do parâmetro.** Cada parâmetro no seu script tem um diálogo **script parametria Properties** para que adicione validação para esse parâmetro. Depois de adicionar validação, deverá obter erros se estiver a introduzir um valor para um parâmetro que não cumpra a sua validação.

A implementação dos scripts PowerShell foi introduzida pela primeira vez na [Pré-visualização Técnica Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Foram introduzidas melhorias adicionais com a [Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) e, em seguida, [a Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Experimente!

Para experimentar a utilização da funcionalidade Executar Scripts, consulte [Criar e executar scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limite os dados melhorados do Windows 10 para apenas enviar dados relevantes para a Saúde do Dispositivo Windows Analytics
<!-- 1356148 -->

Com esta versão, pode agora definir o nível de recolha de dados de diagnóstico do Windows 10 para **Enhanced (Limited)**. Esta definição permite-lhe obter informações acionáveis sobre dispositivos no seu ambiente sem que os dispositivos reportem todos os dados ao nível **do Enhanced** com a versão 1709 do Windows 10 ou mais tarde.

O nível Melhorado (Limitado) inclui métricas do nível básico, bem como um subconjunto de dados recolhidos do nível **melhorado** relevante para o Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center já não distorce ícones maiores do que 250x250  
<!-- 1356194 -->

Com esta versão, o Software Center deixará de distorcer ícones que sejam maiores do que 250x250. O Centro de Software fez com que tais ícones parecessem desfocados. Agora pode definir um ícone com dimensões de pixel até 512x512, e exibe sem distorção.

### <a name="try-it-out"></a>Experimente!
Adicione um ícone para a sua aplicação no Software Center. Para experimentá-lo ver [Criar aplicações](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Verifique a conformidade do Software Center para obter dispositivos cogeridos
<!-- 1356374 -->
Nesta versão, os utilizadores podem utilizar o Software Center para verificar a conformidade dos seus dispositivos cogeridos do Windows 10 mesmo quando o acesso condicional é gerido pela Intune. Para mais detalhes, consulte [a Co-management para dispositivos Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Apoio à Guarda de Exploração
Esta versão adiciona suporte para o Windows Defender Exploit Guard. Pode configurar e implementar políticas que gerem os quatro componentes da Exploit Guard. Estes componentes incluem:
-   Redução da Superfície de Ataque
-   Acesso a pastas controladas
-   Exploit Protection
-   Proteção da rede

Os dados de conformidade para a implementação da política Exploit Guard estão disponíveis a partir da consola Do Gestor de Configuração.

Para obter mais informações sobre exploit Guard e componentes e regras específicos, consulte [o Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) na biblioteca de documentação do Windows.

### <a name="prerequisites"></a>Pré-requisitos
Os dispositivos geridos devem executar o Windows 10 1709 Fall Creators Update ou mais tarde e satisfazer os seguintes requisitos dependendo dos componentes e regras configurados:

|Explorar componente da Guarda |Pré-requisitos adicionais|
|------------------------|------------------------|
| Redução da Superfície de Ataque  | Os dispositivos devem ter [uma proteção]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) do Windows Defender AV em tempo real ativada.  |
| Acesso a pastas controladas  | Os dispositivos devem ter [uma proteção]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) do Windows Defender AV em tempo real ativada.   |
| Exploit Protection  | Nenhuma  |
| Proteção da rede  |  Os dispositivos devem ter [uma proteção]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) do Windows Defender AV em tempo real ativada.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Criar uma política de Exploração da Guarda  <!--1355468 -->
1. Na consola 'Gestor de Configuração', vá para a**Proteção**de **Pontofinal de Ativos e conformidade** > , e, em seguida, clique no **Windows Defender Exploit Guard**.
2. No separador **Home,** no grupo **Criar,** clique em **Criar Política de Exploração**.
3. Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.
4. Em seguida, selecione os componentes da Exploit Guard que pretende gerir com esta política. Para cada componente que selecionar, pode configurar detalhes adicionais.
   - **Redução da superfície** de ataque: Configure a ameaça do Office, scripting ameaças e ameaças de e-mail que pretende bloquear ou auditar. Também pode excluir ficheiros ou pastas específicos desta regra.
   - **Acesso de pasta controlada:** Configure o bloqueio ou a auditoria e, em seguida, adicione Apps que possam contornar esta política.  Também pode especificar pastas adicionais que não estão protegidas por predefinição.
   - **Explorar a proteção:**  Especifique um ficheiro XML que contenha configurações para atenuar as explorações de processos e aplicações do sistema. Pode exportar estas definições a partir da aplicação Do Windows Defender Security Center num dispositivo Windows 10.
   - **Proteção da rede:** Detete a proteção da rede para bloquear ou auditar o acesso a domínios suspeitos.
5. Complete o assistente para criar a política, que poderá posteriormente ser implementada para dispositivos.

### <a name="deploy-an-exploit-guard-policy"></a>Implementar uma política de Exploração da Guarda     
Depois de criar políticas de Exploit Guard, use o assistente de política de exploração de implementação para implantá-las. Para isso, abra a consola do Gestor de Configuração para **Ativos e a conformidade** > **endpoint Protection**, e, em seguida, clique em implementar a Política de Guardar **Exploração**.

## <a name="limited-support-for-cng-certificates"></a>Suporte limitado para certificados de GNC
<!-- 1356191 -->
A partir deste lançamento, pode agora utilizar modelos de certificados de [Encriptação API: Próxima Geração (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) para os seguintes cenários:

- Registo e comunicação do cliente com um ponto de gestão HTTPS.   
- Distribuição de software e implementação de aplicações com um ponto de distribuição HTTPS.   
- Implementação do sistema operativo.  
- SDK de mensagens de cliente (com a mais recente atualização) e IsV Proxy.   
- Configuração de Gateway de Gestão de Nuvem.  

Para utilizar certificados CNG, a sua autoridade de certificação (CA) precisa fornecer modelos de certificadocng para máquinas-alvo.  Os detalhes do modelo variam de acordo com o cenário; todavia, são necessárias as seguintes propriedades:

- **Guia** de compatibilidade

    - **A Autoridade de Certificados** deve ser o Windows Server 2008 ou mais tarde. (Recomenda-se o Windows Server 2012.)

    - **O destinatário do certificado** deve ser windows Vista/Server 2008 ou mais tarde. (Recomenda-se o Windows 8/Windows Server 2012.)

- **Separador de criptografia**

    - **A categoria de fornecedor** deve ser **o Fornecedor de Armazenamento chave.**  (Obrigatório)

Para obter os melhores resultados, recomendamos a construção do Nome do Assunto a partir de informações de Diretório Ativo.  Utilize o **formato** de nome DNS para nome de assunto e inclua o nome DNS no nome de assunto alternativo.  Caso contrário, tem de fornecer estas informações quando o dispositivo se inscreve no perfil do certificado.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descrições melhoradas para reiniciar computador pendente   <!--1356283 -->
Na [pré-visualização técnica 1708,](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)adicionámos a capacidade de identificar dispositivos que estão pendentes de um reinício dentro da consola do Gestor de Configuração.

A partir desta pré-visualização técnica, a consola apresenta detalhes adicionais que fornecem informações sobre o processo ou ação que está a solicitar o reboot.

## <a name="device-guard-policy-changes----1355092---"></a>Alterações na política da Guarda de Dispositivos <!-- 1355092 -->
Com a construção de Pré-visualização Técnica de 1710, foram feitas as seguintes três alterações em relação às políticas da Guarda de Dispositivos:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Políticas de Guarda de Dispositivos renomeadas para políticas de Controlo de Aplicações do Windows Defender
As políticas de Guarda de Dispositivos foram renomeadas para as políticas de Controlo de Aplicações do Windows Defender. Assim, por exemplo, o assistente de **política Create Device Guard** é agora nomeado assistente de política de controlo de **aplicações do Windows Defender**.

### <a name="restart-is-not-required-to-apply-policies"></a>Reiniciar não é necessário aplicar políticas
A partir da Atualização dos Criadores de outono para a versão 1709 do Windows, os dispositivos que utilizam a nova versão do Windows não necessitam de um reinício para aplicar as políticas de Controlo de Aplicações do Windows Defender.

Reiniciar é o padrão.

#### <a name="try-it-out"></a>Experimente!  

Se quiser desligar o reinício, siga estes passos:

1.  Abra o assistente de política de controlo de **aplicações Create Windows Defender.**
2.  Na página **Geral,** limpe a caixa de verificação para **impor um reinício dos dispositivos para que esta política possa ser aplicada para todos os processos**.
3.  Clique em **Seguida** até que o assistente complete.

Para versões mais antigas do Windows, um reinício automatizado ainda é imposto.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Executar automaticamente software fidedigno pelo Gráfico de Segurança Inteligente

Os administradores têm agora a opção de permitir que dispositivos bloqueados executem software fidedigno com uma boa reputação, conforme determinado pelo Microsoft Intelligent Security Graph (ISG). O ISG é composto pelo Windows Defender SmartScreen e outros serviços da Microsoft.

Os dispositivos devem estar a executar o Windows Defender SmartScreen para que o software seja de confiança.

#### <a name="try-it-out"></a>Experimente!  

Para permitir que um dispositivo que execute o Windows Defender SmartScreen execute software fidedigno, siga estes passos:

1.  Abra o assistente de política de controlo de **aplicações Create Windows Defender**.
2.  Na página **Inclusãos,** verifique a caixa para **autorizar software que é fidedigno pelo Gráfico**de Segurança Inteligente .
3.  Nos ficheiros ou na caixa de **pastas Fidedignos,** adicione os ficheiros e pastas em que pretende ser confiado.
4.  Clique em **Seguida** até que o assistente complete.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configure e implemente as políticas de Guarda de Aplicações do Windows Defender <!-- 1351960 -->

[O Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo web sites não confiáveis num recipiente isolado seguro que não é acessível por outras partes do sistema operativo. Nesta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de conformidade do Gestor de Configuração que configura e, em seguida, implantamos para uma coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da Atualização do Criador do Windows 10. Para testar esta funcionalidade agora, deve utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar
Para criar e implementar as políticas do Windows Defender Application Guard, os dispositivos Windows 10 para os quais implementa a política devem ser configurados com uma política de isolamento de rede. Para mais informações, consulte a publicação do blog referenciada posteriormente. Esta capacidade funciona apenas com as atuais construções do Windows 10 Insider. Para testá-lo, os seus clientes devem estar a executar uma recente Construção insider do Windows 10.

### <a name="try-it-out"></a>Experimente!

Para compreender o básico sobre o Windows Defender Application Guard, leia [a publicação do blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Para criar uma política, e para navegar nas definições disponíveis:
1. Na consola **'Gestor de Configuração',** escolha **Ativos e Conformidade.**
2. No espaço de trabalho **de Ativos e Compliance,** escolha **A** > Proteção de**Pontos Finais** > guarda de**aplicação Windows Defender**.
3. No separador **Home,** no grupo **Criar,** clique em Criar a Política de Guarda de **Aplicações do Windows Defender**.
4. Utilizando o post do blog como referência, pode navegar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Neste lançamento, adicionámos a nova página de Definição de Rede ao assistente. Aqui, especifique a identidade corporativa e defina o limite da sua rede corporativa.

    > [!NOTE]
    > Os PCs windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma da Windows Information Protection e outra do Windows Defender Application Guard), e implantá-las para o cliente. Se implementar ambas as políticas, estas listas de isolamento da rede devem coincidir. Se implementar listas que não correspondam ao mesmo cliente, a implementação falhará.

    Pode encontrar mais informações sobre como especificar definições de rede na documentação [De proteção de informações do Windows]- [Proteja os seus dados da empresa utilizando a Proteção de Informações do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Quando terminar, complete o assistente e implemente a política para um ou mais dispositivos Windows 10.

### <a name="further-reading"></a>Mais recursos

Para ler mais sobre o Windows Defender Application Guard, consulte [esta publicação do blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autónomo de guarda de aplicação do Windows Defender, consulte [esta publicação de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Passos Seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
