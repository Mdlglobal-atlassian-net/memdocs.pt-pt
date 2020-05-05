---
title: Pré-requisitos para sites
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos para a instalação dos diferentes tipos de sites do Gestor de Configuração.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8362dbf5cf7264c19f683ce5a224f1e0ec348b36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718148"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Pré-requisitos para instalar sites do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Antes de iniciar uma instalação do site, saiba sobre os pré-requisitos para a instalação dos diferentes tipos de sites do Gestor de Configuração.


## <a name="primary-sites-and-the-central-administration-site"></a>Locais primários e o site da administração central

Aplicam-se os seguintes pré-requisitos à instalação de um dos seguintes tipos:

- Um site de administração central como o primeiro local de uma hierarquia
- Um local primário autónomo
- Um local primário infantil

Se estiver a instalar um site de administração central como parte de uma expansão da hierarquia, consulte [expandir um local primário autónomo.](#bkmk_expand)

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a>Pré-requisitos para a instalação de um local primário ou de um site de administração central  

- As funções, funcionalidades e componentes do Windows Server necessários devem ser instalados. Para mais informações, consulte os [pré-requisitos](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq) do sistema do Site  

- A conta de utilizador que instala o site deve ter os seguintes direitos:  

    - **Administrador** nos seguintes servidores:  
        - O servidor do site  
        - Cada servidor que acolhe a **base de dados** do site  
        - Cada instância do **Fornecedor sms** para o site  

    - **Sysadmin** na instância do SQL Server que acolhe a base de dados do site  

        > [!IMPORTANT]  
        > Quando a configuração do Gestor de Configuração terminar, a conta de computador do servidor do site deve reter direitos de sysadmin para o Servidor SQL. Não remova os direitos de sinadmina SQL desta conta.  

- Se estiver a instalar um site primário, precisa dos seguintes direitos adicionais:  

    - **Administrador** em servidores adicionais onde instala o ponto de gestão inicial e ponto de distribuição, se não no servidor do site  

- Se estiver a instalar um novo site primário infantil abaixo de um site de administração central, precisa dos seguintes direitos adicionais:  

    - **Administrador** no servidor que acolhe o site da administração central  

    - Direitos de administração baseados em funções dentro do Gestor de Configuração que são equivalentes ao papel de segurança do Administrador de **Infraestruturas** ou **administrador completo**  

- Utilize os ficheiros de origem de instalação corretos e execute a configuração a partir desse local. Para obter informações sobre os ficheiros de origem corretos para instalar diferentes tipos de sites, consulte [Opções para instalar diferentes tipos de sites](prepare-to-install-sites.md#bkmk_options).  

- O servidor do site deve ter acesso a ficheiros de configuração atualizados da Microsoft, de uma das seguintes formas:  

    - Antes de iniciar a instalação, faça o download e guarde uma cópia destes ficheiros na sua rede local. Para mais informações, consulte O Downloader de [Configuração](setup-downloader.md).  

    - Se uma cópia local deste ficheiro não estiver disponível, o servidor do site deve ter acesso à Internet. Descarrega estes ficheiros da Microsoft durante a instalação.  

- O servidor do servidor do site e o servidor de base de dados do site devem satisfazer todas as configurações pré-requisitos. Antes de iniciar a configuração do Gestor de Configuração, [execute manualmente o Verificador Pré-Requisito](prerequisite-checker.md) para identificar e corrigir problemas.  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a>Pré-requisitos para expandir um local primário autónomo

Um local primário autónomo deve cumprir os seguintes pré-requisitos antes de poder expandi-lo para uma hierarquia com um site de administração central:

#### <a name="source-file-version-matches-site-version"></a>Versão de ficheiro de origem corresponde à versão do site

Instale o novo site da administração central utilizando meios de comunicação de um CD. Última pasta que corresponde à versão do site primário autónomo. Para se certificar de que as versões correspondem, utilize os ficheiros de origem encontrados no [CD. Última pasta](../../manage/the-cd.latest-folder.md) no site primário autónomo.

Para obter mais informações sobre os ficheiros de origem corretos para instalar diferentes sites, consulte [Opções para instalar diferentes tipos de sites](prepare-to-install-sites.md#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Parar a migração ativa de outra hierarquia

Não é possível configurar o site primário autónomo para migrar dados de outra hierarquia do Gestor de Configuração. Pare a migração ativa para o local primário autónomo de outras hierarquias do Gestor de Configuração e remova todas as configurações para migração. Estas configurações incluem:

- Empregos migratórios que ainda não tenham concluído  
- Recolha de dados  
- A configuração da hierarquia de origem ativa  

Esta configuração é necessária porque o Gestor de Configuração migra dados do site de alto nível da hierarquia. Quando se expande um local primário autónomo, as configurações para a migração não se transferem para o site da administração central.  

Depois de expandir o local primário autónomo, se reconfigurar a migração no local principal, o site da administração central realiza as operações de migração.

Para obter mais informações sobre como configurar a migração, consulte [as hierarquias de origem configure e os locais de origem para a migração.](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

#### <a name="computer-account-as-administrator"></a>Conta de computador como Administrador

A conta de computador do servidor que acolhe o novo site da administração central deve ser um membro do grupo **Administrador** no servidor de site primário autónomo.

Para expandir com sucesso o site primário autónomo, a conta de computador do novo site da administração central deve ter direitos de **administrador** no site primário autónomo. Isto só é necessário durante a expansão do local. Quando a expansão do site terminar, pode remover a conta do grupo de utilizadores no site principal.  

#### <a name="installation-account-permissions"></a>Permissões de conta de instalação

A conta de utilizador que executa a configuração do Gestor de Configuração para instalar o novo site da administração central deve ter direitos de administração baseados em papéis no site primário autónomo.

Para instalar um site de administração central como parte de uma expansão do site, a conta de utilizador que executa a configuração para instalar o site da administração central deve ser definida na administração baseada em papéis no local primário autónomo como administrador **completo** ou administrador de **infraestruturas.**

Para mais informações, incluindo a lista completa das permissões necessárias, consulte a conta de [instalação do Site](../../../plan-design/hierarchy/accounts.md#site-installation-account).

#### <a name="top-level-site-roles"></a>Funções de site de alto nível

Antes de expandir o site, desinstale as seguintes funções do sistema do site a partir do local primário autónomo:

- Ponto de sincronização da Inteligência de Ativos  
- Ponto de Endpoint Protection  
- Ponto de ligação de serviço  

O Gestor de Configuração apenas suporta estas funções no local de alto nível da hierarquia. Desinstale estas funções do sistema do site antes de expandir o local primário autónomo. Depois de expandir o site, reinstale estas funções do sistema do site no site da administração central.  

Todas as outras funções do sistema do site podem permanecer instaladas no local principal.  

#### <a name="open-the-sql-server-service-broker-port"></a>Abra a porta de corretagem de serviço sql server

A porta de rede deve estar aberta para o SQL Server Service Broker (SSB) entre o site primário autónomo e o servidor para o site da administração central.  

Para replicar com sucesso os dados entre um site de administração central e um site primário, o Gestor de Configuração requer uma porta aberta entre os dois sites para a Utilização do SSB. Quando instala um site de administração central e expande um local primário autónomo, a verificação prévia não verifica se a porta que especifica para o SSB está aberta no local principal.  

#### <a name="known-issues-with-azure-services"></a>Questões conhecidas com os serviços do Azure

Depois de expandir o site, precisa de reconfigurar os seguintes serviços Azure com O Gestor de Configuração:

- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  
- [Loja Microsoft para Empresas](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [Gateway de gestão da cloud](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

Na versão 1806 e mais tarde, renovar a chave secreta do inquilino do Azure Ative Directory. Para mais informações, consulte [Renovar a chave secreta.](../configure/azure-services-wizard.md#bkmk_renew)

Em alternativa, remova e recrie a ligação a esse serviço:

1. Na consola 'Gestor de Configuração', elimine o serviço Azure do nó dos **Serviços Azure.**  

2. No portal Azure, apague o inquilino que está associado ao serviço do nó de inquilinos do Azure Ative Directory. Esta ação também elimina a aplicação web Azure AD que está associada ao serviço.  

3. Reconfigure a ligação ao serviço Azure para utilização com o Gestor de Configuração.  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a>Sítios secundários

Seguem-se os pré-requisitos para a instalação de locais secundários:  

- As funções, funcionalidades e componentes do Windows Server necessários devem ser instalados. Para mais informações, consulte os [pré-requisitos](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq) do sistema do Site  

- O administrador que configura a instalação do site secundário na consola do Gestor de Configuração deve ter direitos de administração baseados em papéis equivalentes ao papel de administrador de **infraestrutura** ou **administrador completo.**  

- A conta do computador do local primário dos pais deve ser um **Administrador** no servidor do site secundário.  

- Quando o site secundário utiliza uma instância previamente instalada do SQL Server para alojar a base de dados do site secundário:  

    - A conta de computador do site primário dos pais deve ter direitos de **sisadmina** na instância do SQL Server no servidor de site secundário.  

    - A conta do **Sistema Local** do computador de servidor de site secundário deve ter direitos de **sisadmina** na instância do Servidor SQL no servidor de site secundário.  

        > [!IMPORTANT]  
        > Quando a configuração do Gestor de Configuração terminar, ambas as contas devem manter os direitos de sisadmina para o Servidor SQL. Não retire os direitos de sinadmina destas contas.  

- O servidor de site secundário deve satisfazer todas as configurações pré-requisitos. Estas configurações incluem o SQL Server e as funções padrão do sistema do site do ponto de gestão e ponto de distribuição.  


## <a name="next-steps"></a>Passos seguintes

Depois de confirmar os pré-requisitos, está pronto para executar a configuração. Para mais informações, consulte [Utilize o Assistente de Configuração para instalar os sites do Gestor](use-the-setup-wizard-to-install-sites.md)de Configuração .
