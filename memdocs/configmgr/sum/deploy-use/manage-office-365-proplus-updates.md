---
title: Gerir as atualizações do Office 365 ProPlus
titleSuffix: Configuration Manager
description: O Gestor de Configuração sincroniza as atualizações de clientes do Office 365 do catálogo wSUS para o servidor do site para disponibilizar atualizações para ser implementada aos clientes.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 09d8f0a37e9ed4308c5c8ffcf005c788612be235
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709507"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gerir o Office 365 ProPlus com o Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Note]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

O Gestor de Configuração permite-lhe gerir as aplicações Do Office 365 ProPlus das seguintes formas:

- [Implementação de aplicações do Office 365](#deploy-office-365-apps): Pode iniciar o Instalador office 365 a partir do painel de gestão de [clientes do Office 365](office-365-dashboard.md) para facilitar a experiência inicial de instalação da App Office 365. O assistente permite configurar as definições de instalação do Office 365, transferir ficheiros das Redes de Entrega de Conteúdos do Office (CDNs) e criar e implementar uma aplicação de script com o conteúdo.

- [Implemente as atualizações do Office 365:](#deploy-office-365-updates)Pode gerir as atualizações de clientes do Office 365 utilizando o fluxo de trabalho de gestão de atualizações de software. Quando a Microsoft publicar uma nova atualização de clientes do Office 365 para a Rede de Entrega de Conteúdos do Office (CDN), a Microsoft também publica um pacote de atualização para os Serviços de Atualização do Servidor do Windows (WSUS). Depois de o Gestor de Configuração sincronizar a atualização do cliente do Office 365 do catálogo WSUS para o servidor do site, a atualização está disponível para ser implementada aos clientes.

   > [!NOTE]
   > A partir da versão de 2002 do Gestor de Configuração, pode importar atualizações do Office 365 para ambientes desligados. Para mais informações, consulte [as atualizações do Synchronize Office 365 a partir de um ponto](../get-started/synchronize-office-updates-disconnected.md)de atualização de software desligado .   

- [Adicione idiomas para downloads de atualização do Office 365:](#bkmk_o365_lang)Pode adicionar suporte para O Gestor de Configuração para descarregar atualizações para quaisquer idiomas suportados pelo Office 365. O que significa que o Diretor de Configuração não tem de suportar a linguagem enquanto o Office 365 o fizer. Antes da versão 1610 do Configurmanager, tem de descarregar e implementar atualizações nos mesmos idiomas configurados nos clientes do Office 365.

- [Alterar o canal de atualização](#bkmk_channel): Pode utilizar a política do grupo para distribuir uma alteração de valor chave de registo para os clientes do Office 365 para alterar o canal de atualização.

Para rever a informação do Cliente do Office 365 e iniciar algumas destas ações de gestão do Office 365, utilize o painel de instrumentos de Gestão de [Clientes do Office 365.](office-365-dashboard.md)

## <a name="deploy-office-365-apps"></a>Implementação de aplicações do Office 365  
Inicie o Office 365 Installer a partir do painel de gestão de clientes do Office 365 para a instalação inicial da App Office 365. O assistente permite configurar as definições de instalação do Office 365, transferir ficheiros das Redes de Entrega de Conteúdos do Office (CDNs) e criar e implementar uma aplicação de script para os ficheiros. Até que o Office 365 seja instalado nos clientes e a tarefa de [atualizações automáticas do Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) seja executado, as atualizações do Office 365 não são aplicáveis. Para efeitos de teste, pode executar a tarefa de atualização manualmente.

Para versões anteriores do Gestor de Configuração, deve tomar as seguintes medidas para instalar as aplicações do Office 365 pela primeira vez nos clientes:
- Ferramenta de implantação do Office 365 (ODT)
- Descarregue os ficheiros de origem de instalação do Office 365, incluindo todos os pacotes linguísticos de que necessita.
- Gere a Configuração.xml que especifica a versão e o canal corretos do Office.
- Criar e implementar um pacote legado ou uma aplicação de script para os clientes instalarem as aplicações do Office 365.

### <a name="requirements"></a>Requisitos
- O computador que gere o Instalador office 365 deve ter acesso à Internet.  
- O utilizador que executa o Instalador office 365 deve ter acesso **de Leitura** e **Escrita** à parte de localização do conteúdo fornecida no assistente.
- Se receber um erro de descarregamento 404, copie os seguintes ficheiros para a pasta %temp% do utilizador:
  - [lançamentohistory.xml](https://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](https://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Implementar aplicações do Office 365 utilizando a versão 1806 do Gestor de Configuração: 
A partir do Diretor de Configuração 1806, a Ferramenta de Personalização do Office está integrada com o Instalador office 365 na consola do Gestor de Configuração. Ao criar uma implementação para o Office 365, pode configurar dinamicamente as mais recentes definições de gestão do Office. <!--1358149-->

1. Na consola de Gestor de Configuração, navegue para o Gabinete de Visão Geral da Biblioteca de **Software**  >  **Overview**  >  **365 Gestão**de Clientes.
2. Clique no **Instalador do Office 365** no painel superior direito. Abre o Assistente de Instalação de Clientes do Office 365.
3. Na página Definições de **Aplicação,** forneça um nome e descrição para a aplicação, introduza o local de descarregamento dos ficheiros e, em seguida, clique em **Next**. A localização deve ser especificada como &#92;&#92;*servidor*&#92;*partilhar*.
4. Na página **Definições** do Office, clique em Ir para a ferramenta de **personalização do escritório**. Isto abrirá a ferramenta de personalização do [office para click-to-run](https://config.office.com).
5. Configure as definições desejadas para a instalação do Office 365. Clique no **Submeter** na parte superior direita da página quando completar a configuração. 
6. Na página **de Implantação,** determine se pretende ser implantado agora ou mais tarde. Se optar por implementar mais tarde, poderá encontrar a aplicação em Aplicações de Gestão de Aplicações de **Biblioteca**de  >  **Application Management**  >  **Applications**Software.  
7. Confirme as definições na página **Resumo.** 
8. Clique **em Seguinte,** em seguida, clique em **Fechar** assim que o Assistente de Instalação do Cliente do Office 365 estiver concluído. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Implementar aplicações do Office 365 utilizando a versão 1802 do Gestor de Configuração e anterior:

1. Na consola de Gestor de Configuração, navegue para o Gabinete de Visão Geral da Biblioteca de **Software**  >  **Overview**  >  **365 Gestão**de Clientes.
2. Clique no **Instalador do Office 365** no painel superior direito. Abre o Assistente de Instalação de Clientes do Office 365.
3. Na página Definições de **Aplicação,** forneça um nome e descrição para a aplicação, introduza o local de descarregamento dos ficheiros e, em seguida, clique em **Next**. A localização deve ser especificada como &#92;&#92;*servidor*&#92;*partilhar*.
4. Na página Definições do **Cliente importado,** escolha se importa as definições do cliente do Office 365 a partir de um ficheiro de configuração XML existente ou para especificar manualmente as definições. Clique em **Seguida** quando terminar.  

    Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e salte para o passo 7. Deve especificar a localização no formulário &#92;&#92;*servidor*&#92;*partilhar*&#92;nome *de ficheiro*. XML.
    > [!IMPORTANT]    
    > O ficheiro de configuração XML deve conter apenas [idiomas suportados pelo cliente Do Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Na página **de Produtos clientes,** selecione a suite Office 365 que utiliza. Selecione as aplicações que pretende incluir. Selecione quaisquer produtos adicionais do Office que devam ser incluídos e, em seguida, clique em **Next**.
6. Na página Definições do **Cliente,** escolha as definições para incluir e, em seguida, clique em **Seguinte**.
7. Na página **de Implementação,** escolha se implementa a aplicação e, em seguida, clique em **Seguinte**. <br/>Se optar por não colocar a embalagem no assistente, salte para o passo 9.
8. Configure o resto das páginas do assistente como faria para uma implementação típica da aplicação. Para mais detalhes, consulte [Criar e implementar uma aplicação](../../apps/get-started/create-and-deploy-an-application.md).
9. Conclua o assistente.
10. Pode implementar ou editar **Software Library**a aplicação a partir de aplicações de gestão de  >  **Overview**  >  **Application Management**  >  **aplicações**de visão geral da Biblioteca de Software.    

Depois de criar e implementar aplicações do Office 365 utilizando o Instalador do Office 365, o Gestor de Configuração não gerirá as atualizações do Office por padrão. Para permitir que os clientes do Office 365 recebam atualizações do Gestor de Configuração, consulte [as atualizações do Deploy Office 365 com o Gestor](#deploy-office-365-updates)de Configuração .

Depois de implementar aplicações do Office 365, pode criar regras de implementação automáticas para manter as aplicações. Para criar uma regra de implementação automática para as aplicações do Office 365, clique em **Criar um ADR** a partir do painel de gestão de [clientes do Office 365](office-365-dashboard.md). Selecione **Cliente office 365** quando escolher o produto. Para mais informações, consulte [a implementação automática](automatically-deploy-software-updates.md)de atualizações de software .


## <a name="drill-through-required-office-365-updates"></a>Perfurar através das atualizações necessárias do Office 365
<!--4224414-->
*(Introduzido na versão 1906)*

Pode perfurar as estatísticas de conformidade para ver quais os dispositivos que requerem uma atualização específica do software do Office 365. Para ver a lista do dispositivo, é necessário permissão para visualizar atualizações e as coleções a que os dispositivos pertencem. Para aprofundar a lista do dispositivo:

1. Vá **ao**Gabinete de Gestão de  >  **Clientes 365**Client Management  >  **Office 365 Atualizações.**
1. Selecione qualquer atualização que seja necessária por pelo menos um dispositivo.
1. Olhe para o separador **Resumo** e encontre o gráfico de tartes em **estatísticas.**
1. Selecione a hiperligação necessária para **ver** junto ao gráfico de tartes para aprofundar a lista do dispositivo.
1. Esta ação leva-o a um nó temporário em **Dispositivos** onde pode ver os dispositivos que necessitam da atualização. Você também pode tomar ações para o nó, como criar uma nova coleção a partir da lista.


## <a name="deploy-office-365-updates"></a>Implementação de atualizações do Office 365

Utilize os seguintes passos para implementar as atualizações do Office 365 com o Gestor de Configuração:

1. [Verifique os requisitos](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) para utilizar o Gestor de Configuração para gerir as atualizações do Cliente do Office 365 nos Requisitos para utilizar o Gestor de Configuração para gerir a secção de atualizações de clientes do **Office 365** do artigo.  

2. [Configure os pontos](../get-started/configure-classifications-and-products.md) de atualização de software para sincronizar as atualizações de clientes do Office 365. Detete **atualizações** para a classificação e selecione **O Cliente do Office 365** para o produto. Sincronizar atualizações de software depois de configurar os pontos de atualização de software para utilizar a classificação **Updates.**
3. Ativar os clientes do Office 365 para receber atualizações do Gestor de Configuração. Utilize as definições do cliente do Gestor de Configuração ou a política de grupo para ativar o cliente.

    **Método 1**: Começando na versão 1606 do Gestor de Configuração, pode utilizar a definição de cliente do Gestor de Configuração para gerir o agente cliente do Office 365. Depois de configurar esta definição e implementar atualizações do Office 365, o agente cliente do Gestor de Configuração comunica com o agente cliente do Office 365 para descarregar as atualizações a partir de um ponto de distribuição e instalá-las. O Gestor de Configuração faz o inventário das definições do Cliente ProPlus do Office 365.    

      1. Na consola 'Gestor **Administration**de Configuração', clique em  >  **Configurar**  >  **As Definições**do Cliente de Visão Geral da Administração .  

      2. Abra as definições apropriadas do dispositivo para ativar o agente cliente. Para obter mais informações sobre as definições de clientes padrão e personalizadas, consulte [como configurar as definições](../../core/clients/deploy/configure-client-settings.md)do cliente .  

      3. Clique em **Atualizações de Software** e selecione **Sim** para a gestão ativa da definição de Agente cliente do **Office 365.**  

    **Método 2**: Habilitar os [clientes do Office 365 a receber atualizações](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) do Gestor de Configuração utilizando a Ferramenta de Implementação do Escritório ou a Política de Grupo.  

4. [Implemente as atualizações do Office 365](deploy-software-updates.md) para os clientes.

> [!Important]
> - A partir da versão 1706 Office 365, as atualizações de clientes do Office 365 mudaram-se para o **office 365 Client Management**Office  > **365 Updates.** Este movimento não afetará a configuração atual do ADR. 
> - Antes da versão 1610 do Configurmanager, tem de descarregar e implementar atualizações nos mesmos idiomas configurados nos clientes do Office 365. Por exemplo, digamos que tem um cliente do Office 365 configurado com os idiomas en-us e de-de-de-de-de. No servidor do site, você descarrega e implementa apenas conteúdo en-us para uma atualização do Office 365 aplicável. Quando o utilizador inicia a instalação do Software Center para esta atualização, a atualização fica pendurada enquanto descarrega o conteúdo para de-de-de-de.. 

> [!NOTE]  
>
> Se o Office 365 ProPlus foi instalado recentemente, e dependendo de como foi instalado, é possível que o canal de atualização ainda não tenha sido definido. Nesse caso, as atualizações implementadas serão detetadas como não aplicáveis. Existe uma [tarefa de Atualizações Automáticas programada](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) criada quando o Office 365 ProPlus está instalado. Nesta situação, esta tarefa tem de ser executada pelo menos uma vez para que o canal de atualização seja definido e as atualizações detetadas conforme aplicável.
>
> Se o Office 365 ProPlus foi instalado recentemente e as atualizações implementadas não forem detetadas, para efeitos de teste, pode iniciar manualmente a tarefa de Atualizações Automáticas do Office e, em seguida, iniciar o Ciclo de Avaliação de Implementação de [Atualizações](../understand/software-updates-introduction.md#scan-for-software-updates-compliance-process) de Software no cliente. Para obter instruções sobre como fazê-lo numa sequência de tarefas, consulte o [UpdateIng Office 365 ProPlus numa sequência](manage-office-365-proplus-updates.md#updating-office-365-proplus-in-a-task-sequence)de tarefas .

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Reiniciar o comportamento e as notificações dos clientes para as atualizações do Office 365
Quando implementa uma atualização para um cliente do Office 365, o comportamento de reinício e as notificações do cliente são diferentes dependendo da versão do Gestor de Configuração. A tabela seguinte fornece informações sobre a experiência do utilizador final quando o cliente recebe uma atualização do Office 365:

|Versão do Gestor de Configuração |Experiência do utilizador final|  
|----------------|---------------------|
|1706, 1710|O cliente recebe notificações pop-up e in-app, bem como um diálogo de contagem regressiva, antes de instalar a atualização.|
|1802| O cliente recebe notificações pop-up e in-app, bem como um diálogo de contagem regressiva, antes de instalar a atualização. </br>Se houver pedidos do Office 365 durante uma aplicação de atualização de clientes do Office 365, os pedidos do Office não serão forçados a encerrar. Em vez disso, a instalação da atualização voltará como exigindo um reinício do sistema <!--510006-->|


> [!Important]
>
>Na versão 1706 do Gestor de Configuração, note os seguintes detalhes:
>
>- Um ícone de notificação apresenta na área de notificação na barra de tarefas para aplicações necessárias, onde o prazo é dentro de 48 horas no futuro e o conteúdo da atualização foi descarregado. 
>- Um diálogo de contagem regressiva mostra para aplicações necessárias onde o prazo é dentro de 7.5 horas no futuro e a atualização foi descarregada. O utilizador pode adiar o diálogo de contagem regressiva até três vezes antes do prazo. Quando adiada, a contagem regressiva volta a aparecer após duas horas. Se não for adiada, há uma contagem regressiva de 30 minutos e a atualização é instalada quando a contagem regressiva expirar.
>- Uma notificação pop-up pode não ser exibida até que o utilizador clique no ícone na área de notificação. Além disso, se a área de notificação tiver espaço mínimo, o ícone de notificação pode não ser visível a menos que o utilizador abra ou expanda a área de notificação. 
>- O diálogo de notificação e contagem regressiva pode arrancar enquanto o utilizador não estiver a trabalhar ativamente no dispositivo. Por exemplo, quando o dispositivo está bloqueado durante a noite, é possível que as aplicações do Office que executam o dispositivo possam ser forçadas a fechar para instalar a atualização. Antes de fechar a aplicação, o Office guarda dados da aplicação para evitar a perda de dados. 
>- Se o prazo for no passado ou configurado para começar o mais rapidamente possível, executar aplicações do Office poderá ser forçada a fechar sem notificações. 
>- Se o utilizador instalar uma atualização do Office antes do prazo, o Gestor de Configuração verifica que a atualização está instalada quando o prazo é atingido. Se a atualização não for detetada no dispositivo, a atualização está instalada. 
>- A barra de notificação na aplicação não é exibida numa aplicação do Office que está a ser publicada antes de a atualização ser descarregada. Depois de a atualização ser descarregada, a notificação in-app apresenta apenas para aplicações recém-abertas.
>- Para atualizações do Office desencadeadas por uma janela de serviço ou programadas para horários não comerciais, é possível que as aplicações do Office em execução possam ser forçadas a fechar a atualização sem notificações. 
>- Para mais informações, consulte [notificações de atualização do utilizador final para o Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)


## <a name="add-languages-for-office-365-update-downloads"></a><a name="bkmk_o365_lang"></a>Adicione idiomas para downloads de atualização do Office 365
Pode adicionar suporte para O Gestor de Configuração para descarregar atualizações para quaisquer idiomas suportados pelo Office 365.

### <a name="download-updates-for-additional-languages-in-version-1902"></a>Baixar atualizações para idiomas adicionais na versão 1902
<!--3555955-->

A partir da versão 1902 do Gestor de Configuração, o fluxo de trabalho de atualização separa os 38 idiomas para **a Atualização** do Windows dos inúmeros idiomas adicionais para a Atualização do **Cliente do Office 365**.

Para selecionar os idiomas necessários, utilize a página **de Seleção** de Idiomas nos seguintes locais:
- Criar assistente de regra de implementação automática
- Implementar assistente de atualizações de software
- Descarregue o assistente de atualizações de software
- Propriedades da regra de implementação automática

Na página de **Seleção de Idiomas,** selecione Atualização do **Cliente do Office 365**e, em seguida, clique em **Editar**. Adicione os idiomas necessários para o Office 365 **e,** em seguida, clique OK .

![Screenshot de adicionar idiomas adicionais para o Office 365](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>Para adicionar suporte para baixar atualizações para idiomas adicionais na versão 1810 e anterior

Utilize o seguinte procedimento no ponto de atualização do software no site da administração central ou no site primário autónomo.

> [!IMPORTANT]  
> Configurar idiomas adicionais de atualização do Office 365 é uma definição em todo o site. Depois de adicionar os idiomas utilizando o seguinte procedimento, todas as atualizações do Office 365 são descarregadas nesses idiomas, bem como os idiomas que seleciona na página de Seleção de **Idiomas** nos descarregamentos de software updates ou implemente os assistentes de atualizações de software.

1. A partir de um pedido de comando, escreva *wbemtest* como um utilizador administrativo para abrir o Teste de Instrumentação de Gestão do Windows.
2. Clique em **Ligar**, e, em seguida, *digitar root\sms\site_ &lt; siteCódigo &gt; *.
3. Clique em **Consulta**, e, em seguida, executar a seguinte consulta: *selecione &#42; a partir de SMS_SCI_Component onde o nome componente ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta do WMI](../media/1-wmiquery.png)
4. No painel de resultados, clique duas vezes no objeto com o código do site da administração central ou site primário autónomo.
5. Selecione a propriedade **Props,** clique em **Editar Propriedade,** e, em seguida, clique **em 'Ver Incorporado**' .
   ![Editor de propriedade](../media/2-propeditor.png)
6. A partir do primeiro resultado da consulta, abra cada objeto até encontrar o com **AdicionalUpdateLanguagesForO365** para a propriedade **PropertyName.**
7. Selecione **Value2** e clique em **Editar Propriedade**.  
   ![Editar a propriedade Value2](../media/3-queryresult.png)
8. Adicione idiomas adicionais à propriedade **Value2** e clique em **Guardar Propriedade**. <br/> Por exemplo, pt-pt (para português - Portugal), af-za (para africâner - África do Sul), nn-no (para norueguês (Nynorsk) - Noruega), etc. Escreveria `pt-pt,af-za,nn-no` as línguas de exemplo. Não use espaços entre as línguas.
 
   ![Adicionar idiomas em Editor de Propriedade](../media/4-props.png)  
9. Clique em **Fechar,** clique em **Fechar,** clicar em **Guardar Propriedade**, e clique em **Guardar Objeto** (se clicar em **Fechar** aqui os valores são descartados). Clique em **Fechar**e, em seguida, clique em **Sair** para sair do Teste de Instrumentação de Gestão do Windows.
10. Na consola de Gestor de Configuração, vá ao Gabinete de Visão Geral da **Biblioteca**de Software  >  **Overview**  >  **365**Client Management  >  **Office 365 Atualizações.**
11. Agora, quando descarrega as atualizações do Office 365, as atualizações são descarregadas nos idiomas que seleciona no assistente e configuradas neste procedimento. Para verificar se as atualizações descarregam nos idiomas corretos, aceda à fonte do pacote para a atualização e procure ficheiros com o código de idioma no nome de ficheiro.  
    ![Nomes de ficheiros com idiomas adicionais](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>Atualizar o Office 365 ProPlus numa sequência de tarefas
Ao utilizar a sequência de [tarefas de Instalação](../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates) de Atualizações de Software para instalar atualizações do Office 365, é possível que as atualizações implementadas sejam detetadas como não aplicáveis.  Isto pode acontecer se a tarefa de Atualizações Automáticas do Office não tiver sido executada pelo menos uma vez (ver a nota no [Deploy Office 365 atualizações).](manage-office-365-proplus-updates.md#deploy-office-365-updates) Por exemplo, isto pode acontecer se o Office 365 ProPlus fosse instalado imediatamente antes de executar este passo.

Para garantir que o canal de atualização está definido para que as atualizações implementadas sejam corretamente detetadas, utilize um dos seguintes métodos:

**Método 1:**
1. Numa máquina com a mesma versão do Office 365 ProPlus, aberto Agendador de Tarefas (taskschd.msc) e identificar a tarefa de atualizações automáticas do Office 365. Normalmente, está localizado no âmbito do **Task Scheduler Library**  > **Microsoft** > **Office**.
2. Clique à direita na tarefa de atualizações automáticas e selecione **Propriedades**.
3. Vá ao separador **Ações** e clique em **Editar**. Copie o comando e quaisquer argumentos. 
4. Na consola 'Gestor de Configuração', edite a sua sequência de tarefas.
5. Adicione um novo passo de linha de comando de **execução** antes de instalar atualizações de software na sequência de **tarefas.** Se o Office 365 ProPlus for instalado como parte da mesma sequência de tarefas, certifique-se de que este passo corre após a instalação do Office.
6. Copie no comando e nos argumentos que recolheu da tarefa programada do Office. 
7. Clique em **OK**. 

**Método 2:**
1. Numa máquina com a mesma versão do Office 365 ProPlus, aberto Agendador de Tarefas (taskschd.msc) e identificar a tarefa de atualizações automáticas do Office 365. Normalmente, está localizado no âmbito do **Task Scheduler Library**  > **Microsoft** > **Office**.
2. Na consola 'Gestor de Configuração', edite a sua sequência de tarefas.
3. Adicione um novo passo de linha de comando de **execução** antes de instalar atualizações de software na sequência de **tarefas.** Se o Office 365 ProPlus for instalado como parte da mesma sequência de tarefas, certifique-se de que este passo corre após a instalação do Office.
4. No campo da linha de comando, entre na linha de comando que executará a tarefa programada. Veja o exemplo abaixo, certificando-se de que a cadeia em aspas corresponde ao caminho e nome da tarefa identificada no passo 1.  

    Exemplo: `schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. Clique em **OK**. 

## <a name="update-channels-for-microsoft-365-apps"></a><a name="bkmk_channel"></a>Atualizar canais para aplicações microsoft 365
<!--6298093-->
Quando o Office 365 ProPlus foi renomeado para **microsoft 365 Apps para empresa**, os canais de atualização também foram renomeados. Se utilizar uma regra de implementação automática (ADR) para implementar atualizações, terá de efazer alterações nos seus ADRs se depender da propriedade **Title.** Isto porque o nome dos pacotes de atualização no Catálogo de Atualizações da Microsoft está a mudar.

Atualmente, o título de um pacote de atualização para o Office 365 ProPlus começa com "Office 365 Client Update" como visto no exemplo seguinte:

&nbsp;&nbsp;Office 365 Client Update - Versão semi-anual do Canal 1908 para x64 based Edition (Build 11929.20648)

Para pacotes de atualização lançados em e depois de 9 de junho, o título começará com "Microsoft 365 Apps Update", como se pode ver no seguinte exemplo:

&nbsp;&nbsp;Microsoft 365 Apps Update - Semi-anual Channel Version 1908 para x64 based Edition (Build 11929.50000)
</br>
</br>

|Nome do Novo Canal|Nome do Canal anterior|
|--|--|
|Canal Empresarial SemEstral|Via de Atualizações Semianuais|
|Canal Empresarial SemEstral (Pré-visualização)|Via de Atualizações Semianuais (Direcionada)|
|Canal Empresarial Mensal|ND|
|Canal atual|Canal mensal|
|Canal atual (Pré-visualização)|Canal mensal (Direcionado)|
|Canal Beta|Insider|

Para obter mais informações sobre como modificar os seus ADRs, consulte [automaticamente a implementação de atualizações](automatically-deploy-software-updates.md)de software . Para mais informações sobre a alteração de nome, consulte a [alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Altere o canal de atualização depois de permitir que os clientes do Office 365 recebam atualizações do Gestor de Configuração

Após a implementação do Office 365 ProPlus, pode alterar o canal de atualização com a Política do Grupo ou a Ferramenta de Implementação de Escritórios (ODT). Por exemplo, pode mover um dispositivo do Canal Semi-Anual para o Canal Semi-Anual (Direcionado). Ao alterar o canal, o Office é atualizado automaticamente sem ter de reinstalar ou descarregar a versão completa. Para mais informações, consulte alterar o canal de [atualização do Office 365 ProPlus para dispositivos na sua organização](https://docs.microsoft.com//deployoffice/change-update-channels).


## <a name="next-steps"></a>Próximos passos

Utilize o dashboard office 365 Client Management no Gestor de Configuração para rever as informações do Office 365 e implementar aplicações do Office 365. Para mais informações, consulte o [Office 365 Client Management dashboard](office-365-dashboard.md).
