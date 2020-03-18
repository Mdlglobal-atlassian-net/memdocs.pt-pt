---
title: Atualizar funcionalidades do Windows BIOS utilizando políticas de MDM no Microsoft Intune - Azure Microsoft Docs
description: Adicione um perfil de interface de configuração de firmware de dispositivo (DFCI) para gerir as definições da UEFI, tais como o CPU, hardware incorporado e opções de arranque em dispositivos Windows 10 no Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: df8f6ba6873e98663be853e134995bab640541fc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332105"
---
# <a name="use-device-firmware-configuration-interface-profiles-on-windows-devices-in-microsoft-intune-public-preview"></a>Utilize os perfis de interface de configuração de firmware do dispositivo em dispositivos Windows no Microsoft Intune (pré-visualização pública)



Quando utilizar o Intune para gerir dispositivos Autopilot, pode gerir as definições da UEFI (BIOS) depois de se matricularem, utilizando a Interface de Configuração de Firmware de Dispositivo (DFCI). Para uma visão geral dos benefícios, cenários e pré-requisitos, consulte a [visão geral do DFCI](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

O DFCI permite que [o Windows](https://docs.microsoft.com/windows/client-management/mdm/uefi-csp) passe comandos de gestão de Intune para UEFI (Interface Unificada de Firmware Extensível Extensível).

Em Intune, utilize esta função para controlar as definições de BIOS. Tipicamente, o firmware é mais resistente a ataques maliciosos. Limita o controlo dos utilizadores finais sobre o BIOS, o que é bom numa situação comprometida.

Por exemplo, utiliza dispositivos Windows 10 num ambiente seguro e pretende desativar a câmara. Pode desativar a câmara na camada de firmware, por isso não importa o que o utilizador final faz. A reinstalação do SISTEMA ou a limpeza do computador não volta a ligar a câmara. Noutro exemplo, bloqueie as opções de arranque para evitar que os utilizadores arranquem outro SISTEMA, ou uma versão mais antiga do Windows que não tenha as mesmas funcionalidades de segurança.

Quando reinstalar uma versão mais antiga do Windows, instalar um OS separado ou formatar o disco rígido, não pode sobrepor-se à gestão do DFCI. Esta funcionalidade pode impedir que o malware se comunique com processos de OS, incluindo processos de Os elevados. A cadeia de fidedignidade da DFCI usa criptografia de chaves públicas, e não depende da segurança da senha uefi (BIOS) local. Esta camada de segurança impede os utilizadores locais de acederem a definições geridas a partir dos menus UEFI (BIOS) do dispositivo.

Esta funcionalidade aplica-se a:

- Windows 10 RS5 (1809) e mais tarde no UEFI suportado

## <a name="before-you-begin"></a>Antes de começar

- O fabricante do dispositivo deve adicionar dFCI ao seu firmware UEFI no processo de fabrico, ou como uma atualização de firmware que instala. Trabalhe com os fornecedores do seu dispositivo para determinar [os fabricantes que suportam o DFCI,](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/#oems-that-support-dfci)ou a versão firmware necessária para utilizar o DFCI.

- O dispositivo deve ser registado para o Windows Autopilot por um parceiro do [Microsoft Cloud Solution Provider (CSP),](https://partner.microsoft.com/cloud-solution-provider)ou registado diretamente pelo OEM. 

  Os dispositivos registados manualmente para o Autopilot, como [importados de um ficheiro CSV,](../enrollment/enrollment-autopilot.md#add-devices)não estão autorizados a utilizar o DFCI. Por design, a gestão do DFCI requer atestado externo da aquisição comercial do dispositivo através de um OEM ou de um parceiro CSP microsoft para o Windows Autopilot.

  Uma vez registado o seu dispositivo, o seu número de série é mostrado na lista de dispositivos Do Piloto Automático do Windows.

  Para obter mais informações sobre o Autopilot, incluindo quaisquer requisitos, consulte [os dispositivos DoWindows em Intune utilizando o Windows Autopilot](../enrollment/enrollment-autopilot.md).

## <a name="create-your-azure-ad-security-groups"></a>Crie os seus grupos de segurança Azure AD

Os perfis de implantação do piloto automático são atribuídos aos grupos de segurança da AD Azure. Certifique-se de criar grupos que incluam os seus dispositivos apoiados pelo DFCI. Para dispositivos DFCI, a maioria das organizações pode criar grupos de dispositivos, em vez de grupos de utilizadores. Pondere os seguintes cenários:

- Os Recursos Humanos (HR) têm diferentes dispositivos Windows. Por razões de segurança, não queres que ninguém deste grupo use a câmara nos dispositivos. Neste cenário, pode criar um grupo de utilizadores de segurança de RH para que a política se aplique aos utilizadores do grupo HR, qualquer que seja o tipo de dispositivo.
- No piso de fabrico, tem 10 dispositivos. Em todos os dispositivos, deverá evitar o arranque dos dispositivos a partir de um dispositivo USB. Neste cenário, pode criar um grupo de dispositivos de segurança e adicionar estes 10 dispositivos ao grupo.

Para obter mais informações sobre a criação de grupos em Intune, consulte [Adicionar grupos para organizar utilizadores e dispositivos](../fundamentals/groups-add.md).

## <a name="create-the-profiles"></a>Criar os perfis

Para utilizar o DFCI, crie os seguintes perfis e atribua-os ao seu grupo.

### <a name="create-an-autopilot-deployment-profile"></a>Criar um perfil de implementação do Autopilot

Este perfil configura e pré-configura novos dispositivos. O perfil de [implementação](../enrollment/enrollment-autopilot.md#create-an-autopilot-deployment-profile) do piloto automático lista os passos para criar o perfil.

### <a name="create-an-enrollment-state-page-profile"></a>Criar um perfil de Página de Estado de Inscrição

Este perfil garante que os dispositivos são verificados e ativados para DFCI durante a configuração do Windows. É altamente recomendado usar este perfil para bloquear o uso do dispositivo até que todas as aplicações e perfis estejam instalados. [O perfil da Página do Estado de Inscrição](../enrollment/windows-enrollment-status.md) lista os passos para criar o perfil.

### <a name="create-the-dfci-profile"></a>Criar o perfil DFCI

Este perfil inclui as definições de DFCI que configura.

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **Dispositivos** > Perfis de **Configuração** > **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: Introduza um nome descritivo para o perfil. Atribua nomes às políticas de forma que possa identificá-las facilmente mais tarde. Por exemplo, um bom nome de perfil é **Windows: Configure as definições de DFCI nos dispositivos Windows**.
    - **Descrição:** introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: selecione **Windows 10 e posterior**.
    - **Tipo de perfil**: Selecione **interface de configuração de firmware**do dispositivo .

4. Configure as definições:

    - **Permitir que o utilizador local altere as definições do UEFI (BIOS):** As suas opções:
      - **Apenas definições não configuradas**: O utilizador local pode alterar qualquer *definição* exceto as definições explicitamente definidas para **ativar** ou **desativar** por Intune.
      - **Nenhuma**: O utilizador local não pode alterar nenhuma definição UEFI (BIOS), incluindo definições não mostradas no perfil DFCI.

    - **Virtualização cpu e IO**: As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado**: O BIOS permite que as capacidades de localização de CPU e IO da plataforma possam ser utilizadas pelo OS. Liga as tecnologias de Segurança e Guarda de Dispositivos baseadas na virtualização do Windows.
        - **Desativação**: O BIOS desativa as capacidades de virtualização cpu e IO da plataforma e impede que sejam utilizados.
    - **Câmaras**: As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado**: Todas as câmaras incorporadas geridas diretamente pela UEFI (BIOS) estão ativadas. Periféricos, como câmaras USB, não são afetados.
        - **Desativado**: Todas as câmaras incorporadas geridas diretamente pela UEFI (BIOS) estão desativadas. Periféricos, como câmaras USB, não são afetados.
    - **Microfones e altifalantes**: As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado**: Todos os microfones e altifalantes incorporados diretamente geridos pela UEFI (BIOS) estão ativados. Periféricos, como dispositivos USB, não são afetados.
        - **Desativado**: Todos os microfones e altifalantes incorporados diretamente geridos pela UEFI (BIOS) estão desativados. Periféricos, como dispositivos USB, não são afetados.
    - **Rádios (Bluetooth, Wi-Fi, NFC, etc.)** : As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado**: Todos os rádios incorporados diretamente geridos pela UEFI (BIOS) estão ativados. Periféricos, como dispositivos USB, não são afetados.
        - **Desativado**: Todos os rádios incorporados diretamente geridos pela UEFI (BIOS) estão desativados. Periféricos, como dispositivos USB, não são afetados.

        > [!WARNING]
        > Se desativar a definição de **Rádios,** o dispositivo necessita de uma ligação de rede com fios. Caso contrário, o dispositivo pode ser incontrolável.

    - **Arranque a partir de meios externos (USB, SD)** : As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado:** UEFI (BIOS) permite o arranque do armazenamento de unidades não rígidas.
        - **Desativado:** O UEFI (BIOS) não permite o arranque do armazenamento de unidades não rígidas.
    - **Arranque dos adaptadores de rede**: As suas opções:
        - **Não configurado**: Intune não toca nesta funcionalidade e deixa quaisquer configurações como está.
        - **Ativado:** UEFI (BIOS) permite o arranque a partir de interfaces de rede incorporadas.
        - **Desativado**: UEFI (BIOS) não permite o arranque de interfaces de rede incorporadas.

5. Assim que terminar, selecione **OK** > **Criar** para guardar as alterações. O perfil é criado e apresentado na lista.

## <a name="assign-the-profiles-and-reboot"></a>Atribuir os perfis e reiniciar

Depois de os perfis serem criados, estão [prontos para serem atribuídos.](../configuration/device-profile-assign.md) Certifique-se de atribuir os perfis aos seus grupos de segurança Azure AD que incluem os seus dispositivos DFCI.

Quando o dispositivo executa o Windows Autopilot, durante a página 'Estado de Inscrição', o DFCI pode forçar um reboot. Este primeiro reboot inscreve UEFI para Intune. 

Se quiser confirmar que o dispositivo está matriculado, pode reiniciar o dispositivo novamente, mas não é necessário. Utilize as instruções do fabricante do dispositivo para abrir o menu UEFI e confirme que o UEFI está agora gerido.

Da próxima vez que o dispositivo sincronizar com intune, o Windows recebe as definições de DFCI. Reiniciar o dispositivo. Este terceiro reboot é necessário para que a UEFI receba as definições de DFCI a partir do Windows.

## <a name="update-existing-dfci-settings"></a>Atualizar as definições dFCI existentes

Se quiser alterar as definições de DFCI existentes nos dispositivos que estão a ser utilizados, pode. No seu perfil DFCI existente, altere as definições e guarde as suas alterações. Uma vez que o perfil já está atribuído, as novas definições de DFCI têm efeito quando:

1. O dispositivo faz o check-in com o serviço Intune para rever as atualizações de perfis. Os check-ins acontecem em várias ocasiões. Para mais informações, consulte quando os [dispositivos obtêm uma política, perfil ou atualizações de aplicações.](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)

2. Para impor as novas definições, reinicie o dispositivo remotamente ou [localmente.](../remote-actions/device-restart.md)

Também pode [sinalizar dispositivos para fazer o check-in](../remote-actions/device-sync.md). Depois de uma sincronização bem sucedida, [sinal para reiniciar](../remote-actions/device-restart.md).

>[!NOTE]
> Eliminar o perfil DFCI ou remover um dispositivo do grupo atribuído ao perfil não remove as definições de DFCI nem reativa os menus UEFI (BIOS). Se pretender parar de utilizar dFCI, atualize o perfil DFCI existente. Para obter mais informações sobre os passos, consulte [retire o dispositivo](#retire) neste artigo.

## <a name="reuse-retire-or-recover-the-device"></a>Reutilizar, reformar-se ou recuperar o dispositivo

### <a name="reuse"></a>Reutilização

Se planeia redefinir o Windows para reutilizar o dispositivo, [então limpe o dispositivo](../remote-actions/devices-wipe.md). **Não** retire o registo do dispositivo Autopilot.

Depois de limpar o dispositivo, mova o dispositivo para o grupo designado para os novos perfis DFCI e Autopilot. Certifique-se de que reinicia o dispositivo para reexecutar a configuração do Windows.

### <a name="retire"></a>Extinguir

Quando estiver pronto para retirar o dispositivo e libertá-lo da gestão, atualize o perfil DFCI para as definições da UEFI (BIOS) que deseja no estado de saída. Normalmente, deseja todas as definições ativadas. Por exemplo:

1. Abra o seu perfil DFCI (Perfis de **Configuração**de**Dispositivos** > ).
2. Altere o **utilizador local para alterar as definições UEFI (BIOS)** para **apenas configurações não configuradas**.
3. Detete todas as outras definições para **Não configurar**.
4. Guarde as suas definições.

Estes passos desbloqueiam os menus UEFI (BIOS) do dispositivo. Os valores permanecem os mesmos que o perfil (**Ativado** ou **Desativado)** e não são reparados em quaisquer valores de Os padrão.

Está pronto para limpar o dispositivo. Uma vez que o dispositivo seja apagado, elimine o registo do Piloto Automático. A eliminar o registo impede que o dispositivo se reinscreva automaticamente quando reinicia.

### <a name="recover"></a>Recuperar

Se limpar um dispositivo e apagar o registo do Autopilot antes de desbloquear os menus UEFI (BIOS), os menus permanecem bloqueados. Intune não pode enviar atualizações de perfil para desbloqueá-lo.

Para desbloquear o dispositivo, abra o menu UEFI (BIOS) e refresque a gestão da rede. A recuperação desbloqueia os menus, mas deixa todas as definições DAFI (BIOS) definidas para os valores no perfil DFCI intune anterior.

## <a name="end-user-impact"></a>Impacto do utilizador final

Quando a política dFCI é aplicada, os utilizadores locais não podem alterar as definições configuradas pelo DFCI, mesmo que o menu UEFI (BIOS) esteja protegido por palavra-passe. Dependendo das definições que configura, os utilizadores finais podem receber erros que os componentes de hardware não sejam encontrados ou não possam ser diagnosticados. Certifique-se de fornecer documentação aos utilizadores finais explicando as opções que desativou.  

## <a name="next-steps"></a>Próximos passos

Depois de atribuído o perfil, [monitorize o seu estado](device-profile-monitor.md).
