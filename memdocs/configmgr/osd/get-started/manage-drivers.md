---
title: Gerir controladores
titleSuffix: Configuration Manager
description: Utilize o catálogo de controladores do Gestor de Configuração para importar condutores de dispositivos, agrupar condutores em pacotes e distribuir esses pacotes em pontos de distribuição.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724126"
---
# <a name="manage-drivers-in-configuration-manager"></a>Gerir os condutores no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração fornece um catálogo de controladores que pode utilizar para gerir os controladores do dispositivo Windows no ambiente do Gestor de Configuração. Utilize o catálogo de condutores para importar controladores de dispositivos para o Gestor de Configuração, agrupá-los em pacotes e distribuir esses pacotes em pontos de distribuição. Os controladores de dispositivos podem ser utilizados quando instala o SISTEMA completo no computador de destino e quando utiliza o Windows PE numa imagem de arranque. Os controladores do dispositivo Windows consistem num ficheiro de informação de configuração (INF) e em quaisquer ficheiros adicionais necessários para suportar o dispositivo. Quando implementa um SISTEMA, o Gestor de Configuração obtém as informações de hardware e plataforma para o dispositivo a partir do seu ficheiro INF. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a>Categorias de condutores

Quando importa controladores de dispositivos, pode atribuir os controladores de dispositivos a uma categoria. As categorias de controladores de dispositivos ajudam a agrupar o controladores de dispositivos de utilização semelhante no catálogo de controladores. Por exemplo, coloque todos os controladores adaptadores de rede numa categoria específica. Em seguida, quando criar uma sequência de tarefas que inclua o passo [de Condutores de Aplicação automática,](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) especifique uma categoria de controladores de dispositivos. Em seguida, o Gestor de Configuração digitaliza o hardware e seleciona os controladores aplicáveis dessa categoria para encenar no sistema para a Configuração do Windows usar.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a>Pacotes de motorista

Group similar device drivers in packages to help streamline os implementações de SO. Por exemplo, crie um pacote de controlador para cada fabricante de computadores da sua rede. Pode criar um pacote de condutor ao importar condutores diretamente no catálogo do condutor no nó **dos Pacotes** de Condutor. Depois de criar um pacote de motorista, distribua-o para pontos de distribuição. Em seguida, os computadores clientes do Gestor de Configuração podem instalar os controladores conforme necessário. 

Considere os seguintes pontos:  

- Quando cria um pacote de condutor, a localização de origem do pacote deve apontar para uma partilha de rede vazia que não seja utilizada por outro pacote de condutor. O Provedor de SMS deve ter permissões de **controlo total** para esse local.  

- Quando adiciona os controladores do dispositivo a um pacote de controlador, o Gestor de Configuração copia-o para a localização da fonte do pacote. Pode adicionar a um pacote de condutores apenas controladores que você importou e que estão ativados no catálogo do motorista.  

- Pode copiar um subconjunto dos controladores do dispositivo a partir de um pacote de condutor existente. Primeiro, crie um novo pacote de motorista. Em seguida, adicione o subconjunto dos controladores do dispositivo ao novo pacote e, em seguida, distribua o novo pacote para um ponto de distribuição.  

- Quando utiliza sequências de tarefas para instalar controladores, crie pacotes de controladores que contenham menos de 500 controladores de dispositivo.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a> Criar um pacote de controlador  

> [!IMPORTANT]  
> Para criar um pacote de condutor, deve ter uma pasta de rede vazia que não seja utilizada por outro pacote de condutor. Na maioria dos casos, crie uma nova pasta antes de iniciar este procedimento.  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **os Sistemas Operativos**e, em seguida, selecionar o nó dos **Pacotes de Condutor.**  

2. No separador **Casa** da fita, no grupo **Criar,** selecione **Create Driver Package**.  

3. Especifique um **nome** descritivo para o pacote do condutor.  

4. Introduza um **Comentário** opcional para o pacote de motorista. Utilize esta descrição para fornecer informações sobre o conteúdo ou a finalidade do pacote de motorista.  

5. Na caixa **Caminho** , especifique uma pasta de origem vazia para o pacote de controladores. Cada pacote de controladores terá de utilizar uma pasta exclusiva. Este caminho é necessário como uma localização de rede.  

   > [!IMPORTANT]  
   > A conta do servidor do site deve ter permissões de **controlo completos** para a pasta de origem especificada.  

O novo pacote de motoristas não contém motoristas. O próximo passo adiciona os condutores ao pacote.  

Se o nó **Pacotes de Controladores** contiver diversos pacotes, poderá adicionar pastas ao mesmo para separar os pacotes em grupos lógicos.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Ações adicionais para pacotes de controladores  

Pode fazer ações adicionais para gerir os pacotes de condutor quando selecionar um ou mais pacotes de condutor do nó **do Driver Packages.** 


#### <a name="create-prestage-content-file"></a>Criar Ficheiro de Conteúdo Pré-configurado
Cria ficheiros que pode utilizar para importar manualmente conteúdo e os seus metadados associados. Utilize conteúdo pré-configurado quando tiver reduzida largura de banda de rede entre o servidor de site e os pontos de distribuição em que o pacote de controladores se encontra armazenado.

#### <a name="delete"></a>Eliminar
Remove o pacote de controladores do nó **Pacotes de Controladores** .

#### <a name="distribute-content"></a>Distribuir Conteúdo
Distribui o pacote de controladores aos pontos de distribuição, grupos de pontos de distribuição e grupos de pontos de distribuição associados a coleções.

#### <a name="manage-access-accounts"></a>Gerir Contas de Acesso
Adiciona, modifica ou remove as contas de acesso do pacote de controladores.

Para obter mais informações sobre as contas de acesso ao pacote, consulte [contas utilizadas no Gestor](../../core/plan-design/hierarchy/accounts.md)de Configuração .

#### <a name="move"></a>Mover
Move o pacote de controladores para outra pasta do nó **Pacotes de Controladores** .

#### <a name="update-distribution-points"></a>Atualizar Pontos de Distribuição
Atualiza o pacote de controladores de dispositivo em todos os pontos de distribuição em que o pacote se encontra armazenado. Esta ação copia apenas o conteúdo que foi alterado desde a última vez em que foi distribuído.

#### <a name="properties"></a>Propriedades
Abre a caixa de diálogo **Properties.** Reveja e altere o conteúdo e as propriedades do condutor. Por exemplo, altere o nome e a descrição do controlador, ative-o ou desative-o e especifique em que plataformas pode funcionar. 

<!--3607716, fka 1358270-->
A partir da versão 1810, os pacotes de condutores têm campos de metadados para **fabricante** e **modelo**. Utilize estes campos para etiquetar pacotes de condutores com informações para ajudar na limpeza geral, ou para identificar condutores antigos e duplicados que possa eliminar. No separador **Geral,** selecione um valor existente a partir das listas de abandono ou introduza uma cadeia para criar uma nova entrada.

No nó dos **Pacotes de Condutor,** estes campos apresentam-se na lista como as colunas do Fabricante do **Condutor** e **do Modelo do Condutor.** Também podem ser utilizados como critérios de pesquisa.

A partir da versão 1906, utilize estes atributos para conteúdo pré-cache num cliente. Para mais informações, consulte o [conteúdo pré-cache da Configure](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Controladores de dispositivos

Pode instalar controladores em computadores de destino sem os incluir na imagem de OS que está implantada. O Gestor de Configuração fornece um catálogo de controladores que contém referências a todos os controladores que importa para O Gestor de Configuração. O catálogo de controladores está localizado na área de trabalho **Biblioteca de Software** e é composto por dois nós: **Controladores** e **Pacotes de Controladores**. O nó **dos Condutores** lista todos os condutores que importaste para o catálogo de motoristas.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a>Importadores de dispositivos de importação no catálogo do condutor  

Antes de poder utilizar um condutor quando implementar um Sistema operativo, importe-o para o catálogo do condutor. Para melhor geri-los, importe apenas os condutores que planeia instalar como parte das suas implementações de SO. Guarde várias versões de controladores no catálogo para fornecer uma forma fácil de atualizar os controladores existentes quando os requisitos do dispositivo de hardware mudarem na sua rede.  

Como parte do processo de importação para o controlador do dispositivo, o Gestor de Configuração lê as seguintes propriedades sobre o condutor:
- Fornecedor
- Classe
- Versão
- Assinatura
- Hardware suportado
- Informação da plataforma suportada

Por predefinição, o controlador tem o nome do primeiro dispositivo de hardware que suporta. Pode mudar o nome do controlador do dispositivo mais tarde. A lista de plataformas suportadas baseia-se nas informações do ficheiro INF do controlador. Como a precisão desta informação pode variar, verifique manualmente se o condutor é suportado depois de a importar para o catálogo.  

Depois de importar condutores de dispositivos para o catálogo, adicione-os a pacotes de imagem de condutor ou a boot image.  

> [!IMPORTANT]  
> Não se pode importar condutores de dispositivos diretamente para uma subpasta do nó dos **Condutores.** Para importar um controlador de dispositivo para uma subpasta, importe-o primeiro para o nó **Controladores** e, em seguida, mova-o para a subpasta.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Processo de importação de controladores de dispositivos Windows para o catálogo do condutor  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **sistemas operativos**e selecionar o nó **dos Controladores.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione **Import Driver** para iniciar o Novo Assistente de **Importação**.  

3. Na página **Localizar o Controlador,** especifique as seguintes opções:  

    - **Importar todos os condutores na seguinte trajetória de rede (CNU)**: Para importar todos os condutores de dispositivos numa pasta específica, especifique a sua trajetória de rede. Por exemplo: `\\servername\share\folder`.  

        > [!NOTE]  
        > Se houver muitas subpastas e muitos ficheiros INF do condutor, este processo pode demorar algum tempo.  

    - **Importar um controlador específico**: Para importar um controlador específico de uma pasta, especifique a rota de rede para o ficheiro INF do controlador do dispositivo Windows.  

    - **Especifique a opção para condutores duplicados**: Selecione como pretende que o Gestor de Configuração gere as categorias de condutores quando importar um controlador de dispositivo duplicado  
        - **Importar o condutor e anexar uma nova categoria às categorias existentes**  
        - **Importar o condutor e manter as categorias existentes**  
        - **Importar o condutor e substituir as categorias existentes**  
        - **Não importe o motorista**  

    > [!IMPORTANT]  
    > Quando importa controladores, o servidor do site tem de ter permissão de **Leitura** na pasta ou a importação falhará.  

4. Na página Detalhes do **Condutor,** especifique as seguintes opções:  

    - **Ocultar os condutores que não se encontram numa classe de armazenamento ou de rede (para imagens de arranque)**: Utilize esta definição apenas para exibir os controladores de armazenamento e rede. Esta opção esconde outros condutores que normalmente não são necessários para imagens de arranque, como um condutor de vídeo ou um condutor de modem.  

    - **Ocultar condutores que não estejam assinados digitalmente**: A Microsoft recomenda apenas a utilização de condutores que sejam assinados digitalmente  

    - Na lista de controladores, selecione os que pretende importar para o catálogo de controladores.  

    - **Ativar estes controladores e permitir que os computadores os instalem**: selecione esta definição para permitir que os computadores instalem os controladores do dispositivo. Por predefinição, esta opção encontra-se ativada.  

        > [!IMPORTANT]  
        > Se um controlador de dispositivo estiver a causar um problema ou se pretender suspender a instalação de um controlador de dispositivo, desative-o durante a importação. Também pode desativar os condutores depois de os importar.  

    - Para atribuir os controladores do dispositivo a uma categoria administrativa para fins de filtragem, tais como "Desktops" ou "Notebooks", selecione **Categorias**. Em seguida, escolha uma categoria existente, ou crie uma nova categoria. Utilize categorias para controlar quais os controladores do dispositivo aplicados pelo passo de sequência de tarefas [de autoaplicação dos condutores.](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)  

5. Na página **Adicionar Motorista aos Pacotes,** escolha se deve adicionar os condutores a um pacote.  

    - Selecione os pacotes de controladores utilizados para distribuir os controladores de dispositivo.  

        Se necessário, selecione **New Package** para criar um novo pacote de motorista. Quando criar um novo pacote de motorista, forneça uma partilha de rede que não seja utilizada por outros pacotes de condutores.  

    - Se o pacote já tiver sido distribuído para pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não podeusar os controladores de dispositivos até que sejam distribuídos em pontos de distribuição. Se selecionar **Não,** execute a ação Ponto de Distribuição de **Atualização** antes de utilizar a imagem de arranque. Se o pacote do condutor nunca tiver sido distribuído, deve utilizar a ação **Distribute Content** no nó do **Pacote seleto** do Condutor.  

6. Na página **Adicionar Driver a Boot Images,** escolha se deve adicionar os controladores do dispositivo às imagens de boot existentes.  

    > [!NOTE]  
    > Adicione apenas os controladores de armazenamento e rede às imagens de arranque.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não podeusar os controladores de dispositivos até que sejam distribuídos em pontos de distribuição. Se selecionar **Não,** execute a ação Ponto de Distribuição de **Atualização** antes de utilizar a imagem de arranque. Se o pacote do condutor nunca tiver sido distribuído, deve utilizar a ação **Distribute Content** no nó do **Pacote seleto** do Condutor.  

    - O Gestor de Configuração avisa-o se a arquitetura para um ou mais condutores não corresponder à arquitetura das imagens de arranque que selecionou. Se não corresponderem, selecione **OK**. Volte à página de Detalhes do **Condutor** e limpe os condutores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

        > [!NOTE]  
        > - A arquitetura baseia-se na arquitetura relatada no INF do fabricante.  
        > - Se um condutor informa que apoia ambas as arquiteturas, então pode importá-la em qualquer imagem de arranque.  

    - O Gestor de Configuração avisa-o se adicionar controladores de dispositivos que não são controladores de rede ou armazenamento a uma imagem de arranque. Na maioria dos casos, não são necessários para a imagem do arranque. Selecione **Sim** para adicionar os controladores à imagem do arranque, ou **Não** para voltar e modificar a sua seleção de motorista.  

    - O Gestor de Configuração avisa-o se um ou mais dos controladores selecionados não estiverem devidamente assinados digitalmente. Selecione **Sim** para continuar e selecione **Não** para voltar e fazer alterações na sua seleção de motorista.  

7. Conclua o assistente.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Gerir controladores de dispositivo num pacote de controlador  

Utilize os procedimentos seguintes para modificar pacotes de controladores e imagens de arranque. Para adicionar ou remover um condutor, localize-o primeiro no nó **dos Condutores.** Em seguida, edite as embalagens ou as imagens de arranque com as quais o controlador selecionado está associado.  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **os Sistemas Operativos**e, em seguida, selecionar o nó **dos Controladores.**  

2. Selecione os controladores do dispositivo que pretende adicionar a uma embalagem de controlador.  

3. No separador **Casa** da fita, no grupo **Driver,** selecione **Editar**, e, em seguida, escolha **Pacotes de Condutor**.  

4. Para adicionar um controlador de dispositivo, selecione a caixa de verificação dos pacotes de controladores aos quais pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação dos pacotes de controladores de que pretende remover o controlador de dispositivo.  

    Se estiver a adicionar controladores de dispositivos associados aos pacotes de condutor, pode criar opcionalmente um novo pacote. Selecione **Novo Pacote**, que abre a caixa de diálogo **New Driver Package.**  

5. Se o pacote já tiver sido distribuído para pontos de distribuição, selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não podeusar os controladores de dispositivos até que sejam distribuídos em pontos de distribuição. Se selecionar **Não,** execute a ação Ponto de Distribuição de **Atualização** antes de utilizar a imagem de arranque. Se o pacote do condutor nunca tiver sido distribuído, deve utilizar a ação **Distribute Content** no nó do **Pacote seleto** do Condutor. Antes de os controladores estarem disponíveis, tem de atualizar o pacote de controlador nos pontos de distribuição.  

    Selecione **OK** quando terminar.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Gerir controladores de dispositivo numa imagem de arranque  

Pode adicionar imagens de arranque Os controladores de dispositivos Windows que foram importados para o catálogo. Para adicionar controladores de dispositivos a uma imagem de arranque, utilize as seguintes diretrizes:  

- Adicione apenas controladores de armazenamento e rede para iniciar imagens. Outros tipos de condutores não são geralmente necessários no Windows PE. Os condutores que não são necessários aumentam desnecessariamente o tamanho da imagem do porta-malas.  

- Adicione apenas controladores de dispositivos para o Windows 10 a uma imagem de arranque. A versão necessária do Windows PE baseia-se no Windows 10.  

- Certifique-se de que utiliza o controlador de dispositivo correto para a arquitetura da imagem do arranque. Não adicione um controlador de dispositivo x86 a uma imagem de arranque x64.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Processo para modificar os controladores do dispositivo associados a uma imagem de arranque  

1. Na consola de Configuração Manager, vá ao espaço de trabalho da Biblioteca de **Software.** Expandir **os Sistemas Operativos**e, em seguida, selecionar o nó **dos Controladores.**  

2. Selecione os controladores do dispositivo que pretende adicionar à embalagem do controlador.  

3. No separador **Home** da fita, no grupo **Driver,** selecione **Editar**, e, em seguida, escolha **imagens Boot**.  

4. Para adicionar um controlador de dispositivo, selecione a caixa de verificação da imagem de arranque à qual pretende adicionar os controladores de dispositivo. Para remover um controlador de dispositivo, desmarque a caixa de verificação da imagem de arranque de que pretende remover o controlador de dispositivo.  

5. Se não quiser atualizar os pontos de distribuição onde a imagem de arranque é armazenada, limpe os pontos de **distribuição da Atualização quando terminar** a caixa de verificação. Por predefinição, os pontos de distribuição são atualizados quando a imagem de arranque é atualizada.  

    - Selecione **Sim** na caixa de diálogo para atualizar as imagens de arranque nos pontos de distribuição. Não podeusar os controladores de dispositivos até que sejam distribuídos em pontos de distribuição. Se selecionar **Não,** execute a ação Ponto de Distribuição de **Atualização** antes de utilizar a imagem de arranque. Se o pacote do condutor nunca tiver sido distribuído, deve utilizar a ação **Distribute Content** no nó do **Pacote seleto** do Condutor.  

    - O Gestor de Configuração avisa-o se a arquitetura para um ou mais condutores não corresponder à arquitetura das imagens de arranque que selecionou. Se não corresponderem, selecione **OK**. Volte à página de Detalhes do **Condutor** e limpe os condutores que não correspondem à arquitetura da imagem de arranque selecionada. Por exemplo, se selecionar uma imagem de arranque x64 e x86, todos os controladores têm de suportar ambas as arquiteturas. Se selecionar uma imagem de arranque x64, todos os controladores têm de suportar a arquitetura x64.  

        > [!NOTE]
        > - A arquitetura baseia-se na arquitetura relatada no INF do fabricante.  
        > - Se um controlador suportar ambas as arquiteturas, pode importá-lo para qualquer imagem de arranque.  

    - O Gestor de Configuração avisa-o se adicionar controladores de dispositivos que não são controladores de rede ou armazenamento a uma imagem de arranque. Na maioria dos casos, não são necessários para a imagem do arranque. Selecione **Sim** para adicionar os controladores à imagem de arranque ou **Não** para voltar e modificar a sua seleção de motorista.  

    - O Gestor de Configuração avisa-o se um ou mais dos controladores selecionados não estiverem devidamente assinados digitalmente. Selecione **Sim** para continuar ou selecione **Não** para voltar e fazer alterações na sua seleção de motorista.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a>Ações adicionais para condutores de dispositivos  

Pode fazer ações adicionais para gerir os condutores quando os selecionar no nó **dos Condutores.**  

#### <a name="categorize"></a>Categorizar
Limpa, gere ou define uma categoria administrativa para os condutores selecionados.

#### <a name="delete"></a>Eliminar
Retira o condutor do nó dos **Condutores** e também retira o condutor dos pontos de distribuição associados.

#### <a name="disable"></a>Desativar
Proíbe o condutor de ser instalado. Esta ação desativa temporariamente o condutor. A sequência de tarefas não pode instalar um controlador desativado quando se implementa um Sistema Operativo. 

> [!Note]  
> Esta ação apenas impede que os condutores instalem utilizando o passo de sequência de tarefas **do condutor de aplicação automática.**

#### <a name="enable"></a>Ativar
Permite que os computadores do cliente do Gestor de Configuração e as sequências de tarefas instalem o controlador do dispositivo quando implementar o SISTEMA.

#### <a name="move"></a>Mover
Move o controlador de dispositivo para outra pasta do nó **Controladores** .

#### <a name="properties"></a>Propriedades
Abre a caixa de diálogo **Properties.** Reveja e altere as propriedades do condutor. Por exemplo, altere o seu nome e descrição, ative ou desative-o e especifique quais as plataformas em que pode funcionar.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a>Utilize sequências de tarefas para instalar controladores  

Utilize sequências de tarefas para automatizar a forma como o Sistema operativo é implantado. Cada passo na sequência de tarefas pode fazer uma ação específica, como instalar um controlador. Pode utilizar os seguintes dois passos de sequência de tarefas para instalar os controladores do dispositivo quando implementar um SISTEMA:  

- [Aplicar Controladores Automaticamente](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): este passo permite-lhe fazer corresponder e instalar automaticamente controladores de dispositivo como parte da implementação de um sistema operativo. Pode configurar o passo da sequência de tarefas para instalar apenas o melhor controlador combinado para cada dispositivo de hardware detetado. Em alternativa, especifique que o passo instala todos os controladores compatíveis para cada dispositivo de hardware detetado e, em seguida, deixe o Windows Configurar escolher o melhor controlador. Também pode especificar uma categoria de condutor para limitar os condutores disponíveis para este passo.  

- [Aplicar Pacote de Controlador](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): este passo permite-lhe disponibilizar todos os controladores de dispositivo num pacote de controladores específico para a Configuração do Windows. Nos pacotes de controladores especificados, a Configuração do Windows procura os controladores de dispositivos necessários. Quando cria suportes de dados autónomos, tem de utilizar este passo para instalar controladores de dispositivo.  

Quando utilizar estes passos de sequência de tarefas, também pode especificar como os controladores são instalados no computador onde implementa o SISTEMA. Para obter mais informações, consulte Gerir sequências de [tarefas para automatizar tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a>Relatórios de motorista  

Na categoria de relatórios **Gestão do Controlador** , pode utilizar vários relatórios para determinar as informações gerais sobre os controladores de dispositivos no catálogo de controladores. Para obter mais informações sobre relatórios, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).

