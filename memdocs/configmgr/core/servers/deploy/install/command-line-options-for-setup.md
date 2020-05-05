---
title: Configurar opções de linha de comando
titleSuffix: Configuration Manager
description: Crie scripts de automatização para instalar o Gestor de Configuração a partir de uma linha de comando.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718253"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Opções de linha de comando para configuração do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as seguintes informações para configurar scripts ou para instalar o Gestor de Configuração a partir de uma linha de comando.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a>Opções de linha de comando para configuração

Executar a configuração a `\BIN\X64` partir do diretório do caminho de instalação do Gestor de Configuração no servidor do site.

### `/DEINSTALL`

Desinstale o site. Executar a configuração a partir do computador do servidor do site.  

### `/DONTSTARTSITECOMP`

Instale um site, mas impede que o serviço de Gestor de Componentes do Site comece. Até que o serviço de Gestor de Componentes do Site comece, o site não está ativo. O Gestor de Componentes do Site é responsável pela instalação e arranque do serviço SMS_Executive, e por processos adicionais no site. Depois de concluída a instalação do site, quando iniciar o serviço De Gestor de Componentes do Site, instala o serviço de SMS_Executive e processos adicionais necessários para que o site funcione.  

### `/HIDDEN`

Ocultar a interface do utilizador durante a configuração. Utilize esta opção apenas em conjunto com a opção **/SCRIPT.** O ficheiro script sem supervisão deve fornecer todas as opções necessárias ou falhas de configuração.  

### `/NOUSERINPUT`

Desative a entrada do utilizador durante a configuração, mas exibe o assistente de configuração. Utilize esta opção apenas em conjunto com a opção **/SCRIPT.** O ficheiro script sem supervisão deve fornecer todas as opções necessárias ou falhas de configuração.  

### `/RESETSITE`

Executar um reset do site que repõe a base de dados e as contas de serviço para o site.

Para mais informações, consulte [Executar um reset](../../manage/modify-your-infrastructure.md#bkmk_reset)do site .  

### `/TESTDBUPGRADE`

Faça um teste numa cópia de segurança da base de dados do site para se certificar de que a base de dados pode fazer upgrade.

> [!IMPORTANT]  
> Não execute esta opção de linha de comando na base de dados do site de produção. Executar esta opção de linha de comando na base de dados do seu site de produção atualiza a base de dados do site e pode tornar o seu site inoperável.

#### <a name="usage"></a>Utilização

Forneça o nome da instância e o nome da base de dados para a base de dados do site. Se especificar apenas o nome da base de dados, a configuração utiliza o nome da instância predefinida.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Execute uma atualização sem supervisão de um site. Especifique a chave do`-`produto, incluindo as traços (). Especifique também o caminho para os ficheiros pré-requisitos de configuração previamente descarregados.  

Para obter mais informações sobre os ficheiros pré-requisitos de configuração, consulte o Downloader de [Configuração](setup-downloader.md).  

#### <a name="usage"></a>Utilização

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Executar uma instalação sem vigilância. Utilize um ficheiro de inicialização de configuração com esta opção. Para obter mais informações sobre como executar a configuração sem vigilância, consulte [Instalar sites utilizando uma linha de comando](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Utilização

`/SCRIPT <setup script path>`

### `/SDKINST`

Instale o Fornecedor SMS no computador especificado. Forneça o nome de domínio totalmente qualificado (FQDN) para o computador SMS Provider. Para obter mais informações sobre o Fornecedor de SMS, consulte plan para o Provedor de [SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Utilização

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Desinstale o Fornecedor SMS no computador especificado. Forneça o FQDN para o computador SMS Provider.  

#### <a name="usage"></a>Utilização

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Gerencie os idiomas instalados num site previamente instalado. Forneça a localização do ficheiro do script do idioma que contém as definições do idioma. Para mais informações, consulte as opções da linha de comando para gerir a secção [de idiomas.](#bkmk_Lang)  

#### <a name="usage"></a>Utilização

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>Opções de linha de comando para gerir idiomas

### <a name="identification"></a>Identificação

- **Nome da chave:** ação  

    - **Obrigatório:** sim  

    - **Valores:**`ManageLanguages`  

    - **Detalhes:** Gere o suporte de linguagem do servidor, cliente e cliente móvel num site.  

### <a name="options"></a>Opções

- **Nome-chave:** AdicionarIdiomas Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito.  

- **Nome-chave:** AdicionarIdiomas Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas que estarão disponíveis para computadores clientes. O inglês está disponível por defeito.  

- **Nome-chave:** Eliminar Idiomas do Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas a remover e que deixará de estar disponível para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Eliminar Idiomas do Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas a remover e que deixarão de estar disponíveis para computadores clientes. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Linguagem mobiledevice  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se as línguas do cliente do dispositivo móvel estão instaladas.  

- **Nome da chave:** PrerequisiteComp  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Download  

        - `1`= Já descarregado  

    - **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar `0`um valor de configuração, a configuração descarrega os ficheiros.  

- **Nome da chave:** PrerequisitePath  

    - **Obrigatório:** sim  

    - **Valores:** <*Caminho para configurar ficheiros pré-requisitos*>  

    - **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>Chaves de ficheiro de script de configuração não atendidas

Utilize as seguintes secções para o ajudar a criar o seu script para configuração sem supervisão. As listas mostram:

- As chaves de script de configuração disponíveis e os seus valores correspondentes
- Se forem necessários
- Que tipo de instalação são usadas
- Uma breve descrição da chave

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Instalação não atendida para um site de administração central (CAS)

Utilize os seguintes detalhes para instalar um CAS utilizando um ficheiro de script de configuração não vigiado.  

#### <a name="identification"></a>Identificação

- **Nome da chave:** ação  

    - **Obrigatório:** sim  

    - **Valores:**`InstallCAS`  

    - **Detalhes:** Instala um CAS.  

- **Nome-chave:** CDMais  

    - **Obrigatório:** Sim, só quando se usa os meios de comunicação do CD. Última pasta.

    - **Valores:**

        - `1`= está a usar os meios de comunicação de CD. Últimas

        - Qualquer valor que não seja 1 = não está a usar CD. Últimos meios de comunicação

    - **Detalhes:** Quando instala ou recupera um local primário ou CAS, e executa a configuração do CD. Última pasta, inclua esta chave e valor. Este valor informa a configuração de que está a usar meios de comunicação a partir de CD. O mais tardar.

#### <a name="options"></a>Opções

- **Nome da chave:** ProductID  

    - **Obrigatório:** sim  

    - **Valores:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= uma chave de produto válida com traços

        - `Eval`= instalar a versão de avaliação do Gestor de Configuração

    - **Detalhes:** Especifica a chave de produto de instalação do Gestor de Configuração, incluindo as traços.

- **Nome da chave:** SiteCode  

    - **Obrigatório:** sim  

    - **Valores:** <Código do*site*>, por exemplo,`ABC`

    - **Detalhes:** Especifica três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia.  

- **Nome-chave:** Nome do site  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*site*>  

    - **Detalhes:** Especifica o nome deste site.  

- **Nome da chave:** SMSInstallDir  

    - **Obrigatório:** sim  

    - **Valores:** <Caminho de*instalação do Gestor de Configuração*>  

    - **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.  

- **Nome da chave:** SDKServer  

    - **Obrigatório:** sim  

    - **Valores:** <*SMS Provider FQDN*>  

    - **Detalhes:** especifica o FQDN do servidor que alojará o Fornecedor de SMS. Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

- **Nome da chave:** PrerequisiteComp  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Download  

        - `1`= Já descarregado  

    - **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar `0`um valor de configuração, a configuração descarrega os ficheiros.  

- **Nome da chave:** PrerequisitePath  

    - **Obrigatório:** sim  

    - **Valores:** <*Caminho para configurar ficheiros pré-requisitos*>  

    - **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.  

- **Nome da chave:** AdminConsole  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'.  

- **Nome da chave:** JoinCEIP  

    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não se junte a  

        - `1`= Juntar-se  

    - **Detalhes:** Especifica se deve aderir ao Programa de Melhoria da Experiência do Cliente (CEIP).  

- **Nome-chave:** AdicionarIdiomas Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito.  

- **Nome-chave:** AdicionarIdiomas Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas que estarão disponíveis para computadores clientes. O inglês está disponível por defeito.  

- **Nome-chave:** Eliminar Idiomas do Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Modifica um site depois de instalado. Especifica os idiomas a remover e que deixará de estar disponível para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Eliminar Idiomas do Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Modifica um site depois de instalado. Especifica os idiomas a remover e que deixarão de estar disponíveis para computadores clientes. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Linguagem mobiledevice  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se as línguas do cliente do dispositivo móvel estão instaladas.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome da chave:** SQLServerName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*servidor SQL*>  

    - **Detalhes:** Especifica o nome do servidor ou instância agrupada que está a executar o SQL Server para alojar a base de dados do site.  

- **Nome da chave:** DatabaseName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome da base de dados do*site*> ou nome do site *<nome*>\\<do*site*>  

    - **Detalhes:** Especifica o nome da base de dados do Servidor SQL para criar, ou a base de dados do Servidor SQL para utilizar, quando a configuração instala a base de dados CAS.  

        > [!IMPORTANT]  
        > Se não utilizar a instância predefinida, especifique o nome da instância e o nome da base de dados do site.  

- **Nome da chave:** SQLSSBPort  

    - **Obrigatório:** não  

    - **Valores:** <Número da*porta SSB*>  

    - **Detalhes:** Especifica a porta SQL Server Broker (SSB) que o SQL Server utiliza. Por predefinição, o SSB utiliza a porta TCP 4022, mas pode utilizar uma porta diferente.  

- **Nome-chave:** SQLDataFilepath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro .mdb*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .mdb.  

- **Nome-chave:** SQLLogFilePath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro ldf*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .ldf.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome-chave:** CloudConnector  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se instalar um ponto de ligação de serviço neste local. Uma vez que só pode instalar o ponto de ligação de serviço `1` no local de topo de uma hierarquia, definir este valor para um local primário infantil.  

- **Nome-chave:** CloudConnectorServer  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <Servidor de ponto de*ligação de serviço FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de ponto de ligação de serviço.  

- **Nome-chave:** UseProxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se o ponto de ligação de serviço utiliza um servidor proxy.  

- **Nome-chave:** Nome proxy  

    - **Obrigatório:** Necessário quando **useProxy** é igual a 1  

    - **Valores:** <*Proxy server FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor proxy que o ponto de ligação de serviço utiliza.  

- **Nome-chave:** ProxyPort  

    - **Obrigatório:** Necessário quando **useProxy** é igual a 1  

    - **Valores:** <*Número da porta*>  

    - **Detalhes:** Especifica o número da porta a utilizar para a porta proxy.  

#### <a name="sabranchoptions"></a>SabranchOptions

<!-- SCCMDocs#390 -->

- **Nome-chave:** SAActive

    - **Obrigatório:** não

    - **Valores:**

        - `0`= Não tem Garantia de Software

        - `1`= A Garantia de Software está ativa

    - **Detalhes:** Especifique se tem garantia de software ativa. Para mais informações, consulte [O Produto e licenciar as FAQ.](../../../understand/product-and-licensing-faq.md)

- **Nome-chave:** Ramo atual

    - **Obrigatório:** não

    - **Valores:**

        - `0`= Instalar o LTSB

        - `1`= Instalar o ramo atual

    - **Detalhes:** Especifique se utilizar o ramo atual do Gestor de Configuração ou o ramo de manutenção a longo prazo (LTSB). Para mais informações, consulte qual o [ramo do Gestor de Configuração que devo usar?](../../../understand/which-branch-should-i-use.md)

### <a name="unattended-install-for-a-primary-site"></a>Instalação sem supervisão para um local primário

Utilize os seguintes detalhes para instalar um local primário utilizando um ficheiro de script de configuração não vigiado.  

#### <a name="identification"></a>Identificação

- **Nome da chave:** ação  

    - **Obrigatório:** sim  

    - **Valores:**`InstallPrimarySite`  

    - **Detalhes:** Instala um local primário.  

- **Nome-chave:** CDMais  

    - **Obrigatório:** Sim, só quando se usa os meios de comunicação do CD. Última pasta.

    - **Valores:**

        - `1`= está a usar os meios de comunicação de CD. Últimas

        - Qualquer valor que não seja 1 = não está a usar CD. Últimos meios de comunicação

    - **Detalhes:** Quando instala ou recupera um local primário ou CAS, e executa a configuração do CD. Última pasta, inclua esta chave e valor. Este valor informa a configuração de que está a usar meios de comunicação a partir de CD. O mais tardar.

#### <a name="options"></a>Opções

- **Nome da chave:** ProductID  

    - **Obrigatório:** sim  

    - **Valores:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= uma chave de produto válida com traços

        - `Eval`= instalar a versão de avaliação do Gestor de Configuração

    - **Detalhes:** Especifica a chave de produto de instalação do Gestor de Configuração, incluindo as traços.

- **Nome da chave:** SiteCode  

    - **Obrigatório:** sim  

    - **Valores:** <*Código do site*>  

    - **Detalhes:** Especifica três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia.  

- **Nome da chave:** SiteName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*site*>  

    - **Detalhes:** Especifica o nome deste site.  

- **Nome da chave:** SMSInstallDir  

    - **Obrigatório:** sim  

    - **Valores:** <Caminho de*instalação do Gestor de Configuração*>

    - **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.  

- **Nome da chave:** SDKServer  

    - **Obrigatório:** sim  

    - **Valores:** <*SMS Provider FQDN*>  

    - **Detalhes:** especifica o FQDN do servidor que alojará o Fornecedor de SMS. Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

- **Nome da chave:** PrerequisiteComp  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Download  

        - `1`= Já descarregado  

    - **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar `0`um valor de configuração, a configuração descarrega os ficheiros.  

- **Nome da chave:** PrerequisitePath  

    - **Obrigatório:** sim  

    - **Valores:** <*Caminho para configurar ficheiros pré-requisitos*>  

    - **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.  

- **Nome da chave:** AdminConsole  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'.  

- **Nome da chave:** JoinCEIP  

    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não se junte a  

        - `1`= Juntar-se  

    - **Detalhes:** Especifica se deve aderir ao CEIP.  

- **Nome-chave:** Ponto de gestão  

    - **Obrigatório:** não  

    - **Valores:** <Servidor de site de*ponto de gestão FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de site de pontode gestão.  

- **Nome-chave:** Protocolo ManagementPoint  

    - **Obrigatório:** não  

    - **Valores:** `HTTPS` ou`HTTP`  

    - **Detalhes:** Especifica o protocolo a utilizar para o ponto de gestão.  

- **Nome-chave:** Ponto de Distribuição  

    - **Obrigatório:** não  

    - **Valores:** <Servidor de site de*ponto de distribuição FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de site de pontos de distribuição.  

- **Nome-chave:** Protocolo de Pontos de Distribuição  

    - **Obrigatório:** não  

    - **Valores:** `HTTPS` ou`HTTP`  

    - **Detalhes:** Especifica o protocolo a utilizar para o ponto de distribuição.  

- **Nome-chave:** Protocolo de Comunicação de Papéis  

    - **Obrigatório:** sim  

    - **Valores:** `EnforceHTTPS` ou`HTTPorHTTPS`  

    - **Detalhes:** Especifica se configurar todos os sistemas do site para aceitar apenas a comunicação HTTPS dos clientes, ou configurar o método de comunicação para cada função do sistema do site. Quando selecionar, `EnforceHTTPS`os clientes devem ter um certificado de infraestrutura de chave pública válida (PKI) para autenticação do cliente.  

- **Nome-chave:** ClienteUsePKICertificate  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não utilizar  

        - `1`= Utilização  

    - **Detalhes:** Especifica se os clientes usarão um certificado PKI cliente para comunicar com as funções do sistema do site.  

- **Nome-chave:** AdicionarIdiomas Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito.  

- **Nome-chave:** AdicionarIdiomas Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Especifica os idiomas que estarão disponíveis para computadores clientes. O inglês está disponível por defeito.  

- **Nome-chave:** Eliminar Idiomas do Servidor  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Modifica um site depois de instalado. Especifica os idiomas a remover e que deixará de estar disponível para a consola, relatórios e objetos do Gestor de Configuração. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Eliminar Idiomas do Cliente  

    - **Obrigatório:** não  

    - **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    - **Detalhes:** Modifica um site depois de instalado. Especifica os idiomas a remover e que deixarão de estar disponíveis para computadores clientes. O inglês está disponível por defeito, não pode removê-lo.  

- **Nome-chave:** Linguagem mobiledevice  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se as línguas do cliente do dispositivo móvel estão instaladas.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome da chave:** SQLServerName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*servidor SQL*>  

    - **Detalhes:** Especifica o nome do servidor ou instância agrupada que executa o SQL Server para alojar a base de dados do site.  

- **Nome da chave:** DatabaseName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome da base de dados do*site*> ou nome do site *<nome*>\\<do*site*>  

    - **Detalhes:** Especifica o nome da base de dados do Servidor SQL para criar ou a base de dados do Servidor SQL para utilizar ao instalar a base de dados do site principal.  

        > [!IMPORTANT]  
        > Se não utilizar a instância predefinida, especifique o nome da instância e o nome da base de dados do site.  

- **Nome da chave:** SQLSSBPort  

    - **Obrigatório:** não  

    - **Valores:** <Número da*porta SSB*>  

    - **Detalhes:** Especifica a porta SSB que o SQL Server utiliza. Por predefinição, o SSB utiliza a porta TCP 4022, mas pode utilizar uma porta diferente.  

- **Nome-chave:** SQLDataFilepath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro .mdb*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .mdb.  

- **Nome-chave:** SQLLogFilePath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro ldf*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .ldf.  

#### <a name="hierarchyexpansionoption"></a>HierarquiaExpansionOption

- **Nome da chave** CCARSiteServer  

    - **Obrigatório:** não  

    - **Valores:** <*Central administration site FQDN*>  

    - **Detalhes:** Especifica o CAS a que um site primário se liga quando se junta à hierarquia do Gestor de Configuração. Especifique o CAS durante a configuração.  

- **Nome da chave:** CASRetryInterval  

    - **Obrigatório:** não  

    - **Valores:** <*Intervalo em minutos*>  

    - **Detalhes:** Especifica o intervalo de repetição em minutos para tentar uma ligação ao CAS após a falha da ligação. Por exemplo, se a ligação ao CAS falhar, o site principal aguarda o número de minutos que especifica para o valor **CASRetryInterval** e, em seguida, retenta a ligação.  

- **Nome da chave:** WaitForCASTimeout  

    - **Obrigatório:** não  

    - **Valores:** <*Intervalo em minutos de 0 a 100*>  

    - **Detalhes:** Especifica o valor máximo do tempo limite em minutos para um local primário ligar ao CAS. Por exemplo, se um local primário não ligar a um CAS, o local primário retenta a ligação ao CAS com base no valor **CASRetryInterval** até que o período **WaitForCASTimeout** seja atingido. Pode especificar um `0` valor `100`de .  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome-chave:** CloudConnector  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se instalar um ponto de ligação de serviço neste local. Uma vez que só pode instalar o ponto de ligação de serviço `0` no local de topo de uma hierarquia, definir este valor para um local primário infantil.  

- **Nome-chave:** CloudConnectorServer  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <Servidor de ponto de*ligação de serviço FQDN*\>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de ponto de ligação de serviço.  

- **Nome-chave:** UseProxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se o ponto de ligação de serviço utiliza um servidor proxy.  

- **Nome-chave:** Nome proxy  

    - **Obrigatório:** Necessário quando **useProxy** é igual a 1  

    - **Valores:** <*Proxy server FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor proxy que o ponto de ligação de serviço utiliza.  

- **Nome-chave:** ProxyPort  

    - **Obrigatório:** Necessário quando **useProxy** é igual a 1  

    - **Valores:** <*Número da porta*>  

    - **Detalhes:** Especifica o número da porta a utilizar para a porta proxy.  

#### <a name="sabranchoptions"></a>SabranchOptions

<!-- SCCMDocs#390 -->

- **Nome-chave:** SAActive

    - **Obrigatório:** não

    - **Valores:**

        - `0`= Não tem Garantia de Software

        - `1`= A Garantia de Software está ativa

    - **Detalhes:** Especifique se tem garantia de software ativa. Para mais informações, consulte [O Produto e licenciar as FAQ.](../../../understand/product-and-licensing-faq.md)

- **Nome-chave:** Ramo atual

    - **Obrigatório:** não

    - **Valores:**

        - `0`= Instalar o LTSB

        - `1`= Instalar o ramo atual

    - **Detalhes:** Especifique se utilizar o ramo atual do Gestor de Configuração ou o ramo de manutenção a longo prazo (LTSB). Para mais informações, consulte qual o [ramo do Gestor de Configuração que devo usar?](../../../understand/which-branch-should-i-use.md)

### <a name="unattended-recovery-for-a-cas"></a>Recuperação não atendida para um CAS

Utilize os seguintes detalhes para recuperar um CAS utilizando um ficheiro de script de configuração não vigiado.  

#### <a name="identification"></a>Identificação

- **Nome da chave:** ação  

    - **Obrigatório:** sim  

    - **Valores:**`RecoverCCAR`  

    - **Detalhes:** Recupera um CAS.  

- **Nome-chave:** CDMais  

    - **Obrigatório:** Sim, só quando se usa os meios de comunicação do CD. Última pasta.

    - **Valores:**

        - `1`= está a usar os meios de comunicação de CD. Últimas

        - Qualquer valor que não seja 1 = não está a usar CD. Últimos meios de comunicação

    - **Detalhes:** Quando instala ou recupera um local primário ou CAS, e executa a configuração do CD. Última pasta, inclua esta chave e valor. Este valor informa a configuração de que está a usar meios de comunicação a partir de CD. O mais tardar.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nome da chave:** ServerRecoveryOptions  

    - **Obrigatório:** sim  

    - **Valores:**

        - `1`= Recuperar servidor do site e servidor SQL

        - `2`= Recuperar apenas o servidor do site

        - `4`= Recuperar apenas o Servidor SQL  

    - **Detalhes:** Especifica se a configuração recupera o servidor do site, o Servidor SQL ou ambos. São também necessárias as seguintes opções com base no valor especificado:  

        - **1** ou **2**: Para recuperar o site utilizando uma cópia de segurança do site, especifique um valor para **o SiteServerBackupLocation**. Se não especificar um valor, a configuração reinstala o site sem o restaurar a partir de um conjunto de cópias de segurança.  

        - **4**: A chave **BackupLocation** é necessária quando configurar um valor de **10** para a chave **DatabaseRecoveryOptions,** que é restaurar a base de dados do site a partir de cópia seletiva.  

- **Nome da chave:** DatabaseRecoveryOptions  

    - **Obrigatório:** Esta chave é necessária quando a definição **de ServerRecoveryOptions** tem um valor de **1** ou **4**.  

    - **Valores:**

        - `10`= Restaurar a base de dados do site a partir de cópias de segurança.  

        - `20`= Utilize uma base de dados do site que recuperou manualmente com outro método.  

        - `40`= Criar uma nova base de dados para o site. Utilize esta opção quando não houver cópia de segurança na base de dados do site disponível. O site recupera dados globais e do site através da replicação de outros sites.  

        - `80`= Saltar a recuperação da base de dados.  

    - **Detalhes:** Especifica como a configuração recupera a base de dados do site no Servidor SQL.  

- **Nome da chave:** ReferenceSite  

    - **Obrigatório:** Esta chave é necessária quando a definição **DatabaseRecoveryOptions** tem um valor de **40**.  

    - **Valores:** <Site de*referência FQDN*>  

    - **Detalhes:** Se a cópia de segurança da base de dados for mais antiga do que o período de retenção de rastreio de alterações, ou quando recuperar o site sem uma cópia de segurança, especifique o site primário de referência que o CAS utiliza para recuperar dados globais.  

        Quando não especifica um site de referência, e a cópia de segurança é mais antiga do que o período de retenção de rastreio de alterações, todos os sites primários são reinicializados com os dados restaurados do CAS.  

        Quando não especifica um site de referência, e a cópia de segurança está dentro do período de retenção de rastreio de alterações, apenas alterações que são feitas após a cópia de segurança ser replicada a partir de locais primários. Quando há mudanças contraditórias de diferentes locais primários, o CAS usa o primeiro que recebe.  

- **Nome da chave:** SiteServerBackupLocation  

    - **Obrigatório:** não  

    - **Valores:** <Conjunto de backup do*servidor do site*>  

    - **Detalhes:** especifica o caminho para o conjunto de cópias de segurança do servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, a configuração reinstala o site sem o restaurar a partir de um conjunto de cópias de segurança.  

- **Nome da chave:** BackupLocation  

    - **Obrigatório:** Esta chave é necessária quando configura rumit um valor de **1** ou **4** para a chave **ServerRecoveryOptions,** e configura um valor de **10** para a chave **DatabaseRecoveryOptions.**  

    - **Valores:** <Conjunto de backup da base de*dados do site*>  

    - **Detalhes:** especifica o caminho para o conjunto de cópias de segurança da base de dados do site.  

#### <a name="options"></a>Opções

- **Nome da chave:** ProductID  

    - **Obrigatório:** sim  

    - **Valores:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= uma chave de produto válida com traços

        - `Eval`= instalar a versão de avaliação do Gestor de Configuração

    - **Detalhes:** Especifica a chave de produto de instalação do Gestor de Configuração, incluindo as traços.

- **Nome da chave:** SiteCode  

    - **Obrigatório:** sim  

    - **Valores:** <*Código do site*>  

    - **Detalhes:** Especifica três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia. Especifique o código do site que o site usou antes da falha.

- **Nome da chave:** SiteName  

    - **Obrigatório:** não  

    - **Valores:** <Nome do*site*>  

    - **Detalhes:** Especifica o nome deste site.  

- **Nome da chave:** SMSInstallDir  

    - **Obrigatório:** sim  

    - **Valores:** <Caminho de*instalação do Gestor de Configuração*>  

    - **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.  

- **Nome da chave:** SDKServer  

    - **Obrigatório:** sim  

    - **Valores:** <*SMS Provider FQDN*>  

    - **Detalhes:** Especifica o FQDN para o servidor que acolhe o Provedor SMS. Especifique o servidor que acolheu o Fornecedor SMS antes da falha.  

        Após a instalação inicial, pode configurar fornecedores de SMS adicionais para o site. Para obter mais informações sobre o Fornecedor de SMS, consulte plan para o Provedor de [SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nome da chave:** PrerequisiteComp  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Download  

        - `1`= Já descarregado  

    - **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar um valor de **0**, a configuração descarrega os ficheiros.  

- **Nome da chave:** PrerequisitePath  

    - **Obrigatório:** sim  

    - **Valores:** <*Caminho para configurar ficheiros pré-requisitos*>  

    - **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.  

- **Nome da chave:** AdminConsole  

    - **Obrigatório:** Esta chave é necessária exceto quando a definição **de ServerRecoveryOptions** tem um valor de **4**.  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'.  

- **Nome da chave:** JoinCEIP  

    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não se junte a  

        - `1`= Juntar-se  

    - **Detalhes:** Especifica se deve aderir ao CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome da chave:** SQLServerName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*servidor SQL*>  

    - **Detalhes:** Especifica o nome do servidor ou instância agrupada que está a executar o SQL Server e que acolhe a base de dados do site. Especifique o mesmo servidor que acolheu a base de dados do site antes da falha.  

- **Nome da chave:** DatabaseName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome da base de dados do*site*> ou nome do site *<nome*>\\<do*site*>  

    - **Detalhes:** Especifica o nome da base de dados do Servidor SQL para criar ou a base de dados do Servidor SQL para utilizar na instalação da base de dados CAS. Especifique o mesmo nome de base de dados que foi usado antes da falha.  

        > [!IMPORTANT]  
        > Se não utilizar a instância predefinida, especifique o nome da instância e o nome da base de dados do site.  

- **Nome da chave:** SQLSSBPort  

    - **Obrigatório:** sim  

    - **Valores:** <Número da*porta SSB*>  

    - **Detalhes:** Especifica a porta SSB que o SQL Server utiliza. Por predefinição, o SSB utiliza a porta TCP 4022. Especifique a mesma porta SSB que foi utilizada antes da falha.  

- **Nome-chave:** SQLDataFilepath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro .mdb*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .mdb.  

- **Nome-chave:** SQLLogFilePath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro ldf*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .ldf.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome-chave:** CloudConnector  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se instalar um ponto de ligação de serviço neste local. Como só pode instalar o ponto de ligação de serviço no local de topo de uma hierarquia, este valor deve ser **0** para um local primário infantil.  

- **Nome-chave:** CloudConnectorServer  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <Servidor de ponto de*ligação de serviço FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de ponto de ligação de serviço.  

- **Nome-chave:** UseProxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se o ponto de ligação de serviço utiliza um servidor proxy.  

- **Nome-chave:** Nome proxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <*Proxy server FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor proxy que o ponto de ligação de serviço utiliza.  

- **Nome-chave:** ProxyPort  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <*Número da porta*>  

    - **Detalhes:** Especifica o número da porta a utilizar para a porta proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperação não acompanhada para um local primário

Utilize os seguintes detalhes para recuperar um site primário utilizando um ficheiro de script de configuração não vigiado.  

#### <a name="identification"></a>Identificação

- **Nome da chave:** ação  

    - **Obrigatório:** sim  

    - **Valores:**`RecoverPrimarySite`  

    - **Detalhes:** Recupera um local primário.  

- **Nome-chave:** CDMais  

    - **Obrigatório:** Sim, só quando se usa os meios de comunicação do CD. Última pasta.

    - **Valores:**

        - `1`= está a usar os meios de comunicação de CD. Últimas

        - Qualquer valor que não seja 1 = não está a usar CD. Últimos meios de comunicação

    - **Detalhes:** Quando instala ou recupera um local primário ou CAS, e executa a configuração do CD. Última pasta, inclua esta chave e valor. Este valor informa a configuração de que está a usar meios de comunicação a partir de CD. O mais tardar.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nome da chave:** ServerRecoveryOptions  

    - **Obrigatório:** sim  

    - **Valores:**

        - `1`= Recuperar servidor do site e servidor SQL

        - `2`= Recuperar apenas o servidor do site

        - `4`= Recuperar apenas o Servidor SQL  

    - **Detalhes:** Especifica se a configuração recupera o servidor do site, o Servidor SQL ou ambos. São também necessárias as seguintes opções com base no valor especificado:  

        - **1** ou **2**: Para recuperar o site utilizando uma cópia de segurança do site, especifique um valor para **o SiteServerBackupLocation**. Se não especificar um valor, a configuração reinstala o site sem o restaurar a partir de um conjunto de cópias de segurança.  

        - **4**: A chave **BackupLocation** é necessária quando configurar um valor de **10** para a chave **DatabaseRecoveryOptions,** que é restaurar a base de dados do site a partir de cópia seletiva.  

- **Nome da chave:** DatabaseRecoveryOptions  

    - **Obrigatório:** Esta chave é necessária quando a definição **de ServerRecoveryOptions** tem um valor de **1** ou **4**.  

    - **Valores:**

        - `10`= Restaurar a base de dados do site a partir de cópias de segurança.  

        - `20`= Utilize uma base de dados do site que recuperou manualmente com outro método.  

        - `40`= Criar uma nova base de dados para o site. Utilize esta opção quando não houver cópia de segurança na base de dados do site disponível. O site recupera dados globais e do site através da replicação de outros sites.  

        - `80`= Saltar a recuperação da base de dados.  

    - **Detalhes:** Especifica como a configuração recupera a base de dados do site no Servidor SQL.  

- **Nome da chave:** SiteServerBackupLocation  

    - **Obrigatório:** não  

    - **Valores:** <Conjunto de backup do*servidor do site*>  

    - **Detalhes:** especifica o caminho para o conjunto de cópias de segurança do servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, a configuração reinstala o site sem o restaurar a partir de um conjunto de cópias de segurança.  

- **Nome da chave:** BackupLocation  

    - **Obrigatório:** Esta chave é necessária quando configurar um valor de **1** ou **4** para a chave **ServerRecoveryOptions** e configurar um valor de **10** para a chave **DatabaseRecoveryOptions.**  

    - **Valores:** <Conjunto de backup da base de*dados do site*>  

    - **Detalhes:** especifica o caminho para o conjunto de cópias de segurança da base de dados do site.  

#### <a name="options"></a>Opções

- **Nome da chave:** ProductID  

    - **Obrigatório:** sim  

    - **Valores:**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`= uma chave de produto válida com traços

        - `Eval`= instalar a versão de avaliação do Gestor de Configuração

    - **Detalhes:** Especifica a chave de produto de instalação do Gestor de Configuração, incluindo as traços.

- **Nome da chave:** SiteCode  

    - **Obrigatório:** sim  

    - **Valores:** <*Código do site*>  

    - **Detalhes:** Especifica três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia. Especifique o código do site que o site usou antes da falha.

- **Nome da chave:** SiteName  

    - **Obrigatório:** não  

    - **Valores:** <Nome do*site*>  

    - **Detalhes:** Especifica o nome deste site.  

- **Nome da chave:** SMSInstallDir  

    - **Obrigatório:** sim  

    - **Valores:** <Caminho de*instalação do Gestor de Configuração*>  

    - **Detalhes:** Especifica a pasta de instalação para os ficheiros do programa 'Gestor de Configuração'.  

- **Nome da chave:** SDKServer  

    - **Obrigatório:** sim  

    - **Valores:** <*SMS Provider FQDN*>  

    - **Detalhes:** Especifica o FQDN para o servidor que acolhe o Provedor SMS. Especifique o servidor que acolheu o Fornecedor SMS antes da falha. Após a instalação inicial, pode configurar fornecedores de SMS adicionais para o site. Para obter mais informações sobre o Fornecedor de SMS, consulte plan para o Provedor de [SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nome da chave:** PrerequisiteComp  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Download  

        - `1`= Já descarregado  

    - **Detalhes:** Especifica se os ficheiros pré-requisitos de configuração já foram descarregados. Por exemplo, se utilizar um valor de **0**, a configuração descarrega os ficheiros.  

- **Nome da chave:** PrerequisitePath  

    - **Obrigatório:** sim  

    - **Valores:** <*Caminho para configurar ficheiros pré-requisitos*>  

    - **Detalhes:** Especifica o caminho para os ficheiros pré-requisitos de configuração. Dependendo do valor **pré-requisiteComp,** a configuração utiliza este caminho para armazenar ficheiros descarregados ou para localizar ficheiros previamente descarregados.  

- **Nome da chave:** AdminConsole  

    - **Obrigatório:** Esta chave é necessária exceto quando a definição **de ServerRecoveryOptions** tem um valor de **4**.  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se deve instalar a consola 'Gestor de Configuração'.  

- **Nome da chave:** JoinCEIP  

    > [!Note]  
    > A partir da versão 1802 do Gestor de Configuração, a função CEIP é removida do produto.

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não se junte a  

        - `1`= Juntar-se  

    - **Detalhes:** Especifica se deve aderir ao CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nome da chave:** SQLServerName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome do*servidor SQL*>  

    - **Detalhes:** Especifica o nome do servidor ou instância agrupada que executa o SQL Server para alojar a base de dados do site. Especifique o mesmo servidor que acolheu a base de dados do site antes da falha.  

- **Nome da chave:** DatabaseName  

    - **Obrigatório:** sim  

    - **Valores:** <Nome da base de dados do*site*> ou nome do site *<nome*>\\<do*site*>

    - **Detalhes:** Especifica o nome da base de dados do Servidor SQL para criar ou a base de dados do Servidor SQL para utilizar na instalação da base de dados CAS. Especifique o mesmo nome de base de dados que foi usado antes da falha.  

        > [!IMPORTANT]  
        > Se não utilizar a instância predefinida, especifique o nome da instância e o nome da base de dados do site.  

- **Nome da chave:** SQLSSBPort  

    - **Obrigatório:** sim  

    - **Valores:** <Número da*porta SSB*>  

    - **Detalhes:** Especifica a porta SSB que o SQL Server utiliza. Por predefinição, o SSB utiliza a porta TCP 4022. Especifique a mesma porta SSB que foi utilizada antes da falha.  

- **Nome-chave:** SQLDataFilepath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro .mdb*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .mdb.  

- **Nome-chave:** SQLLogFilePath  

    - **Obrigatório:** não  

    - **Valores:** <*Caminho para base de dados .ficheiro ldf*>  

    - **Detalhes:** Especifica uma localização alternativa para criar o ficheiro base de dados .ldf.  

#### <a name="hierarchyexpansionoptions"></a>HierarquiaExpansionOptions

- **Nome da chave** CCARSiteServer  

    - **Obrigatório:** Veja os detalhes.  

    - **Valores:** <*Código do site para CAS*>  

    - **Detalhes:** Especifica o CAS ao qual um site primário se liga quando se junta à hierarquia do Gestor de Configuração. Esta definição é necessária se o local principal foi ligado a um CAS antes da falha. Especifique o código do site que foi usado para o CAS antes da falha.  

- **Nome da chave:** CASRetryInterval  

    - **Obrigatório:** não  

    - **Valores:** <*Intervalo em minutos*>  

    - **Detalhes:** Especifica o intervalo de repetição em minutos para tentar uma ligação ao CAS após a falha da ligação. Por exemplo, se a ligação ao CAS falhar, o site principal aguarda o número de minutos que especifica para o valor **CASRetryInterval** e, em seguida, tenta a ligação novamente.  

- **Nome da chave:** WaitForCASTimeout  

    - **Obrigatório:** não  

    - **Valores:** <*Tempo de tempo em minutos*>  

    - **Detalhes:** Especifica o valor máximo do tempo limite em minutos para um local primário ligar ao CAS. Por exemplo, se um local primário não ligar a um CAS, o local primário retenta a ligação ao CAS com base no valor **CASRetryInterval** até que o período **WaitForCASTimeout** seja atingido. Pode especificar um `0` valor `100`de .  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nome-chave:** CloudConnector  

    - **Obrigatório:** sim  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se instalar um ponto de ligação de serviço neste local. Como só pode instalar o ponto de ligação de serviço no local `0` de topo de uma hierarquia, este valor deve ser para um local primário infantil.  

- **Nome-chave:** CloudConnectorServer  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <Servidor de ponto de*ligação de serviço FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor que irá acolher a função do sistema de ponto de ligação de serviço.  

- **Nome-chave:** UseProxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:**

        - `0`= Não instale  

        - `1`= Instalar  

    - **Detalhes:** Especifica se o ponto de ligação de serviço utiliza um servidor proxy.  

- **Nome-chave:** Nome proxy  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <*Proxy server FQDN*>  

    - **Detalhes:** Especifica o FQDN do servidor proxy que o ponto de ligação de serviço utiliza.  

- **Nome-chave:** ProxyPort  

    - **Obrigatório:** Necessário quando **o CloudConnector** é igual a 1  

    - **Valores:** <*Número da porta*>  

    - **Detalhes:** Especifica o número da porta a utilizar para a porta proxy.  
