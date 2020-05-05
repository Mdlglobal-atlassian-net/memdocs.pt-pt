---
title: Criar uma sequência de tarefas para instalar um SO
titleSuffix: Configuration Manager
description: Utilize sequências de tarefas no Gestor de Configuração para instalar automaticamente uma imagem de OS e outros conteúdos num computador de destino.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723013"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Criar uma sequência de tarefas para instalar um SO

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize sequências de tarefas no Gestor de Configuração para instalar automaticamente uma imagem de OS num computador de destino. Cria uma sequência de tarefas que faz referência a uma imagem de arranque utilizada para iniciar o computador de destino, a imagem de OS que pretende instalar no computador de destino, e qualquer outro conteúdo adicional, como outras aplicações ou atualizações de software, que pretende instalar. Em seguida, tem de implementar a sequência de tarefas na coleção que contém o computador de destino.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>Criar uma sequência de tarefas para instalar um SISTEMA

Existem vários cenários para implementar um S para computadores no seu ambiente. Na maioria dos casos, crie uma sequência de tarefas e selecione **Instalar um pacote** de imagem existente no Assistente de Sequência de Tarefas Criar. Esta opção cria uma sequência de tarefas que instala o SISTEMA, migra as definições do utilizador, aplica atualizações de software e instala aplicações.

### <a name="prerequisites"></a>Pré-requisitos

Antes de criar uma sequência de tarefas para instalar um SISTEMA, devem estar em vigor os seguintes requisitos:

#### <a name="required"></a>Necessário

- Uma [imagem de bota](../get-started/manage-boot-images.md)  

- Uma [imagem de OS](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Necessário (se utilizado)

- Sincronizar [atualizações](../../sum/get-started/synchronize-software-updates.md) de software  

- Adicionar [aplicações](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Processo para criar uma sequência de tarefas que instala um SO  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar sequência de **tarefas**. Esta ação inicia o Assistente de Sequência de Tarefas Create.  

3. Na página **Criar uma nova sequência** de tarefas, selecione **Instale um pacote**de imagem existente , e, em seguida, selecione **Next**.  

4. Na página **informação** da sequência de tarefas, especifique as seguintes definições:  

    - **Nome da sequência de tarefas**: especifique um nome que identifique a sequência de tarefas.  

    - **Descrição**: Especificar uma descrição do que a sequência de tarefas faz.  

    - **Imagem de arranque**: Especifique a imagem de arranque que a sequência de tarefas utiliza para instalar o SISTEMA no computador de destino. A imagem de arranque contém uma versão do Windows PE, além de quaisquer controladores adicionais de dispositivos necessários. Para mais informações, consulte [Gerir imagens](../get-started/manage-boot-images.md)de arranque .  

        > [!IMPORTANT]  
        > A arquitetura da imagem de arranque deve ser compatível com a arquitetura de hardware do computador de destino.  

5. Na página De instalar o **Windows,** especifique as seguintes definições:  

    - **Pacote de imagem**: Especifique a embalagem que contém a imagem DE Os para instalar. Para mais informações, consulte [Gerir imagens do OS](../get-started/manage-operating-system-images.md).  

    - **Imagem**: Se o pacote de imagem OS tiver várias imagens, especifique o índice da imagem de OS para instalar.  

    - **Partição e formato do computador-alvo que instala o sistema operativo**: Especifique se pretende que a sequência de tarefas seja partição e forme o computador de destino antes de instalar o SISTEMA.  

    - **Chave do produto**: Especifique a chave do produto Windows, se necessário. Pode especificar chaves de licenciamento em volume codificadas e chaves de produto padrão. Se utilizar uma chave de produto não codificada, cada grupo de cinco`-`caracteres deve ser separado por um painel (). Por exemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Modo de licenciamento do servidor**: especifique se a licença do servidor é **Por posto**, **Por servidor**ou se não é especificada qualquer licença. Se a licença do servidor for **Por servidor**, especifique também o número máximo de ligações de servidor.  

    - Especifique como lidar com a conta do administrador para o novo SISTEMA:  

        - **Gera a palavra-passe da conta do administrador local e desativa a conta em todas as plataformas suportadas (recomendadas)**: O Windows desativa a conta de administrador local após a sequência de tarefas implementar a imagem DES.  

        - **Ative a conta e especifique a palavra-passe**do administrador local: O Windows utiliza a mesma palavra-passe para a conta do administrador local em todos os computadores onde a sequência de tarefas implementa a imagem do SISTEMA.  

6. Na página **da Rede Configurar,** especifique as seguintes definições:  

    - **Junte-se**a um grupo de trabalho : Adicione o computador de destino a um grupo de trabalho.  

    - **Junte-se**a um domínio : Adicione o computador de destino a um domínio. Em **Domínio**, especifique o nome do domínio.  

        > [!IMPORTANT]  
        > Pode navegar para localizar domínios na floresta local, mas tem de especificar o nome de domínio de uma floresta remota.  

        Também pode especificar uma unidade organizacional (OU) no campo **Domain OU.** Esta definição é opcional e especifica o nome lDAP X.500 distinguido da U. Se ainda não existir, o Windows cria a conta de computador neste OU.  

    - **Conta**: O nome do utilizador e a palavra-passe para a conta que tem permissões para aderir ao domínio especificado. Por exemplo: *domínio\utilizador* ou *%variable%*.  

        > [!IMPORTANT]  
        > Se pretender migrar as definições de domínio ou as definições do grupo de trabalho, introduza as credenciais de domínio apropriadas.  

7. Na página 'Gestor de **Configuração de Instalação',** especifique o pacote de cliente do Gestor de Configuração para instalar no computador de destino. Também pode incluir quaisquer propriedades de instalação.  

8. Na página **emigração do Estado,** especifique as seguintes informações:  

    - **Capturar as definições do utilizador**: A sequência de tarefas captura o estado do utilizador. Para obter mais informações sobre como capturar e restaurar o estado do utilizador, consulte gerir o [estado do utilizador](../get-started/manage-user-state.md).  

    - **Definições de rede de captura**: A sequência de tarefas captura as definições de rede a partir do computador de destino. Captura a adesão ao domínio ou grupo de trabalho, também as definições de adaptador de rede.  

    - **Capturar as definições**do Microsoft Windows : A sequência de tarefas captura as definições do Windows a partir do computador de destino antes de instalar a imagem DES. Captura o nome do computador, o nome do utilizador e da organização registados e as definições do fuso horário.  

9. Na página **Incluir Atualizações,** especifique se deve instalar atualizações de software necessárias, todas as atualizações de software ou nenhuma atualização de software. Se especificar para instalar atualizações de software, o Gestor de Configuração instala apenas as atualizações de software que são direcionadas para as coleções de que o computador de destino é membro.  

10. Na página De instalação de **aplicações,** especifique as aplicações a instalar no computador de destino. Se especificar várias aplicações, poderá também especificar que a sequência de tarefas deverá continuar se a instalação de uma aplicação específica falhar.  

11. Conclua o assistente.  

Agora, pode implementar a sequência de tarefas numa coleção de computadores. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Conteúdo pré-cache

<!--4224642-->
A partir da versão 1906, pode ativar este tipo de sequência de tarefas para o conteúdo pré-cache. A função pré-cache para implementações disponíveis de sequências de tarefas permite que os clientes descarreguem conteúdo relevante antes de um utilizador instalar a sequência de tarefas.  

Para mais informações, consulte o [conteúdo pré-cache da Configure](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a>Sequência de tarefas de exemplo

Utilize a tabela seguinte como guia à medida que cria uma sequência de tarefas que implementa um SISTEMA utilizando uma imagem existente. A tabela ajuda-o a decidir a sequência geral para os passos da sua sequência de tarefas e como organizar e estruturar esses passos de sequência de tarefas em grupos lógicos. A sequência de tarefas que criar pode ser diferente da deste exemplo, podendo conter mais ou menos passos de sequência de tarefas e grupos.  

> [!NOTE]  
> Utilize o Assistente de Sequência de Tarefas Criar esta sequência de tarefas.  
>
> Quando utilizao o Assistente de Sequência de Tarefas Create para criar esta nova sequência de tarefas, alguns dos nomes de passo são diferentes do que seriam se adicionasse manualmente estes passos de sequência de tarefas a uma sequência de tarefas existente.

|Grupo ou passo de sequência de tarefas|Descrição|  
|---------------------------------|-----------------|  
|Capturar Ficheiros e Definições - (Novo grupo de sequência de **tarefas)**|Criar um grupo de sequência de tarefas. Os grupos de sequência de tarefas mantêm agrupados os passos de sequência de tarefas semelhantes para uma melhor organização e um melhor controlo de erros.<br /><br /> Este grupo contém os passos necessários para capturar ficheiros e definições do sistema operativo de um computador de referência.|  
|Capturar Definições do Windows|Utilize este passo de sequência de tarefas para identificar as definições do Microsoft Windows para capturar a partir do computador de referência. Pode capturar o nome do computador, informações do utilizador e da organização e as definições de fuso horário.|  
|Capturar definições de rede|Utilize este passo de sequência de tarefas para capturar definições de rede a partir do computador de referência. Pode capturar a associação a domínios ou grupos de trabalho do computador de referência e as informações de definições da placa de rede.|  
|Capturar Ficheiros e Definições do Utilizador - **(novo subgrupo** de sequência de tarefas)|Crie um grupo de sequência de tarefas dentro de um grupo de sequência de tarefas. Este subgrupo contém os passos necessários para capturar os dados de estado do utilizador. À semelhança do grupo inicial que adicionou, este subgrupo mantém passos semelhantes de sequência de tarefas em conjunto para um melhor controlo de organização e erro.|  
|Solicitar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para pedir acesso a um ponto de migração de estado onde os dados de estado de utilizador estão armazenados. Pode configurar este passo de sequência de tarefas para capturar ou restaurar as informações de estado do utilizador.|  
|Capturar Definições e Ficheiros do Utilizador|Utilize este passo de sequência de tarefas para utilizar a Ferramenta de Migração do Estado do Utilizador (USMT) para capturar o estado do utilizador e as definições do computador de referência que receberão a sequência de tarefas associada a este passo de tarefa. Pode capturar as opções padrão ou configurar quais opções capturar.|  
|Libertar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para notificar o ponto de migração de estado de que a ação de captura ou restauro está concluída.|  
|Instalar sistema operativo - (Novo grupo de sequência de **tarefas)**|Criar outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para instalar e configurar o ambiente Windows PE.|  
|Reiniciar no Windows PE|Utilize este passo de sequência de tarefas para especificar as opções de reinício para o computador de destino que recebe esta sequência de tarefas. Este passo apresentará uma mensagem ao utilizador a indicar que o computador será reiniciado para que a instalação possa continuar.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSInWinPE** . Se o valor associado for igual a **false** , o passo de sequência de tarefas continuará.|  
|Criar Partições do Disco 0|Este passo de sequência de tarefas especifica as ações necessárias para formatar o disco rígido no computador de destino. O número de disco predefinido é **0**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSClientCache** . Este passo funciona se a cache do cliente do Gestor de Configuração não existir.|  
|Aplicar Sistema Operativo|Utilize este passo de sequência de tarefas para instalar a imagem do sistema operativo no computador de destino. Este passo elimina primeiro todos os ficheiros do volume, com exceção de quaisquer ficheiros de controlo específicos do Gestor de Configuração. Em seguida, aplica todas as imagens de volume contidas no ficheiro WIM ao correspondente volume sequencial de disco no computador-alvo. Pode especificar um ficheiro de resposta **sysprep** , bem como configurar a partição de disco a utilizar para a instalação.|  
|Aplicar Definições do Windows|Utilize este passo de sequência de tarefas para configurar as informações de configuração das definições do Windows para o computador de destino. As definições do Windows que pode aplicar são informações da organização e do utilizador, informações da chave de licença ou produto, fuso horário e a palavra-passe de administrador local.|  
|Aplicar Definições de Rede|Utilize este passo de sequência de tarefas para especificar as informações de configuração da rede ou do grupo de trabalho para o computador de destino. Também pode especificar se o computador utiliza um servidor DHCP ou pode atribuir estaticamente as informações de endereço IP.|  
|Aplicar Controladores de Dispositivo|Utilize este passo de sequência de tarefas para instalar controladores como parte da implementação do sistema operativo. Pode permitir que a Configuração do Windows pesquise todas as categorias de controladores existentes ao selecionar **Considerar controladores de todas as categorias** ou limitar as categorias de controladores que a Configuração do Windows pode pesquisar ao selecionar **Limitar a correspondência de controladores para apenas considerar controladores nas categorias selecionadas**.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Este passo de sequência de tarefa saem apenas se o valor da variável não for igual a **FullMedia**.|  
|Aplicar Pacote de Controlador|Utilize este passo de sequência de tarefas para disponibilizar todos os controladores de dispositivo de um pacote de controladores para utilização pela configuração do Windows.|  
|Sistema Operativo de configuração - (Novo grupo de sequência de **tarefas)**|Criar outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para configurar o sistema operativo instalado.|  
|Configurar Windows e ConfigMgr|Utilize este passo de sequência de tarefas para instalar o software cliente do Gestor de Configuração. O Gestor de Configuração instala e regista o cliente do Gestor de Configuração GUID. Pode atribuir os parâmetros de instalação necessários na janela **Propriedades de instalação** .|  
|Instalar Atualizações|Utilize este passo de sequência de tarefas para especificar a forma como as atualizações de software são instaladas no computador de destino. O computador de destino não é avaliado para atualizações de software aplicáveis até que este passo de sequência de tarefas seja executado. Nessa altura, o computador de destino é avaliado para atualizações de software semelhantes a qualquer outro cliente gerido pelo Gestor de Configuração.<br /><br /> Este passo utiliza a variável de sequência de tarefas só de leitura **_SMSTSMediaType** . Este passo de sequência de tarefa saem apenas se o valor da variável não for igual a **FullMedia**.|  
|Restaurar ficheiros e definições do utilizador - **(novo subgrupo** de sequência de tarefas)|Criar outro subgrupo de sequência de tarefas. Este subgrupo contém os passos necessários para restaurar as definições e ficheiros do utilizador.|  
|Solicitar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para pedir acesso a um ponto de migração de estado onde os dados de estado de utilizador estão armazenados.|  
|Restaurar Definições e Ficheiros do Utilizador|Utilize este passo de sequência de tarefas para executar a Ferramenta de Migração do Estado do Utilizador (USMT) para restaurar o estado do utilizador e as definições para um computador de destino.|  
|Libertar Armazenamento de Estados do Utilizador|Utilize este passo de sequência de tarefas para notificar o ponto de migração de estado de que os dados de estado do utilizador já não são necessários.|  
