---
title: Explorador da Biblioteca de Conteúdos
titleSuffix: Configuration Manager
description: Utilize o Explorador da Biblioteca de Conteúdos para visualizar e resolver problemas na biblioteca de conteúdos num ponto de distribuição do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078537"
---
# <a name="content-library-explorer"></a>Explorador da Biblioteca de Conteúdos

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Explorador da Biblioteca de Conteúdos é uma das ferramentas do Gestor de [Configuração.](tools.md) Utilize a ferramenta para as seguintes atividades:  

- Explore a biblioteca de conteúdos num ponto de distribuição específico  

- Problemas de resolução de problemas com a biblioteca de conteúdos  

- Copiar pacotes, conteúdos, pastas e ficheiros fora da biblioteca de conteúdos  

- Redistribuir pacotes para o ponto de distribuição  

- Validar pacotes em pontos de distribuição remota  



## <a name="requirements"></a>Requisitos

- Executar a ferramenta utilizando uma conta que tenha acesso administrativo a:  

    - O ponto de distribuição do alvo  

    - O fornecedor wMI no servidor do site  

    - O fornecedor de Gestor de Configuração  

- Apenas as funções **de Administrador Completo** e Analista de **Leitura** têm direitos suficientes para visualizar todas as informações desta ferramenta.  

    - Outras funções, como o Administrador de **Aplicação,** podem ver informações parciais. Para mais informações, consulte [pacotes de deficientes](#bkmk_disabled-packages).  

    - O **Analista De Leitura não** pode redistribuir pacotes desta ferramenta.  

- Executar a ferramenta a partir de qualquer computador, desde que possa ligar a:  

    - O ponto de distribuição do alvo  

    - O servidor principal do site  

    - O fornecedor de Gestor de Configuração  

- Se o ponto de distribuição for colocalizado com o servidor do site, ainda é necessário ter acesso administrativo ao servidor do site.  



## <a name="usage"></a>Utilização 

Quando iniciar **contentLibraryExplorer.exe,** introduza o nome de domínio totalmente qualificado (FQDN) do ponto de distribuição do alvo. Em seguida, liga-se ao ponto de distribuição. Se o ponto de distribuição faz parte de um site secundário, solicita-lhe o FQDN do servidor principal do site e o código do site primário.

No painel esquerdo, veja as embalagens que são distribuídas para este ponto de distribuição. Expanda os pacotes e explore a estrutura das pastas. Esta estrutura corresponde à estrutura da pasta a partir da qual criou o pacote.

Quando seleciona uma pasta, exibe no painel certo quaisquer ficheiros dentro da pasta. Esta visão inclui as seguintes informações: 
- Nome de ficheiro
- Tamanho dos ficheiros
- Que unidade está em
- Outros pacotes que usam o mesmo ficheiro na unidade
- Quando o ficheiro foi alterado pela última vez no ponto de distribuição

A ferramenta também se liga ao fornecedor de Gestor de Configuração. Esta ligação é para determinar quais os pacotes distribuídos para o ponto de distribuição, e se estão realmente na biblioteca de conteúdos do ponto de distribuição. Por exemplo, um pacote pendente de distribuição pode ainda não existir na biblioteca de conteúdos. Tal pacote apareceria como "PENDENTE" na ferramenta, e não são ativadas ações para este pacote.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a>Pacotes com deficiência

Alguns pacotes estão presentes no ponto de distribuição, mas não visíveis na consola Do Gestor de Configuração. Estes pacotes são marcados com\*um asterisco . Não podem ser realizadas ações nestes pacotes. Outros pacotes também podem ser marcados com um asterisco e ter ações desativadas. 

Existem três razões principais para os pacotes com deficiência:  

- O pacote é o upgrade do cliente do Gestor de Configuração. Este pacote inclui "ccmsetup.exe".  

- A sua conta de utilizador não pode aceder ao pacote, provavelmente devido à administração baseada em papéis. Por exemplo, a função Autor da **Aplicação** não pode ver os pacotes de condutor na consola, pelo que quaisquer pacotes de condutores no ponto de distribuição são marcados como desativados.  

- O pacote está órfão no ponto de distribuição.  


### <a name="validate-packages"></a>Validar pacotes

Valide as embalagens utilizando o **Pacote** > **Validate** na barra de ferramentas. Primeiro selecione um nó de embalagem no painel esquerdo Não selecione um conteúdo ou uma pasta. A ferramenta liga-se ao fornecedor wMI no ponto de distribuição para esta ação. Quando a ferramenta começa, as embalagens que faltam um ou mais conteúdos são marcadas como inválidas. A validação do pacote revela qual o conteúdo que falta. Se todos os conteúdos estiverem presentes, mas os dados forem corrompidos, a validação deteta a corrupção.


### <a name="redistribute-packages"></a>Redistribuir pacotes

Redistribua as embalagens utilizando a**Redistribuição** do **Pacote** > na barra de ferramentas. Primeiro selecione um nó de embalagem no painel esquerdo. Esta ação requer permissões para redistribuir pacotes.


### <a name="other-actions"></a>Outras ações

Utilize a**Cópia** **de Edição** > para copiar pacotes, conteúdos, pastas e ficheiros da biblioteca de conteúdos para uma pasta especificada. Não se pode copiar a própria biblioteca de conteúdos. Selecione mais do que um ficheiro, mas não pode selecionar várias pastas.

Procure pacotes usando **o** > **Pacote Editar Encontrar**. Esta ação procura a sua consulta no nome do pacote e id pacote.



## <a name="limitations"></a>Limitações

- A ferramenta não pode manipular a biblioteca de conteúdos diretamente de forma alguma. As alterações na biblioteca de conteúdos podem resultar em avarias.  

- A ferramenta pode redistribuir pacotes, mas apenas para o ponto de distribuição do alvo.  

- Ao colocar o ponto de distribuição com o servidor do site, não pode validar os dados do pacote. Utilize a consola 'Gestor de Configuração'. A ferramenta ainda inspeciona a embalagem para se certificar de que todo o conteúdo está presente, embora não necessariamente intacto.  

- Não é possível apagar conteúdo com esta ferramenta.



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [A biblioteca de conteúdos](../plan-design/hierarchy/the-content-library.md)
