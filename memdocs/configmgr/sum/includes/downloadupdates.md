1.  Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software** e selecione o nó de Atualizações de **Software.**  

2.  Escolha a atualização de software a transferir utilizando um dos seguintes métodos:  

    -   Selecione um ou mais grupos de atualização de software a partir do nó dos Grupos de Atualização de **Software.** Em seguida, clique em **Baixar** na fita.  

    -   Selecione uma ou mais atualizações de software a partir do nó **de Todas as Atualizações** de Software. Em seguida, clique em **Baixar** na fita.  

        > [!NOTE]  
        >  No nó **All Software Updates,** o Gestor de Configuração apresenta apenas atualizações de software com uma classificação **Crítica** e **Segurança** que foram lançadas nos últimos 30 dias.  

        > [!TIP]  
        >  Clique em **Critérios de Adicionar** para filtrar as atualizações de software que são apresentadas no nó de Atualizações de **Software.** Guarde os critérios de pesquisa que utiliza frequentemente e, em seguida, gere pesquisas guardadas no separador **'Pesquisa'.**  


3.  Na página do Pacote de **Implementação** do Assistente de Atualizações de Software de Descarregamento, configure as seguintes definições:  

    -  **Selecionar pacote de implementação**: escolha esta definição para selecionar um pacote de implementação existente para as atualizações de software incluídas na implementação.  

        > [!NOTE]  
        >  As atualizações de software que o site já descarregou para o pacote de implementação selecionado não serão descarregadas novamente.  

    -  **Criar um novo pacote de implementação**: selecione esta definição para criar um novo pacote de implementação para as atualizações de software na implementação. Configure as seguintes definições:  

        -   **Nome**: especifica o nome do pacote de implementação. O pacote deverá ter um nome exclusivo que descreva resumidamente o conteúdo do pacote. Está limitado a 50 caracteres.  

        -   **Descrição**: especifique uma descrição que disponibilize informações sobre o pacote de implementação. A descrição opcional está limitada a 127 caracteres.    

        -   **Origem do pacote**: especifica a localização dos ficheiros de origem de atualização de software. Digite um caminho de rede para `\\server\sharename\path`a localização de origem, por exemplo, ou clique **em Navegar** para encontrar a localização da rede. Crie a pasta partilhada para os ficheiros de origem do pacote de implementação antes de passar para a página seguinte.  

             - Não pode utilizar a localização especificada como fonte de outro pacote de implementação de software.  

             - Pode alterar a localização da fonte do pacote nas propriedades do pacote de implementação após o Gestor de Configuração criar o pacote de implementação. Se o fizer, copie primeiro o conteúdo da fonte original do pacote para a nova localização de origem do pacote.  

             -  A conta de computador do Fornecedor SMS e do utilizador que está a executar o assistente para descarregar as atualizações de software deve ter permissões **de Escrita** para o local de descarregamento. Restrinja o acesso ao local de descarregamento. Esta restrição reduz o risco de os atacantes adulterarem os ficheiros de origem da atualização de software.  

        - Ativar a **replicação diferencial binária**: Ative esta definição para minimizar o tráfego de rede entre os locais. A replicação diferencial binária (BDR) apenas atualiza o conteúdo que mudou no pacote, em vez de atualizar todo o conteúdo do pacote. Para obter mais informações, consulte a [replicação diferencial binária](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  Na página pontos de **distribuição,** especifique os pontos de distribuição ou os grupos de pontos de distribuição para alojar os ficheiros de atualização de software. Para obter mais informações sobre os pontos de distribuição, veja [Configurações de pontos de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Esta página apenas está disponível ao criar um novo pacote de implementação da atualização de software.  

5.  A página **Definições** de Distribuição só está disponível quando criar um novo pacote de implementação de atualização de software. Especifique as seguintes definições:  

    -   **Prioridade de distribuição**: utilize esta definição para especificar a prioridade de distribuição para o pacote de implementação. A prioridade de distribuição aplica-se quando o pacote de implementação é enviado para pontos de distribuição em sites subordinados. Os pacotes de implantação são enviados por ordem prioritária: alto, médio ou baixo. Os pacotes com prioridades idênticas são enviados pela ordem em que foram criados. Se não houver atrasos, o pacote processa imediatamente, independentemente da sua prioridade. Por padrão, o site envia pacotes com prioridade **média.**  

    -   **Ativar a distribuição a pedido**: Utilize esta definição para permitir a distribuição de conteúdos a pedido para pontos de distribuição configurados para esta funcionalidade e no atual grupo de fronteirado do cliente. Quando permite esta definição, o ponto de gestão cria um gatilho para que o gestor de distribuição distribua o conteúdo para todos esses pontos de distribuição quando um cliente solicita o conteúdo para o pacote e o conteúdo não está disponível. Para mais informações, consulte a [distribuição de conteúdos a pedido.](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)  

    -   **Definições pré-configuradas de ponto de distribuição**: utilize esta definição para especificar a forma como pretende distribuir conteúdo para pontos de distribuição pré-configurados. Selecione uma das seguintes opções:  

        -   **Transferir o conteúdo automaticamente quando os pacotes são atribuídos aos pontos de distribuição**: utilize esta definição para ignorar as definições pré-configuradas e distribuir conteúdo para o ponto de distribuição.   

        -   **Transferir apenas alterações de conteúdo para o ponto de distribuição**: utilize esta definição para pré-configurar o conteúdo inicial para o ponto de distribuição e, em seguida, distribuir as alterações de conteúdo para o ponto de distribuição.  

        -   **Copiar manualmente o conteúdo deste pacote para o ponto de distribuição**: utilize esta definição para pré-configurar sempre o conteúdo no ponto de distribuição. Esta é a opção predefinida.  

        Para obter mais informações sobre a pré-configuração de conteúdo para pontos de distribuição, veja [Utilizar conteúdo pré-configurado](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  Na página **de Descarregamento,** especifique a localização que o Gestor de Configuração utiliza para descarregar os ficheiros de origem da atualização de software. Utilize uma das seguintes opções:  

    -   **Descarregue as atualizações de software a partir da Internet**: Selecione esta definição para descarregar as atualizações de software a partir da localização na internet. Esta é a opção predefinida.  

    -   **Descarregue as atualizações de software a partir de uma localização da minha rede**: Selecione esta definição para descarregar as atualizações de software a partir de um diretório local ou pasta partilhada. Esta definição é útil quando o computador que executa o assistente não tem acesso à Internet. Qualquer computador com acesso à Internet pode descarregar preliminarmente as atualizações de software. Em seguida, guarde-os num local da rede local acessível a partir do computador que executa o assistente.  


7.  Na página de Seleção de **Idiomas,** selecione os idiomas para os quais o site descarrega as atualizações de software selecionadas. O site só descarrega estas atualizações se estiverem disponíveis nos idiomas selecionados. As atualizações de software que não são específicas do idioma são sempre descarregadas. Por padrão, o assistente seleciona os idiomas configurados nas propriedades do ponto de atualização do software. Terá de estar selecionado pelo menos um idioma para que possa prosseguir para a página seguinte. Quando seleciona apenas idiomas que uma atualização de software não suporta, o download falha na atualização.  

8. Na página **Resumo,** verifique as definições selecionadas no assistente e clique em **Next** para descarregar as atualizações do software.  

9. Na página **'Conclusão',** verifique se as atualizações de software foram descarregadas com sucesso e, em seguida, clique em **Fechar**.  
