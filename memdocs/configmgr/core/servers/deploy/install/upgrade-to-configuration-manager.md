---
title: Upgrade para o ramo atual
titleSuffix: Configuration Manager
description: Aprenda os passos para executar uma atualização bem sucedida no local a partir de um site e hierarquia que executa o System Center 2012 Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717966"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Upgrade para o ramo atual do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Faça um upgrade no local para o gerente de configuração a partir de um site e hierarquia que executa o System Center 2012 Configuration Manager. Antes de atualizar a partir do System Center 2012 Configuração Manager, você deve preparar os sites. Esta preparação requer que remova configurações específicas que possam impedir uma atualização bem sucedida. Em seguida, siga a sequência de atualização quando estiver envolvido mais de um único site.  

> [!TIP]  
> Ao gerir o site do Gestor de Configuração e a infraestrutura da hierarquia, os termos *de atualização,* *atualização*e *instalação* são usados para descrever três conceitos distintos. Para saber como cada termo é usado, consulte [sobre atualização, atualização e instalação.](../../../understand/upgrade-update-install.md)

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a>Caminhos de upgrade no local  

As seguintes opções são os caminhos de atualização atualmente suportados no local:

### <a name="upgrade-to-version-2002"></a>Upgrade para a versão 2002

Pode atualizar os seguintes produtos para uma versão *totalmente licenciada* do Gestor de Configuração, versão atual da sucursal 2002:

- Uma instalação de *avaliação* do Gestor de Configuração, versão atual do ramo 2002
- System Center 2012 Gestor de Configuração com Pacote de Serviço 1
- System Center 2012 Gestor de Configuração com Pacote de Serviço 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager com Pacote de Serviço 1

Para mais informações, consulte [frequentemente perguntas para as sucursais do Gestor de Configuração e licenciamento.](../../../understand/product-and-licensing-faq.md)

> [!TIP]  
> Ao atualizar a partir de uma versão do System Center 2012 Configuration Manager para o ramo atual, poderá ser capaz de agilizar o seu processo de upgrade. Para obter mais informações, consulte o seguinte:  
>
> - [Versões de base e atualização](../../manage/updates.md#bkmk_Baselines)  
> - [A pasta CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Caminhos não apoiados

Os seguintes caminhos não são apoiados:

- Não é suportado para atualizar um ramo de pré-visualização técnica para uma instalação totalmente licenciada. Uma versão de pré-visualização técnica só pode atualizar para uma versão posterior da pré-visualização técnica.  

- A migração de uma pré-visualização técnica para uma versão totalmente licenciada não é suportada.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a> Listas de verificação de atualização  

As seguintes listas de verificação podem ajudá-lo a planear um upgrade bem sucedido para O Gestor de Configuração.  

### <a name="before-you-upgrade"></a>Antes da atualização  

Reveja estes passos antes de fazer o upgrade para O Gestor de Configuração.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Reveja o ambiente do Gestor de Configuração do Centro de Sistemas 2012

Resolver problemas conforme detalhado no seguinte artigo do Microsoft Support: [Os clientes do Gestor de Configuração reinstalam a cada cinco horas devido a uma tarefa recorrente de retry e podem causar uma atualização inadvertida do cliente](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Certifique-se de que o seu ambiente cumpre as configurações suportadas

- Reveja a versão OS do servidor em uso para hospedar funções do sistema do site:  

  - Alguns sistemas operativos mais antigos suportados pelo System Center 2012 Configuration Manager não são suportados pelo atual ramo do Gestor de Configuração. Antes da atualização, remova as funções do sistema do site nessas versões DES. Para obter mais informações, consulte [sistemas operativos suportados para servidores](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do site .

  - O verificador pré-requisito para O Gestor de Configuração não verifica os pré-requisitos para as funções do sistema do site no servidor do site ou em sistemas de site remotos  

- A revisão exigia pré-requisitos para cada computador que acolhe uma função do sistema do site. Por exemplo, para implementar um SISTEMA, o Gestor de Configuração utiliza o Kit de Avaliação e Implementação do Windows 10 (Windows ADK). Antes de executar o Programa de Configuração, tem de transferir e instalar o Windows 10 ADK no servidor do site e em cada computador que execute uma instância do Fornecedor de SMS.  

Para obter mais informações sobre plataformas suportadas e configurações pré-requisitos, consulte [configurações suportadas](../../../plan-design/configs/supported-configurations.md).  

Para obter mais informações sobre a utilização do Windows ADK com O Gestor de Configuração, consulte [os requisitos de infraestrutura para a implementação do OS](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Reveja o estado do site e da hierarquia e verifique se não existem questões por resolver

Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, do servidor da base de dados do site e de funções de sistema de sites que se encontrem instaladas em computadores remotos. Uma atualização do site pode falhar devido a problemas operacionais existentes.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que acolhem o site, o servidor de base de dados do site e as funções do sistema de site remoto

Antes de atualizar um site, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do service pack.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Desinstale as funções do sistema do site não suportadas pelo Gestor de Configuração

As seguintes funções do sistema do site já não são utilizadas no 'Gestor de Configuração'. Desinstale-os antes de atualizar a partir do System Center 2012 Configuration Manager:  

- Ponto de Gestão Fora de Banda  

- Ponto de Validação do Estado de Funcionamento do Sistema  

- Ponto de site de catálogo de aplicações e ponto de serviço web

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Desativar réplicas de bases de dados para pontos de gestão em locais primários

O Gestor de Configuração não pode atualizar um site primário que tenha uma réplica de base de dados para pontos de gestão. Desative a replicação de base de dados antes de:  

- Criar uma cópia de segurança da base de dados do site para testar a atualização da base de dados  

- Atualize o site de produção para o ramo atual do Gestor de Configuração  

Para obter mais informações, veja os artigos seguintes:  

- System Center 2012 Diretor de Configuração: [Configure réplicas](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config) de bases de dados para pontos de gestão  

- Gestor de Configuração, ramo atual: [Réplicas de base de dados para pontos](../configure/database-replicas-for-management-points.md) de gestão  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Reconfigurar os pontos de atualização de software que usam o NLB

O Gestor de Configuração não pode atualizar um site que utilize um cluster de equilíbrio de carga de rede (NLB) para hospedar pontos de atualização de software.  

Se utilizar clusters de NLB em pontos de atualização de software, utilize o PowerShell para remover o cluster de NLB. (Começando com system center 2012 Configuration Manager SP1, não havia opção na consola do Gestor de Configuração para configurar um cluster NLB.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Desative todas as tarefas de manutenção do site em cada local durante a duração da atualização desse site

Antes de fazer o upgrade para o Gestor de Configuração, desative quaisquer tarefas de manutenção do site que possam ser executadas durante o tempo em que o processo de atualização estiver ativo. Esta lista inclui, mas não se limita às seguintes tarefas:  

- Servidor do Site de Reserva  
- Eliminar Operações de Cliente Desatualizadas  
- Eliminar Dados de Deteção Desatualizados  

Se uma tarefa de manutenção da base de dados do site for executado durante o processo de atualização, a atualização do site pode falhar.  

Antes de desativar uma tarefa, registe a agenda da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.

Para obter mais informações sobre as tarefas de manutenção do site, consulte os seguintes artigos:  

- System Center 2012 Diretor de Configuração: [Planeamento para operações no local](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Gestor de Configuração, ramo atual: [Referência para tarefas de manutenção](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Executar verificador pré-requisito de configuração

Antes de atualizar um site, execute o **Verificador Pré-Requisito** independentemente da configuração para validar que o seu site cumpre os pré-requisitos. Mais tarde, quando atualiza o site, o verificador pré-requisito corre novamente.  

A verificação prévia independente avalia o site para atualização tanto para o ramo atual como para o ramo de manutenção a longo prazo (LTSB) do Gestor de Configuração. Como algumas funcionalidades não são suportadas pelo LTSB, pode ver entradas no **log ConfigMgrPrereq** que são como os seguintes exemplos:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Se planeia fazer upgrade para o ramo atual, os erros para a edição LTSB podem ser ignorados com segurança. Só se aplicam se planeia fazer upgrade para o LTSB.

Mais tarde, quando executar a configuração do Gestor de Configuração para fazer a atualização, a verificação pré-requisito volta a ser executada. Avalia o seu site com base no ramo do Gestor de Configuração que escolhe instalar (ramo atual, ou LTSB). Se optar por fazer upgrade para o ramo atual, não verifica as funcionalidades que não são suportadas pelo LTSB.

Para mais informações, consulte o [verificador pré-requisito](prerequisite-checker.md) e [a lista de verificações pré-requisitos](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Descarregue ficheiros pré-requisitos e ficheiros redistribuíveis para O Gestor de Configuração

Utilize o Downloader de **Configuração** para descarregar ficheiros redistribuíveis pré-requisitos, pacotes de idiomas e as mais recentes atualizações de produto para O Gestor de Configuração.  

Para obter informações, consulte O Downloadr de [Configuração](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Plano para gerir idiomas de servidore cliente

Quando atualiza um site, a atualização do site instala apenas as versões do pacote de idiomas que selecionar durante a atualização.  

- A configuração analisa a configuração atual do seu site. Em seguida, identifica os pacotes de idiomas que estão disponíveis na pasta onde armazena ficheiros pré-requisitos previamente descarregados.  

- Pode afirmar a seleção dos pacotes de idiomas de servidor e cliente atuais, ou alterar as seleções para adicionar ou remover suporte para idiomas.  

- Só podem ser selecionados pacotes linguísticos disponíveis quando executa a Configuração.  

> [!NOTE]  
> Não é possível utilizar os pacotes de idiomas do System Center 2012 Configuration Manager para ativar os idiomas para um site de ramificação atual do Gestor de Configuração.  

Para mais informações sobre pacotes linguísticos, consulte [pacotes de idiomas.](language-packs.md)  

#### <a name="review-considerations-for-site-upgrades"></a>Rever considerações para atualizações do site

Ao atualizar um site, algumas funcionalidades e configurações são repostas para uma configuração predefinida. Para ajudá-lo a preparar-se para estas e alterações relacionadas, consulte [considerações para upgrade](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Criar uma cópia de segurança da base de dados do site no site da administração central e nos principais sites

Antes de atualizar um site, faça o backup da base de dados do site para se certificar de que tem um backup de sucesso para utilizar para a recuperação de desastres.  

Para mais informações, consulte [Backup e recuperação.](../../manage/backup-and-recovery.md)  

#### <a name="back-up-a-customized-configurationmof-file"></a>Faça uma configuração personalizada.mof arquivo

Se utilizar um ficheiro de configuração personalizado.mof para definir as classes de dados que utiliza com o inventário de hardware, crie uma cópia de segurança deste ficheiro. Após a atualização, devolva este ficheiro ao seu site. Para mais informações, consulte [Como alargar o inventário de hardware](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Teste o processo de atualização da base de dados numa cópia da mais recente cópia da base de dados do site

Antes de atualizar um site de administração central do Configuration Manager ou um site primário, teste o processo de atualização da base de dados do site numa cópia da base de dados do site.  

- Teste o processo de atualização da base de dados do site. Ao atualizar um site, a base de dados do site pode ser modificada.  

- Embora não seja necessário testar a atualização da base de dados, pode identificar problemas para a atualização antes de a sua base de dados de produção ser afetada.  

- Uma atualização da base de dados do site efetuada incorretamente pode deixar a base de dados do site inoperável, podendo ser necessário efetuar uma recuperação do site de forma a restaurar o funcionamento  

- Embora a base de dados do site seja partilhada entre os sites de uma hierarquia, planeie o teste da base de dados em cada site aplicável antes de atualizar esse site  

- Se utiliza réplicas de bases de dados para pontos de gestão num site primário, desative a replicação antes de criar a cópia de segurança da base de dados do site  

O Gestor de Configuração não suporta a cópia de segurança de sites secundários ou o upgrade de teste de uma base de dados de site secundário.  

Não é suportado para fazer uma atualização da base de dados de testes na base de dados do site de produção. Tal procedimento atualiza a base de dados do site, podendo fazer com que este deixe de funcionar.  

Para obter mais informações, veja [Testar a atualização da base de dados do site](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Reiniciar o servidor do site e cada computador que acolhe uma função do sistema de site

Faça esta ação para garantir que não existem ações pendentes de uma instalação recente de atualizações ou de pré-requisitos.  

#### <a name="upgrade-sites"></a>Atualizar sites

Começando no site de alto nível da hierarquia, executar Setup.exe a partir dos meios de origem do Gestor de Configuração.  

Após as atualizações do site de alto nível, pode iniciar a atualização de cada site infantil. Complete a atualização de cada site antes de começar a atualizar o próximo site.  

Até que todos os sites da sua hierarquia atualizem para O Gestor de Configuração, a sua hierarquia funciona num modo de versão mista.  

Para obter informações sobre como executar a atualização, consulte [os sites de upgrade](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Depois da atualização  

Reveja estes passos depois de fazer o upgrade para O Gestor de Configuração.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Atualizar as consolas de Gestor de Configuração autónoma

Por padrão, ao atualizar um site de administração central ou um site primário, a instalação também atualiza a consola do Gestor de Configuração que está instalada no servidor do site. Atualize manualmente cada consola instalada num computador que não seja o servidor do site.  

> [!TIP]  
> Feche cada consola aberta antes de iniciar a atualização.  

Para mais informações, consulte as [consolas do Gestor](install-consoles.md)de Configuração de Instalação .  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Reconfigurar réplicas de bases de dados para pontos de gestão em sites primários

Se utilizar réplicas de bases de dados para pontos de gestão em sites primários, desinstale as réplicas da base de dados antes de atualizar o site. Após atualizar um site primário, reconfigure a réplica da base de dados para pontos de gestão.

Para mais informações, consulte réplicas de Base de [Dados para pontos](../configure/database-replicas-for-management-points.md)de gestão .  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Reconfigurar quaisquer tarefas de manutenção da base de dados que desativou antes da atualização

Se desativar [as tarefas](../../manage/reference-for-maintenance-tasks.md) de manutenção da base de dados num site antes da atualização, reconfigure essas tarefas no site utilizando as mesmas definições que estavam em vigor antes da atualização.  

#### <a name="upgrade-clients"></a>Atualizar clientes

Depois de todos os seus sites atualizarem para O Gestor de Configuração, planeie atualizar os clientes.  

Ao atualizar um cliente, o software atual do cliente é desinstalado e é instalada a nova versão do software de cliente. Para atualizar os clientes, pode utilizar qualquer método suportado pelo Configuration Manager.  

> [!TIP]  
> Ao atualizar o site de nível superior de uma hierarquia, também é atualizado o pacote de instalação de cliente de cada ponto de distribuição da hierarquia. Ao atualizar um site primário, o pacote de upgrade do cliente que está disponível a partir desse site principal é atualizado.  

Para mais informações, consulte [Como atualizar os clientes para computadores Windows](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a>Considerações para a atualização  

### <a name="automatic-actions"></a>Ações automáticas

Quando atualiza para o Gestor de Configuração, as seguintes ações ocorrem automaticamente:  

- Um reset do site. Esta ação inclui uma reinstalação de todas as funções do sistema do site.  

- Caso o site seja o site de nível superior de uma hierarquia, atualizará o pacote de instalação de cliente em todos os pontos de distribuição da hierarquia. O site também atualiza as imagens de boot padrão para usar a nova versão do Windows PE que está incluída no Windows Assessment and Deployment Kit 10. No entanto, a atualização não atualiza os meios existentes para utilização com a implementação da imagem.  

- Caso o site seja um site primário, atualizará o pacote de atualização de cliente para esse site.  

### <a name="manual-actions-after-an-upgrade"></a>Ações manuais após uma atualização

Depois de atualizar um site, certifique-se de que faz as seguintes ações:  

- Certifique-se de que os clientes atribuídos a cada atualização do site primário e a instalação da nova versão do cliente  

- Atualize cada consola do Gestor de Configuração que se conecta ao site e que funciona num computador que é remoto do servidor do site  

- Nos sites primários onde utiliza réplicas de bases de dados para pontos de gestão, reconfigure as réplicas de base de dados  

- Após a atualização do site, atualize manualmente os meios físicos como ficheiros ISO para CDs, DVDs ou pen drives USB. Também inclui meios pré-encenados fornecidos a fornecedores de hardware. A atualização do site atualiza as imagens de boot predefinidas, não pode atualizar estes ficheiros de mídia ou dispositivos utilizados externos ao 'Gestor de Configuração'.  

- Planeie atualizar as imagens de boot personalizadas quando não necessitar da versão mais antiga do Windows PE.  

### <a name="actions-that-affect-configurations-and-settings"></a>Ações que afetam configurações e configurações

Quando um site atualiza para O Gestor de Configuração, algumas configurações e configurações não persistem após a atualização. Algumas configurações estão definidas para um novo padrão. A lista que se segue inclui algumas definições que não persistem ou que mudam:  

- **Centro de Software**  
    Os seguintes itens do Centro de Software são repostos nos valores predefinidos:  

  - **A informação de trabalho** é reposto para o horário de trabalho das **5h às** **22h de** segunda a sexta-feira.  

  - O valor de **Manutenção do computador** é definido como **Suspender as atividades do Centro de Software quando o computador estiver em modo de apresentação**.  

  - O valor de **Controlo remoto** é definido com o valor existente nas definições de cliente que foram atribuídas ao computador.  

- **Calendários**de resumo de atualização de software : Os horários de resumição personalizados para atualizações de software ou grupos de atualização de software são redefinidos para o valor padrão de 1 hora. Após a conclusão da atualização, reponha os valores de resumo personalizados na frequência pretendida.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a> Testar a atualização da base de dados do site  

As seguintes informações aplicam-se apenas quando estiver a atualizar uma versão anterior como System Center 2012 Configuration Manager para configuração do ramo atual.

Antes de atualizar um site, teste uma cópia da base de dados desse site para a atualização.  

Para testar a base de dados para uma atualização, primeiro restaure uma cópia da base de dados do site para uma instância do SQL Server que não acolhe um site do Gestor de Configuração. A versão do SQL Server que utiliza para alojar a cópia da base de dados deve ser uma versão do SQL Server que o Gestor de Configuração suporta.  

Depois de restaurar a base de dados do site, no computador SQL Server, executar configuração do Gestor de Configuração a partir da pasta de suporte de origem para 'Configuração Manager'. Utilize `/TESTDBUPGRADE` a opção linha de comando.  

Para obter mais informações, veja os artigos seguintes:

- [Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração](../../manage/backup-and-recovery.md)  

- [Opções de linha de comando para configuração](command-line-options-for-setup.md#bkmk_setup)  

- [Suporte para versões do SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Se integrar o Microsoft Intune com o Gestor de Configuração:  
>
> Quando executa um teste de atualização da base de dados numa cópia da base de dados do site com 5 ou mais dias, poderá receber uma das seguintes mensagens:  
>
> - AVISO: A atualização irá forçar a sincronização completa com a nuvem.  
> - ERRO: A atualização da base de dados irá forçar a sincronização completa com a nuvem.  
>
> Ambos podem ser ignorados com segurança durante o teste de uma atualização da base de dados. Não indicam uma falha ou problema com a atualização do teste. Em vez disso, indicam que durante a atualização real, os dados do grupo de replicação da base de dados **Cloud** podem sincronizar com o Microsoft Intune.  

### <a name="test-a-site-database-for-upgrade"></a>Testar uma base de dados do site para upgrade  

Utilize o seguinte procedimento em cada site da administração central e local primário que pretende atualizar:  

1. Faça uma cópia da base de dados do site. Em seguida, restaure essa cópia para uma instância do SQL Server que usa a mesma edição que a base de dados do seu site, e que não acolhe um site do Gestor de Configuração. Por exemplo, se a base de dados do site for executada numa instância da edição Enterprise do SQL Server, certifique-se de que restaura a base de dados para uma instância do SQL Server que também execute a edição Enterprise do SQL Server.  

2. Depois de restaurar a cópia da base de dados, executar Configuração a partir do meio de origem para o ramo atual do Gestor de Configuração. Quando executar a configuração, utilize a opção linha `/TESTDBUPGRADE` de comando. Se a instância Do Servidor SQL que acolhe a cópia da base de dados não for a instância padrão, também forneça os argumentos da linha de comando para identificar a instância que acolhe a cópia da base de dados do site.  

    Por exemplo, planeia atualizar uma base de dados do site denominada SMS_ABC. Restaura uma cópia desta base de dados do site para uma instância suportada do SQL Server com o nome de instância DBTest. Para testar uma atualização desta cópia da base de dados do site, utilize a seguinte linha de comando:`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Configuração.exe está no seguinte local nos meios de origem do Gestor de Configuração:`SMSSETUP\BIN\X64`  

3. Na instância do SQL Server em que executou o teste da atualização da base de dados, monitorize o progresso e êxito do ficheiro ConfigMgrSetup.log, na raiz da unidade do sistema:  

    - Se a atualização do teste falhar, resolva quaisquer problemas relacionados com a falha de atualização da base de dados do site. Em seguida, crie uma nova cópia de segurança da base de dados do site e teste a atualização da nova cópia da base de dados do site.  

    - Após a conclusão do processo com êxito, poderá eliminar a cópia da base de dados.  

        > [!NOTE]  
        > Não é suportado para restaurar a cópia da base de dados do site que utiliza para a atualização do teste para utilização como base de dados do site em qualquer site.  

Depois de atualizar com sucesso uma cópia da base de dados do site, continue com a atualização do site do Gestor de Configuração e da sua base de dados do site.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a>Atualizar sites  

Está pronto para atualizar o site do Gestor de Configuração depois de completar as seguintes tarefas:

- Configurações de pré-upgrade para o seu site
- Testar a atualização da base de dados do site numa cópia da base de dados
- Descarregue ficheiros e pacotes de idiomas pré-requisitos para a versão que pretende instalar

Ao atualizar um site numa hierarquia, deverá atualizar primeiro o site de nível superior da hierarquia. Este site de nível superior é um site de administração central ou um site primário autónomo. Depois de concluir a atualização de um site da administração central, pode atualizar os sites primários infantis por qualquer ordem que pretenda. Depois de atualizar um site primário, pode atualizar os sites secundários para crianças do site ou atualizar sites primários adicionais antes de atualizar quaisquer sites secundários.  

Para atualizar um site de administração central ou site primário, executar Configuração a partir dos meios de origem do Gestor de Configuração. Não faça supôs configuração para atualizar sites secundários. Em vez disso, utiliza a consola 'Gestor de Configuração' para atualizar um site secundário depois de concluir a atualização do seu principal site-mãe.  

Antes de atualizar um site, feche a consola do Gestor de Configuração no servidor do site até que a atualização do site esteja concluída. Além disso, feche cada consola do Gestor de Configuração que funciona em computadores diferentes do servidor do site. Poderá voltar a ligar a consola após a conclusão da atualização do site. No entanto, até atualizar uma consola de Configuração Manager para a nova versão do 'Gestor de Configuração', essa consola não pode apresentar alguns objetos e informações disponíveis na nova versão do 'Gestor de Configuração'.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Atualizar um site de administração central ou local primário  

1. Certifique-se de que o utilizador que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    - **Direitos** do Administrador Local no servidor do site  

    - Se o servidor de base de dados do site estiver afastado do servidor do site, o **Administrador** local dever-se direito no mesmo.  

2. No servidor do site, abra `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`o seguinte programa: . Esta ação abre o assistente de configuração do Gestor de Configuração.  

3. Leia as informações na página **Antes de Começar** e, em seguida, selecione **Next**.  

4. Na página **Getting Started,** selecione 'Atualizar este site ' Gestor de **Configuração',** e depois selecione **Next**.  

5. Na página chave do **produto:**  

    Se já instalou a Avaliação do Gestor de Configuração, pode selecionar **instalar a edição licenciada deste produto.** Em seguida, introduza a chave do produto para a instalação completa do Gestor de Configuração. Esta ação converte o site para a versão completa.  

    Também pode especificar a data de validade da Garantia de **Software** do seu contrato de licenciamento como um lembrete conveniente dessa data. Se não introduzir este valor durante a configuração, poderá especificá-lo mais tarde a partir da consola 'Gestor de Configuração'.  

    > [!NOTE]  
    > A Microsoft não valida a data de validade que inseriu e não utilizará esta data para validação da licença. Pode usá-lo como um lembrete da sua data de validade. O Gestor de Configuração verifica periodicamente novas atualizações de software oferecidas online e o seu estado de licença de garantia de software deve ser atual para ser elegível para usar estas atualizações adicionais.

    Para mais informações, consulte [Licenciamento e Balcões.](../../../understand/learn-more-editions.md)

6. Na página De Termos de Licença de Software da **Microsoft,** leia e aceite os termos da licença e, em seguida, selecione **Next**.  

7. Na página **De Licenças Pré-Requisitos,** leia e aceite os termos da licença para o software pré-requisito e, em seguida, selecione **Next**. A configuração descarrega e instala automaticamente o software nos sistemas do site ou nos clientes quando é necessário. Antes de poder continuar para a página seguinte, concorde com todos os termos.  

8. Na página **Descarregamentos Pré-Requisito,** especifique se configurar descarrega os conteúdos mais recentes da internet ou se utiliza ficheiros previamente descarregados. Este conteúdo inclui ficheiros redistribuíveis pré-requisitos, pacotes de idiomas e as atualizações mais recentes do produto. Se tiver transferido anteriormente os ficheiros através do Dispositivo de Transferência da Configuração, selecione **Utilizar ficheiros anteriormente transferidos** e especifique a pasta para transferência. Para mais informações, consulte O Downloader de [Configuração](setup-downloader.md).  

    > [!NOTE]  
    > Quando utilizar ficheiros transferidos anteriormente, verifique se o caminho para a pasta de transferência contém a versão mais recente dos ficheiros.  

9. Na página **Seleção do Idioma do Servidor** , veja a lista de idiomas atualmente instalados para o site. Selecione idiomas adicionais disponíveis neste site para a consola Do Gestor de Configuração e para relatórios. Também pode limpar idiomas que já não quer apoiar neste site. Por padrão, o inglês é selecionado e não pode ser removido.  

    > [!IMPORTANT]  
    > Cada versão do 'Gestor de Configuração' não pode utilizar pacotes de idiomas a partir de uma versão anterior do 'Gestor de Configuração'. Para permitir o suporte para um idioma num site do Gestor de Configuração que atualize, tem de utilizar a versão do pack de idiomas para essa nova versão. Por exemplo, durante a atualização do System Center 2012 Configuration Manager para o configurador do ramo atual, se a versão atual de um pacote de idiomas não estiver disponível com os ficheiros pré-requisitos que descarrega, não pode instalar suporte para esse idioma.  

10. Na página **Seleção do Idioma do Cliente** , veja a lista de idiomas atualmente instalados para o site. Selecione idiomas adicionais disponíveis neste site para computadores cliente ou desmarque os idiomas que já não seja necessário suportar no site. Especifique se pretende ativar todos os idiomas de cliente para clientes de dispositivos móveis e clique em **Seguinte**. Por padrão, o inglês é selecionado e não pode ser removido.  

11. Na página Resumo das **Definições,** reveja a configuração. Quando estiver pronto, selecione **Next** para iniciar o Pré-Requisito checker para verificar a prontidão do servidor para a atualização do site.  

12. Na página de Verificação de **Instalações Pré-Requisitos,** caso não existam problemas listados, selecione **Next** para atualizar as funções do site e do sistema do site.

    Se o Verificador Pré-Requisito encontrar um problema, selecione um item na lista para obter detalhes sobre como resolver o problema. Antes de continuar a Configuração, resolva todos os itens da lista com estado de **Erro** . Depois de resolver o problema, clique em **Executar Verificação** para reiniciar a verificação de pré-requisitos. Pode também abrir o ficheiro ConfigMgrPrereq.log na raiz da unidade do sistema para rever os resultados do Verificador de Pré-requisitos. O ficheiro de registo pode conter informações adicionais que não estão apresentadas na interface do utilizador. Para obter uma lista de regras e descrições pré-requisitos de instalação, consulte [o Verificador Pré-Requisito](list-of-prerequisite-checks.md).

Na página **Atualizar** , a Configuração apresenta o estado do progresso global. Quando o Programa de Configuração concluir a instalação do servidor do site principal e do sistema de sites, pode fechar o assistente. A configuração do site continua em segundo plano.  

### <a name="upgrade-a-secondary-site"></a>Atualizar um site secundário  

1. Certifique-se de que o utilizador administrativo que executa o Programa de Configuração possui os seguintes direitos de segurança:  

    - **Direitos** do Administrador Local no servidor de site secundário  

    - **Administrador de Infraestrutura** ou papel de segurança **do Administrador Completo** no local principal dos pais  

    - Os direitos do administrador do sistema **(SA)** na base de dados do site secundário  

2. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó **de Sites.**  

3. Selecione o site secundário que pretende atualizar. No separador **Home** da fita, no grupo **Site,** selecione **Upgrade**.  

4. Selecione **Sim** para confirmar a decisão e para iniciar a atualização do site secundário.  

A atualização do site secundário corre em segundo plano. Depois de concluída a atualização, confirme o estado na consola 'Gestor de Configuração'. Selecione o servidor de site secundário e, em seguida, no separador **Home** da fita, no grupo **Site,** selecione **'Mostrar Estado**de Instalação .  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a>Tarefas pós-actualização  

Depois de atualizar um site, poderá ter de completar tarefas adicionais para concluir a atualização ou reconfigurar o site. Estas tarefas podem incluir os seguintes itens:

- Clientes do Gestor de Configuração de Upgrade
- Consolas de Gestor de Configuração de Upgrade
- Reativar réplicas de bases de dados para pontos de gestão
- Restaurar as definições para a funcionalidade do Gestor de Configuração que utiliza e que não persiste após a atualização  
