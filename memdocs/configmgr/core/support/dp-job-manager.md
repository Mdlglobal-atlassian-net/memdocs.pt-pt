---
title: Gestor de Fila de Tarefas de DP
titleSuffix: Configuration Manager
description: Utilize o DP Job Queue Manager para resolver problemas e gerir os trabalhos de distribuição de conteúdos para pontos de distribuição do Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713661"
---
# <a name="dp-job-queue-manager"></a>Gestor de Fila de Tarefas de DP

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Fila de Trabalho do Ponto de Distribuição (DP) é uma das ferramentas do Gestor de [Configuração](tools.md). Use-o para resolver problemas e gerir os trabalhos de distribuição de conteúdos em curso para pontos de distribuição do Gestor de Configuração. 

A ferramenta apresenta a lista de trabalhos que a componente gestora de transferência seleções tem na sua fila. Mostra também o estatuto dos postos de trabalho: prontos para serem executados, executados ou retentados. Permite-lhe manipular os empregos na fila, mover empregos mais altos na lista, cancelar um emprego ou começar a trabalhar manualmente.

Também obtém informações do servidor do site em que ponto de distribuição está a executar um trabalho. A ferramenta liga-se através do fornecedor ao servidor do site. Não se liga a todos os pontos de distribuição remota para recolher esta informação. Como desencadeia ações e obtém informações através do fornecedor, há um atraso em refletir alterações dos pontos de distribuição remota.



## <a name="usage"></a>Utilização

Executar **DPJobMgr.exe**. O menu principal da ferramenta contém os seguintes separadores: 

- [Ligação](#bkmk_connect): Estabelecer a ligação inicial ao servidor do site primário  

- [Resumo](#bkmk_overview): Resume, numa única vista, todos os postos de trabalho que estão a funcionar em todos os pontos de distribuição  

- [Distribution Point Info](#bkmk_dp-info): Pontos de distribuição multi-selecionados para rastreá-los, e gerir um único trabalho de interesse  

- [Gerir empregos](#bkmk_manage-jobs): Mostra de uma só vez uma lista de todos os empregos e seus estatutos. Manipular empregos, movê-los para cima, cancelar ou começar manualmente.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Ligar o separador

Utilize este separador para estabelecer a ligação inicial ao servidor do site primário. Utiliza as credenciais do utilizador atualmente assinadas. Não é possível ligar-se ao site da administração central ou aos locais secundários. A ligação requer a função de segurança **do Administrador Completo.**

Uma vez que a ferramenta estabelece com sucesso uma ligação, uma notificação na parte inferior da ferramenta confirma que está ligada ao servidor do site. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a>Separador de visão geral

Mostra um resumo de todos os trabalhos em todos os pontos de distribuição. Consulte as seguintes colunas:  

- **Ponto de distribuição**: Lista os nomes dos pontos de distribuição  

- **Empregos**em execução : Mostra o número de postos de trabalho simultâneos que estão a funcionar num determinado ponto de distribuição.  

    > [!Tip]  
    > O número de distribuições de software simultâneas é uma definição de site. Modificou esta definição nas propriedades dos componentes de distribuição de software.  

- **Empregototal**: Mostra o número de todos os postos de trabalho direcionados para um determinado ponto de distribuição. Este número inclui os trabalhos que estão a funcionar, a tentar ou à espera de serem executados.  

- **Total de Retries**: Mostra o número de vezes que os postos de trabalho têm vindo a ser retentados num determinado ponto de distribuição. Um número mais elevado pode representar um problema geral com esse ponto de distribuição específico.  


> [!Tip]  
> - Para classificar cada coluna neste separador, clique no nome da coluna  
> 
> - Atualizar manualmente a informação neste separador clicando em **Refresh**  
> 
> - Afrese automaticamente a informação neste separador clicando em **Iniciar Atualização Automática** e definindo o intervalo de atualização automática. O intervalo de atualização padrão é de dois minutos.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a>Separador de info ponto de distribuição

Mostra a lista de todos os pontos de distribuição sob o site conectado. O painel à esquerda lista todos os pontos de distribuição. Clique em **Selecionar Tudo** ou **Desmarcar Tudo** se necessário ou vários pontos de distribuição específicos nesta lista. O painel à direita mostra os trabalhos para os pontos de distribuição selecionados.

Há oito colunas:  

- **Ícone do estado**: Existem três possíveis ícones de estado:  

    - **Pronto**: Indica que um determinado trabalho terminou todas as etapas de verificação. Está pronto para ser adicionado aos trabalhos simultâneos. Os empregos neste estado costumam estar numa fase de espera. Esperam que os processos de corrida atuais terminem para lhes abrir um espaço.  

    - **Execução**: Indica que um determinado trabalho está atualmente a funcionar num ponto de distribuição. Para empregos de longa duração (grandes pacotes), normalmente há tempo para obter o progresso (%) para a conclusão. Mostra esta percentagem na coluna **Progress** neste ponto de vista. Para pequenas embalagens, a coluna **Progress** pode permanecer vazia. O trabalho pode já estar concluído quando receber o estatuto do ponto de distribuição remota.  

    - **Retry**: Indica que um determinado trabalho falhou e está agora em estado de novo. Este trabalho é novamente julgado após o intervalo de novo. Este intervalo é configurável e definido para 30 minutos por padrão.  

- **Software**: Nome do pacote que é direcionado para um determinado ponto de distribuição  

- **ID do pacote**: Id do pacote que é direcionado para um determinado ponto de distribuição  

- **Tamanho**: Tamanho da embalagem em KB  

- **Progresso**: Percentagem de conclusão de emprego. Para mais informações, consulte a descrição do ícone do estado **de execução.**  

- **Início/Tempo de Arranque**: Para um trabalho em funcionamento, este valor é o tempo de início (verde). Para um trabalho de novo, este valor é o momento em que vai voltar a tentar o trabalho.  

- **Repetições**: Número de vezes que voltou a experimentar este pacote.  

- **Nome**do ponto de distribuição : O nome de domínio totalmente qualificado (FQDN) do ponto de distribuição  

> [!Tip]  
> - Para classificar cada coluna neste separador, clique no nome da coluna  
> 
> - Atualizar manualmente a informação neste separador clicando em **Refresh**  
> 
> - Afrese automaticamente a informação neste separador clicando em **Iniciar Atualização Automática** e definindo o intervalo de atualização automática. O intervalo de atualização padrão é de dois minutos.  
> 
> - Se precisar modificar um determinado trabalho, clique no trabalho nesta vista e selecione **Manage Job**. Esta ação abre o [separador Gerir empregos.](#bkmk_manage-jobs)  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a>Gerir o separador Jobs

Mostra de uma só vez uma lista de todos os empregos e seus estatutos. Contém as mesmas oito colunas que o [separador Info](#bkmk_dp-info)ponto de distribuição . Nesta perspetiva, clique à direita nos trabalhos para as seguintes ações:  

- **Run**: Começa um trabalho que está em qualquer estado que não correr  

- **Move To Top**: Move um ou mais empregos para o topo da fila. Esta ação pode resultar em postos de trabalho a funcionar imediatamente. Um trabalho de menor prioridade pode parar por causa desta ação.  

- **Move Up**: Move um trabalho particular uma linha acima. Um trabalho de menor prioridade pode parar de funcionar por causa desta ação.  

- **Move Down**: Move um trabalho particular uma linha abaixo.  

- **Mova-se para baixo:** Move um ou mais empregos para o fundo da fila.  

    > [!Tip]  
    > Empregos drag-and-drop na lista para movê-los.  

- **Cancelamento**: Tenta cancelar um ou mais postos de trabalho.  

    > [!Note]  
    > Não pode cancelar os empregos perto do tempo final de conclusão. Se o servidor do site também for um ponto de distribuição, não pode cancelar trabalhos no servidor do site.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Gestor de transferência de pacotes](../plan-design/hierarchy/package-transfer-manager.md)
