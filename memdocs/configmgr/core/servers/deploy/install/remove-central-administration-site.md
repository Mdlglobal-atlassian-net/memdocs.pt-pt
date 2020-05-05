---
title: Remover o CAS
titleSuffix: Configuration Manager
description: Remova o site da administração central (CAS) para simplificar a sua infraestrutura de Gestor de Configuração para um único local primário autónomo.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6704075d707306f55a50a937185c9bdd28b18cc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718113"
---
# <a name="remove-the-central-administration-site"></a>Remova o site da administração central

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!-- 3607277 -->

A partir da versão 2002, se a hierarquia consistir no site da administração central (CAS) e num único local primário infantil, pode remover o CAS. Esta ação simplifica a sua infraestrutura de Gestor de Configuração para um único local primário autónomo. Remove as complexidades da replicação site-to-site, e centra as suas tarefas de gestão no único site.

> [!IMPORTANT]
> Nesta versão do 'Gestor de Configuração', esta funcionalidade é pré-lançamento e não está ativada por predefinição. Atualmente está disponível para clientes Microsoft Premier.
>
> Para ativar esta funcionalidade, contacte o gestor de conta técnica para obter assistência:
>
> - O seu TAM abre um caso consultivo, que utilizará as suas horas premier da Microsoft.
> - Não pode mudar a gravidade do caso.
> - O Microsoft Support irá ajudar estes casos de aconselhamento durante o horário normal de trabalho durante a semana.

## <a name="plan"></a>Planear

- A hierarquia tem de ser constituída pelo CAS e por um único local primário infantil. O local principal pode ter locais secundários. Para remover outros locais primários infantis da hierarquia, reveja as etapas de planeamento e os pré-requisitos para [desinstalar um local primário](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Certifique-se de que o local primário do seu filho satisfaz os requisitos de tamanho e escala para um [local primário autónomo](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Mova ou retire quaisquer funções do site no CAS, exceto o ponto de ligação de serviço e o ponto de atualização do software. A configuração do Gestor de Configuração trata destas duas funções quando remove o CAS.

  As seguintes funções são mais comuns no CAS, que precisa de se reformar ou mudar-se para o local principal:

  - Ponto de sincronização da Inteligência de Ativos
  - Ponto de Endpoint Protection
  - Ponto do Reporting Services
  - Ponto de serviço de armazém de dados
  - Gateway de gestão de nuvem (CMG)

    > [!NOTE]
    > Se ativar o CMG para conteúdos, planeie redistribuir o conteúdo depois de recriar o CMG no site principal.<!-- 6608659 -->

- Desligue as vistas distribuídas

- O Gestor de Configuração lida automaticamente com as localizações de origem de pacotes para pacotes incorporados, como o cliente do Gestor de Configuração. Reveja todos os outros locais de origem de conteúdo para se certificar de que não estão a usar uma parte no CAS.

- Pare com quaisquer trabalhos de migração ativos e remova todas as configurações para a migração. Para mais informações, consulte Parar a [migração ativa de outra hierarquia.](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy)

- Se utilizar regras de implementação automáticas para atualizações de software, recrie-as no site primário da criança.

- Se utilizar o Gestor de Configuração ou o System Center Updates Publisher para gerir [atualizações de software de terceiros,](../../../../sum/deploy-use/third-party-software-updates.md)exporte o certificado de assinatura WSUS a partir do ponto de atualização do software no CAS.

  - Antes de remover o CAS, aguarde os prazos de quaisquer implementações necessárias de atualizações de software de terceiros. Os clientes pré-descarregam os conteúdos para implementações necessárias e, quando alterao o ponto de atualização de software, o hash de conteúdo muda com *a publicação local* de atualizações de software. (Este comportamento não afeta outros tipos de conteúdo, apenas a publicação local de atualizações de software de terceiros.) Se remover o CAS com estas implementações necessárias ainda em curso, eles falharão nos clientes com um erro de incompatibilidade de hash.

- Reveja qualquer software de terceiros que possa ter uma dependência do CAS.

## <a name="prerequisites"></a>Pré-requisitos

- O utilizador administrativo que executa a configuração do Gestor de Configuração precisa dos seguintes direitos de segurança:

  - **Direitos** do Administrador Local no servidor CAS

  - Se o servidor de base de dados CAS estiver remoto do servidor do site, os direitos do **Administrador** local no servidor de base de dados do site remoto para o CAS.

  - **Direitos de sisadmina** na base de dados do site CAS

  - **Direitos** do Administrador Local no servidor do site principal

  - Se o servidor de base de dados do site primário estiver remoto do servidor do site principal, os direitos do **Administrador** local no servidor de base de dados do site remoto para o site principal.

  - **Direitos de sisadmina** na base de dados do site primário

  - **Administrador de Infraestruturas** ou papel de segurança **do Administrador Completo** no CAS e local primário

- Apenas um local primário infantil na hierarquia. Para mais informações, consulte [Desinstalar um site primário](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Processo

1. Configurar o Gestor de Configuração no servidor CAS utilizando um dos seguintes métodos:

    - No menu **Iniciar,** selecione Configuração do Gestor de **Configuração**.

    - No diretório para os meios de `\SMSSETUP\BIN\X64\setup.exe`instalação do Gestor de *Configuração,* aberto. Certifique-se de que esta versão é a mesma que a versão do site.

    - No diretório onde o Gestor de `\BIN\X64\setup.exe`Configuração está *instalado,* aberto.

1. Reveja as informações na página **Antes de Começar.**

1. Na página **Getting Started,** selecione **Executar a manutenção do site ou redefinir este site**.

1. Na página de Manutenção do **Site,** selecione Remover o site da **administração central**. <!-- or is it still "delete"? -->

1. Na página de Reconfiguração de Funções do **Sistema do Site Existente:**

    - **Ponto de ligação**ao serviço : Introduza o nome de domínio totalmente qualificado do sistema do site no local principal para acolher esta função necessária. Para mais informações, consulte sobre o ponto de [ligação ao serviço](../configure/about-the-service-connection-point.md).

    - **Ponto de atualização**de software : Selecione um ponto de atualização de software existente no site principal. Configuração configura esta atualização de software aponta para sincronizar o mesmo que a configuração CAS.

    A configuração verifica se os servidores especificados cumprem os pré-requisitos. Selecione **Iniciar Instalar** quando estiver pronto para continuar.

Se a configuração se deparar com um problema, utilize o assistente para voltar a tentar o processo.

Quando a configuração estiver concluída, repõe o local principal. Para mais informações, consulte [Executar um reset](../../manage/modify-your-infrastructure.md#bkmk_reset)do site .

## <a name="monitor-and-verify"></a>Monitorizar e verificar

Reveja os seguintes registos durante o processo de configuração:

- `C:\ConfigMgrSetup.log`no servidor CAS

- **hman.log** no diretório de logs do Gestor de Configuração no servidor do site primário

Utilize o nó **da Hierarquia** do Site no espaço de trabalho **de Monitorização** para visualizar as alterações à hierarquia. Por exemplo, o seguinte gráfico mostra o antes e o depois da comparação do **SHY** **CAS,** do local primário haw e do site secundário **VWT:**

| Antes  | Depois   |
|---------|---------|
|![Vista de hierarquia do site de exemplo de um CAS, local primário e local secundário](media/3607277-cas-primary-secondary.png)|![Vista hierárquica do site do site primário e local secundário](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Tarefas pós-configuração

Depois de remover o CAS, reveja os seguintes passos à medida que se aplicam ao seu ambiente.

- Remova manualmente a conta do servidor CAS dos grupos locais do local do local do local.

- A chave de raiz fidedigna alterada, que pode requerer ações adicionais:

  - Atualize as imagens de boot de implementação do SISTEMA para incluir os mais recentes binários do Gestor de Configuração.

  - Recrie [os meios de implantação do OS](../../../../osd/deploy-use/create-task-sequence-media.md).

- Se ligar o Gestor de Configuração ao [Monitor Azure,](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context)tem de redefinir a ligação. O primeiro passo para resolver quaisquer problemas é [renovar a chave secreta.](../configure/azure-services-wizard.md#bkmk_renew) Se isso não resolver o problema, recrie a ligação.<!-- 5584635 -->

- Na versão 2002, se ativar a sincronização dos controladores Surface, reconfigure esta funcionalidade depois de remover o CAS. Para mais informações, consulte [Incluir os controladores Microsoft Surface e as atualizações de firmware](../../../../sum/get-started/configure-classifications-and-products.md#bkmk_Surface).<!-- 5728727 -->

- Se gerir atualizações de software de terceiros:

  1. Exporte o certificado de assinatura WSUS a partir do ponto de atualização de software no CAS, se ainda não o fez.

  1. Antes de criar novas implementações, remova a atualização de quaisquer implementações existentes e pacotes de atualização de software.

  1. Para recuperar os metadados de atualização de software num estado utilizável, ressincronizar os catálogos subscritos. Também pode esperar que o Gestor de Configuração ressincronizasse automaticamente.

  1. Inicie ou aguarde um processo normal de sincronização de atualização de software para atualizar o Gestor de Configuração com o estado atual da WSUS. Opcionalmente, utilize cmdlets SCUP ou WSUS PowerShell para eliminar e ler atualizações.

  1. Republique conteúdo para atualizações que precisa de implementar.
