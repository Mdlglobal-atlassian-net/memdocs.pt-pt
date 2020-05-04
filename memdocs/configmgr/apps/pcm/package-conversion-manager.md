---
title: Gestor de Conversão de Pacotes
titleSuffix: Configuration Manager
description: Saiba mais sobre o Gestor de Conversão de Pacotes para converter pacotes em aplicações no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709916"
---
# <a name="package-conversion-manager"></a>Gestor de Conversão de Pacotes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

A partir da versão 1806, o Gestor de Conversão de Pacotes ajuda-o a converter pacotes legados do Gestor de Configuração em aplicações. As aplicações têm benefícios adicionais, tais como dependências, regras de requisitos, métodos de deteção e afinidade do dispositivo do utilizador.

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1806 como [uma funcionalidade de pré-lançamento.](../../core/servers/manage/pre-release-features.md) A partir da versão 1810, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


Uma aplicação De Configuração Manager contém ficheiros e programas que implementa para dispositivos de cliente. No entanto, ao contrário de pacotes e programas legados, uma aplicação fornece funcionalidades centradas no utilizador adicionais. Por exemplo, uma aplicação pode conter tipos de implementação para uma instalação local de um pacote de software, um pacote de aplicação virtual, ou uma versão da aplicação para dispositivos móveis.

Para obter mais informações, veja os artigos seguintes: 
- [Introdução à gestão de aplicações](../understand/introduction-to-application-management.md)  
- [Pacotes e programas](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Se já instalou uma versão mais antiga do Gestor de Conversão de Pacotes, desinstale-o primeiro antes de atualizar o seu site. Esta versão integrada não requer instalação, mas pode entrar em conflito com as versões existentes.  

Esta versão integrada do Gestor de Conversão de Pacotes trabalha em pacotes no site atual do Gestor de Configuração. Não é uma ferramenta autónoma. Se tiver pacotes e programas numa versão mais antiga do Gestor de Configuração, primeiro migra os pacotes para o seu site de filial atual. Para obter mais informações, consulte os [dados migrados entre hierarquias](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
A versão 1902 do Gestor de Configuração inclui as seguintes melhorias:
- A análise do pacote programado é feita a cada 7 dias por padrão
- PowerShell cmdlets para analisar e converter pacotes
- Correções e melhorias gerais de bugs



## <a name="planning"></a>Planeamento

Antes de começar a converter pacotes em aplicações, primeiro desenvolva um plano. O seguinte processo é um plano de exemplo:

- [Definir um plano de conversão de pacote detalhado](#bkmk_define)  

- [Selecione e prepare pacotes para conversão](#bkmk_prepare)  

- [Selecione pacotes de teste](#bkmk_test)  

- [Analisar, investigar e converter pacotes](#bkmk_analyze)  

- [Testar e implementar as aplicações](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Definir um plano de conversão de pacote detalhado

Esta secção descreve dois planos de conversão de pacotes de amostra:  

- [Um ambiente de teste de alto recurso:](#bkmk_define-high)Você tem um ambiente de teste com os recursos, permissões e arquitetura para replicar totalmente o seu ambiente de produção.  

- [Um ambiente de teste de recursos limitados:](#bkmk_define-limited)Você não tem um ambiente de teste que replica totalmente o seu ambiente de produção.  

Ajuste estes planos conforme necessário para outras questões específicas do seu ambiente.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a>Plano de amostra para um ambiente de teste de alto recurso

O seu ambiente de teste tem os recursos, permissões e arquitetura semelhantes ao seu ambiente de produção. Utilize o ambiente de teste para analisar e converter eficazmente todos os seus pacotes e, em seguida, testar todas as aplicações do Seu Gestor de Configuração. Depois de concluir esse trabalho, transfira-o para o ambiente de produção. 

O seu plano de conversão do pacote pode ser semelhante aos seguintes passos:  

1.  Selecione os pacotes que pretende converter.  

2.  Emigra os pacotes para conversão no seu ambiente de teste.  

3.  Prepare os pacotes para conversão.  

4.  Selecione pacotes de teste.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste as aplicações convertidas.  

7.  Analise e converta os restantes pacotes (não-testados).  

8.  Exportar as aplicações do ambiente de ensaio. Importe-os para o seu ambiente de produção.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a>Plano de amostrapara um ambiente de teste de recursos limitados

O seu ambiente de teste não tem recursos, permissões e arquitetura semelhante ao seu ambiente de produção. Não pode analisar, testar e converter todos os seus pacotes. Neste cenário, apenas analise, investigue, converta e teste os seus pacotes de teste. Em seguida, migrar os pacotes restantes para o ambiente de produção para analisar e converter. 

O seu plano de conversão do pacote pode ser semelhante aos seguintes passos:

1.  Selecione os pacotes que pretende converter.  

2.  Selecione pacotes de teste.  

3.  Migra os pacotes de teste para o teu ambiente de teste.  

4.  Prepare os pacotes de teste para conversão.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste as aplicações convertidas.  

7.  Exportar os pedidos de ensaio do ambiente de ensaio. Em seguida, importe-os para o seu ambiente de produção.  

8.  Migrar os restantes pacotes para o ambiente de produção e prepará-los para a conversão.  

9.  Analisar, investigar e converter os restantes pacotes no ambiente de produção.  

10. Liberte as restantes aplicações para o ambiente de produção.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Selecione e prepare pacotes para conversão

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a>Selecione os pacotes que pretende converter

Nem todos os pacotes são adequados para serem convertidos em aplicações. Antes de começar a converter pacotes, identifique os pacotes que não serão convertidos. 

Os melhores tipos de pacote para conversão para aplicações são aqueles que contêm software orientado para o utilizador, por exemplo:  

- Ficheiros do Instalador do Windows (.msi e .msu)  

- Programas de virtualização de aplicações da Microsoft (App-V)  

- Windows executável ficheiros (.exe)  

Os tipos de pacote que são melhor conservados como pacotes e não convertidos em aplicações incluem:

- Ferramentas de manutenção do sistema. Por exemplo, scripts ou serviços de backup.  

- Pacotes para software que estão fora de suporte.

> [!Tip]  
> Depois de identificar pacotes que não são adequados para conversão em aplicações, mova-os para uma pasta separada na consola 'Gestor de Configuração'. Para criar uma pasta de pacote na consola 'Gestor de Configuração':  
> - Clique no nó dos **Pacotes.**  
> - Selecione **pastas,** e, em seguida, **selecione Criar pasta**.  
> - Introduza o nome `Not Converted`da pasta, por exemplo.  
> - Clique em **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Prepare os pacotes para conversão

Para cada pacote que pretende converter, certifique-se de que estão em conformidade com as seguintes condições:  

- A localização dos ficheiros de origem `\\Server\Share\File`é um caminho completo da UNC, por exemplo.  

- Os ficheiros do Instalador do Windows utilizam apenas um código de produto único.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a>Selecione pacotes de teste

Se possível, o seu grupo de pacotes de teste deve incluir pacotes que satisfaçam os seguintes critérios:  

- Pelo menos um pacote de ensaio com um estado de prontidão de **Automático**.  

- Pelo menos um pacote de ensaio com um estado de prontidão do **Manual**.  

Idealmente, os seus pacotes de teste devem ser pacotes centrais, por exemplo:  

- Pacotes que conhece bem.  

- Pacotes que são os mais importantes para a sua organização.  

- Pacotes que mais facilmente pode testar.  

Identifique os pacotes adequados para testes. Em seguida, mova-os para uma pasta separada na consola 'Gestor de Configuração'.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Analisar, investigar e converter pacotes

#### <a name="analyze-packages"></a>Analisar pacotes

Para analisar um pacote individual ou um pequeno grupo, utilize o Gestor de Conversão de Pacotes integrado na consola Do Gestor de Configuração. Para mais informações, consulte [Como analisar e converter pacotes.](how-to-analyze-and-convert.md)  

> [!NOTE]  
> Consulte o nó **do Estado** de Conversão do Pacote no espaço de trabalho de **monitorização.** Exibe informações sumárias sobre os processos de análise e conversão.  

#### <a name="investigate-analysis-results"></a>Investigar resultados da análise

Depois de analisar os pacotes de teste, investigue as embalagens com um estado de prontidão de **Manual** ou **Erro**. Determina as razões pelas quais têm aquele estado. Algumas razões comuns para um estado de prontidão de **Manual** ou **Erro** incluem:

- O pacote não contém as informações necessárias para criar um método de deteção num tipo de implementação de aplicações.  

- O pacote não contém as informações necessárias para converter coleções em condições e requisitos globais.  

- O pacote contém mais de um programa.  

- O pacote depende de outro pacote que não converteu para uma aplicação.  

Para mais informações, utilize os seguintes recursos:  

- Reveja as mensagens de erro e as correções na [referência técnica para mensagens](error-messages.md) de erro do Gestor de Conversão de Pacotes  

- Reveja o ficheiro de registo **PCMTrace.log**  

- [Resolução de Problemas do Gestor de Conversão de Pacotes](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Converter os pacotes

Para obter mais informações sobre como converter pacotes, consulte [como analisar e converter pacotes](how-to-analyze-and-convert.md).

> [!NOTE]  
> Consulte o nó **do Estado** de Conversão do Pacote no espaço de trabalho de **monitorização.** Exibe informações sumárias sobre os processos de análise e conversão.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a>Testar e implementar as aplicações

Teste as aplicações, quer no seu ambiente de teste, quer no seu ambiente de produção, de acordo com o seu plano de conversão de pacotes detalhado.



## <a name="recommendations"></a>Recomendações

- Utilize o nó **de conversão** do pacote no espaço de trabalho **de monitorização.** Exibe informações sumárias sobre os processos de análise e conversão.  

- Investigue os programas nos seus pacotes conhecidos como invólucros. Utilize o plug-in do Gestor de Conversão de Pacotes para converter as suas funções na funcionalidade de Gestor de Configuração equivalente.  

- Certifique-se de que testa completamente cada aplicação convertida antes de a implementar num ambiente de produção.  



## <a name="next-steps"></a>Passos seguintes

[Como analisar e converter pacotes](how-to-analyze-and-convert.md)
