---
title: Recuperação não atendida
titleSuffix: Configuration Manager
description: Utilize um script para recuperar os seus sites no Gestor de Configuração.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720801"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperação do site não atendido para Gestor de Configuração   

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Para realizar uma [recuperação sem supervisão](recover-sites.md#site-recovery-procedures) de um site de administração central do Gestor de Configuração ou do site primário, pode criar um script de instalação sem supervisão e, em seguida, utilizar a configuração com a opção de comando **/script.** O script fornece o mesmo tipo de informação que o assistente de configuração solicita, exceto que não existem definições predefinidas. Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de recuperação que está a utilizar.

 Para utilizar a opção de linha de comando /script configuração, tem de criar um ficheiro de inicialização. Em seguida, especifique este nome de ficheiro após a opção /script. O nome do ficheiro não é importante desde que tenha a extensão do nome do ficheiro **.ini.** Quando referenciar o ficheiro de inicialização da configuração na linha de comandos, tem de fornecer o caminho completo do ficheiro. Por exemplo, se o seu ficheiro de inicialização de configuração for nomeado *configuração.ini*, e estiver armazenado na *pasta C:\configuração*, a sua linha de comando seria:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Deve ter direitos de administrador para executar a configuração. Quando executar a configuração com o script sem supervisão, inicie o pedido de comando num contexto de Administrador utilizando **o Run como administrador**.

 O script contém nomes de secções, nomes de chaves e valores. Os nomes de chaves de secção necessários variam consoante o tipo de recuperação que pretende realizar com o script. A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes. As chaves não são sensíveis ao caso. Quando fornece valores de chaves, o nome da chave tem de ser seguido de um sinal de igual (=) e do valor da chave.

 Utilize as secções seguintes para criar o script para a recuperação de site automática. As tabelas apresentam as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, para que tipo de instalação são utilizadas e uma descrição breve da chave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central automática
 Utilize as seguintes informações para configurar um ficheiro de script de configuração não acompanhado para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** ação

    -   **Obrigatório:** sim
    -   **Valores:** RecoverCCAR
    -   **Detalhes:** recupera um site de administração central


-   **Nome-chave:** CDMais

    -   **Obrigatório:** Sim – Só quando se utiliza mídia do CD. Última pasta.
    -   **Valores:** 1 Qualquer valor que não 1 é considerado como não utilizar CD. O mais tardar.
    -   **Detalhes:** O seu script deve incluir esta chave e valor quando executa a configuração dos meios de comunicação num CD. Última pasta com o propósito de instalar um site de administração primária ou central, ou recuperar um site de administração primária ou central. Este valor informa a configuração de que os meios de comunicação formam CD. O mais recente está a ser usado.

**RecoveryOptions**   
-   **Nome da chave:** ServerRecoveryOptions   

    -   **Obrigatório:** sim
    -   **Valores:** 1, 2 ou 4  
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, o Servidor SQL ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:  
        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatório:** talvez
    -   **Valores:**   
         - **10** = Restaurar a base de dados do site a partir de cópias de segurança.  
         - **20** = Utilize uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.   
         - **40** = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         - **80** = saltar a recuperação da base de dados.
    -   **Detalhes:** Especifica como a configuração recupera a base de dados do site no Servidor SQL. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** ReferenceSite  

    -   **Obrigatório:** talvez
    -   **Valores:** &lt;ReferenceSiteFQDN\>
    -   **Detalhes:** Especifica o local primário de referência. Se a cópia de segurança da base de dados for mais antiga do que o período de retenção de rastreio de alterações, ou se recuperar o site sem uma cópia de segurança, o site da administração central utiliza o site de referência para recuperar dados globais.

         Quando não especifica um site de referência, e a cópia de segurança é mais antiga do que o período de retenção de rastreio de alterações, todos os sites primários são reinicializados com os dados restaurados do site da administração central.

         Quando não especifica um site de referência, e a cópia de segurança está dentro do período de retenção de rastreio de alterações, apenas alterações uma vez que a cópia de segurança é replicada a partir de locais primários. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.

         Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.

-   **Nome da chave:** SiteServerBackupLocation

    -   **Obrigatório:** não
    -   **Valores:** &lt;PathtositeServerBackupSet\>
    -   **Detalhes:** especifica o caminho para o conjunto de cópias de segurança do servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.


-   **Nome da chave:** BackupLocation

    -   **Obrigatório:** talvez
    -   **Valores:** &lt;PathtoSiteDatabaseBackupSet\>
    -   **Detalhes:** especifica o caminho para o conjunto de cópias de segurança da base de dados do site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .


**Opções**

- **Nome da chave:** ProductID
  -   **Obrigatório:** sim
  -   **Valores:**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Detalhes:** A chave de produto de instalação do Gestor de Configuração, incluindo as traços. O Enter **Eval** pode instalar a versão de avaliação do 'Gestor de Configuração'.  


- **Nome da chave:** SiteCode

  -   **Obrigatório:** sim
  -   **Valores:** &lt;Código do site\>
  -   **Detalhes:** Três caracteres alfa-numéricos que identificam exclusivamente o site na sua hierarquia. Especifique o código do site que foi usado pelo site antes da falha.


- **Nome da chave:** SiteName

  -   **Obrigatório:** sim
  -   **Valores:** SiteName
  -   **Detalhes:** descrição deste site.


- **Nome da chave:** SMSInstallDir

  - **Obrigatório:** sim
  - **Valores:** &lt;*ConfigMgrInstallationPath*>
  - **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.
    > [!NOTE]   
    >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Gestor de Configuração.

- **Nome da chave:** SDKServer

  -   **Obrigatório:** sim
  -   **Valores:** &lt;*FQDN do Fornecedor de SMS*>
  -   **Detalhes:** Especifica o FQDN para o servidor que acolhe o Provedor SMS. Especifique o servidor que acolheu o Fornecedor SMS antes da falha.

       Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

- **Nome da chave:** PrerequisiteComp

  -   **Obrigatório:** sim
  -   **Valores:** 0 ou 1  
       0 = transferir   
       1 = já transferido
  -   **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar um valor de 0, a configuração descarrega os ficheiros.  


- **Nome da chave:** PrerequisitePath

  -   **Obrigatório:** sim
  -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.

- **Nome da chave:** AdminConsole

  -   **Obrigatório:** talvez
  -   **Valores:** 0 ou 1 0 = não instalar   
       1 = instalar
  -   **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.


- **Nome da chave:** JoinCEIP   
  > [!Note]  
  > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

  -   **Obrigatório:** sim
  -   **Valores:** 0 ou 1  
       0 = não aderir  
       1 = aderir
  -   **Detalhes:** especifica se pretende aderir ao Programa de Melhoramento da Experiência do Cliente.

**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatório:** sim
    -   **Valores:** * &lt;SQLServerNameName\>*
    -   **Detalhes:** O nome do servidor, ou nome de instância agrupado, executando o SQL Server que acolhe a base de dados do site. Especifique o mesmo servidor que acolheu a base de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatório:** sim
    -   **Valores:** * &lt;SiteDatabaseName\> * ou\\ * &lt;Nome\>* do*&lt;Site NameName\> *
    -   **Detalhes:** o nome da base de dados do SQL Server para criar ou utilizar na instalação da base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi usado antes da falha.

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, deve especificar o nome da instância e o nome da base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatório:** não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Especifique a mesma porta SSB que foi utilizada antes da falha.

## <a name="recover-a-primary-site-unattended"></a>Recuperar um Site Primário em Modo Automático
 Utilize as seguintes informações para configurar um ficheiro de script de configuração não acompanhado para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** ação

    -   **Obrigatório:** sim
    -   **Valores:** RecoverPrimarySite
    -   **Detalhes:** recupera um site primário


-   **Nome-chave:** CDMais

    -   **Obrigatório:** Sim – Só quando se utiliza mídia do CD. Última pasta.
    -   **Valores:** 1 Qualquer valor que não 1 é considerado como não utilizar CD. O mais tardar.
    -   **Detalhes:** O seu script deve incluir esta chave e valor quando executa a configuração dos meios de comunicação num CD. Última pasta com o propósito de instalar um site de administração primária ou central, ou recuperar um site de administração primária ou central. Este valor informa a configuração de que os meios de comunicação formam CD. O mais recente está a ser usado.

**RecoveryOptions**

-   **Nome da chave:** ServerRecoveryOptions

    -   **Obrigatório:** sim
    -   **Valores:** 1, 2 ou 4    
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, o Servidor SQL ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:

        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Obrigatório:** talvez
    -   **Valores:**   
         - **10** = Restaurar a base de dados do site a partir de cópias de segurança.  
         - **20** = Utilize uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.     
         - **40** = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         - **80** = saltar a recuperação da base de dados.
    -   **Detalhes:** Especifica como a configuração recupera a base de dados do site no Servidor SQL. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** SiteServerBackupLocation

    -   **Obrigatório:** não
    -   **Valores:** &lt;PathtositeServerBackupSet\>
    -   **Detalhes:** especifica o caminho para o conjunto de cópias de segurança do servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.     


-   **Nome da chave:** BackupLocation

    -   **Obrigatório:** talvez
    -   **Valores:** &lt;PathtoSiteDatabaseBackupSet\>
    -   **Detalhes:** especifica o caminho para o conjunto de cópias de segurança da base de dados do site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .

**Opções**

-   **Nome da chave:** ProductID

    -   **Obrigatório:** sim
    -   **Valores:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Detalhes:** A chave de produto de instalação do Gestor de Configuração, incluindo as traços. O Enter **Eval** pode instalar a versão de avaliação do 'Gestor de Configuração'.  


-   **Nome da chave:** SiteCode

    -   **Obrigatório:** sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** Três caracteres alfa-numéricos que identificam exclusivamente o site na sua hierarquia. Especifique o código do site que foi usado pelo site antes da falha.


-   **Nome da chave:** SiteName

    -   **Obrigatório:** sim
    -   **Valores:** SiteName
    -   **Detalhes:** descrição deste site.


-   **Nome da chave:** SMSInstallDir

    -   **Obrigatório:** sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.

        > [!NOTE]   
        >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Gestor de Configuração.

-   **Nome da chave:** SDKServer

    -   **Obrigatório:** sim
    -   **Valores:** &lt;*FQDN do Fornecedor de SMS*>
    -   **Detalhes:** Especifica o FQDN para o servidor que acolhe o Provedor SMS. Especifique o servidor que acolheu o Fornecedor SMS antes da falha.

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Obrigatório:** sim
    -   **Valores:** 0 ou 1    
         0 = transferir   
         1 = já transferido   
    -   **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar um valor de 0, a configuração descarrega os ficheiros.


-   **Nome da chave:** PrerequisitePath

    -   **Obrigatório:** sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.


-   **Nome da chave:** AdminConsole

    -   **Obrigatório:** talvez
    -   **Valores:** 0 ou 1  
         0 = não instalar   
         1 = instalar  
    -   **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

    -   **Obrigatório:** sim
    -   **Valores:** 0 ou 1    
         0 = não aderir  
         1 = aderir
    -   **Detalhes:** especifica se pretende aderir ao Programa de Melhoramento da Experiência do Cliente.


**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Obrigatório:** sim
    -   **Valores:** * &lt;SQLServerNameName\>*
    -   **Detalhes:** O nome do servidor, ou nome de instância agrupado, executando o SQL Server que acolhe a base de dados do site. Especifique o mesmo servidor que acolheu a base de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Obrigatório:** sim
    -   **Valores:** * &lt;SiteDatabaseName\> * ou\\ * &lt;Nome\>* do*&lt;Site NameName\> *
    -   **Detalhes:** o nome da base de dados do SQL Server para criar ou utilizar na instalação da base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi usado antes da falha.

        > [!IMPORTANT]    
        >  Se não utilizar a instância predefinida, deve especificar o nome da instância e o nome da base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Obrigatório:** não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** especifica a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Especifique a mesma porta SSB que foi utilizada antes da falha.

**ExpansionOption de hierarquia**

-   **Nome da chave** CCARSiteServer

    -   **Obrigatório:** talvez
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalhes:** Especifica o site da administração central a que um site primário se liga quando se junta à hierarquia do Gestor de Configuração. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Especifique o código do site que foi usado para o site da administração central antes da falha.

-   **Nome da chave:** CASRetryInterval

    -   **Obrigatório:** não
    -   **Valores:** &lt;*Interval*>
    -   **Detalhes:** especifica o intervalo entre tentativas (em minutos) para ligar ao site de administração central, após uma falha da ligação. Por exemplo, se a ligação ao site da administração central falhar, o site principal aguarda o número de minutos que especifica para o CASRetryInterval e, em seguida, retenta a ligação.


-   **Nome da chave:** WaitForCASTimeout

    -   **Obrigatório:** não
    -   **Valores:** &lt;*Timeout*>
    -   **Detalhes:** especifica o valor de tempo limite máximo (em minutos) para um site primário se ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, tenta efetuar de novo a ligação com base no CASRetryInterval, até atingir o WaitForCASTimeout. Pode especificar um valor entre 0 e 100.
