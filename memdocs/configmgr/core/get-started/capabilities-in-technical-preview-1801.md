---
title: Antevisão Técnica 1801 / Microsoft Docs
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão de pré-visualização técnica 1801 para O Gestor de Configuração.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074219"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1801 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1801. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. 

Reveja a [pré-visualização técnica para o Gestor](technical-preview.md) de Configuração antes de instalar esta versão da pré-visualização técnica. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Questões Conhecidas nesta Pré-Visualização Técnica:**
- **A atualização para uma nova versão de pré-visualização falha quando tiver um servidor de site em modo passivo**. Se tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)então tem de desinstalar o servidor do site do modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site do modo passivo depois de o site completar a atualização.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola do Gestor de Configuração, vá a Servidores de**Configuração** > de Site de Visão**Geral** > da **Administração** > **e às Funções**do Sistema do Site, e, em seguida, selecione o servidor do site de modo passivo.
  2. No painel de **funções** do Sistema do Site, clique à direita na função do **servidor do Site** e, em seguida, escolha remover a **função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Criar implementações faseadas
<!-- 1357405 -->
As implementações faseadas automatizam um lançamento coordenado e sequenciado de software sem criar várias implementações. Nesta versão De pré-visualização técnica, o assistente de implementação faseado pode ser concluído para sequências de tarefas na consola de administração. No entanto, não são criadas implantações. 

### <a name="try-it-out"></a>Experimente!  
  Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**
2. Clique à direita numa sequência de tarefas existente e selecione **Criar implantação faseada**. 
3. No separador **Geral,** dê à implantação faseada um nome, descrição (opcional) e selecione **automaticamente criar fases**piloto e de produção padrão . 
4. Povoar os campos de recolha e recolha de **produção** **de pilotos.** Selecione **Seguinte**.
5. No separador **Definições,** escolha uma opção para cada uma das definições de agendamento e selecione **Seguinte** quando estiver completo. 
6. No separador **Fases,** edite qualquer uma das fases, se necessário, clique em **Seguinte**.
7. Confirme as suas seleções no separador **Resumo** e clique em **Next** para proceder.

## <a name="co-management-reporting"></a>Relatórios de cogestão
<!-- 1356648 -->
Se estiver a utilizar as capacidades [de cogestão,](../../comanage/overview.md) pode agora ver um dashboard com informações sobre cogestão no seu ambiente. Na consola 'Gestor de Configuração', navegue para o espaço de trabalho **de monitorização,** expanda a **prontidão**de upgrade e selecione o painel de **cogestão.** O painel inclui os seguintes azulejos:
- **Dispositivos cogeridos**: a percentagem de dispositivos no seu ambiente que permitiu para cogestão
- **Distribuição do OS**: avaria dos sistemas operativos (OS) por versão. Este gráfico utiliza os seguintes agrupamentos:
  - Windows 7 & 8.x
  - Windows 10 inferior a 1709
  - Windows 10 1709 e acima
    > [!NOTE] 
    > Windows 10, versão 1709 e mais tarde, é um pré-requisito para a cogestão
- **Estado de cogestão:** desagregação do sucesso do dispositivo ou falha nas seguintes categorias:
   - Sucesso, AD Azure híbrido Juntou-se
   - Sucesso, Azure AD Juntou-se
   - Falha: Falha na inscrição automática
- **Transição de carga**de trabalho : um gráfico de barras que mostra o número de dispositivos que transferiu para o Microsoft Intune para as três cargas de trabalho disponíveis: 
   - Compliance Policies
   - Acesso a Recursos
   - Windows Update para Empresas

### <a name="prerequisites"></a>Pré-requisitos
- O computador que executa a consola Do Gestor de Configuração requer o Internet Explorer 9 ou mais tarde.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Melhorias no calendário automático de avaliação das regras de implementação
<!-- 1357133 -->
Com base no feedback de voz do [utilizador,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)pode agora agendar a avaliação da regra de implementação automática (ADR) para ser compensada a partir de um dia base. Por exemplo, uma compensação de dois dias após a segunda terça-feira do mês avalia a regra na quinta-feira. 

### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava. <br/>

**Crie um horário personalizado que avalie e ADR compense a partir de um dia base** </br>
1.  No espaço de trabalho da Biblioteca de **Software,** expanda **as Atualizações**de Software e selecione **Regras de Implementação Automática.**
2. Clique no clique direito nas Regras de **Implementação Automática** e escolha criar a regra de **implementação automática**. 
3. Siga as instruções para completar os separadores **Geral**, Definições de **Implementação**e Atualizações de **Software.** 
4. No separador 'Agenda de **Avaliação',** selecione **Executar a regra num horário** e **personalizar**.
5. Para o horário personalizado, selecione **Monthly** e coloque em um dia base como a segunda terça-feira. 
6. Verifique o **Offset (dias)** e o número de dias para a compensação e depois **OK** quando estiver terminado.  
7. Complete o resto do Assistente de Regra de **Implementação Automática Create**. 



## <a name="reassign-distribution-point"></a>Ponto de distribuição de reatribuir
<!-- 1306937 -->
Muitos clientes têm grandes infraestruturas de Gestor de Configuração, e estão a reduzir os locais primários ou secundários para simplificar o seu ambiente. Ainda precisam de reter pontos de distribuição em sucursais para servir conteúdo a clientes geridos. Estes pontos de distribuição contêm frequentemente vários terabytes ou mais de conteúdo. Este conteúdo é dispendioso em termos de tempo e largura de banda da rede para distribuir a estes servidores remotos. 

Esta funcionalidade permite-lhe reatribuir um ponto de distribuição a outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição do sistema do site enquanto persiste todo o conteúdo no servidor. Se precisar de reatribuir vários pontos de distribuição, realize primeiro esta ação num único ponto de distribuição e, em seguida, proceda a servidores adicionais um de cada vez.

> [!IMPORTANT]
> O servidor do sistema do site só pode acolher a função do ponto de distribuição. Se o servidor do sistema do site acolher outra função de servidor do Gestor de Configuração, como o ponto de migração do Estado, não pode reatribuir o ponto de distribuição. Não é possível reatribuir um ponto de distribuição em nuvem. 

Esta opção não está funcional com esta versão devido ao limite de pré-visualização técnica de um único local primário. Considere o cenário e, em seguida, envie **feedback** do separador **Home** da fita, sobre as capacidades desta ação.
1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.**
2. Clique no ponto de distribuição do alvo e selecione Ponto de **Distribuição de Reatribuir**. 
  ![Ponto de distribuição de reatribuição](media/1306937-reassign-dp.png)
3. Selecione o servidor do site e o código do site para o qual pretende reatribuir este ponto de distribuição. 
  ![Selecione um Servidor de Site](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Melhorias no inventário de hardware
<!-- 1357389 -->
Para classes recém-adicionadas, os comprimentos de corda superiores a 255 caracteres podem ser especificados para propriedades de inventário de hardware que não são chaves.

### <a name="try-it-out"></a>Experimente!  
Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.<br/>

1. No espaço de trabalho **da Administração,** clique em **Definições de Cliente** realçar uma definição de dispositivo cliente para editar, clique no clique direito e, em seguida, selecione **Propriedades**. 
2. Selecione **inventário de hardware,** em **seguida, definir classes,** e **adicionar**.
3. Clique no botão **Ligar.**
4. Preencha o **nome do computador**, espaço de nome **WMI,** selecione **recursivo** se necessário. Forneça credenciais se necessário para se ligar. Clique em **Ligar** para ver as classes espaço de nome.
5. Selecione uma nova classe e, em seguida, clique em **Editar**.
6. Altere o **comprimento** de pelo menos uma propriedade que é uma corda, além da chave, para ser superior a 255. Clique em **OK**. 
7. Certifique-se de que a propriedade editada é selecionada para Adicionar Classe de Inventário de **Hardware** e clique em **OK**. 
8. Colete o inventário de hardware com a classe recém-adicionada contendo uma propriedade superior a 255 caracteres de comprimento. 



## <a name="improvements-to-client-settings-for-software-center"></a>Melhorias nas definições do cliente para o Centro de Software
<!-- 1351224 & 1355146 -->
Nesta versão da Pré-Visualização Técnica, foram feitas melhorias para a personalização do Software Center sob as definições do cliente. 

1. As definições do cliente para o Software Center têm agora um botão **Personalizar.**
2. Foi adicionada uma pré-visualização para mostrar como é o banner do Software Center.<!--1351224-->
    - Se um logotipo não for selecionado, a pré-visualização mostra o texto e a cor do nome da empresa.
    - Se for selecionado um logótipo, a pré-visualização mostra o logotipo e o texto do nome da empresa.  
3.  **Ocultar aplicações não aprovadas no Software Center** é uma nova configuração para o Software Center. Quando esta opção está ativada, as aplicações disponíveis do utilizador que requerem aprovação estão escondidas no Software Center.<!--1355146-->

### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. No espaço de trabalho da **Administração,** clique nas **Definições do Cliente**. Selecione uma definição de dispositivo cliente para editar. Clique à direita nele e selecione **Properties** e depois **Software Center**.
2.  Clique no botão **Personalizar.** Experimente as diferentes definições de personalização, incluindo a pré-visualização.
3. Ativar a definição **Ocultar aplicações não aprovadas no Centro**de Software . Observe as mudanças no Centro de Software. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Novas definições para guarda de aplicações do Windows Defender
<!-- 1356256 -->
Para a versão 1709 do Windows 10 e dispositivos posteriores, existem duas novas definições de interação de anfitriões para o [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. Os websites podem ter acesso ao processador de gráficos virtuais do anfitrião. 
2. Os ficheiros descarregados no interior do contentor podem ser persistidos no hospedeiro. </br>



## <a name="improvements-to-run-scripts"></a>Melhorias para executar scripts
<!-- 1236459 -->
A funcionalidade [ **Executar Scripts** ](../../apps/deploy-use/create-deploy-scripts.md) permite-lhe agora importar e executar scripts PowerShell assinados. 
- Para manter a integridade do guião, os scripts assinados devem ser importados em vez de utilizar cópia/pasta. 
- Os scripts assinados importados não podem ser editados após a importação.
    
>[!IMPORTANT]
>Nesta Pré-visualização Técnica, existem duas limitações temporárias.
>- Os scripts só podem ser importados na funcionalidade 'Scripts' e não podem ser editados diretamente a partir da consola.
>- Os scripts importados com uma codificação não Unicode podem ser exibidos incorretamente na consola. O guião ainda será executado como originalmente escrito.





## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
