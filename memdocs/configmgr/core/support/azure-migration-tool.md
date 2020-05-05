---
title: Alargar e migrar no local para o Microsoft Azure
titleSuffix: Configuration Manager
description: Saiba como usar a ferramenta de migração para criar programáticamente máquinas virtuais Azure para O Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723454"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Alargar e migrar o site no local para o Microsoft Azure

*Aplica-se a: Gestor de Configuração (Ramo Atual)*


Esta ferramenta, introduzida na versão 1910, ajuda-o a criar programáticamente máquinas virtuais Azure (VMs) para O Gestor de Configuração. <!--3556022--> Pode instalar com as definições padrão do site funções como um servidor de site passivo, pontos de gestão e pontos de distribuição. Assim que validar as novas funções, utilize-as como sistemas adicionais do site para uma elevada disponibilidade. Também pode remover a função do sistema de site no local e apenas manter a função Azure VM.

## <a name="prerequisites"></a>Pré-requisitos

- Uma subscrição do Azure.

- Rede virtual Azure com gateway ExpressRoute

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- A sua conta de utilizador tem de ser um **Administrador Completo** do Gestor de Configuração e ter direitos de administrador no servidor principal do site.

- Para adicionar um servidor passivo, o site principal deve satisfazer os [elevados requisitos](../servers/deploy/configure/site-server-high-availability.md#prerequisites)de disponibilidade do servidor do site . Por exemplo, requer uma biblioteca de [conteúdos remotos.](../plan-design/hierarchy/the-content-library.md#bkmk_remote)

### <a name="required-azure-permissions"></a>Permissões do Azure necessárias

Necessitará das seguintes permissões em Azure quando executar a ferramenta:
<!--5789222-->
Microsoft.Recursos/subscrições/recursosGroups/read <br>
Microsoft.Recursos/subscrições/recursosGroups/write <br>
Microsoft.Recursos/implementações/leitura <br>
Microsoft.Recursos/implementações/escrita <br>
Microsoft.Recursos/implementações/validação/ação <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Armazenamento/armazenamentoContas/leitura <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Armazenamento/armazenamentoContas/blobServices/containers/write <br>
Microsoft.Armazenamento/armazenamentoContas/blobServices/contentores/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


Para obter mais informações sobre permissões e atribuindo funções, consulte [Gerir o acesso aos recursos do Azure utilizando](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)o RBAC .

## <a name="run-the-tool"></a>Executar a ferramenta

1. Inscreva-se no servidor do site principal e execute a seguinte ferramenta no diretório de instalação do Gestor de Configuração:`Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Reveja as informações no separador **Geral** e, em seguida, mude para o separador **Informação Azure.**

1. No separador **Informação Azure,** escolha o seu **ambiente Azure**, e, em seguida, **inscreva-se**.

    > [!TIP]
    > Poderá ter de `https://*.microsoft.com` adicionar à sua lista de sites fidedignos para iniciar sessão corretamente.

    [![Separador de informação Azure na ferramenta Extend and Migrate](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Depois de iniciar sessão, selecione o ID de **subscrição** e **a rede Virtual**. A ferramenta apenas lista redes com um gateway ExpressRoute.

## <a name="site-server-high-availability"></a>Alta Disponibilidade do Servidor do Site

1. No separador De alta disponibilidade do Servidor do **Site,** selecione **Verificar** para avaliar a prontidão do seu site.

    Se alguma das verificações falhar, selecione **Mais detalhes** para determinar como remediar o problema. Para obter mais informações sobre estes pré-requisitos, consulte a elevada disponibilidade do [servidor do Site](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Se pretender estender ou migrar o servidor do seu site para o Azure, selecione Criar um servidor de **site no Azure**. Em seguida, preencha os seguintes campos:

    |Nome|Descrição|
    |---|---|
    |**Subscrição**|Leia apenas. Mostra o nome da subscrição e id.|
    |**Grupo de recursos**| Lista os grupos de recursos disponíveis. Se precisar de criar um novo grupo de recursos, utilize o [portal Azure](https://portal.azure.com)e, em seguida, refaça esta ferramenta.|
    |**Localização**| Leia apenas. Determinado pela localização da sua rede virtual|
    |**Tamanho VM**|Escolha um tamanho para se adaptar à sua carga de trabalho. A Microsoft recomenda a **Standard_DS3_v2**.|
    |**Sistema Operativo**|Leia apenas. A ferramenta utiliza o Windows Server 2019.|
    |**Tipo de disco**|Leia apenas. A ferramenta utiliza SSD Premium para melhor desempenho.|
    |**Rede virtual**|Leia apenas.|
    |**Sub-rede**|Selecione a sub-rede para utilizar. Se precisar de criar uma nova subrede, utilize o [portal Azure.](https://portal.azure.com)|
    |**Nome da máquina**|Introduza o nome do servidor passivo vM do servidor do site em Azure. É o mesmo nome mostrado no [portal Azure.](https://portal.azure.com)|
    |**Nome de utilizador de administração local**|Introduza o nome do utilizador administrativo local que o Azure VM cria antes de se juntar ao domínio.|
    |**Senha de administração local**|A senha do utilizador administrativo local. Para proteger a palavra-passe durante a implementação do Azure, guarde a palavra-passe como um segredo no [Cofre de Chaves Azure](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Então, use a referência aqui. Se necessário, crie um novo a partir do [portal Azure.](https://portal.azure.com)|
    |**Domínio FQDN**|O nome de domínio totalmente qualificado para o domínio do Diretório Ativo aderir. Por predefinição, a ferramenta obtém este valor da sua máquina atual.|
    |**Nome de utilizador de domínio**|O nome do utilizador do domínio permitiu aderir ao domínio. Por predefinição, a ferramenta utiliza o nome do utilizador atualmente assinado.|
    |**Senha de domínio**|A palavra-passe do utilizador do domínio para aderir ao domínio. A ferramenta verifica-o depois de selecionar **Iniciar**. Para proteger a palavra-passe durante a implementação do Azure, guarde a palavra-passe como um segredo no [Cofre de Chaves Azure](https://docs.microsoft.com/azure/key-vault/key-vault-overview). Então, use a referência aqui. Se necessário, crie um novo a partir do [portal Azure.](https://portal.azure.com)|
    |**DNS DE Domínio IP**|Usado para aderir ao domínio. Por predefinição, a ferramenta utiliza o DNS atual da sua máquina atual.|
    |**Tipo**|Leia apenas. Mostra o *Servidor de Site Passivo* como o tipo.|

    > [!IMPORTANT]
    > Por predefinição, as máquinas virtuais estão definidas para **Não** para **utilização**da licença existente do Windows Server . Se pretender utilizar as suas licenças no Local do Windows Server com garantia de software, configure esta definição no [portal Azure](https://portal.azure.com) depois de as máquinas virtuais estarem aprovisionadas. Para mais informações, consulte [O Benefício Híbrido Azure para o Servidor windows](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit).

1. Para começar a fornecer o VM Azure, selecione **Iniciar**. Para monitorizar o estado de implantação, mude para as **implantações do** separador Azure na ferramenta. Para obter o estado mais recente, selecione o estado de **implementação Refresh**.

    > [!TIP]
    > Também pode utilizar o [portal Azure](https://portal.azure.com) para verificar o estado, encontrar erros e determinar possíveis correções.

1. Quando a implementação terminar, vá aos seus servidores SQL e conceda permissões para o novo VM Azure. Para mais informações, consulte a elevada disponibilidade do [servidor do Site - Pré-requisitos](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Para adicionar o VM Azure como servidor de site em modo passivo, selecione **Adicionar servidor de site no modo passivo**.

1. Uma vez que o site adiciona o servidor do site em modo passivo, o separador de alta disponibilidade do **Servidor do Site** mostra o estado.

   [![Servidor de site passivo adicionado ao separador de alta disponibilidade do Servidor do Site](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Em seguida, vá ao separador [Azure](#bkmk_deploy-azure) para terminar a implantação.

## <a name="site-database"></a>Base de dados do site

A ferramenta não tem atualmente nenhuma tarefa de migrar a base de dados do local para o Azure. Pode optar por mover a base de dados de um servidor SQL no local para um VM do Servidor SQL Azure. A ferramenta lista os seguintes artigos no separador Base de Dados do **Site** para ajudar:

- [Backup e restaurar a base de dados](../servers/manage/backup-and-recovery.md)
- [Configure o SQL Sempre Ligado e permita que os dados se reproduzam](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migrar uma base de dados SQL para um VM do servidor Azure SQL](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Funções do sistema de sites

1. Mude para o separador Funções do **Sistema do Site.** Para fornecer uma nova função do sistema do site com as definições predefinidas, selecione **Criar nova**. Pode fornecer funções como o ponto de gestão, ponto de distribuição e ponto de atualização de software. Nem todas as funções estão atualmente disponíveis na ferramenta.

    [![Separador de funções do sistema do site na ferramenta Extend and Migrate](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. Na janela de provisionamento, preencha os campos para fornecer o VM do local em Azure. Estes detalhes são semelhantes à lista acima para o servidor do site.

1. Para começar a fornecer o VM Azure, selecione **Iniciar**. Para monitorizar o estado de implantação, mude para as **implantações do** separador Azure na ferramenta. Para obter o estado mais recente, selecione o estado de **implementação Refresh**.

    > [!TIP]
    > Também pode utilizar o [portal Azure](https://portal.azure.com) para verificar o estado, encontrar erros e determinar possíveis correções.

1. Repita este processo para adicionar mais funções do sistema do site.

1. Em seguida, vá ao separador [Azure](#bkmk_deploy-azure) para terminar a implantação.

1. Quando a implementação terminar, vá à consola Do Gestor de Configuração para fazer alterações adicionais na função do site.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a>Implantações em Azure

1. Assim que o Azure criar o VM, mude para as **implantações no** separador Azure na ferramenta. Selecione **'Implementar'** para configurar a função com as definições predefinidas.

1. Selecione **Executar** para iniciar o script PowerShell.

    [![Implementar funções de site executando o script PowerShell gerado](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Repita este processo para configurar mais funções.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a>Adicione as funções do site a uma implementação de máquina virtual existente
<!--5665775, 6307931-->
A partir da versão de 2002 do Configuration Manager, o site de extensão e migração no local para a ferramenta Microsoft Azure suporta o fornecimento de várias funções do sistema de site numa única máquina virtual Azure. Pode adicionar funções do sistema do site após a implementação inicial da máquina virtual Azure ter concluído. Para adicionar um novo papel a uma máquina virtual existente, faça os seguintes passos:
1. No separador **Implantações em Azure,** clique numa implementação de máquina virtual com um estado **completo.**
1. Clique no novo botão **Criar** para adicionar um papel adicional à máquina virtual.


## <a name="next-steps"></a>Passos seguintes

Reveja as suas alterações no [portal Azure](https://portal.azure.com)
