---
title: Implementar uma sequência de tarefas
titleSuffix: Configuration Manager
description: Utilize estas informações para implementar uma sequência de tarefas para os computadores numa coleção.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2347275ffdc194e73cf792d6f83ffa75732f8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711414"
---
# <a name="deploy-a-task-sequence"></a>Implementar uma sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de criar uma sequência de tarefas e distribuir o conteúdo referenciado, implemente-o para uma recolha de dispositivos. Esta ação permite que a sequência de tarefas seja executada num dispositivo. Uma sequência de tarefas implementada pode ser executada automaticamente, ou quando instalada por um utilizador do dispositivo.

> [!WARNING]  
> Pode gerir o comportamento de implementações de sequência de tarefas de alto risco. Uma implementação de alto risco é uma implementação que é automaticamente instalada e que tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas que tem um propósito de **Exigir** que implementa um Sistema operativo é considerada uma implantação de alto risco. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## <a name="process"></a>Processo

Utilize o seguinte procedimento para implementar uma sequência de tarefas nos computadores de uma coleção.  

> [!NOTE]  
> As mensagens de estado para a implementação da sequência de tarefas são exibidas na janela da mensagem num local primário, mas não são exibidas num site de administração central.  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e, em seguida, selecione o nó de sequências de **tarefas.**  

2. Na lista **Sequência de Tarefas** , selecione a sequência de tarefas que pretende implementar.  

3. No separador **Home** da fita, no grupo **de implantação,** selecione **Deploy**.  

    > [!NOTE]  
    > Se o **Deploy** não estiver disponível, a sequência de tarefas tem uma referência que não é válida. Corrija a referência e tente implementar a sequência de tarefas novamente.  

4. Na página **Geral,** especifique as seguintes informações.  

    - **Sequência de tarefas**: Especifique a sequência de tarefas a ser implantada. Por predefinição, esta caixa apresenta a sequência de tarefas selecionada.  

    - **Recolha**: Selecione a recolha que contém os computadores para executar a sequência de tarefas.  

        Não implemente uma sequência de tarefas que instale um SO em coleções inadequadas, como uma recolha de todos os seus servidores do centro de dados. Certifique-se de que a coleção selecionada contém apenas os computadores que pretende executar a sequência de tarefas.  

        Para obter mais informações sobre implementações de alto risco, consulte [implementações de alto risco](#bkmk_high-risk).

    - Utilize grupos de pontos de **distribuição predefinidos associados a esta recolha**: Guarde o conteúdo da sequência de tarefas no grupo de pontos de distribuição predefinido da coleção. Se não associou a coleção selecionada a um grupo de pontos de distribuição, esta opção está cinzenta.  

    - **Distribua automaticamente o conteúdo para dependências**: Se algum conteúdo referenciado tiver dependências, então o site também envia conteúdo dependente para pontos de distribuição.  

    - **Pré-descarregue o conteúdo para esta sequência de tarefas**: Para mais informações, consulte o [conteúdo pré-cache configurar](configure-precache-content.md).  

    - **Selecione modelo de implementação**: Guarde e especifique um modelo de implementação para uma sequência de tarefas.<!--1357391-->  

        > [!IMPORTANT]  
        > Alguns itens não são guardados no modelo.<!--510610--> Certifique-se de que aplica os seguintes itens quando executar o assistente de implantação:  
        >
        > - Instalação de Software
        > - Agendamento
        > - Conteúdo de pré-download

    - **Comentários (opcional)**: especifique informações adicionais que descrevam esta implementação da sequência de tarefas.  

5. Na página definições de **implementação,** especifique as seguintes informações:  

    - **Objetivo**: na lista pendente, escolha uma das seguintes opções:  

        - **Disponível**: O utilizador vê a sequência de tarefas no Centro de Software e pode instalá-la a pedido.  

        - **Requerido**: O Gestor de Configuração executa automaticamente a sequência de tarefas de acordo com o horário configurado. Se a sequência de tarefas não estiver oculta, um utilizador ainda pode rastrear o seu estado de implementação. Também podem usar o Software Center para instalar a sequência de tarefas antes do prazo.  

        > [!NOTE]
        > Se vários utilizadores forem assinados no dispositivo, as implementações de sequências de pacotes e de tarefas podem não aparecer no Centro de Software.  

    - **Fique à disposição do seguinte**: Especifique se a sequência de tarefas está disponível para um dos seguintes tipos:  

        - Apenas clientes do Gestor de Configuração  
        - Clientes, meios de comunicação e PXE do Gestor de Configuração  
        - Apenas suportes de dados e PXE  
        - Apenas suportes de dados e PXE (oculto)  

        > [!IMPORTANT]  
        > Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Para que o computador arranque automaticamente na implementação sem interação do utilizador, selecione Permitir a implementação do **sistema operativo sem supervisão** e definir a variável **SMSTSPreferredAdvertID** como parte dos meios de comunicação. Para obter mais informações sobre variáveis de sequência de [tarefas,](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID)consulte variáveis de sequência de tarefas .  

    - **Envie pacotes de despertar**: Se a implementação for **necessária** e selecionar esta opção, o site envia um pacote de despertar para computadores antes de o cliente espacer a implementação. Este pacote acorda o computador do sono no prazo de instalação. Antes de utilizar esta opção, os computadores e as redes devem ser configurados para Wake On LAN. Para mais informações, consulte [Plan como acordar os clientes.](../../core/clients/deploy/plan/plan-wake-up-clients.md)  

    - **Permitir que os clientes numa ligação à Internet medido descarreguem conteúdos após o prazo de instalação, o que pode incorrer em custos adicionais**: Esta opção só está disponível para implementações **necessárias.** Quando tem uma sequência de tarefas personalizada que instala uma aplicação mas não implementa um SISTEMA, pode especificar se permite que os clientes descarreguem conteúdo após um prazo de instalação quando utilizam ligações à Internet medidos. Por vezes, os fornecedores de Internet cobram pela quantidade de dados que utilizam quando se está numa ligação à Internet com medido.  

        > [!NOTE]  
        > Embora a utilização de uma ligação de internet medido possa funcionar para sequências de tarefas que não implementem um SISTEMA, não é suportado.  

6. Na página **de Agendamento,** especifique as seguintes informações:  

    > [!IMPORTANT]  
    > Quando um cliente do Windows PE começa a partir de PXE ou boot media, o cliente não avalia os horários de implementação. Estes horários incluem início, expiração e prazos. Configure apenas horários em implementações para clientes que partam de todo o Sistema Operativo Windows. Considere a utilização de outros métodos, como janelas de manutenção, para controlar sequências de tarefas ativas implementadas em clientes iniciados a partir do Windows PE.  

    - **Agendar quando esta implementação ficará disponível**: especifique a data e a hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Ao selecionar a opção **UTC,** a sequência de tarefas está disponível para vários computadores ao mesmo tempo. Caso contrário, a implementação está disponível em momentos diferentes, de acordo com a hora local em cada computador.  

        Se a hora de início for mais precoce do que o tempo necessário, o cliente descarrega o conteúdo da sequência de tarefas na hora de início.  

    - **Agendar quando esta implementação expirará**: especifique a data e a hora em que a sequência de tarefas irá expirar no computador de destino. Quando seleciona a opção **UTC,** a sequência de tarefas expira em vários computadores de destino ao mesmo tempo. Caso contrário, a implementação expira em momentos diferentes, de acordo com a hora local em cada computador.  

    - **Agenda de atribuição**: Para uma implementação **necessária,** especifique quando o cliente executa a sequência de tarefas. Pode adicionar múltiplas agendas. O calendário de atribuição pode ter uma das seguintes configurações:  

        - Uma data e hora específicas  
        - Padrão mensal, semanal ou personalizado de recorrência  
        - O mais rapidamente possível  
        - Iniciar sessão ou iniciar eventos  

        > [!NOTE]  
        > Se agendar uma hora de início para uma implementação necessária que seja mais cedo do que a data e hora em que a sequência de tarefas está disponível, o cliente do Gestor de Configuração descarrega o conteúdo na hora de início atribuída. Este comportamento ocorre mesmo que tenha agendado a sequência de tarefas para estar disponível mais tarde.<!--SCCMDocs issue 777-->  

    - **Reexecutar o comportamento**: Especifique quando a sequência de tarefas voltar a funcionar. Selecione uma das seguintes opções:  

        - **Nunca reexecutar**o programa implementado : Se o cliente já executou previamente a sequência de tarefas, não refunciona. A sequência de tarefas não se regere mesmo que tenha falhado inicialmente ou os ficheiros da sequência de tarefas tenham mudado.  

        - **Sempre reexecutar o programa**: A sequência de tarefas repete-se sempre no cliente quando a implementação está programada. Repete-se mesmo que a sequência de tarefas já tenha corrido com sucesso. Esta definição é útil quando utiliza implementações recorrentes em que a sequência de tarefas é rotineiramente atualizada.  

            > [!IMPORTANT]  
            > Esta opção está selecionada por predefinição. No entanto, não tem qualquer efeito até que atribua uma implementação necessária. Um utilizador pode sempre reexecutar as implementações disponíveis.  

        - **Reexecutar se falhar a tentativa anterior**: A sequência de tarefas repete-se quando a implantação está programada, apenas se não tiver sido executada anteriormente. Esta definição é útil para uma implementação necessária. Se a última tentativa de fuga não foi bem sucedida, tenta-se automaticamente reexecutar de acordo com o calendário de atribuição.  

        - **Reexecutar se tiver sido bem sucedido na tentativa anterior**: A sequência de tarefas só se repete se anteriormente foi executada com sucesso no cliente. Esta definição é útil se utilizar implementações periódicas cuja sequência de tarefas seja regularmente atualizada e cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.  

        > [!NOTE]  
        > Um utilizador pode reexecutar uma implementação de sequência de tarefas disponível. Antes de implementar uma sequência de tarefas disponível num ambiente de produção, teste primeiro o que acontece se um utilizador reproduzir a sequência de tarefas várias vezes.  

7. Na página **Experiência de Utilizador** , especifique as seguintes informações:  

    - **Permitir que o utilizador execute o programa de forma independente das atribuições**: Especifique se um utilizador pode executar uma implementação necessária fora do calendário de atribuição. Esta opção está sempre ativada para implementações disponíveis.  

    - **Mostrar o progresso**da sequência de tarefas : Especifique se o cliente do Gestor de Configuração apresenta o progresso da sequência de tarefas.  

    - **Instalação do software**: Especifique se o utilizador pode instalar software fora de uma janela de manutenção configurada após a hora programada.  

    - **Reinício do sistema (se for necessário para concluir a instalação)**: especifique se o utilizador tem permissão para reiniciar o computador após uma instalação de software fora de uma janela de manutenção configurada e depois da hora da atribuição.  

    - **Escreva o manuseamento do filtro para dispositivos Incorporados**do Windows : Esta definição controla o comportamento de instalação em dispositivos Incorporados do Windows que estão ativados com um filtro de escrita. Escolha a opção de cometer alterações no prazo de instalação ou durante uma janela de manutenção. Quando selecionar esta opção, é necessário reiniciar e as alterações persistem no dispositivo. Caso contrário, a aplicação é instalada na sobreposição temporária, e comprometida posteriormente. Quando implementar uma sequência de tarefas num dispositivo Incorporado do Windows, certifique-se de que o dispositivo é membro de uma coleção que tem uma janela de manutenção configurada.  

    - Permitir que a sequência de **tarefas seja executada para o cliente na Internet**: Especifique se a sequência de tarefas é permitida a ser executada num cliente baseado na Internet. As operações que requerem um suporte de arranque, como a instalação de um Sistema operativo, não são suportadas com esta configuração. Utilize esta opção apenas para instalações genéricas de software ou sequências de tarefas baseadas em scripts que executam operações no SISTEMA padrão.  

        - Esta definição é suportada para implementações de uma sequência de tarefas de upgrade do Windows 10 para clientes baseados na Internet através do gateway de gestão de nuvem. Para mais informações, consulte [a atualização do Windows 10 no local via CMG](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. Na página **Alertas,** especifique as definições de alerta que pretende para esta implementação da sequência de tarefas.  

9. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    - **Opções de implementação**: especifique uma das seguintes opções:  

        > [!NOTE]  
        > Quando utilizar o multicast para implementar um SISTEMA, descarregue o conteúdo para os computadores, quer se necessário, quer antes de a sequência de tarefas ser executado.  

        - **Descarregue os conteúdos localmente quando necessário pela sequência**de tarefas de execução : Especifique que os clientes descarregam conteúdo a partir do ponto de distribuição, tal como é necessário pela sequência de tarefas. O cliente inicia a sequência de tarefas. Quando um passo na sequência de tarefas requer conteúdo, é descarregado antes do passo correr.  

        - **Descarregue todos os conteúdos localmente antes**de iniciar a sequência de tarefas : Especifique que os clientes descarreguem todos os conteúdos a partir do ponto de distribuição antes da sequência de tarefas ser executado. Se disponibilizar a sequência de tarefas para pXE e implementações de suportes de arranque na página definições de **implementação,** esta opção não é mostrada.  

        - **Aceda diretamente ao conteúdo a partir de um ponto de distribuição quando necessário pela sequência**de tarefas de execução : Especifique que os clientes executam o conteúdo a partir do ponto de distribuição. Esta opção só está disponível quando permite que todos os pacotes associados à sequência de tarefas utilizem uma parte de pacote no ponto de distribuição. Para permitir que os conteúdos utilizem uma partilha de pacote, consulte o separador **Acesso a Dados** nas **Propriedades** de cada pacote.  

            > [!IMPORTANT]  
            > Para maior segurança, selecione as opções para **descarregar conteúdo localmente quando necessário pela sequência** de tarefas de execução ou **descarregue todos os conteúdos localmente antes**de iniciar a sequência de tarefas . Ao selecionar qualquer uma destas opções, o Gestor de Configuração acerta o pacote, para que possa garantir a integridade do pacote. Quando seleciona a opção de aceder diretamente ao conteúdo a partir de um ponto de distribuição quando necessário pela sequência de tarefas de **execução,** o Gestor de Configuração não verifica o hash do pacote antes de executar o programa especificado. Como o site não pode garantir a integridade do pacote, é possível que os utilizadores com direitos administrativos alterem ou adulteram o conteúdo do pacote.  

    - Quando não houver um ponto de **distribuição local disponível, utilize um ponto**de distribuição remoto : Especifique se os clientes podem usar pontos de distribuição de um grupo de fronteira sinuoso para descarregar o conteúdo que é exigido pela sequência de tarefas.  

    - Permitir que os **clientes utilizem pontos de distribuição do grupo**de limites do site padrão : Especifique se os clientes devem descarregar conteúdo a partir de um ponto de distribuição no grupo de limites padrão do site, quando não estiver disponível a partir de um ponto de distribuição nos grupos de fronteira atuais ou vizinhos.  

        > [!Note]  
        > A partir da versão 1810, quando um dispositivo executa uma sequência de tarefas e precisa de adquirir conteúdo, utiliza comportamentos de grupo de limites semelhantes ao cliente do Gestor de Configuração. Para obter mais informações, consulte o suporte da [sequência de tarefas para grupos de fronteira](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).<!--1359025-->  

10. Para guardar estas definições para voltar a utilizar, no separador **Resumo** selecione **Guardar como modelo**. Forneça um nome para o modelo e selecione as definições para guardar.  

11. Conclua o assistente.  

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implementar atualização no local do Windows 10 via CMG

<!-- 1357149 -->
A sequência de tarefas de upgrade do Windows 10 no local suporta a implementação de clientes baseados na Internet geridos através do gateway de [gestão](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) de nuvem (CMG). Esta capacidade permite que os utilizadores remotos atualizem mais facilmente para o Windows 10 sem necessidade de se ligarem à intranet.

Certifique-se de que todos os conteúdos referenciados pela sequência de tarefas de atualização no local são distribuídos por um CMG ativado por conteúdo. (Ativar a [definição cmg:](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings)Permitir que a CMG funcione como um ponto de distribuição em **nuvem e sirva o conteúdo do armazenamento Azure**.) Também pode utilizar um ponto de distribuição em [nuvem.](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) Caso contrário, os dispositivos não podem executar a sequência de tarefas.

Quando implementar uma sequência de tarefas de atualização, utilize as seguintes definições:

- Permitir que a sequência de **tarefas se decorra para o cliente na Internet,** no separador User Experience da implementação.  

- Escolha uma das seguintes opções no separador Pontos de Distribuição da implementação:

  - **Descarregue os conteúdos localmente quando necessário pela sequência de tarefas em execução**. A partir da versão 1910, o motor de sequência de tarefas pode descarregar pacotes a pedido a partir de um CMG ativado por conteúdo ou um ponto de distribuição em nuvem. Esta alteração proporciona flexibilidade adicional com as implementações de upgrade do Windows 10 para dispositivos baseados na Internet.<!--3601238-->

  - **Descarregue todos os conteúdos localmente antes**de iniciar a sequência de tarefas . Na versão 1906 e anterior do Configurmanager, outras opções, como **o descarregamento de conteúdos localmente quando necessários pela sequência** de tarefas de execução, não funcionam neste cenário. O motor de sequência de tarefas não pode descarregar conteúdo de uma fonte de nuvem. O cliente do Gestor de Configuração deve descarregar o conteúdo a partir da fonte cloud antes de iniciar a sequência de tarefas. Ainda pode utilizar esta opção na versão 1910, se necessário para satisfazer os seus requisitos.

- *(Opcional)* **Pré-descarregue o conteúdo para esta sequência de tarefas,** no separador Geral da implementação. Para mais informações, consulte o [conteúdo pré-cache da Configure](configure-precache-content.md).  

> [!NOTE]
> Inicie a sequência de tarefas do Centro de Software. Este cenário não suporta os meios de comunicação Windows PE, PXE ou task sequence.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>Implantações de alto risco

Ao implementar uma implementação de alto risco, como um SISTEMA, a janela **Select Collection** exibe apenas as coleções personalizadas que cumprem as definições de verificação de implementação que estão configuradas nas propriedades do site. As implementações de alto risco são sempre limitadas a coleções personalizadas, coleções criadas por si e à coleção incorporada **Computadores Desconhecidos** . Quando cria uma implementação de alto risco, não se pode selecionar uma coleção incorporada, como **a All Systems**. Para ver todas as coleções personalizadas que contenham menos clientes do que o tamanho máximo configurado, desative a opção de ocultar coleções com uma contagem de **membros maior do que a configuração de tamanho mínimo do site**. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

As definições de verificação da implementação são baseadas na associação atual da coleção. Depois de implementar a sequência de tarefas, o Gestor de Configuração não reavalia a subscrição da coleção para as definições de implementação de alto risco.  

Por exemplo, digamos que definiu o **tamanho padrão** para 100 e o **tamanho máximo** para 1000. Quando cria uma implementação de alto risco, a janela **Select Collection** apenas exibe coleções que contenham menos de 100 clientes. Se limpar as coleções Hide com uma contagem de **membros maior do que a configuração de tamanho mínimo do site,** a janela exibe coleções que contêm menos de 1000 clientes.  

Quando seleciona uma coleção que contenha uma função do site, aplica-se o seguinte comportamento:  

- Se a recolha contiver um servidor de sistema de site, e configurar as definições de verificação de implementação para bloquear as coleções com servidores do sistema do site, então ocorre um erro. Não podes continuar a criar a implantação.  

- Se um dos seguintes critérios se aplicar, o Assistente de Software de Implantação apresenta um aviso de alto risco. Para continuar, precisa concordar em criar uma implantação de alto risco. O site gera uma mensagem de estado de auditoria.  

  - Se a coleção contiver um servidor de sistema de site, e configurar as definições de verificação de implementação para alertar em coleções com servidores do sistema do site  

  - Se a coleção exceder o valor de tamanho padrão

  - Se a coleção contiver um servidor  

## <a name="see-also"></a>Consulte também

[Gerir sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md)
