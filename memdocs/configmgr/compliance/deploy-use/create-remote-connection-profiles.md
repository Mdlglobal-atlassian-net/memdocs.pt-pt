---
title: Criar perfis de ligação remota
titleSuffix: Configuration Manager
description: Utilize perfis de ligação remota do Gestor de Configuração para permitir aos seus utilizadores ligarem-se remotamente aos computadores de trabalho.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c9a06e1b7c14cda02a8029925785c2109ea4204b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712352"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Perfis de ligação remota no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize perfis de ligação remota do Gestor de Configuração para permitir que os seus utilizadores se conectem remotamente a computadores de trabalho. Estes perfis permitem-lhe implementar definições de Ligação remota de ambiente de trabalho aos utilizadores da sua hierarquia. Os utilizadores podem aceder a qualquer um dos seus computadores de trabalho primário através do Remote Desktop através de uma ligação VPN.  

> [!IMPORTANT]  
> Quando especifica as definições de perfil de ligação remota com o Gestor de Configuração, o cliente armazena as definições na política local do Windows. Estas definições podem sobrepor-se às definições do Ambiente de Trabalho Remoto que configura com outra aplicação. Além disso, se utilizar a Política do Grupo Windows para configurar as definições do Ambiente de Trabalho Remoto, as definições especificadas na Política de Grupo anularão as definições do Gestor de Configuração.

O Gestor de Configuração cria um grupo de segurança em clientes, **Remote PC Connect**. Ao implementar um perfil de ligação remota, o cliente adiciona os principais utilizadores do computador a este grupo. Um administrador local pode adicionar ou remover manualmente os utilizadores a este grupo, mas o Gestor de Configuração atualiza a adesão quando avalia o cumprimento do perfil.

> [!IMPORTANT]  
> Se a relação de afinidade do dispositivo de utilizador entre um utilizador e um dispositivo mudar, o Gestor de Configuração desativa o perfil de ligação remota e as definições do Windows Firewall para evitar ligações ao computador.

## <a name="prerequisites"></a>Pré-requisitos  

### <a name="external-dependencies"></a>Dependências externas  

- Se pretender ativar os utilizadores para se conectarem a partir da internet, instalar e configurar um servidor Gateway de Ambiente de Trabalho Remoto. Para obter mais informações sobre como instalar e configurar um servidor Remote Desktop Gateway, consulte [Remote Desktop Services - Access from anywhere](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Se os clientes executarem uma firewall baseada no hospedeiro, deve ativar o programa mstsc.exe. Quando configurar um perfil de ligação remota, ative a definição para permitir a exceção do **Windows Firewall para ligações nos domínios do Windows e em redes privadas**. Esta definição permite ao Gestor de Configuração configurar automaticamente o Windows Firewall.

    > [!TIP]
    > As definições de Política de Grupo para configurar a Firewall do Windows poderão substituir a configuração definida no Configuration Manager. Se utilizar a Política de Grupo para configurar o Windows Firewall, certifique-se de que as definições de Política de Grupo não bloqueiam mstsc.exe.

    Se os clientes executarem uma firewall diferente baseada no hospedeiro, configure manualmente esta dependência da firewall.  

### <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

- Para que um utilizador se conectem a um computador de trabalho, esse computador deve ser um dispositivo primário do utilizador. Para mais informações, consulte os [utilizadores e dispositivos do Link com afinidade](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)do dispositivo do utilizador .

- Para gerir perfis de ligação remota, a sua conta de utilizador necessita de permissões específicas no 'Gestor de Configuração'. A função incorporada **do Compliance Settings Manager** inclui as permissões necessárias para gerir estes perfis. Para mais informações, consulte a [configuração da administração baseada em papéis](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Considerações de segurança e privacidade

### <a name="security-considerations"></a>Considerações de segurança  

- Especifique manualmente a afinidade dispositivo/utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Não ative a configuração baseada no uso.

  - Antes de poder implementar um perfil de ligação remota, tem de ativar a opção de **permitir que todos os utilizadores primários do computador de trabalho conectem remotamente**. Com esta configuração, deve sempre especificar manualmente a afinidade do dispositivo do utilizador. Não considere a informação que o Gestor de Configuração recolhe dos utilizadores ou do dispositivo como autoritária. Se implementar um perfil e um utilizador administrativo de confiança não especificar a afinidade do utilizador, os utilizadores não autorizados podem receber privilégios elevados e podem ligar-se remotamente aos computadores.

  - O Gestor de Configuração recolhe informações baseadas no uso através de mensagens estatais, que é um canal de comunicação rápido mas inseguro. Para ajudar a atenuar esta ameaça, utilize a assinatura de Bloco de Mensagem de Servidor (SMB) ou o protocolo IPsec (Internet Protocol Security) entre os computadores cliente e o ponto de gestão.

- Restrinja os direitos administrativos locais no computador do servidor de site. Um administrador local no servidor do site pode adicionar manualmente membros ao grupo de segurança **Remote PC Connect** que o Gestor de Configuração cria e mantém automaticamente. Esta ação pode causar uma elevação de privilégios porque os membros recebem permissões remotas de ambiente de trabalho.

### <a name="privacy-considerations"></a>Considerações de privacidade  

Quando um utilizador se conecta remotamente a um computador de trabalho, descarrega um ficheiro .wsrdp. Este ficheiro contém o nome do dispositivo e o nome do Servidor gateway do ambiente de trabalho remoto. Estes valores são necessários para criar a sessão de Ambiente de Trabalho Remoto. O ficheiro .wsrdp é transferido e guardado localmente, de forma automática. O ficheiro será substituído da próxima vez que o utilizador executar uma sessão de Ambiente de Trabalho Remoto.  

## <a name="create-a-profile"></a>Criar um perfil

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione Perfis de **Ligação Remota**.  

1. No separador **Casa** da fita, no grupo **Criar,** selecione Criar perfil de **ligação remota**.  

1. Na página **geral** do Assistente de Perfil de **Ligação Remota Criar,** especifique um nome e uma descrição opcional para o perfil. Ambos os valores têm um limite máximo de 256 caracteres.  

1. Na página Definições de **Perfil,** especifique as seguintes definições:  

    - **Nome completo e porta do servidor Remote Desktop Gateway (opcional)**: Especifique o nome do Servidor de Gateway de Ambiente de Trabalho Remoto para utilizar para ligações. Este valor tem os seguintes requisitos:

        - O nome do servidor não pode ser superior a 256 caracteres.
        - Pode conter maiúsculas, minúsculas e caracteres numéricos.
        - Além dos`.`períodos () entre`:`segmentos e um cólon ( )`–`antes da`_`porta, os únicos caracteres especiais são traço ( ) e sublinhado ( ).
        - O Gestor de Configuração não suporta o uso de um nome de domínio internacionalizado para este valor.

    - **Permitir ligações apenas a partir de computadores que executam o Ambiente de Trabalho Remoto com a autenticação**do nível de rede : Ativado por padrão, esta definição adiciona um nível adicional de segurança para a ligação. Para mais informações, consulte o acesso ao [Ambiente de Trabalho Remoto grant](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Ativar as seguintes definições de ligação:

        - **Permitir ligações remotas a computadores de trabalho**

        - **Permitir a ligação remota de todos os utilizadores primários do computador de trabalho**

        - **Permitir exceção da Firewall do Windows para ligações em domínios do Windows e em redes privadas**

        > [!IMPORTANT]  
        > As três definições devem ser as mesmas antes de poder continuar.

        Desative estas definições apenas quando aciona rumum um perfil para desligar as ligações remotas.

1. Conclua o assistente.

O novo perfil é apresentado no nó de Perfis de **Ligação Remota** no espaço de trabalho **De Ativos e Compliance.**  

## <a name="deploy"></a>Implementação

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione Perfis de **Ligação Remota**.

1. Na lista de Perfis de **Ligação Remota,** selecione o perfil que pretende implementar. No separador **Home** da fita, no grupo **de implantação,** selecione **Deploy**.  

1. Na janela de perfil de **ligação remota de implantação,** especifique as seguintes informações:

    - **Recolha**: Navegue para selecionar a recolha do dispositivo onde pretende implementar o perfil.

    - **Remediar as regras não conformes quando suportadas**: Ativar esta definição para remediar automaticamente as definições de perfil quando não estiverem em conformidade com um dispositivo. O perfil pode ser incompatível quando não existe.

    - **Permitir a reparação fora da janela de manutenção**: Se configurar uma janela de manutenção para a recolha à qual implementa o perfil, ative esta opção para permitir que o Gestor de Configuração o reapresente fora da janela de manutenção. Para mais informações, consulte [Como utilizar as janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Gerar um alerta**: Ative esta opção para configurar um alerta de conformidade.

    - **Especifique o calendário de avaliação de conformidade para esta linha**de base de configuração : Especifique um calendário simples ou personalizado através do qual o cliente avalia o perfil.

1. Selecione **OK** para fechar a janela e criar a implementação.

### <a name="client-evaluation"></a>Avaliação do cliente

O cliente avalia o perfil quando um utilizador assina.

Se um dispositivo deixar uma coleção para a qual implementa um perfil de ligação remota, o Gestor de Configuração desativa as definições do dispositivo. No entanto, para que este processo decorra corretamente, deve ter implementado pelo menos um item de configuração ou uma linha de base de configuração que contenha um item de configuração do site.

### <a name="conflict-resolution"></a>Resolução de conflitos

Não desloque mais do que um perfil de ligação remota com configurações contraditórias para o mesmo dispositivo. Por exemplo, implementa dois perfis com configurações diferentes para a mesma coleção. Apenas configura uma implementação de um perfil para **remediar regras não conformes quando suportadas**. Esta implementação pode anular as definições no outro perfil. O Gestor de Configuração não suporta este tipo de implementação de perfil de ligação remota.

## <a name="monitor"></a>Monitorizar

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione **Implementações**. Na lista de **Implementações,** selecione a implementação do perfil de ligação remota.

Poderá rever as informações de resumo sobre a conformidade da implementação do perfil de ligação remota na página principal. Para ver informações mais detalhadas, selecione a implementação do perfil. Em seguida, no separador **Home** da fita, no grupo **de implantação,** selecione **'Ver Status**. Esta ação abre a página **'Status' de implantação.**  

A página **Estado da Implementação** contém os seguintes separadores:  

- **Conformidade**: Mostra a conformidade do perfil de ligação remota com base no número de ativos afetados.

    > [!IMPORTANT]  
    > O cliente não avalia um perfil de ligação remota se não for aplicável. No entanto, continua a ser conforme.

- **Erro**: Apresenta uma lista de todos os erros para a implementação do perfil de ligação remota selecionada com base no número de ativos afetados.

- **Não Conforme**: Apresenta uma lista de todas as regras não conformes dentro do perfil de ligação remota com base no número de ativos afetados.

- **Desconhecido**: Apresenta uma lista de todos os dispositivos que não reportaram a conformidade com a implementação do perfil de ligação remota selecionada, juntamente com o estado atual do cliente dos dispositivos.

Em qualquer separador, abra uma regra para criar um subnódoo temporário sob o nó **dos Utilizadores** no espaço de trabalho De Ativos **e Conformidade.** Este subnótono contém todos os dispositivos com o estado de conformidade do separador selecionado.

O painel **de detalhes** de ativos exibe os dispositivos com o estado de conformidade selecionado para este perfil. Abra um dispositivo na lista para apresentar informações adicionais.

## <a name="reports"></a>Relatórios

O Gestor de Configuração inclui relatórios incorporados que pode utilizar para monitorizar informações sobre perfis de ligação remota. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
> Utilize o carácter`%`wildcard () quando utilizar os parâmetros **O filtro do dispositivo** e o filtro do **utilizador** nos relatórios para as definições de conformidade.  

Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).  
