---
title: Atualizar infraestrutura no local
titleSuffix: Configuration Manager
description: Saiba como atualizar a infraestrutura, como o SQL Server e o OS dos sistemas de sites.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 033c5de1a85ce2fa8b11fe7a187fcc4d5c023931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720731"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Upgrade de infraestrutura no local que suporta o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize as informações deste artigo para ajudá-lo a atualizar a infraestrutura do servidor que executa o Gestor de Configuração.  

- Se quiser *fazer upgrade* de uma versão anterior para 'Gestor de Configuração', ramo atual, consulte Upgrade para 'Gestor de [Configuração'.](../deploy/install/upgrade-to-configuration-manager.md)  

- Se pretender *atualizar* o seu Gestor de Configuração, ramo atual, infraestrutura para uma nova versão, consulte [Atualizações para Gestor de Configuração](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a>Atualizar o Sistema operativo dos sistemas do site  

O Gestor de Configuração suporta a atualização no local do SISTEMA do servidor que acolhe um servidor de site e qualquer função do sistema do site, nas seguintes situações:  

- Se o Gestor de Configuração ainda suportar o nível de pacote de serviço resultante do Windows, este suporta a atualização no local para um pacote de serviços posterior do Windows Server.  

- Upgrade no local a partir de:  

    - Windows Server 2016 para Windows Server 2019  

    - Windows Server 2012 R2 para Windows Server 2019  

    - Windows Server 2012 R2 para Windows Server 2016  

    - Windows Server 2012 para Windows Server 2016  

    - Windows Server 2012 para Windows Server 2012 R2  

    - Windows Server 2008 R2 para Windows Server 2012 R2  

Para atualizar um servidor, utilize os procedimentos de atualização fornecidos pelo SISTEMA para o qual está a atualizar. Consulte os seguintes artigos:  

- [Centro de atualização do servidor do Windows](https://aka.ms/upgradecenter)  

- [Opções de upgrade e conversão para Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Opções de upgrade para Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a>Upgrade para Windows Server 2016 ou 2019

Utilize os passos nesta secção para qualquer um dos seguintes cenários de atualização:  

- Atualize o Windows Server 2012 R2 ou o Windows Server 2016 para o Windows Server 2019  

- Atualize o Windows Server 2012 ou o Windows Server 2012 R2 para o Windows Server 2016  

#### <a name="before-upgrade"></a>Antes da atualização

- (Windows Server 2012 ou Windows Server 2012 R2): Remova o cliente de Proteção de Pontofinal do Centro de Sistema (SCEP). O Windows Server tem agora o Windows Defender incorporado, que substitui o cliente SCEP. A presença do cliente SCEP pode impedir uma atualização para o Windows Server.  

- Retire a função WSUS do servidor se estiver instalada. Pode manter o SUSDB e recolocá-lo quando a WSUS for reinstalada.  

- Se estiver a atualizar o SISTEMA do servidor do site, certifique-se de que a [replicação baseada em ficheiros](../../plan-design/hierarchy/file-based-replication.md) é saudável para o site. Verifique todas as caixas de entrada para obter um atraso nos sites de envio e receção. Se houver muitos trabalhos de replicação presos ou pendentes, espere até que se limpem.<!-- SCCMDocs#1792 -->
    - No site de envio, reveja **o remetente.log**.
    - No site recetor, reveja o **registo de despooler**.

#### <a name="after-upgrade"></a>Após a atualização

- Certifique-se de que o Windows Defender está ativado, preparado para iniciar automaticamente e funcionar.  

- Certifique-se de que os seguintes serviços do Gestor de Configuração estão a funcionar:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Certifique-se de que os serviços de **Ativação** do Processo do Windows e **os serviços WWW/W3svc** estão ativados e definidos para o arranque automático. O processo de upgrade desativa estes serviços, por isso certifique-se de que estão a concorrer para as seguintes funções do sistema do site:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de Web site do Catálogo de Aplicações  

- Certifique-se de que cada servidor que acolhe uma função do sistema do site continua a satisfazer todos os [pré-requisitos](../../plan-design/configs/site-and-site-system-prerequisites.md). Por exemplo, poderá necessitar de reinstalar BITS, WSUS ou configurar configurações específicas para iIS.  

- Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que os serviços estão iniciados e operacionais.  

- Se estiver a atualizar o servidor principal do site, [então faça um reset](modify-your-infrastructure.md#bkmk_reset)do site .  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conhecido para consolas de Gestor de Configuração remota

Depois de atualizar o servidor do site, ou uma instância do Fornecedor SMS, não pode ligar-se à consola 'Gestor de Configuração'. Para resolver este problema, restaure manualmente as permissões para o grupo **SMS Admins** no WMI. As permissões devem ser definidas no servidor do site e em cada servidor remoto que acolhe uma instância do Provedor de SMS:

1. Nos servidores aplicáveis, abra a Consola de Gestão da Microsoft (MMC) e adicione o snap-in para **o Controlo WMI**, e, em seguida, selecione o **computador Local**.  

2. No MMC, abra as **propriedades** do **Controlo WMI (Local)** e selecione o separador **Segurança.**  

3. Expanda a árvore abaixo da Raiz, selecione o nó **SMS** e, em seguida, escolha **Segurança**.  Certifique-se de que o grupo **SMS Admins** tem as seguintes permissões:  

    - Ativar conta  

    - Viabilidade remota  

4. No **separador Segurança** abaixo do nó **SMS,** selecione o **código de site_&lt;**> nó e, em seguida, escolha **Segurança**. Certifique-se de que o grupo **SMS Admins** tem as seguintes permissões:  

    - Métodos de Execução  

    - Escrita do Provedor  

    - Ativar conta  

    - Viabilidade remota  

5. Guarde as permissões para restaurar o acesso à consola 'Gestor de Configuração'.  

#### <a name="known-issue-for-remote-site-systems"></a>Problema conhecido para sistemas de sites remotos

Depois de atualizar um servidor que acolhe `Software\Microsoft\SMS` uma função do sistema do site, o valor pode estar em falta na seguinte chave de registo:`HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Se este valor estiver em falta depois de atualizar o Windows no servidor, adicione-o manualmente. Caso contrário, as funções do sistema do site podem ter problemas no upload de ficheiros para as caixas de entrada do servidor do site.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a>Upgrade para Windows Server 2012 R2

Quando atualiza si do Windows Server 2008 R2 ou do Windows Server 2012 para o Windows Server 2012 R2, aplicam-se as seguintes condições:

#### <a name="before-upgrade"></a>Antes da atualização

- No Windows Server 2012: Remova a função WSUS do servidor se estiver instalada. Pode manter o SUSDB e recolocá-lo quando a WSUS for reinstalada.  

- No Windows Server 2008 R2: Antes de fazer o upgrade para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 a partir do servidor. Pode manter o SUSDB e recolocá-lo quando a WSUS for reinstalada. Para mais informações, consulte a visão geral dos Serviços de [Atualização do Servidor do Windows](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Se estiver a atualizar o SISTEMA do servidor do site, certifique-se de que a [replicação baseada em ficheiros](../../plan-design/hierarchy/file-based-replication.md) é saudável para o site. Verifique todas as caixas de entrada para obter um atraso nos sites de envio e receção. Se houver muitos trabalhos de replicação presos ou pendentes, espere até que se limpem.<!-- SCCMDocs#1792 -->
    - No site de envio, reveja **o remetente.log**.
    - No site recetor, reveja o **registo de despooler**.

#### <a name="after-upgrade"></a>Após a atualização

- O processo de atualização desativa os Serviços de Implementação do Windows. Certifique-se de que este serviço está iniciado e a funcionar para as seguintes funções do sistema do site:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de Web site do Catálogo de Aplicações  

- Certifique-se de que os serviços de **Ativação** do Processo do Windows e **os serviços WWW/W3svc** estão ativados e definidos para o arranque automático. O processo de upgrade desativa estes serviços, por isso certifique-se de que estão a concorrer para as seguintes funções do sistema do site:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de Web site do Catálogo de Aplicações  

- Certifique-se de que cada servidor que acolhe uma função do sistema do site continua a satisfazer todos os [pré-requisitos](../../plan-design/configs/site-and-site-system-prerequisites.md). Por exemplo, poderá necessitar de reinstalar BITS, WSUS ou configurar configurações específicas para iIS.  

    Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que os serviços estão iniciados e operacionais.  

### <a name="unsupported-upgrade-scenarios"></a>Cenários de upgrade não suportados

Os seguintes cenários de atualização do Windows Server são geralmente questionados sobre, mas não suportados pelo Gestor de Configuração:  

- Windows Server 2008 para Windows Server 2012 ou mais tarde  

- Windows Server 2008 R2 para Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a>Atualizar o Sistema de So dos clientes  

O Gestor de Configuração suporta uma atualização do OS para clientes do Gestor de Configuração nas seguintes situações:  

- Se o Gestor de Configuração suportar o nível de pacote de serviço resultante, ele suporta a atualização no local para um pacote de serviços Windows posterior.  

- Atualização em vigor do Windows de uma versão suportada para o Windows 10. Para mais informações, consulte [o Upgrade Windows para a versão mais recente.](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  

- Atualizações de manutenção do Windows 10. Para mais informações, consulte [Gerir o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a>Upgrade SQL Server  

O Gestor de Configuração suporta uma atualização do SQL Server no servidor de base de dados do site.

Para obter informações sobre as versões do SQL Server que o Gestor de Configuração suporta, consulte [suporte para versões SQL Server](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Atualizar a versão do service pack do SQL Server

Se o Gestor de Configuração ainda suportar o nível de pacote de serviço SQL Server resultante, suporta a atualização no local do SQL Server para um pacote de serviço posterior.

Quando você tem mais de um site de Configuração Manager em uma hierarquia, cada site pode executar uma versão de pacote de serviço diferente do SQL Server. Não há nenhuma limitação à ordem em que os sites atualizam a versão do pacote de serviços do SQL Server.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Upgrade para uma nova versão do SQL Server

O Gestor de Configuração suporta a atualização no local do SQL Server para as seguintes versões:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Isto inclui a atualização do SQL Server Express para uma versão mais recente do SQL Server Express em sites secundários.

Ao atualizar a versão do SQL Server que acolhe a base de dados do site, tem de atualizar a versão SQL Server que é utilizada nos sites na seguinte ordem:

1. Upgrade SQL Server no site da administração central primeiro  

2. Atualize os sites secundários antes de atualizar o site primário do site secundário  

3. Por último, atualize os sites primários principais. Estes sites incluem ambos os locais primários infantis que reportam a um site de administração central, e locais primários autónomos que são o local de alto nível de uma hierarquia.  

### <a name="sql-server-cardinality-estimation-level"></a>Nível de estimativa de cardinalidade do Servidor SQL

Ao atualizar uma base de dados do site a partir de uma versão anterior do SQL Server, a base de dados mantém o nível de estimativa de cardinalidade SQL existente, se for no mínimo permitido para esse exemplo de SQL Server. Atualizar o SQL Server com uma base de dados a um nível de compatibilidade inferior ao nível permitido define automaticamente a base de dados para o nível de compatibilidade mais baixo permitido pelo SQL Server.

O quadro seguinte identifica os níveis de compatibilidade recomendados para as bases de dados do site do Gestor de Configuração:

|Versão do SQL Server | Níveis de compatibilidade suportados | Nível recomendado |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar o nível de compatibilidade de estimativa de cardinalidade do Servidor SQL em uso para a sua base de dados do site, ecorra a seguinte consulta SQL no servidor de base de dados do site:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Para obter mais informações sobre os níveis de compatibilidade ce sQL e como defini-los, consulte [alter DATABASE Compatibilidade Level (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Para mais informações sobre a atualização do Servidor SQL, consulte os seguintes artigos do SQL Server:  

- [Upgrade para SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Upgrade para SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Atualizar para o SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor da base de dados do site  

1. Pare todos os serviços do Gestor de Configuração no site  

2. Atualize o SQL Server para uma versão suportada  

3. Reiniciar os serviços do Gestor de Configuração  

> [!NOTE]  
> Quando muda a edição do SQL Server em uso no site da administração central de Standard para um Datacenter ou Enterprise, a divisória de base de dados não muda. Esta partilha de bases de dados limita o número de clientes que a hierarquia suporta.  
