---
title: Instalar funções do sistema de sites
titleSuffix: Configuration Manager
description: Adicione as funções do sistema do site a um servidor de sistema de site existente ou novo no site.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 102d07f29b9addd1f2c37dd741db09e972cd5802
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718841"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Instalar funções de sistema de site para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Existem dois métodos na consola Do Gestor de Configuração para instalar funções do sistema do site:

- **Adicionar funções**de sistema do site : Adicionar as funções do sistema do site a um servidor de sistema de site existente no site.

- Criar o Servidor do Sistema do **Site:** Especifique um novo servidor como servidor de sistema de site e, em seguida, instale uma ou mais funções. Este método é o mesmo que as **Funções**do Sistema adicionar site, exceto na primeira página. Primeiro especifica o nome do servidor e o site no qual pretende instalá-lo.

> [!TIP]
> Quando instala uma função num computador remoto, o Gestor de Configuração adiciona a conta de computador do computador remoto a um grupo local no servidor do site.
>
> Quando instala o site num controlador de domínio, o grupo no servidor do site é um grupo de domínio em vez de um grupo local. Neste caso, a função do sistema de site remoto não funciona imediatamente. O servidor do sistema do site precisa de reiniciar, ou atualiza o bilhete Kerberos para a conta de computador do servidor remoto. Para mais informações, consulte [contas utilizadas](../../../plan-design/hierarchy/accounts.md).

Antes de instalar a função do sistema do site, o Gestor de Configuração verifica o computador de destino para se certificar de que cumpre os pré-requisitos para as funções selecionadas.

Por predefinição, quando o Gestor de Configuração instala uma função do sistema de site, instala ficheiros na primeira unidade de disco formada ntfs disponível que tem o espaço de disco gratuito mais disponível. Para evitar que o Gestor de Configuração instale em unidades específicas, antes de instalar o servidor do sistema do site, crie um ficheiro vazio chamado **no_sms_on_drive.sms** na raiz da unidade.

O Gestor de Configuração utiliza a conta de **instalação** do sistema do site para instalar funções. Especifica esta conta quando instala a função. Por padrão, esta conta é a conta do sistema local do computador servidor do site. Pode especificar uma conta de utilizador de domínio como conta de instalação do sistema do site. Para mais informações, consulte Contas - Conta de [instalação do sistema do site](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a>Instale funções num servidor de sistema de site existente

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a configuração do **site,** e selecionar o nó de **Funções de Servidores e Derôs** o sistema. Selecione o servidor do sistema de site existente no qual pretende instalar novas funções do sistema do site.

1. Na fita, no separador **Home,** no grupo **Server,** selecione **Adicionar Funções**do Sistema do Site .

1. Na página **Geral,** reveja as definições.

    > [!TIP]
    >  Para aceder à função do sistema do site a partir da internet, certifique-se de que especifica um nome de domínio totalmente qualificado (FQDN) na Internet.

1. Na página **Proxy,** se as funções neste servidor requerem um proxy de internet, então especifique as definições para um servidor proxy. Para mais informações, consulte o [suporte do servidor Proxy](../../../plan-design/network/proxy-server-support.md).

1. Na página de Seleção de Funções do **Sistema,** selecione as funções do sistema do site que pretende adicionar.

1. Conclua o assistente. Podem aparecer páginas adicionais para funções específicas. Para mais informações, consulte as opções de [Configuração para funções do sistema do site](configuration-options-for-site-system-roles.md).

> [!TIP]
> O cmdlet Windows PowerShell, **New-CMSiteSystemServer,** desempenha a mesma função que este procedimento. Para mais informações, consulte [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a>Instale funções num novo servidor de sistema de site

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a configuração do **site,** e selecionar o nó de **Funções de Servidores e Derôs** o sistema.

1. Na fita, no separador **Home,** no grupo **Criar,** selecione **Criar servidor de sistema**de site .

1. Na página **Geral,** especifique as definições gerais para o sistema de site.

    > [!TIP]
    > Para aceder à função do novo sistema de site a partir da internet, certifique-se de que especifica uma Internet FQDN.

1. Na página **Proxy,** se as funções neste servidor requerem um proxy de internet, então especifique as definições para um servidor proxy. Para mais informações, consulte o [suporte do servidor Proxy](../../../plan-design/network/proxy-server-support.md).

1. Na página de Seleção de Funções do **Sistema,** selecione as funções do sistema do site que pretende adicionar.

1. Conclua o assistente. Podem aparecer páginas adicionais para funções específicas. Para mais informações, consulte as opções de [Configuração para funções do sistema do site](configuration-options-for-site-system-roles.md).

> [!TIP]
> O cmdlet Windows PowerShell, **New-CMSiteSystemServer,** desempenha a mesma função que este procedimento. Para mais informações, consulte [New-CMSiteSystemServer](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Passos seguintes

- [Opções de configuração para funções do sistema de sites](configuration-options-for-site-system-roles.md)

- [Remover o papel](../install/uninstall-sites-and-hierarchies.md#bkmk_role)
