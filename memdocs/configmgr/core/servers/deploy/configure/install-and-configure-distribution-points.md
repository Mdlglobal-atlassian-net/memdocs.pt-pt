---
title: Gerir pontos de distribuição
titleSuffix: Configuration Manager
description: Utilize pontos de distribuição para alojar o conteúdo que implementa para dispositivos e utilizadores.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1cc931bd0e02be66f608db11e0052fde571a427
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718855"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Instalar e configurar pontos de distribuição no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Instale pontos de distribuição do Gestor de Configuração para alojar os ficheiros de conteúdo que implementa para dispositivos e utilizadores. Crie grupos de pontos de distribuição para simplificar a forma como gere os pontos de distribuição e como distribui conteúdo para pontos de distribuição.  

*Instale um novo ponto* de distribuição utilizando o assistente de instalação. Para mais informações, consulte [Instale um ponto de distribuição](#bkmk_install). Para *gerir as propriedades de um ponto de distribuição existente,* edite as propriedades do ponto de distribuição. Para mais informações, consulte [Configure um ponto de distribuição](#bkmk_configs).

Configure a maioria das definições do ponto de distribuição com qualquer um dos métodos. Algumas definições só estão disponíveis quando estiver a instalar ou a editar, mas não ambas:  

- Definições que só estão disponíveis quando estiver a instalar um ponto de distribuição:  

    - **Permitir que o Gestor de Configuração instale o IIS no computador do ponto de distribuição**

    - **Configure as definições de espaço de acionamento para o ponto de distribuição**  

- Definições que só estão disponíveis quando está a editar as propriedades de um ponto de distribuição:  

    - **Gerir as relações de grupo de pontos de distribuição**  

    - **Ver Conteúdo implantado no ponto de distribuição**  

    - **Limites de taxa de configuração para transferências de dados para pontos de distribuição**  

    - **Configure horários para transferências de dados para pontos de distribuição**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a>Instalar um ponto de distribuição  

Escolha um servidor de sistema de site como um ponto de distribuição antes que o conteúdo possa ser disponibilizado aos computadores clientes. Atribuir um ponto de distribuição a pelo menos um [grupo de fronteiras](boundary-groups.md#distribution-points) antes de no local os computadores clientes podem usar esse ponto de distribuição como uma localização de fonte de conteúdo. Adicione a função de ponto de distribuição a um novo servidor do sistema do site, ou adicione-a a um servidor de sistema de site existente.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a>Pré-requisitos

Quando instala um novo ponto de distribuição, utiliza um assistente de instalação que o acompanha através das definições disponíveis. Antes de começar, considere os seguintes pré-requisitos:  

- Deve ter as seguintes permissões de segurança para criar e configurar um ponto de distribuição:  

    - **Leia** para o objeto ponto de **distribuição**  

    - **Copiar para Ponto de Distribuição** para o objeto ponto de **distribuição**  

    - **Modificar** para o objeto **do Site**  

    - **Gerir Certificados para implantação** do sistema operativo para o objeto **do Site**  

- Instale serviços de informação de Internet (IIS) no servidor Windows que acolhe o ponto de distribuição. Ou, quando instalar a função do sistema do site, o Configurmanager pode instalar e configurar o IIS para si.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Procedimento para instalar um ponto de distribuição  

Utilize este procedimento para adicionar um novo ponto de distribuição. Para alterar a configuração de um ponto de distribuição existente, consulte a secção de pontos de [distribuição Do Configure.](#bkmk_configs)  

Comece com o procedimento geral para [instalar as funções](install-site-system-roles.md)do sistema do site . Selecione a função ponto **de distribuição** na página de seleção de **funções** do sistema do assistente do Servidor do Sistema de Criação. Esta ação adiciona as seguintes páginas ao assistente:  

- [Ponto de distribuição](#bkmk_config-general)
- [Comunicação](#bkmk_config-comm)
- [Definições de unidade](#bkmk_config-drive)
- [Ponto de distribuição de puxar](#bkmk_config-pull)
- [Definições de PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação do Conteúdo](#bkmk_config-valid)
- [Grupos de Fronteiras](#bkmk_config-boundary)

> [!Important]  
> As seguintes definições só estão disponíveis quando estiver a instalar um ponto de distribuição:  
>
> - **Permitir que o Gestor de Configuração instale o IIS no computador do ponto de distribuição**  
>
> - **Configure as definições de espaço de acionamento para o ponto de distribuição**  

Para obter mais informações sobre as páginas do assistente específicas da função do ponto de distribuição, consulte a secção de pontos de [distribuição Do Configure.](#bkmk_configs) Por exemplo, se pretender instalar o ponto de distribuição como ponto de distribuição de [puxar,](#bkmk_config-pull)escolha a opção de ativar este ponto de **distribuição para retirar conteúdo de outros pontos de distribuição**. Em seguida, faça as configurações adicionais que os pontos de distribuição de puxar exigem.  

Depois de terminar o assistente do Servidor do Sistema de Sistema seleção, o site adiciona a função do ponto de distribuição ao servidor do sistema do site.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a>Gerir grupos de pontos de distribuição  

Os grupos de pontos de distribuição permitem um agrupamento lógico de pontos de distribuição para distribuição de conteúdos. Utilize estes grupos para gerir e monitorizar o conteúdo de um local central para pontos de distribuição que abrangem vários sites. Tenha em mente o seguinte ponto:

- Adicione um ou mais pontos de distribuição de qualquer site da hierarquia a um grupo de pontos de distribuição.  

- Adicione um ponto de distribuição a mais de um grupo de pontos de distribuição.  

- Quando distribui conteúdo para um grupo de pontos de distribuição, o Gestor de Configuração distribui o conteúdo para todos os pontos de distribuição que são membros do grupo.  

- Se adicionar um ponto de distribuição ao grupo após uma distribuição inicial de conteúdo, o Gestor de Configuração distribui automaticamente o conteúdo ao novo membro do ponto de distribuição.  

- Associe uma coleção com um grupo de pontos de distribuição. Quando distribui conteúdo para essa coleção, o Gestor de Configuração determina quais os grupos associados à coleção. Em seguida, distribui o conteúdo para todos os pontos de distribuição que são membros desses grupos.  

    > [!NOTE]  
    > Depois de distribuir conteúdo a uma coleção, se, em seguida, associar a coleção a um novo grupo de pontos de distribuição, terá de redistribuir o conteúdo para a recolha antes de o conteúdo ser distribuído para o novo grupo de pontos de distribuição.  

As secções seguintes listam os procedimentos para as seguintes ações de gestão dos grupos de pontos de distribuição:  

- [Criar e configurar um novo grupo de pontos de distribuição](#bkmk_dpgroup-create)
- [Modificar um grupo de pontos de distribuição existentes](#bkmk_dpgroup-modify)
- [Adicione pontos de distribuição selecionados aos grupos de pontos de distribuição existentes](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Procedimento para criar e configurar um novo grupo de pontos de distribuição  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Grupos de Pontos de **Distribuição.**  

2. Na fita, selecione **Criar Grupo**.  

3. Na janela Create New Distribution Point Group, introduza o **Nome**e opcionalmente uma **Descrição** para o grupo.  

4. No separador **Membros,** selecione **Adicionar**.  

5. Na janela Pontos de Distribuição Add, selecione um ou mais pontos de distribuição para adicionar como membros do grupo. Em seguida, escolha **OK**.  

6. Se necessário, mude para o separador **Coleções** da janela Create New Distribution Point Group e selecione **Adicionar**.  

7. Na janela Select Collections, selecione as coleções para se associar ao grupo de pontos de distribuição e, em seguida, escolha **OK**.  

8. Na janela Create New Distribution Point Group, escolha **OK** para criar o grupo.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Criar um novo grupo a partir de um ponto de distribuição existente

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.** Selecione um ou mais pontos de distribuição para adicionar a um novo grupo de pontos de distribuição.  

2. Na fita, selecione **Adicionar Itens Selecionados**, e, em seguida, selecione **Adicionar itens selecionados ao Novo Grupo**de Pontos de Distribuição .  

Este processo povoa automaticamente o separador **Membros** da janela Create New Distribution Point Group com os servidores selecionados.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Procedimento para modificar um grupo de pontos de distribuição existente  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó de Grupos de Pontos de **Distribuição.**  

2. Selecione um grupo de pontos de distribuição existente para modificar. Na fita, selecione **Propriedades**.  

3. Para associar novas coleções a este grupo, mude para o separador **Coleções** e escolha **Adicionar**. Selecione as coleções e, em seguida, escolha **OK**.  

4. Para adicionar novos pontos de distribuição a este grupo, mude para o separador **Membros** e escolha **Adicionar**. Selecione os pontos de distribuição e, em seguida, escolha **OK**.  

5. Escolha **OK** para guardar alterações no grupo de pontos de distribuição.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Procedimento para adicionar pontos de distribuição selecionados aos grupos de pontos de distribuição existentes  

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.** Selecione um ou mais pontos de distribuição para adicionar a um grupo existente.  

2. Na fita, selecione **Adicionar itens selecionados**, e, em seguida, selecione **Adicionar itens selecionados aos grupos de pontos**de distribuição existentes .  

3. Nos **grupos de pontos**de distribuição disponíveis, selecione os grupos aos quais são adicionados os pontos de distribuição selecionados como membros. Em seguida, escolha **OK**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a>Reatribuir um ponto de distribuição

<!-- 1306937 -->

Muitos clientes têm grandes infraestruturas de Gestor de Configuração, e estão a reduzir os locais primários ou secundários para simplificar o seu ambiente. Ainda precisam de reter pontos de distribuição em sucursais para servir conteúdo a clientes geridos. Estes pontos de distribuição contêm frequentemente vários terabytes ou mais de conteúdo. Este conteúdo é dispendioso em termos de tempo e largura de banda da rede para distribuir a estes servidores remotos.

Esta funcionalidade permite-lhe reatribuir um ponto de distribuição a outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição do sistema do site enquanto persiste todo o conteúdo no servidor. Se precisar de reatribuir vários pontos de distribuição, execute primeiro esta ação num único ponto de distribuição. Em seguida, proceda com servidores adicionais um de cada vez.

> [!IMPORTANT]  
> O servidor alvo só pode acolher a função de ponto de distribuição. Se o servidor do sistema do site acolher outra função de servidor do Gestor de Configuração, como o ponto de migração do Estado, não pode reatribuir o ponto de distribuição. Não é possível reatribuir um ponto de distribuição em nuvem.

Antes de reatribuir um ponto de distribuição, adicione a conta de computador do servidor do site de destino ao grupo de administrador local no servidor de ponto de distribuição do alvo.

Siga estes passos para reatribuir um ponto de distribuição:

1. Na consola 'Gestor de Configuração', ligue-se ao site da administração central.  

2. Vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.**  

3. Clique no ponto de distribuição do alvo e selecione Ponto de **Distribuição de Reatribuir**.  

4. Selecione o servidor do site alvo e o código do site para o qual pretende reatribuir este ponto de distribuição.  

Monitorize a reatribuição da mesma forma que quando adicionar um novo papel. O método mais simples é refrescar a vista da consola após vários minutos. Adicione a coluna de código do site à vista. Este valor muda quando o Gestor de Configuração reatribui o servidor. Se tentar realizar outra ação no servidor alvo antes de atualizar a visão da consola, ocorre um erro de "objeto não encontrado". Certifique-se de que o processo está completo e refresque a vista da consola antes de iniciar quaisquer outras ações no servidor.

Depois de reatribuir um ponto de distribuição, refresque o certificado do servidor. O novo servidor do site precisa de voltar a encriptar este certificado utilizando a sua chave pública e armazená-lo na base de dados do site. Para mais informações, consulte a Criação de **um certificado auto-assinado ou importe um certificado de cliente de infraestrutura de chave pública (PKI) para a definição** do ponto de distribuição no separador [Geral](#bkmk_config-general) das propriedades do ponto de distribuição.

- Para certificados PKI, não precisa de criar um novo certificado. Importar o mesmo. PFX e introduza a senha.  

- Para certificados auto-assinados, ajuste a data de validade ou a hora de atualizá-lo.  

- Se não atualizar o certificado, o ponto de distribuição ainda serve conteúdo, mas as seguintes funções falham:  

    - Mensagens de validação de conteúdo (o distmgr.log mostra que não pode desencriptar o certificado)  

    - Suporte pXE para clientes  

### <a name="tips"></a>Sugestões

- Execute esta ação a partir do site da administração central. Esta prática ajuda na replicação aos locais primários.  

- Não distribua conteúdo para o servidor alvo e tente reatribuí-lo. Distribuir as tarefas de conteúdo que estão em curso pode falhar durante o processo de reatribuição, mas retenta por normal.  

- Se o servidor também for um cliente do Gestor de Configuração, certifique-se de também reatribuir o cliente ao novo site primário. Este passo é especialmente fundamental para os pontos de distribuição de puxar, que utilizam os componentes do cliente para descarregar conteúdo.  

- Este processo remove o ponto de distribuição do grupo de fronteira padrão do antigo site. Tem de adicioná-lo manualmente ao grupo de limites padrão do novo site, se necessário. Todas as outras missões de grupo de fronteiras permanecem as mesmas.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a>Modo de manutenção

<!--3555754-->

A partir da versão 1902, pode definir um ponto de distribuição no modo de manutenção. Ative o modo de manutenção quando estiver a instalar atualizações de software ou a fazer alterações de hardware no servidor.

Enquanto o ponto de distribuição está no modo de manutenção, tem os seguintes comportamentos:

- O site não distribui nenhum conteúdo.  

- Os pontos de gestão não devolvem a localização deste ponto de distribuição aos clientes.

- Ao atualizar o site, um ponto de distribuição no modo de manutenção ainda atualiza.

- As propriedades do ponto de distribuição são apenas de leitura. Por exemplo, não pode alterar o certificado ou adicionar grupos de fronteira.  

- Qualquer tarefa agendada, como a validação de conteúdos, ainda funciona no mesmo horário.

Tenha cuidado ao permitir o modo de manutenção em mais de um ponto de distribuição. Esta ação pode causar um impacto de desempenho nos seus outros pontos de distribuição. Dependendo das configurações do seu grupo de limites, os clientes podem ter aumentado os tempos de descarregamento ou não conseguir descarregar conteúdo.

O modo de manutenção não deve ser um estado a longo prazo para qualquer ponto de distribuição. Para quaisquer ações com longa duração, considere primeiro remover a função do ponto de distribuição.

> [!NOTE]
> Enquanto um ponto de distribuição estiver no modo de manutenção, não faça as seguintes ações:<!-- SCCMDocs-pr #4699 -->
>
> - Remover o papel
> - Ponto de distribuição de reatribuir

### <a name="enable-maintenance-mode"></a>Ativar o modo de manutenção

Para colocar um ponto de distribuição no modo de manutenção, a sua conta de utilizador requer a permissão **Modificar** na classe **Site.** Por exemplo, o Administrador de **Infraestruturas** e as funções **full** administrator incorporadas têm esta permissão.<!-- SCCMDocs-pr issue #3407 -->

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.**  

2. Selecione o nó pontos de **distribuição.**  

3. Selecione o ponto de distribuição do alvo e escolha o **modo de manutenção Ativar** a partir da fita.  

Para ver o estado atual dos pontos de distribuição, adicione a coluna "Modo manutenção" ao nó **pontos** de distribuição na consola.

Para obter mais informações sobre automatizar este processo com o Gestor de Configuração SDK, consulte o [método SetDPMaintenanceMode na classe SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a>Configure um ponto de distribuição  

Os pontos de distribuição individuais suportam uma variedade de configurações diferentes. No entanto, nem todos os tipos de pontos de distribuição suportam todas as configurações. Por exemplo, os pontos de distribuição em nuvem não suportam implementações ativadas por PXE ou multicast. Para obter mais informações sobre limitações específicas, consulte os seguintes artigos:  

- [Use um ponto de distribuição de nuvem](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Utilizar um ponto de distribuição de extração](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

As seguintes secções descrevem as configurações do ponto de distribuição quando está [a instalar uma nova](#bkmk_install-procedure) ou a editar uma [existente:](#bkmk_change-procedure)  

- [Definições gerais](#bkmk_config-general)
- [Comunicação](#bkmk_config-comm)
- [Definições de unidade](#bkmk_config-drive)
- [Definições de firewall](#bkmk_firewall)
- [Ponto de distribuição de puxar](#bkmk_config-pull)
- [Definições de PXE](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Validação do Conteúdo](#bkmk_config-valid)
- [Grupos de Fronteiras](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a>Procedimento para alterar um ponto de distribuição

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da **Administração** e selecione o nó pontos de **distribuição.**  

2. Selecione o ponto de distribuição para configurar. Na fita, escolha **Propriedades**.  

3. Utilize a informação nas seguintes secções quando estiver a editar as propriedades do ponto de distribuição.  

4. Depois de efetuar as alterações que deseja, selecione **OK** para guardar as suas definições e fechar as propriedades do ponto de distribuição.  

### <a name="general"></a><a name="bkmk_config-general"></a>Geral  

> [!Note]  
> Na versão 1902 e anterior, esta página tem configurações adicionais para HTTP/HTTPS e certificados. A partir da versão 1906, estas definições estão agora na página de [Comunicação.](#bkmk_config-comm)

As seguintes definições estão na página de ponto de **distribuição** do assistente do Servidor do Sistema do Site Create, e no separador **Geral** da janela de propriedades do ponto de distribuição:  

- **Descrição**: Uma descrição opcional para esta função de ponto de distribuição.  

- **Instale e configure o IIS se necessário pelo Gestor**de Configuração : Se o IIS ainda não estiver instalado no servidor, o Gestor de Configuração instala e configura o mesmo. O Gestor de Configuração requer IIS em todos os pontos de distribuição. Se não escolher esta definição e o IIS não estiver instalado no servidor, instale primeiro o IIS antes de o Gestor de Configuração poder instalar com sucesso o ponto de distribuição.  

    > [!NOTE]  
    > Esta opção está apenas na página de ponto de **distribuição** do assistente do Servidor do Sistema do Site Create. Só está disponível quando estiver a instalar um novo ponto de [distribuição.](#bkmk_install-procedure)  

- **Ative e configure o BranchCache para este ponto de distribuição:** Escolha esta definição para permitir que o Gestor de Configuração configure o Windows BranchCache no servidor de pontode distribuição. Para mais informações, consulte [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Ajuste a velocidade de descarregamento para utilizar a largura de banda da rede não utilizada (Windows LEDBAT)**<!--1358112-->: A partir da versão 1806, permitir que os pontos de distribuição utilizem o controlo de congestionamento da rede. Para mais informações, consulte [o Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Requisitos mínimos para o suporte LEDBAT:<!-- SCCMDocs issue 883 -->  

    - Versão do Gestor de Configuração 1806 (versão geral)  

        - Windows Server, versão 1709 ou mais tarde  

    - Configuração Manager versão 1806 com rollup de atualização (4462978), ou mais tarde  

        - Windows Server, versão 1709 ou mais tarde
        - Windows Server 2016 com as atualizações KB4132216 e KB4284833

    - Versão 1810 ou mais tarde do Gestor de Configuração:

        - Windows Server, versão 1709 ou mais tarde
        - Windows Server 2016 com as atualizações KB4132216 e KB4284833
        - Windows Server 2019  

- **Ativar este ponto de distribuição para conteúdo pré-encenado**: Esta definição permite-lhe adicionar conteúdo ao servidor antes de distribuir o software. Como os ficheiros de conteúdo já estão na biblioteca de conteúdos, não transferem a rede quando distribui o software. Para mais informações, consulte [o conteúdo pré-encenado.](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)  

- **Ativar este ponto de distribuição para ser utilizado como servidor Microsoft Connected Cache**: A partir da versão 1906, pode instalar um servidor Microsoft Connected Cache nos seus pontos de distribuição. Ao gravar este conteúdo no local, os seus clientes podem beneficiar da funcionalidade de Otimização de Entrega, mas pode ajudar a proteger os links WAN. Para obter mais informações, incluindo a descrição das definições adicionais, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](../../../plan-design/hierarchy/microsoft-connected-cache.md)


### <a name="communication"></a><a name="bkmk_config-comm"></a>Comunicação

> [!Note]  
> A partir da versão 1906, as seguintes definições estão no separador **Comunicação.** Na versão 1902 e anterior, estas definições estão no separador [Geral.](#bkmk_config-general)

As seguintes definições estão na página de **Comunicação** do assistente do Servidor do Sistema do Site Criar e na janela de propriedades do ponto de distribuição:  

- **Configure como os dispositivos clientes comunicam com o ponto**de distribuição : Existem vantagens e desvantagens em utilizar **HTTP** ou **HTTPS**. Para mais informações, consulte [as melhores práticas de segurança para a gestão de conteúdos.](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)  

- **Permitir que os clientes se conectem anonimamente**: Esta definição especifica se o ponto de distribuição permite ligações anónimas dos clientes do Gestor de Configuração à biblioteca de conteúdos.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Criar um certificado auto-assinado ou importar um certificado**de cliente PKI : O Gestor de Configuração utiliza este certificado para os seguintes fins:  

    - Autentica o ponto de distribuição para um ponto de gestão antes que o ponto de distribuição envie mensagens de estado.  

    - Quando ativa o **suporte PXE para clientes** na página De **Definições PXE,** o ponto de distribuição envia-o para computadores que o PXE arranca. Estes computadores usam-no então para se ligar a um ponto de gestão durante o processo de implementação do SISTEMA.  

    Quando configurar todos os seus pontos de gestão no site para HTTP, selecione a opção de **Criar certificado auto-assinado**. Quando configurar os pontos de gestão para HTTPS, utilize a opção de **importar certificado** a partir do PKI.  

    Para importar o certificado, navegue para um ficheiro padrão de criptografia de chave pública válido (PKCS #12). Este ficheiro PFX ou CER tem o certificado PKI com os seguintes requisitos para O Gestor de Configuração:  

    - O uso pretendido inclui a autenticação do cliente  

    - Permitir a exportação da chave privada  

    > [!TIP]  
    > Não existem requisitos específicos para o sujeito do certificado ou nome alternativo sujeito (SAN). Se necessário, utilize o mesmo certificado para vários pontos de distribuição.  

    Para obter mais informações sobre os requisitos do certificado, consulte [os requisitos do certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    Por exemplo, a implementação deste certificado, consulte [a implantação do certificado de cliente para pontos de distribuição](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Definições de unidade  

> [!NOTE]  
> Estas opções só estão disponíveis quando estiver a instalar um novo ponto de distribuição.  

Especifique as definições de unidade para o ponto de distribuição. Configure até duas unidades de disco para a biblioteca de conteúdos e duas unidades de disco para a partilha do pacote. O Gestor de Configuração pode utilizar unidades adicionais quando os dois primeiros chegarem à reserva de espaço de acionamento configurado. A página **Definições de Acionamento** configura a prioridade para as unidades de disco e a quantidade de espaço de disco livre que permanece em cada unidade de disco.  

- Reserva de espaço de **acionamento (MB)**: Este valor determina a quantidade de espaço livre numa unidade antes que o Gestor de Configuração escolha uma unidade diferente e continue o processo de cópia para essa unidade. Os ficheiros de conteúdo podem abranger várias unidades.  

- **Localização do conteúdo**: Especifique as localizações para a biblioteca de conteúdos e a partilha de pacotes neste ponto de distribuição. Por predefinição, todas as localizações de conteúdo estão definidas como **Automáticas**. O Gestor de Configuração copia o conteúdo para a localização do conteúdo primário até que a quantidade de espaço livre atinja o valor especificado para a **reserva espacial Drive (MB)**. Quando seleciona **Automatic**, O Gestor de Configuração define as localizações de conteúdo primário para a unidade do disco com o maior espaço de disco na instalação. Define as localizações secundárias para a unidade de disco com o segundo espaço de disco mais livre. Quando as localizações primárias e secundárias chegam à reserva espacial de acionamento, o Select Manager seleciona outra unidade disponível com o espaço de disco mais livre para continuar o processo de cópia.  

> [!Tip]  
> Para evitar que o Gestor de Configuração instale numa unidade específica, crie um ficheiro vazio chamado **no_sms_on_drive.sms** e copie-o para a pasta raiz da unidade antes de instalar o ponto de distribuição.  

Para mais informações, consulte a biblioteca de [conteúdos.](../../../plan-design/hierarchy/the-content-library.md)

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>Definições de firewall

O ponto de distribuição deve ter as seguintes regras de entrada configuradas na firewall do Windows:

- Instrumentação de Gestão de Janelas (DCOM-In)
- Instrumentação de Gestão de Janelas (WMI-In)

Sem estas regras, os clientes receberão erro 0x801901F4 no DataTransferService.log ao tentarem descarregar conteúdo.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a>Ponto de distribuição de puxar  

Quando **activaeste este ponto de distribuição para retirar conteúdo de outros pontos de distribuição,** torna-se um ponto de distribuição de puxar. Muda-se o comportamento de como o ponto de distribuição obtém o conteúdo que distribui. Para mais informações, consulte [Utilize um ponto de distribuição de puxar](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

Para cada ponto de distribuição de puxar que configure, especifique um ou mais pontos de distribuição de origem a partir dos quais obtém o conteúdo:  

- Escolha **adicionar**, e, em seguida, selecione um ou mais dos pontos de distribuição disponíveis para serem fontes.  

- Utilize os botões de seta para ajustar a prioridade. Quando o ponto de distribuição de puxar tenta transferir conteúdo, a prioridade é a ordem em que contacta os pontos de distribuição de origem. Primeiro contacta pontos de distribuição com o valor mais baixo.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a>PXE  

Especifique se ativar o PXE no ponto de distribuição. Utilize o PXE para iniciar implementações de OS nos clientes. Para obter mais informações sobre como utilizar o PXE no 'Gestor de Configuração', consulte [o Use PXE para implementar o Windows sobre a rede](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

Quando ativa o PXE, o Gestor de Configuração instala os Serviços de Implementação do Windows (WDS) no servidor, se necessário. WDS é o serviço que executa a bota PXE para instalar sistemas operativos. Depois de terminar o assistente para criar o ponto de distribuição, o Gestor de Configuração instala um fornecedor em WDS que utiliza as funções de arranque PXE.

A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS.

Selecione a opção de ativar o **suporte PXE para os clientes**e, em seguida, configurar as seguintes definições:  

> [!Note]  
> Selecione **Sim** na caixa de diálogo Exigida para a **revisão para** confirmar que pretende ativar o PXE. O Gestor de Configuração configura automaticamente as portas predefinidas na firewall do Windows. Se utilizar uma firewall diferente, configure manualmente as portas.  
>
> Se instalar WDS e DHCP no mesmo servidor, configure o WDS para ouvir uma porta diferente. Por defeito, o DHCP ouve na mesma porta. Para obter mais informações, veja [Considerações sobre quando tiver o WDS e DHCP no mesmo servidor](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Permita que este ponto de distribuição responda aos pedidos de PXE que chegam**: Especifique se permite que a WDS responda aos pedidos de serviço PXE. Utilize esta definição para ativar e desativar o serviço sem remover a funcionalidade PXE do ponto de distribuição.  

- **Ativar suporte de computador desconhecido**: Especifique se permite o suporte para computadores que o Gestor de Configuração não gere. Para mais informações, consulte [Prepare-se para implementações de computadordesconhecidas](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **Ativar um serviço de resposta PXE sem o Serviço**de Implementação do Windows : A partir da versão 1806, esta opção permite um resposta PXE no ponto de distribuição, o que não requer WDS. Este resposta PXE suporta redes IPv6. Se ativar esta opção num ponto de distribuição já ativado por PXE, o Gestor de Configuração suspende o serviço WDS. Se desativar esta opção, mas ainda assim ativar o **suporte PXE para os clientes,** então o ponto de distribuição volta a ativar o WDS.<!--1357580-->  

    > [!Note]  
    > Na versão 1810 e anterior, não é suportado para usar o resposta PXE sem WDS em servidores que também estão executando um servidor DHCP.
    >
    > A partir da versão 1902, quando ativa um xeque PXE num ponto de distribuição sem o Windows Deployment Service, pode agora estar no mesmo servidor que o serviço DHCP. <!--3734270-->  

- **Exija uma palavra-passe quando os computadores usam PXE**: Para fornecer segurança adicional para as suas implementações PXE, especifique uma palavra-passe forte.  

- **Afinidade do dispositivo do utilizador**: Especifique como pretende que o ponto de distribuição associe os utilizadores ao computador de destino para implementações de PXE. Selecione uma das seguintes opções:  

  - **Permitir a finidade**do dispositivo do utilizador com a aprovação automática : Escolha esta definição para associar automaticamente os utilizadores ao computador de destino sem esperar pela aprovação.  

  - **Permitir a afinidade**do utilizador pendente de aprovação do administrador : Escolha esta definição para aguardar a aprovação de um utilizador administrativo antes que os utilizadores estejam associados ao computador de destino.  

  - **Não permita a finção**do dispositivo do utilizador : Escolha esta definição para especificar que os utilizadores não estão associados ao computador de destino. Esta é a predefinição.  

    Para obter mais informações sobre a finção do dispositivo do utilizador, consulte [os utilizadores e dispositivos do Link com a finidade](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .  

- **Interfaces de rede**: Especificar que o ponto de distribuição responde aos pedidos de PXE de todas as interfaces de rede ou de interfaces de rede específicas. Se o ponto de distribuição responder a interfaces de rede específicas, forneça o endereço MAC para cada interface de rede.  

    > [!Note]  
    > Ao alterar a interface de rede, reinicie o serviço WDS para se certificar de que guarda corretamente a configuração. A partir da versão 1806, quando utilizar o serviço de resposta PXE, reinicie o **Serviço de Resposta ConfigMgr PXE** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Especifique o atraso de resposta do servidor PXE (segundos)**: Quando utilizar vários servidores PXE, especifique quanto tempo este ponto de distribuição ativado pelo PXE deve esperar antes de responder aos pedidos do computador. Por predefinição, o ponto de distribuição ativado pelo Gestor de Configuração PXE responde imediatamente.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a>Multicast  

Especifique se permite o multicast no ponto de distribuição. As implementações multicast conservam a largura de banda da rede enviando simultaneamente dados para vários clientes do Gestor de Configuração. Sem multicast, o servidor envia uma cópia dos dados a cada cliente sobre uma ligação separada. Para obter mais informações sobre a utilização de multicast para implementação de OS, consulte [Utilizar o multicast para implementar o Windows através da rede](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Quando ativa o Multicast, o Gestor de Configuração instala os Serviços de Implementação do Windows (WDS) no servidor, se necessário.  

Selecione a opção de ativar o **multicast para simultaneamente enviar dados para vários clientes,** e, em seguida, configurar as seguintes definições:  

- **Conta de Ligação Multicast**: Especifique a conta a utilizar quando configurar as ligações de base de dados do Gestor de Configuração para o multicast. Para mais informações, consulte a conta de [ligação Multicast](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Definições de endereço seletos**: Especifique os endereços IP para o envio de dados para os computadores de destino. Por predefinição, obtém o endereço IP de um servidor DHCP que está habilitado a distribuir endereços multicast. Dependendo do ambiente da rede, pode especificar uma gama de endereços IP de 239.0.0.0 a 239.255.255.255.  

    > [!IMPORTANT]  
    > Os endereços IP que configura devem ser acessíveis pelos computadores de destino que solicitam a imagem de OS. Verifique se os routers e firewalls permitem tráfego multicast entre o computador de destino e o ponto de distribuição.  

- Gama de portau-se **a várias castas:** Especifique a gama de portas UDP que são utilizadas para enviar dados para os computadores de destino.  

    > [!IMPORTANT]  
    > As portas uDP devem ser acessíveis pelos computadores de destino que solicitam a imagem de OS. Verifique se os routers e firewalls permitem tráfego multicast entre o computador de destino e o servidor do site.  

- **Clientes máximos**: Especifique o número máximo de computadores de destino que podem descarregar a imagem de OS a partir deste ponto de distribuição.  

- Ativar o **multicast programado:** Especifique como o Gestor de Configuração controla quando começar a implantar sistemas operativos para computadores de destino. Configure as seguintes opções:  

    - Atraso de início da **sessão (minutos)**: Especifique o número de minutos que o Gestor de Configuração aguarda antes de responder ao primeiro pedido de implantação.  

    - **Tamanho mínimo da sessão (clientes)**: Especifique quantos pedidos devem ser recebidos antes de o Gestor de Configuração começar a implementar o sistema operativo.  

> [!IMPORTANT]  
> A partir da versão 1806, para ativar e configurar o multicast no separador **Multicast** das propriedades do ponto de distribuição, o ponto de distribuição deve utilizar o Serviço de Implementação do Windows.  
>
> - Se **ativar o suporte PXE para clientes** e ativar o **multicast para enviar simultaneamente dados a vários clientes,** então não pode **ativar um resposta PXE sem o Serviço**de Implementação do Windows .  
>
> - Se **ativar o suporte PXE para clientes** e **ativar um serviço de resposta PXE sem o Serviço de Implementação do Windows,** então não pode permitir que o **multicast envie simultaneamente enviar dados a vários clientes**  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a>Relações de grupo  

> [!NOTE]  
> Estas opções só estão disponíveis quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

Gerir os grupos de pontos de distribuição em que este ponto de distribuição é membro.  

Para adicionar este ponto de distribuição como membro a um grupo de pontos de distribuição existente, escolha **Adicionar**. Na janela Adicionar aos Grupos de Pontos de Distribuição, selecione um grupo existente e, em seguida, escolha **OK**.  

Para remover este ponto de distribuição de um grupo de pontos de distribuição, selecione o grupo na lista e, em seguida, escolha **Remover**. A remoção do ponto de distribuição de um grupo de pontos de distribuição não remove qualquer conteúdo do ponto de distribuição.

### <a name="content"></a><a name="bkmk_config-content"></a>Conteúdo  

> [!NOTE]  
> Estas opções só estão disponíveis quando está a editar as propriedades de um ponto de distribuição previamente instalado.  

Gerencie o conteúdo que distribuiu até ao ponto de distribuição. Selecione na lista de pacotes de implementação e execute as seguintes ações:  

- **Validar**: Inicie o processo para validar a integridade dos ficheiros de conteúdo do software. Para visualizar os resultados do processo de validação de conteúdos, no espaço de trabalho **de Monitorização,** expandir o Estado de **Distribuição,** e, em seguida, escolher o nó de Estado do **Conteúdo.** Para mais informações, consulte [Validar o conteúdo](deploy-and-manage-content.md#validate-content).  

- **Redistribuição**: Copia todos os ficheiros de conteúdo do software selecionado para o ponto de distribuição e substitui os ficheiros existentes. Normalmente, utiliza esta ação para reparar ficheiros de conteúdo. Para mais informações, consulte [Redistribuir o conteúdo](deploy-and-manage-content.md#redistribute-content).  

- **Remover**: Remove os ficheiros de conteúdo do software do ponto de distribuição. Para mais informações, consulte [Remover o conteúdo](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a>Validação de conteúdos  

Detete um calendário para validar a integridade dos ficheiros de conteúdo no ponto de distribuição. Quando ativa a validação de conteúdos numa programação, o Gestor de Configuração inicia o processo na hora programada. Verifica todos os conteúdos no ponto de distribuição com base na classe Local SMS_PackagesInContLib SCCMDP. Também pode configurar a prioridade de validação de conteúdos. Por padrão, a prioridade está definida para **o Mais Baixo**. Aumentar a prioridade pode aumentar a utilização do processador e do disco no servidor durante o processo de validação, mas deve ser concluído mais rapidamente.

Para visualizar os resultados do processo de validação de conteúdos, no espaço de trabalho **de Monitorização,** expandir o Estado de **Distribuição,** e, em seguida, escolher o nó de Estado do **Conteúdo.** Mostra o conteúdo de cada tipo de software, por exemplo, aplicação, pacote de atualização de software e imagem de arranque.  

> [!WARNING]  
> Embora especifique o calendário de validação de conteúdos utilizando a hora local para o computador, a consola Do Gestor de Configuração mostra a programação na UTC.  

Para mais informações, consulte [Validar o conteúdo](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a>Grupos de fronteira  

Gerencie os grupos de fronteira a que atribui este ponto de distribuição. Adicione o ponto de distribuição a pelo menos um grupo de fronteiras. Durante a implementação de conteúdos, os clientes devem estar num grupo de limites associado a um ponto de distribuição para utilizar esse ponto de distribuição como local de origem para o conteúdo.

Configure *relações* de grupo de limites que definam quando e aos grupos de fronteira que um cliente pode recuar para encontrar conteúdo. Para mais informações, consulte [os grupos de fronteira](boundary-groups.md).

Escolha **Adicionar** e selecione um grupo de limites existente na lista.

Para criar um novo grupo de limites para este ponto de distribuição, escolha **Criar**. Para obter mais informações sobre como criar e configurar um grupo de fronteiras, consulte [procedimentos para grupos de fronteiras](boundary-group-procedures.md).

Quando estiver a editar as propriedades de um ponto de distribuição previamente instalado, gerencie a opção de Permitir a distribuição a **pedido**. Esta opção permite que o Gestor de Configuração distribua automaticamente conteúdo para este servidor quando um cliente o solicita. Para mais informações, consulte a [distribuição de conteúdos a pedido.](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)

### <a name="schedule"></a><a name="bkmk_config-sched"></a>Horário  

> [!NOTE]  
> Estas opções só estão disponíveis quando está a editar as propriedades de um ponto de distribuição previamente instalado.
>
> Este separador só está disponível quando edita as propriedades para um ponto de distribuição que é remoto do servidor do site.  

Configure um horário que restrinja quando o Gestor de Configuração pode transferir dados para o ponto de distribuição. Restringir os dados por prioridade ou fechar a ligação por períodos de tempo selecionados.

Para restringir os dados, selecione o período de tempo na grelha e, em seguida, escolha uma das seguintes definições para **disponibilidade:**  

- **Aberto para todas as prioridades**: O Gestor de Configuração envia dados para o ponto de distribuição sem restrições. Esta definição é a predefinição para todos os períodos de tempo.  

- Permitir prioridade **média e alta:** O Gestor de Configuração envia apenas dados de prioridade média e alta prioridade para o ponto de distribuição.  

- **Permitir apenas alta prioridade:** O Gestor de Configuração envia apenas dados de alta prioridade para o ponto de distribuição.  

- **Fechado**: O Gestor de Configuração não envia nenhum dado para o ponto de distribuição.  

Configure a prioridade de **distribuição** do software no separador **Definições** de Distribuição das propriedades do software.

> [!IMPORTANT]  
> O horário baseia-se no fuso horário do local de envio, não no ponto de distribuição.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a>Limites de taxas  

> [!NOTE]  
> Estas opções só estão disponíveis quando está a editar as propriedades de um ponto de distribuição previamente instalado.  
>
> Este separador só está disponível quando edita as propriedades para um ponto de distribuição que é remoto do servidor do site.  

Configure os limites de taxa para controlar a largura de banda da rede que o Gestor de Configuração utiliza para transferir conteúdo para o ponto de distribuição. Pode escolher uma das seguintes opções:  

- **Ilimitado no envio para este destino:** O Gestor de Configuração envia conteúdo para o ponto de distribuição sem restrições de limite de tarifas. Esta é a predefinição.  

- **Modo de pulso**: Esta opção especifica o tamanho dos blocos de dados que o servidor do site envia para o ponto de distribuição. Também pode especificar um atraso de tempo entre o envio de cada bloco de dados. Utilize esta opção quando tiver de enviar dados através de uma ligação de rede de largura de banda muito baixa ao ponto de distribuição. Por exemplo, tem restrições para enviar 1 KB de dados a cada cinco segundos, independentemente da velocidade do link ou da sua utilização num dado momento.  

- **Limitado a taxas máximas**de transferência especificadas por hora : Especifique esta definição para que um site envie dados para um ponto de distribuição utilizando apenas a percentagem de tempo que configura. Quando utiliza esta opção, o Gestor de Configuração não identifica a largura de banda disponível da rede. Em vez disso, divide o tempo que pode enviar dados. O servidor envia dados por um curto período de tempo, que é seguido por períodos de tempo em que os dados não são enviados. Por exemplo, se definir limite de largura de **banda disponível** para **50%,** o Gestor de Configuração transmite dados por um período de tempo seguido de um período de tempo igual quando não são enviados dados. A quantidade real de dados, ou tamanho do bloco de dados, não é gerida. Só gere a quantidade de tempo durante o qual envia dados.  
