---
title: Implementar conteúdo
titleSuffix: Configuration Manager
description: Depois de instalar pontos de distribuição para O Gestor de Configuração, eis como pode começar a implementar conteúdo para eles.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7478eff1a14eeffd4d12b1539df7c5573c6a7cb6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722978"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Implementar e gerir conteúdos para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de instalar pontos de distribuição para O Gestor de Configuração, pode começar a implementar conteúdo para os mesmos. Normalmente, o conteúdo transfere-se para pontos de distribuição em toda a rede, mas existem outras opções para obter conteúdo para os pontos de distribuição. Após transferências de conteúdo para um ponto de distribuição, pode atualizar, redistribuir, remover e validar esse conteúdo nos pontos de distribuição.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>Distribuir conteúdo  
Normalmente, distribui conteúdo para pontos de distribuição para que esteja disponível para computadores clientes. (A exceção a isto é quando se utiliza a distribuição de conteúdo a pedido para uma implementação específica.)  Quando distribui conteúdo, o Gestor de Configuração armazena ficheiros de conteúdo num pacote e, em seguida, distribui o pacote para o ponto de distribuição. Os tipos de conteúdo que pode distribuir, incluem:  

- Tipos de implementação de aplicações  

- Pacotes  

- Pacotes de implementação  

- Pacotes de controladores  

- Imagens de sistema operativo  

- Instaladores de sistemaoperativo  

- Imagens de arranque  

- Sequências de tarefas  

Quando cria um pacote que contém ficheiros de origem, como um tipo de implementação de aplicações ou pacote de implementação, o site no qual o pacote é criado torna-se o proprietário do site para a fonte de conteúdo do pacote. O Gestor de Configuração copia os ficheiros de origem do ficheiro de origem que especifica para o objeto na biblioteca de conteúdos no servidor do site que detém a fonte de conteúdo do pacote.  Em seguida, o Gestor de Configuração replica a informação para sites adicionais. (Consulte [a biblioteca](../../../../core/plan-design/hierarchy/the-content-library.md) de conteúdos para obter mais informações sobre isto.)  

Utilize o seguinte procedimento para distribuir conteúdo em pontos de distribuição.  

#### <a name="to-distribute-content-on-distribution-points"></a>Para distribuir conteúdo em pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    - **Aplicações**: Expandir aplicações de **gestão** > de**aplicações**e, em seguida, selecionar as aplicações que pretende distribuir.  

    - **Pacotes**: Expandir**pacotes**de **gestão** >  de aplicações e, em seguida, selecionar os pacotes que pretende distribuir.  

    - **Pacotes de implementação**: Expandir pacotes de**implementação**de **atualizações** >  de software e, em seguida, selecionar os pacotes de implementação que pretende distribuir.  

    - **Pacotes de controladores**: Expandir pacotes de controladores de **sistemas** >  **operativos**e, em seguida, selecionar os pacotes de controlador que pretende distribuir.  

    - **Imagens do sistema operativo**: Expandir imagens do sistema operativo dos **sistemas** >  **operativos**e, em seguida, selecionar as imagens do sistema operativo que pretende distribuir.  

    - **Instaladores de sistemaoperativo**: Expandir**instaladores**de **sistemas operativos** > e, em seguida, selecionar os instaladores do sistema operativo que pretende distribuir.  

    - **Imagens de arranque**: Expandir**as imagens**de arranque dos **sistemas operativos** >  e, em seguida, selecionar as imagens de arranque que pretende distribuir.  

    - **Sequências de tarefas**: Expandir as sequências de tarefas **dos sistemas** >  **operativos**e, em seguida, selecionar a sequência de tarefas que pretende distribuir. Embora as sequências de tarefas não contenham conteúdo, têm dependências de conteúdo associadas que são distribuídas.  

      > [!NOTE]  
      > Se modificar a sequência de tarefas, terá de redistribuir o conteúdo.  

3.  No separador **Início** , no grupo **Implementação** , clique em **Distribuir Conteúdo** O Assistente de Conteúdo distribuído abre.  

4.  Na página **Geral,** verifique se o conteúdo listado é o conteúdo que pretende distribuir, escolha se pretende que o Gestor de Configuração detete dependências de conteúdo que estejam associadas ao conteúdo selecionado e adicione as dependências à distribuição e, em seguida, clique em **Next**.  

    > [!NOTE]  
    > Tem a opção de configurar as **dependências de conteúdo associadas ao Detect e adicioná-las a esta definição** de distribuição apenas para o tipo de conteúdo da aplicação. O Gestor de Configuração configura automaticamente esta definição para sequências de tarefas e não pode ser modificada.  

5.  No separador **Conteúdo,** se apresentado, verifique se o conteúdo listado é o conteúdo que pretende distribuir e, em seguida, clique em **Seguinte**.  

    > [!NOTE]  
    > A página **de Conteúdo** exibe apenas quando as dependências de **conteúdo associadas detetam e as adicionam a esta** definição de distribuição na página **geral** do assistente.  

6.  Na página Destino do **Conteúdo,** clique em **Adicionar,** escolha um dos seguintes e siga o passo associado:  

    - **Coleções**: Selecione **Coleções** de utilizadores ou coleções de **dispositivos,** clique na recolha associada a um ou mais grupos de pontos de distribuição e, em seguida, clique em **OK**.  

        > [!NOTE]  
        > Apenas são apresentadas as coleções que estão associadas a um grupo de pontos de distribuição. Para obter mais informações sobre a associação de coleções com grupos de pontos de distribuição, consulte [Gerir grupos](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) de pontos de distribuição no tópico [de Instalação e configurar pontos](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) de distribuição para o tópico do Gestor de Configuração.  

    - **Ponto de distribuição:** Selecione um ponto de distribuição existente e, em seguida, clique em **OK**. Os pontos de distribuição que receberam previamente o conteúdo não são apresentados.  

    - **Grupo ponto de distribuição:** Selecione um grupo de pontos de distribuição existente e, em seguida, clique em **OK**. Os grupos de pontos de distribuição que receberam previamente o conteúdo não são apresentados.  

    Quando terminar de adicionar destinos de conteúdo, clique em **Next**.  

7.  Na página **Resumo,** reveja as definições para a distribuição antes de continuar. Para distribuir o conteúdo para os destinos selecionados, clique em **Next**.  

8.  A página **Progress** mostra o progresso da distribuição.  

9. A página de **Confirmação** mostra se o conteúdo foi atribuído com sucesso aos pontos. Para monitorizar a distribuição de conteúdos, consulte [o monitor de conteúdos que distribuiu com o Gestor de Configuração](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>Utilizar conteúdo pré-encenado  
Pode pré-encenar ficheiros de conteúdo para aplicações e tipos de pacotes:  

- Na consola 'Gestor de Configuração', seleciona o conteúdo de que necessita e, em seguida, utiliza o Assistente de Ficheiros de **Conteúdo Pré-encenado** para criar um ficheiro de conteúdo pré-encenado comprimido que contenha os ficheiros e metadados associados para o conteúdo que selecionou.  

- Em seguida, pode importar manualmente o conteúdo num servidor de site, site secundário ou ponto de distribuição.  

- Quando importa o ficheiro de conteúdo pré-encenado num servidor de site, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no servidor do site e, em seguida, registados na base de dados do servidor do site.  

- Quando importa o ficheiro de conteúdo pré-encenado num ponto de distribuição, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no ponto de distribuição, e uma mensagem de estado é enviada para o servidor do site que informa o site de que o conteúdo está disponível no ponto de distribuição.  

**Limitações e considerações para conteúdos pré-encenados:**  

- Quando o ponto de **distribuição estiver localizado no servidor do site,** não ative o ponto de distribuição para conteúdo pré-encenado. Em vez disso, utilize o procedimento em [Como pré-encenar conteúdo num ponto](#bkmk_dpsiteserver)de distribuição num servidor de site .  

- Quando o ponto de **distribuição estiver configurado como um ponto de distribuição de puxar,** não ative o ponto de distribuição para conteúdo pré-encenado. A configuração de conteúdo pré-estágio para um ponto de distribuição substitui a configuração do ponto de distribuição de puxar. Um ponto de distribuição de puxar configurado para conteúdo pré-encenado não retira conteúdo do ponto de distribuição de origem e não recebe conteúdo do servidor do site.  

- A biblioteca de conteúdos deve ser criada no ponto de distribuição antes de **poder pré-encenar o conteúdo até ao ponto**de distribuição . Distribua conteúdo pela rede pelo menos uma vez antes de pré-fase do conteúdo para o ponto de distribuição.  

- **Quando pré-encenar conteúdo para um pacote com um longo caminho** de origem de pacote (por exemplo, mais de 140 caracteres), a ferramenta de linha de comando extrato content o pode não extrair com sucesso o conteúdo dessa embalagem para a biblioteca de conteúdos.  

Para obter informações sobre quando pré-encenar ficheiros de conteúdo, consulte *conteúdo pré-encenado* na largura de banda da rede Manage para tópico de gestão de [conteúdos.](../../../plan-design/hierarchy/manage-network-bandwidth.md)  

Utilize as seguintes secções para pré-fase do conteúdo.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>Passo 1: Criar um ficheiro de conteúdo pré-encenado  
Pode criar um ficheiro de conteúdo pré-encenado comprimido que contenha os ficheiros e metadados associados para o conteúdo que seleciona na consola 'Gestor de Configuração'. Utilize o seguinte procedimento para criar um ficheiro de conteúdo pré-encenado.  

##### <a name="to-create-a-prestaged-content-file"></a>Para criar um ficheiro de conteúdo pré-encenado  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende pré-encenar:  

    - **Aplicações**: Expandir gestão de **aplicações,** clicar em **Aplicações**e, em seguida, selecionar as aplicações que pretende fazer o pré-estágio.  

    - **Pacotes**: Expandir gestão de **aplicações,** clicar **em Pacotes**e, em seguida, selecionar os pacotes que pretende fazer o pré-estágio.  

    - **Pacotes de controlador**: Expandir **sistemas operativos,** clicar **em Pacotes de Condutor**e, em seguida, selecionar os pacotes de controlador que pretende fazer o estágio.  

    - **Imagens do sistema operativo**: Expandir **sistemas operativos,** clicar em **Imagens do Sistema Operativo**e, em seguida, selecionar as imagens do sistema operativo que pretende fazer o pré-estágio.  

    - **Instaladores de sistemaoperativo**: Expandir **sistemas operativos,** clicar em **Instaladores de Sistemaoperativo,** e, em seguida, selecionar os instaladores do sistema operativo que pretende fazer o pré-estágio.  

    - **Imagens de arranque**: Expandir **sistemas operativos,** clicar em **Boot Images**e, em seguida, selecionar as imagens de arranque que pretende fazer o pré-estágio.  

    - **Sequências de tarefas**: Expandir **sistemas operativos,** clicar em sequências de **tarefas**e, em seguida, selecionar a sequência de tarefas que pretende realizar.  

3.  No separador **Home,** no grupo **Deimplantação,** clique em Criar Ficheiro de **Conteúdo pré-encenado**. O Assistente de Ficheiros de Conteúdo Pré-Encenado cria.  

    > [!NOTE]  
    > **Para candidaturas:** No separador **Casa,** no grupo **Aplicação,** clique em Criar Ficheiro de **Conteúdo Pré-Encenado**.  
    >   
    > **Para pacotes:** No separador **Home,** no &lt;grupo *'Nome pacote*>', clique em Criar Ficheiro de Conteúdo **Pré-encenado**.  

4.  Na página **Geral,** clique em **Navegar,** escolha a localização para o ficheiro de conteúdo pré-encenado, especifique um nome para o ficheiro e, em seguida, clique em **Guardar**. Utiliza este ficheiro de conteúdo pré-encenado em servidores de sites primários, servidores de sites secundários ou pontos de distribuição para importar o conteúdo e os metadados.  

5.  Para aplicações, selecione **Exportar todas as dependências** para que o Gestor de Configuração detete e adicione as dependências associadas à aplicação ao ficheiro de conteúdo pré-encenado. Por predefinição, esta definição está selecionada.  

6.  Nos **comentários do Administrador,** introduza comentários opcionais sobre o ficheiro de conteúdo pré-encenado e, em seguida, clique em **Next**.  

7.  Na página **de Conteúdo,** verifique se o conteúdo listado é o conteúdo que pretende adicionar ao ficheiro de conteúdo pré-encenado e, em seguida, clique em **Next**.  

8.  Na página **'Localizações de Conteúdo',** especifique os pontos de distribuição a partir dos quais se podem recuperar os ficheiros de conteúdo para o ficheiro de conteúdo pré-encenado. Pode selecionar mais de um ponto de distribuição para recuperar o conteúdo. Os pontos de distribuição estão listados na secção de localização de Conteúdos. A coluna **Content** mostra quantos pacotes ou aplicações selecionados estão disponíveis em cada ponto de distribuição. O Gestor de Configuração começa com o primeiro ponto de distribuição da lista para recuperar o conteúdo selecionado e, em seguida, move-se para baixo da lista de forma a recuperar o conteúdo restante necessário para o ficheiro de conteúdo pré-encenado. Clique em **Mover-se** ou **mover-se** para baixo para alterar a ordem prioritária dos pontos de distribuição. Quando os pontos de distribuição da lista não contiverem todos os conteúdos selecionados, deve adicionar pontos de distribuição à lista que contenham o conteúdo ou saiam do assistente, distribuir o conteúdo para pelo menos um ponto de distribuição e, em seguida, reiniciar o assistente.  

9. Na página **resumo,** confirme os detalhes. Pode voltar às páginas anteriores e fazer alterações. Clique em **Seguir** para criar o ficheiro de conteúdo pré-encenado.  

10. A página **Progress** apresenta o conteúdo que está a ser adicionado ao ficheiro de conteúdo pré-encenado.  

11. Na página **'Conclusão',** verifique se o ficheiro de conteúdo pré-encenado foi criado com sucesso e, em seguida, clique em **Fechar**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>Passo 2: Atribuir o conteúdo aos pontos de distribuição  
 Depois de pré-encenar o ficheiro de conteúdo, atribua o conteúdo aos pontos de distribuição.  

> [!NOTE]  
> Quando utiliza um ficheiro de conteúdo pré-encenado para recuperar a biblioteca de conteúdos num servidor de site, e não tem de pré-encenar os ficheiros de conteúdo num ponto de distribuição, pode ignorar este procedimento.  

 Utilize o seguinte procedimento para atribuir o conteúdo no ficheiro de conteúdo pré-encenado aos pontos de distribuição.  

> [!IMPORTANT]  
> Verifique se os pontos de distribuição que pretende pré-estágio são configurados como pontos de distribuição pré-encenados, ou que o conteúdo é distribuído para os pontos de distribuição utilizando a rede.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Para atribuir o conteúdo aos pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que selecionou quando criou o ficheiro de conteúdo pré-encenado:  

    - **Aplicações**: Expandir gestão de **aplicações,** clicar em **Aplicações**e, em seguida, selecionar as aplicações que encenou.  

    - **Pacotes**: Expandir gestão de **aplicações,** clicar **em Pacotes**e, em seguida, selecionar os pacotes que encenou.  

    - **Pacotes de implementação**: Expandir atualizações de **software,** clicar **em Pacotes de Implementação**e, em seguida, selecionar os pacotes de implementação que encenou.  

    - **Pacotes de controlador**: Expandir **sistemas operativos,** clicar **em Pacotes de Condutor**e, em seguida, selecionar os pacotes de controlador que encenou.  

    - **Imagens do sistema operativo**: Expandir **sistemas operativos,** clicar em **Imagens do Sistema Operativo**e, em seguida, selecionar as imagens do sistema operativo que encenou.  

    - **Instaladores de sistemaoperativo**: Expandir **sistemas operativos,** clicar em **Instaladores de Sistemaoperativo,** e, em seguida, selecionar os instaladores do sistema operativo que encenou.  

    - **Imagens de arranque**: Expandir **sistemas operativos,** clicar em **Boot Images**e, em seguida, selecionar as imagens de arranque que encenou.  

3.  No separador **Início** , no grupo **Implementação** , clique em **Distribuir Conteúdo** O Assistente de Conteúdo distribuído abre.  

4.  Na página **Geral,** verifique se o conteúdo listado é o conteúdo que precenou, escolha se deseja que o Gestor de Configuração detete dependências de conteúdo que estejam associadas ao conteúdo selecionado e adicione as dependências à distribuição e, em seguida, clique em **Next**.  

    > [!NOTE]  
    > Tem a opção de configurar as **dependências de conteúdo associadas ao Detect e adicioná-las a esta definição** de distribuição apenas para o tipo de conteúdo da aplicação. O Gestor de Configuração configura automaticamente esta definição para sequências de tarefas e não pode ser modificada.  

5.  Na página **'Conteúdo',** se visualizado, verifique se o conteúdo listado é o conteúdo que pretende distribuir e, em seguida, clique em **Seguinte**.  

    > [!NOTE]  
    > A página **de Conteúdo** exibe apenas quando as dependências de **conteúdo associadas detetam e as adicionam a esta** definição de distribuição na página **geral** do assistente.  

6.  Na página Destino do **Conteúdo,** clique em **Adicionar,** escolha um dos seguintes pontos de distribuição a ser pré-encenado e, em seguida, siga o passo associado:  

    - **Coleções**: Selecione **Coleções** de utilizadores ou coleções de **dispositivos,** clique na recolha associada a um ou mais grupos de pontos de distribuição e, em seguida, clique em **OK**.  

      > [!NOTE]  
      > Apenas são apresentadas as coleções que estão associadas a um grupo de pontos de distribuição.  Para mais informações, consulte [Gerir grupos](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) de pontos de distribuição no [tópico de Instalação e configurar pontos](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) de distribuição para o tópico do Gestor de Configuração.  

    - **Ponto de distribuição:** Selecione um ponto de distribuição existente e, em seguida, clique em **OK**. Os pontos de distribuição que receberam previamente o conteúdo não são apresentados.  

    - **Grupo ponto de distribuição:** Selecione um grupo de pontos de distribuição existente e, em seguida, clique em **OK**. Os grupos de pontos de distribuição que receberam previamente o conteúdo não são apresentados.  

    Quando terminar de adicionar destinos de conteúdo, clique em **Next**.  

7.  Na página **Resumo,** reveja as definições para a distribuição antes de continuar. Para distribuir o conteúdo para os destinos selecionados, clique em **Next**.  

8.  A página **Progress** mostra o progresso da distribuição.  

9. A página de **Confirmação** mostra se o conteúdo foi ou não atribuído com sucesso aos pontos de distribuição. Para monitorizar a distribuição de conteúdos, consulte [o monitor de conteúdos que distribuiu com o Gestor de Configuração](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>Passo 3: Extrair o conteúdo do Ficheiro de Conteúdo Pré-Encenado  
Depois de criar o ficheiro de conteúdo pré-encenado e atribuir o conteúdo a pontos de distribuição, pode extrair os ficheiros de conteúdo para a biblioteca de conteúdos num servidor de site ou ponto de distribuição. Normalmente, copiou o ficheiro de conteúdo pré-encenado para uma unidade portátil como uma unidade USB, ou queimou conteúdo para meios como um DVD, e tem-no disponível na localização do servidor do site ou ponto de distribuição que requer o conteúdo.  

Utilize o seguinte procedimento para exportar manualmente os ficheiros de conteúdo do ficheiro de conteúdo pré-encenado utilizando a ferramenta de linha de comando extrato content.  

> [!IMPORTANT]  
> Quando executa a ferramenta de linha de comando de extrato content, a ferramenta cria um ficheiro temporário à medida que cria o ficheiro de conteúdo pré-encenado. Em seguida, o ficheiro é copiado para a pasta de destino e o ficheiro temporário é eliminado. Deve ter espaço suficiente para este ficheiro temporário ou o processo falha. O ficheiro temporário é criado no seguinte local:  
>   
> - O ficheiro temporário é criado na mesma pasta que especifica como pasta de destino para o ficheiro de conteúdo pré-encenado.  

> [!IMPORTANT]  
> O utilizador que executa a ferramenta de linha de comando de extrato de conteúdo deve ter direitos **de administrador** no computador a partir do qual está a extrair o conteúdo pré-encenado.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Para extrair os ficheiros de conteúdo do ficheiro de conteúdo pré-encenado  

1.  Copie o ficheiro de conteúdo pré-encenado para o computador do qual pretende extrair o conteúdo.  

2.  Copie a ferramenta de &lt;linha de comando de extrato de conteúdo da\\&lt;*plataforma* *ConfigMgrInstallationPath*>\bin> para o computador do qual pretende extrair o ficheiro de conteúdo pré-encenado.  

3.  Abra o pedido de comando e navegue até à localização da pasta do ficheiro de conteúdo pré-encenado e da ferramenta Extract Content.  

    > [!NOTE]  
    > Pode extrair um ou mais ficheiros de conteúdo pré-encenados num servidor de site, servidor de site secundário ou ponto de distribuição.  

4.  Tipo **de extração /P:**&lt;*PrestagedFileLocation PrestagedLocation*>**\\**&lt;*PrestagedFileName*> **/S** para importar um único ficheiro.  

    Tipo **de extração de conteúdo /P:**&lt;*PrestagedFileLocation*> **/S** para importar todos os ficheiros pré-encenados na pasta especificada.  

    Por exemplo, o extrato de tipo **/P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** onde `D:\PrestagedFiles\` está o PrestagedFileLocation, `MyPrestagedFile.pkgx` é o nome de ficheiro pré-encenado, e `/S` informa o Gestor de Configuração para extrair apenas ficheiros de conteúdo que são mais recentes do que o que está atualmente no ponto de distribuição.  

    Quando extrai o ficheiro de conteúdo pré-encenado num servidor de site, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no servidor do site e, em seguida, a disponibilidade de conteúdo é registada na base de dados do servidor do site. Quando exporta o ficheiro de conteúdo pré-encenado num ponto de distribuição, os ficheiros de conteúdo são adicionados à biblioteca de conteúdos no ponto de distribuição, o ponto de distribuição envia uma mensagem de estado para o servidor do site principal dos pais, e então a disponibilidade de conteúdo é registada na base de dados do site.  

    > [!IMPORTANT]  
    > No seguinte cenário, deve atualizar o conteúdo extraído de um ficheiro de conteúdo pré-encenado quando o conteúdo é atualizado para uma nova versão:  
    >   
    >  1.  Cria um ficheiro de conteúdo pré-encenado para a versão 1 de um pacote.  
    >  2.  Atualiza os ficheiros de origem do pacote com a versão 2.  
    >  3.  Extrai o ficheiro de conteúdo pré-encenado (versão 1 da embalagem) num ponto de distribuição.  
    >   
    > O Gestor de Configuração não distribui automaticamente a versão do pacote 2 para o ponto de distribuição. Tem de criar um novo ficheiro de conteúdo pré-encenado que contenha a nova versão do ficheiro e, em seguida, extrair o conteúdo, atualizar o ponto de distribuição para distribuir os ficheiros que mudaram ou redistribuir todos os ficheiros da embalagem.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>Como pré-encenar conteúdo num ponto de distribuição num servidor de site  
Quando um ponto de distribuição é instalado num servidor de site, deve utilizar o seguinte procedimento para pré-fase de estágio com sucesso. Isto porque os ficheiros de conteúdo já estão na biblioteca de conteúdos.  

Quando o ponto de distribuição não estiver ativado para o conteúdo pré-estágio ou quando o ponto de distribuição não estiver localizado num servidor de site, consulte a secção de [conteúdo pré-encenado](#bkmk_prestage) de utilização neste tópico.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Para pré-encenar conteúdo em pontos de distribuição localizados num servidor de site  

1.  Utilize os seguintes passos para verificar se o ponto de distribuição não está ativado para conteúdo pré-encenado.  

    1.  Na consola do Configuration Manager, clique em **Administração**.  

    2.  No espaço de trabalho da **Administração,** clique em **Pontos de Distribuição**e, em seguida, selecione o ponto de distribuição que está localizado no servidor do site.  

    3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

    4.  No separador **Geral,** verifique se o ponto de distribuição Enable para a caixa de verificação de **conteúdo pré-encenado** não foi selecionado.  

2.  Crie o ficheiro de conteúdo pré-encenado utilizando o Passo 1: Criar uma secção de [Ficheirode Conteúdo Pré-encenado](#BKMK_CreatePrestagedContentFile) neste tópico.  

3.  Atribuir o conteúdo ao ponto de distribuição utilizando a secção [Passo 2: Atribuir o Conteúdo à](#BKMK_AssignContentToDistributionPoint) secção Pontos de Distribuição neste tópico.  

4.  No servidor do site, extraio o conteúdo do ficheiro de conteúdo pré-encenado utilizando o Passo 3: Extrair o Conteúdo da secção Ficheiro [de Conteúdo Pré-encenado](#BKMK_ExportContentFromPrestagedContentFile) neste tópico.  

    > [!NOTE]  
    > Quando o ponto de distribuição estiver num site secundário, aguarde pelo menos 10 minutos e, em seguida, utilizando uma consola de Configuração Manager que esteja ligada ao local principal dos pais, atribua o conteúdo ao ponto de distribuição no site secundário.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>Gerir o conteúdo que distribuiu  
Tem as seguintes opções para gerir conteúdos:  
- [Atualizar conteúdo](#update-content)
- [Redistribuir conteúdo](#redistribute-content)
- [Remover conteúdo](#remove-content)
- [validar o conteúdo](#validate-content)

### <a name="update-content"></a>Atualizar conteúdo
Quando a localização do ficheiro de origem para uma implementação for atualizada adicionando novos ficheiros ou substituir ficheiros existentes por uma versão mais recente, pode atualizar os ficheiros de conteúdo nos pontos de distribuição utilizando os Pontos de **Distribuição de Atualização** ou a ação **de Atualização de Conteúdos:**  
- Os ficheiros de conteúdo são copiados da rota de ficheiros de origem para a biblioteca de conteúdos no site que detém a fonte de conteúdo do pacote  
- A versão do pacote é incrementada  
- Cada instância da biblioteca de conteúdos nos servidores do site e nas atualizações de pontos de distribuição apenas com os ficheiros que mudaram  

> [!WARNING]  
> A versão do pacote para aplicações é sempre 1. Quando atualiza o conteúdo para um tipo de implementação de aplicações, o Gestor de Configuração cria um novo ID de conteúdo para o tipo de implementação, e o pacote refere o novo ID de conteúdo.  

#### <a name="to-update-content-on-distribution-points"></a>Para atualizar conteúdos em pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    - **Aplicações**: Expandir aplicações de **gestão** > de**aplicações**e, em seguida, selecionar as aplicações que pretende distribuir. Clique no separador Tipos de **Implementação** e, em seguida, selecione o tipo de implementação que pretende atualizar.  

    - **Pacotes**: Expandir**pacotes**de **gestão** > de aplicações e, em seguida, selecionar os pacotes que pretende atualizar.  

    - **Pacotes de implementação**: Expandir pacotes de**implementação**de **atualizações** > de software e, em seguida, selecionar os pacotes de implementação que pretende atualizar.  

    - **Pacotes de controladores**: Expandir pacotes de controladores de **sistemas** > **operativos**e, em seguida, selecionar os pacotes de controlador que pretende atualizar.  

    - **Imagens do sistema operativo**: Expandir**as imagens**do sistema operativo dos **sistemas** > operativos e, em seguida, selecionar as imagens do sistema operativo que pretende atualizar.  

    - **Instaladores de sistemaoperativo**: Expandir**instaladores**de **sistemas operativos** > e, em seguida, selecionar os instaladores do sistema operativo que pretende atualizar.  

    - **Imagens de arranque**: Expandir**as imagens**de arranque dos **sistemas operativos** >  e, em seguida, selecionar as imagens de arranque que pretende atualizar.  

3.  No separador **Home,** no grupo **'Implementação',** clique em Pontos de Distribuição de **Atualização**e clique em **OK** para confirmar que pretende atualizar o conteúdo.  

    > [!NOTE]  
    > Para atualizar o conteúdo para aplicações, clique no separador **'Tipos de Implementação',** clique no tipo de implementação, clique no **Conteúdo de Atualização**e clique em **OK** para confirmar que pretende renovar o conteúdo.  

    > [!NOTE]  
    > Quando atualiza o conteúdo para imagens de arranque, o Assistente de Ponto de Distribuição de Gestão abre. Reveja as informações na página **Resumo** e, em seguida, complete o assistente para atualizar o conteúdo.  

### <a name="redistribute-content"></a>Redistribuir conteúdo
Pode redistribuir um pacote para copiar todos os ficheiros de conteúdo do pacote para pontos de distribuição ou grupos de pontos de distribuição e, assim, substituir os ficheiros existentes.  

Utilize esta operação para reparar ficheiros de conteúdo na embalagem ou reenviar o conteúdo quando a distribuição inicial falhar. Pode redistribuir um pacote a partir de:  

- Propriedades de pacote  
- Propriedades de ponto de distribuição  
- Propriedades do grupo de pontos de distribuição.  


#### <a name="to-redistribute-content-from-package-properties"></a>Para redistribuir conteúdo das propriedades do pacote  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende distribuir:  

    - **Aplicações**: Expandir aplicações de **gestão** >  de**aplicações**e, em seguida, selecionar a aplicação que pretende redistribuir.  

    - **Pacotes**: Expandir**pacotes**de **gestão** > de aplicações e, em seguida, selecionar o pacote que pretende redistribuir.  

    - **Pacotes de implementação**: Expandir pacotes de**implementação**de **atualizações** >  de software e, em seguida, selecionar o pacote de implementação que pretende redistribuir.  

    - **Pacotes de controladores**: Expandir pacotes de controladores de **sistemas** > **operativos**e, em seguida, selecionar o pacote de controlador que pretende redistribuir.  

    - **Imagens do sistema operativo**: Expandir imagens do sistema operativo dos **sistemas** > **operativos**e, em seguida, selecionar a imagem do sistema operativo que pretende redistribuir.  

    - **Instaladores de sistemaoperativo**: Expandir**instaladores**de **sistemas operativos** > e, em seguida, selecionar o instalador do sistema operativo que pretende redistribuir.  

    - **Imagens de arranque**: Expandir**as imagens**de arranque dos **sistemas operativos** >  e, em seguida, selecionar a imagem de arranque que pretende redistribuir.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **'Localização de Conteúdo',** selecione o ponto de distribuição ou o grupo de pontos de distribuição no qual pretende redistribuir o conteúdo, clique em **Redistribuir,** e depois clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Para redistribuir conteúdo das propriedades do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** clique em **Pontos de Distribuição**e, em seguida, selecione o ponto de distribuição no qual pretende redistribuir conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **Content,** selecione o conteúdo para redistribuir, clique em **Redistribuir,** e depois clique em **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Para redistribuir conteúdo das propriedades do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** clique em Grupos de **Pontos**de Distribuição e, em seguida, selecione o grupo de pontos de distribuição no qual pretende redistribuir conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **Content,** selecione o conteúdo para redistribuir, clique em **Redistribuir,** e depois clique em **OK**.  

    > [!IMPORTANT]  
    > O conteúdo do pacote é redistribuído para todos os pontos de distribuição do grupo de pontos de distribuição.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Use o SDK para forçar a replicação de conteúdos
Pode utilizar o método de classificação de gestão do Windows de Replicação de **RetryContent** (WMI) do Gestor de Configuração SDK para forçar o Gestor de Distribuição a copiar conteúdo da localização de origem para a biblioteca de conteúdos.  

Utilize apenas este método para forçar a replicação quando tiver de redistribuir o conteúdo depois de existirem problemas com a replicação normal de conteúdos (normalmente confirmados pela utilização do nó de monitorização da consola).   

Para obter mais informações sobre esta opção SDK, consulte o Método de [Replicação de RetryContent em classe SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) em MSDN. Microsoft.com.

### <a name="remove-content"></a>Remover conteúdo
Quando já não necessitar de conteúdo nos seus pontos de distribuição, pode remover os ficheiros de conteúdo no ponto de distribuição.  

- Propriedades de pacote  
- Propriedades de ponto de distribuição  
- Propriedades do grupo de pontos de distribuição.  

No entanto, quando o conteúdo está associado a outro pacote que foi distribuído ao mesmo ponto de distribuição, não é possível remover o conteúdo.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Para remover ficheiros de conteúdo de pacote dos pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende eliminar:  

    - **Aplicações**: Expandir aplicações de **gestão** > de**aplicações**e, em seguida, selecionar a aplicação que pretende remover.  

    - **Pacotes**: Expandir**pacotes**de **gestão** > de aplicações e, em seguida, selecionar o pacote que pretende remover.  

    - **Pacotes de implementação**: Expandir pacotes de**implementação**de **atualizações** > de software e, em seguida, selecionar o pacote de implementação que pretende remover.  

    - **Pacotes de controladores**: Expandir pacotes de controladores de **sistemas** > **operativos**e, em seguida, selecionar o pacote de controlador que pretende remover.  

    - **Imagens do sistema operativo**: Expandir imagens do sistema operativo dos **sistemas** > **operativos**e, em seguida, selecionar a imagem do sistema operativo que pretende remover.  

    - **Instaladores de sistemaoperativo**: Expandir instaladores de **sistemas** > **operativos**e, em seguida, selecionar o instalador do sistema operativo que pretende remover.  

    - **Imagens de arranque**: Expandir**as imagens**de arranque dos **sistemas operativos** > e, em seguida, selecionar a imagem de arranque que pretende remover.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **'Localização de Conteúdo',** selecione o ponto de distribuição ou o grupo de pontos de distribuição a partir do qual pretende remover o conteúdo, clique em **Remover**, e depois clique em **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Para remover o conteúdo do pacote das propriedades do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** clique em **Pontos de Distribuição**e, em seguida, selecione o ponto de distribuição no qual pretende eliminar o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **'Conteúdo',** selecione o conteúdo para remover, clique em **Remover**, e depois clique **em OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Para remover o conteúdo das propriedades do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** clique em Grupos de **Pontos**de Distribuição e, em seguida, selecione o grupo de pontos de distribuição no qual pretende remover o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  Clique no separador **'Conteúdo',** selecione o conteúdo para remover, clique em **Remover**, e depois clique **em OK**.  


### <a name="validate-content"></a>Validar o conteúdo
O processo de validação de conteúdos verifica a integridade dos ficheiros de conteúdo nos pontos de distribuição. Permite a validação de conteúdos numa programação ou pode iniciar manualmente a validação de conteúdos a partir das propriedades dos pontos de distribuição e pacotes.  

Quando o processo de validação de conteúdos começa, o Gestor de Configuração verifica os ficheiros de conteúdo nos pontos de distribuição, e se o hash do ficheiro for inesperado para os ficheiros no ponto de distribuição, o Gestor de Configuração cria uma mensagem de estado que pode rever no espaço de trabalho **de Monitorização.**  

Para obter mais informações sobre a configuração do calendário de validação de conteúdos, consulte [as configurações](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) do ponto de distribuição no tópico [de Instalação e configuração](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) de pontos de distribuição para o tópico do Gestor de Configuração.  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Para iniciar a validação de conteúdos para todos os conteúdos num ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No espaço de trabalho **da Administração,** clique em **Pontos de Distribuição**e, em seguida, selecione o ponto de distribuição no qual pretende validar o conteúdo.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No separador **Content,** selecione o pacote no qual pretende validar o conteúdo, clique em **Validar,** clique em **OK**e, em seguida, clique **em OK**. O processo de validação de conteúdos inicia-se para o pacote no ponto de distribuição.  

5.  Para visualizar os resultados do processo de validação de conteúdos, no espaço de trabalho **de Monitorização,** expandir o Estado de **Distribuição,** e clicar no nó de Estado do **Conteúdo.** O conteúdo de cada tipo de pacote (por exemplo, Aplicação, Pacote de Atualização de Software e Imagem de Arranque) é apresentado. Para obter mais informações sobre a monitorização do estado do conteúdo, consulte [o conteúdo do Monitor que distribuiu com o Gestor de Configuração](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Para iniciar a validação de conteúdos para um pacote  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  No espaço de trabalho da Biblioteca de **Software,** selecione um dos seguintes passos para o tipo de conteúdo que pretende validar:  

    - **Aplicações**: Expandir aplicações de **gestão** > de**aplicações**e, em seguida, selecionar a aplicação que pretende validar.  

    - **Pacotes**: Expandir**pacotes**de **gestão** > de aplicações e, em seguida, selecionar o pacote que pretende validar.  

    - **Pacotes de implementação**: Expandir pacotes de**implementação**de **atualizações** > de software e, em seguida, selecionar o pacote de implementação que pretende validar.  

    - **Pacotes de controladores**: Expandir pacotes de controladores de **sistemas** > **operativos**e, em seguida, selecionar o pacote de controlador que pretende validar.  

    - **Imagens do sistema operativo**: Expandir imagens do sistema operativo dos **sistemas** > **operativos**e, em seguida, selecionar a imagem do sistema operativo que pretende validar.  

    - **Instaladores de sistemaoperativo**: Expandir**instaladores**de **sistemas operativos** >  e, em seguida, selecionar o instalador do sistema operativo que pretende validar.  

    - **Imagens de arranque**: Expandir**as imagens**de arranque dos **sistemas operativos** > e, em seguida, selecionar a imagem de arranque que pretende fazer o pré-estágio.  

3.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No separador **'Localização de Conteúdo',** selecione o ponto de distribuição ou o grupo de pontos de distribuição para validar o conteúdo, clique em **Validar,** clique em **OK**e, em seguida, clique em **OK**. O processo de validação de conteúdos começa para o conteúdo no ponto de distribuição selecionado ou grupo de pontos de distribuição.  

5.  Para visualizar os resultados do processo de validação de conteúdos, no espaço de trabalho **de Monitorização,** expandir o Estado de **Distribuição,** e clicar no nó de Estado do **Conteúdo.** O conteúdo de cada tipo de pacote (por exemplo, Aplicação, Pacote de Atualização de Software e Imagem de Arranque) é apresentado. Para obter mais informações sobre a monitorização do estado do conteúdo, consulte o [conteúdo do Monitor que distribuiu com o Gestor de Configuração](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
