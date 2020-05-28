---
title: Encontrar ajuda
titleSuffix: Configuration Manager
description: Encontre recursos para informações adicionais sobre o Gestor de Configuração.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bae98a8df1d8b8ff843bd333083c4c6ad68848c
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343189"
---
# <a name="find-help-for-using-configuration-manager"></a>Encontre ajuda para usar o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece as seguintes secções com vários recursos para encontrar ajuda para a utilização do Gestor de Configuração:  

- [Documentação do produto](#bkmk_Info)  

- [Partilhar feedback do produto](#product-feedback)  

- [Siga o blog da equipa do Gestor de Configuração](#BKMK_ProductGroupBlog)  

- [Opções de apoio e recursos comunitários](#BKMK_SupportOptions)  

Para obter ajuda na acessibilidade do produto, consulte [as funcionalidades de acessibilidade.](accessibility-features.md)  



##  <a name="product-documentation"></a><a name="bkmk_Info"></a>Documentação do produto  

Para aceder à documentação mais atual do produto, comece pelo índice da [biblioteca.](https://docs.microsoft.com/sccm/)  

<a name="BKMK_SearchTips"></a>  

Para obter dicas sobre pesquisa, fornecer feedback e mais informações sobre a utilização da documentação do produto, consulte [como utilizar os docs](use-docs.md).  



<a name="product-feedback"></a>

## <a name="product-feedback-starting-with-version-1806"></a><a name="BKMK_1806Feedback"></a>Feedback do produto a partir da versão 1806

A partir da versão 1806 do Gestor de Configuração, pode enviar o feedback do produto diretamente a partir da consola. Se precisar de anexar registos, utilize o [Feedback Hub](#BKMK_FeedbackHub). Pode fazer as seguintes coisas: <!--1357542-->

- **Envie um sorriso**: Envie feedback sobre o que gostou.
- **Envie uma testa:** Envie feedback sobre o que não gostou.
- **Envie uma sugestão**: Leva-o ao [site userVoice](https://configurationmanager.uservoice.com/) para partilhar a sua ideia.

  ![Enviar feedback no Gestor de Configuração 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile-or-send-a-frown"></a>Envie um sorriso ou envie uma franja

Para enviar feedback sobre algo que gostou siga as instruções abaixo:

1. No canto superior direito da consola, clique na face sorridente.
2. No menu suspenso, selecione **Enviar um sorriso** ou enviar uma **franja**.
3. Use a caixa de texto para explicar o que gostou ou o que não gostou. 
4. Escolha se quiser partilhar o seu endereço de e-mail e uma imagem.
5. Clique em **Submeter feedback**
     - Se não tiver conectividade com a Internet, clique em **Guardar** na parte inferior. Siga as instruções no [feedback do Enviar que guardou para](#BKMK_NoInternet) a secção de submissão posterior para enviá-la para a Microsoft. 

![Submeta formulário de feedback no Gestor de Configuração 1806](media/1806-feedback-form.png)

#### <a name="status-messages-for-send-a-smile"></a>Mensagens de estado para enviar um sorriso
<!--5891852-->
A partir do Diretor de Configuração 2002, quando **envia um sorriso** ou envia uma **testa,** é criada uma mensagem de estado quando o feedback é submetido. Esta melhoria fornece um registo de:
- Quando o feedback foi submetido
- Quem submeteu o feedback
- O ID de feedback
- Se a submissão do feedback foi bem sucedida ou não
   - Identificação da mensagem de 53900 para uma submissão bem sucedida.
   - Identificação da mensagem de 53901 para uma submissão falhada.

Ver mensagens de estado a partir de consultas de mensagem de estado do sistema de **monitorização**  >  **System Status**  >  **Status Message Queries**. Comece com a consulta **de Todas as Mensagens de Estado** e selecione o seu prazo. Quando as mensagens carregarem, clique no botão de **mensagens Filter** e filtre para id de mensagem 53900 ou 53901.

As mensagens de estado não são criadas se [enviar feedback que guardou para posterior submissão](find-help.md#BKMK_NoInternet).

[![Mensagem de estado para submeter com sucesso feedback](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### <a name="send-a-suggestion"></a>Enviar uma sugestão

Quando **enviar uma sugestão**, é direcionado para [userVoice](https://configurationmanager.uservoice.com/), um site de terceiros, para partilhar a sua ideia. A equipa de produto Do Gestor de Configuração utiliza os seguintes valores de estado userVoice:

- **Nota -** Entendemos o pedido e faz sentido. Adicionámos isso ao nosso atraso.
- **Planejado** - Começamos a codificar para esta funcionalidade e esperamos que apareça numa pré-visualização tecnológica nos próximos meses.
- **Iniciado** - A funcionalidade está agora numa pré-visualização tecnológica. Vai verificar e dá-nos feedback. Informe-nos se a funcionalidade está no caminho certo ou não. Coloque feedback adicional na secção de comentários do pedido original para que outros vejam e comentem. Vamos ler isso e usar o feedback para tentar melhorar a funcionalidade.
- **Concluída** - A primeira versão da funcionalidade encontra-se numa construção de produção. Este estado não significa que estamos 100% acabados com a funcionalidade, e não vai mais melhorá-lo. Mas significa que v1 das características está numa construção de produção, e você pode começar a usá-lo de verdade. Estamos a marcá-lo completo porque:
  - Queremos que saiba que a funcionalidade está pronta para a produção.
  - Queremos devolver os seus votos userVoice para que possa usá-los em outros itens.
  - Pode apresentar novos Pedidos de Mudança de Design para esta funcionalidade para nos ajudar a conhecer a próxima melhoria mais importante para esta funcionalidade.

### <a name="information-sent-with-feedback"></a>Informação enviada com feedback

Quando **enviar um sorriso** ou **enviar uma testa,** as seguintes informações são enviadas com o feedback:

- Os construir informações
- ID da hierarquia do Gestor de Configuração
- Informação sobre construção de produtos
- Informação linguística
- Identificador de dispositivo 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:Machineid



### <a name="send-feedback-that-you-saved-for-later-submission"></a><a name="BKMK_NoInternet"></a>Envie feedback que guardou para posterior submissão

1. Clique em **Guardar** na parte inferior da janela de **feedback fornecer.** 
2. Guarde o ficheiro .zip. Se a máquina local não tiver acesso à Internet, copie o ficheiro para uma máquina ligada à Internet. 
3. Se necessário, copie a pasta UploadOfflineFeedback localizada em`cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - Para mais informações sobre a última pasta do CD., consulte [o CD. Última pasta](../servers/manage/the-cd.latest-folder.md)

4. Numa máquina ligada à internet, abra um pedido de comando. 
5. Executar o seguinte comando:`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Opcionalmente, pode especificar os seguintes parâmetros:
        -  `-t, --timeout`Tempo de tempo em segundos para enviar os dados. 0 é ilimitado. O padrão é 30.
        - `-s --silent`Sem registo para consola (Não pode combinar com --verbose)
        - `-v, --verbose`Produção verbosa logging para consola (Não pode combinar com --silencioso)
        - `--help`Exibe o ecrã de ajuda
    
    - A partir da versão 1910, o utilitário UploadOfflineFeedback suporta a utilização de um servidor proxy. Pode especificar os seguintes parâmetros:
        - `-x, --proxy`Especifica um servidor proxy para ligar a Internet.
        - `-o, --port`Especifica a porta para o servidor proxy ligar a internet.
        - `-u, --user`Especifica o nome do utilizador para o servidor proxy ligar a Internet.
        - `-w, --password`Especifica a palavra-passe para o servidor proxy ligar a Internet. Digite um asterisco (&#42;) para produzir um aviso para a palavra-passe. A palavra-passe não é apresentada quando a digita no pedido de senha. Recomendamos vivamente a utilização de um asterisco (&#42;) para produzir um aviso para a entrada de palavra-passe, uma vez que o texto simples na linha de comando é menos seguro.
        - `-i`Verificação de ligação skip: Ignora a verificação de ligação de rede, basta fazer upload do feedback com definições especificadas.

## <a name="confirmation-of-console-feedback"></a><a name="bkmk_feedbackid"></a>Confirmação do feedback da consola

<!--3556010-->
A partir da versão 1902, quando envia feedback através da consola Do Gestor de Configuração ou do UploadOfflineFeedback.exe, mostra uma mensagem de confirmação. Esta mensagem inclui um ID de **feedback**, que pode dar à Microsoft como identificador de rastreio.

- Para copiar o ID de **feedback,** selecione o ícone da cópia ao lado do ID ou utilize o atalho da tecla **CTRL**  +  **C.**
  - Esta identificação não está armazenada no seu computador, por isso certifique-se de copiá-la antes de fechar a janela.
- Clicar em **Não mostrar novamente esta mensagem** irá suprimir a caixa de diálogo e impedir que apareça no futuro.

   ![Confirmação de feedback da consola em Configuration Manager 1902](media/1902-feedback-id-example.png)
- A ferramenta de comando **UploadOfflineFeedback** escreve o **FeedbackID** para a consola a menos que -s ou --silent seja usado.

  ![Confirmação de feedback de UploadOfflineFeedback.exe no Gestor de Configuração 1902](media/1902-offline-feedback-id-example.png)

##  <a name="product-feedback-for-versions-1802-and-earlier"></a><a name="BKMK_FeedbackHub"></a>Feedback do produto para versões 1802 e anteriores

Reporte potenciais defeitos de produto através da [aplicação Feedback Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) incorporada no Windows 10. Quando **adicionar um novo feedback,** certifique-se de selecionar a categoria **de Gestão empresarial** e, em seguida, escolher entre uma das seguintes subcategorias:
- Cliente do Configuration Manager
- Consola do Configuration Manager
- Implantação do Sistema de Configuração OS
- Servidor de gestor de configuração

Continue a utilizar a [página UserVoice](https://configurationmanager.uservoice.com/) para votar em novas ideias de funcionalidade no Gestor de Configuração. A equipa de produto Do Gestor de Configuração utiliza os seguintes valores de estado userVoice:

- **Nota -** Entendemos o pedido e faz sentido. Adicionámos isso ao nosso atraso.
- **Planejado** - Começamos a codificar para esta funcionalidade e esperamos que apareça numa pré-visualização tecnológica nos próximos meses.
- **Iniciado** - A funcionalidade está agora numa pré-visualização tecnológica. Vai verificar e dá-nos feedback. Informe-nos se a funcionalidade está no caminho certo ou não. Coloque feedback adicional na secção de comentários do pedido original para que outros vejam e comentem. Vamos ler isso e usar o feedback para tentar melhorar a funcionalidade.
- **Concluída** - A primeira versão da funcionalidade encontra-se numa construção de produção. Este estado não significa que estamos 100% acabados com a funcionalidade, e não vai mais melhorá-lo. Mas significa que v1 das características está numa construção de produção, e você pode começar a usá-lo de verdade. Estamos a marcá-lo completo porque:
  - Queremos que saiba que a funcionalidade está pronta para a produção.
  - Queremos devolver os seus votos userVoice para que possa usá-los em outros itens.
  - Pode apresentar novos Pedidos de Mudança de Design para esta funcionalidade para nos ajudar a conhecer a próxima melhoria mais importante para esta funcionalidade.

##  <a name="configuration-manager-team-blog"></a><a name="BKMK_ProductGroupBlog"></a>Blog de equipe de gestor de configuração  

As equipas de engenharia e parceiros do Gestor de Configuração utilizam o [blog Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para lhe fornecer informações técnicas e outras notícias sobre o Gestor de Configuração e tecnologias relacionadas. As nossas publicações no blogue completam a documentação do produto e as informações de suporte.  


##  <a name="support-options-and-community-resources"></a><a name="BKMK_SupportOptions"></a>Opções de apoio e recursos comunitários  

As hiperligações seguintes fornecem informações sobre as opções de suporte e os recursos da comunidade:  

-   [Suporte da Microsoft](https://aka.ms/cmcbsupport)  

-   [Configuração Manager Community: Guia de sobrevivência do Gestor de Configuração (Ramo Atual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de fóruns do Gestor de Configuração](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
