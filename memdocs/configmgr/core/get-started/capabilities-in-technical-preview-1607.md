---
title: Capacidades na Pré-visualização Técnica 1607
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 7ec5802a8931bc4397eaf302920f09d8597802fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721613"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1607 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1607. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Melhoramentos à Política de Atualização de Edição do Windows 10

Nesta versão, foram introduzidas as seguintes melhorias nesta política:

* Agora pode utilizar a política de upgrade da edição com pCs windows 10 que executam o cliente do Gestor de Configuração, além dos PCs do Windows 10 estão matriculados no Microsoft Intune.
* Pode fazer o upgrade do Windows 10 Professional para qualquer uma das plataformas do assistente compatível com o seu hardware.

[Leia mais sobre a Política de Atualização da Edição do Windows 10](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Experimente!

1. Utilize a informação no tópico de política de upgrade da [edição existente](../../compliance/deploy-use/upgrade-windows-version.md) para criar uma política de upgrade de edição.
2. Implemente esta política para um PC windows 10 que executa o cliente do Gestor de Configuração.
Assim que a política atingir um PC Windows de destino, o PC será reiniciado dentro de duas horas para aplicar a atualização. Não pode suprimir este recomeço. Certifique-se de que informa quaisquer utilizadores para os quais implementa a política ou agende a política para funcionar fora do horário de trabalho dos utilizadores.

### <a name="known-issue-with-this-release"></a>Problema conhecido com este lançamento
Nas definições do cliente do Gestor de Configuração, poderá ver as definições para **upgrade de edição**. Nesta versão, estas definições não estão funcionais. Utilize as instruções acima dadas para atualizar o Windows 10 para uma versão mais recente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software

A marca personalizada para o Software Center foi introduzida na versão 1602 do Gestor de Configuração. Na versão 1607 de Pré-visualização Técnica, essa marca é agora estendida a todas as caixas de diálogo associadas e notificações de barras de tarefas para proporcionar uma experiência mais consistente aos utilizadores do Software Center.

### <a name="try-it-out"></a>Experimente!

A marca personalizada para o Centro de Software é aplicada de acordo com as seguintes regras:

1. Se a função do site do site do Catálogo de Aplicações não estiver instalada, então o Software Center apresentará o nome da organização especificado no nome de organização de definição de cliente do **Agente Informático** exibido no Centro de **Software**. Para obter instruções, consulte [Como configurar as definições do cliente](../../core/clients/deploy/configure-client-settings.md).

2. Se a função do site do site do Catálogo de Aplicações for instalada, então o Software Center apresentará o nome e a cor da organização especificados nas propriedades do servidor do site do site do Catálogo de Aplicações. Para mais informações, consulte opções de configuração para o ponto de site do Catálogo de [Aplicações.](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)

3. Se uma subscrição do Microsoft Intune estiver configurada e ligada ao ambiente do Gestor de Configuração, então o Software Center apresentará o nome, cor e logotipo da empresa especificados nas propriedades de subscrição intune.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Utilize o mesmo adaptador de rede para múltiplas implementações iniciadas pelo PXE
Na versão 1607 de Pré-visualização Técnica, quando utiliza um adaptador de ethernet para imagem de vários dispositivos (como um adaptador USB ethernet que utiliza em vários dispositivos), pode ativar uma nova definição que lhe permite introduzir identificadores de hardware para os adaptadores de ethernet. O Gestor de Configuração ignora os identificadores de hardware na lista ao realizar uma instalação PXE e para o registo do cliente.

Para mais informações sobre este problema, consulte o Blog da Equipa de [Apoio ao Sistema de Suporte osd do Gestor](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/)de Configuração .  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Ativar a funcionalidade para gerir identificadores de hardware duplicados  
1. Na consola de Configuração Manager, vá a Atualizações de**Overview** > **Serviços** > cloud e**funcionalidades**de**serviços** > de manutenção da **Administração.** > 
2. No painel de visualização, selecione **Gerir identificadores de hardware duplicados**.
3. No separador **Home,** no grupo **Funcionalidades,** clique **em Ligar**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Adicione identificadores de hardware para o Gestor de Configuração ignorar  
1. Na consola do Gestor de Configuração, vá a**Sites**de**Configuração** > do Site de**Visão Geral** > da **Administração** > .
2. No separador **Home Page** , no grupo **Sites** , clique em **Definições de Hierarquia**.
3. Vá ao separador De Aprovação de **Clientes e Registos Contraditórios.**
4. Clique em **Adicionar** na secção **de identificadores de hardware Duplicate** para adicionar novos identificadores de hardware.
