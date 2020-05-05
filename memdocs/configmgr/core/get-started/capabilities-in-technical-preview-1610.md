---
title: Capacidades na Pré-visualização Técnica 1610
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 6402205ae694d719845492b1af37000a0b9335c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721473"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1610 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*



Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1610. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrar pelo tamanho do conteúdo nas regras de implementação automática
Agora pode filtrar o tamanho do conteúdo para atualizações de software em regras de implementação automática. Por exemplo, pode definir o filtro **Content Size (KB)** para **< 2048** para apenas descarregar atualizações de software inferiores a 2MB. A utilização deste filtro impede que as grandes atualizações de software descarreguem automaticamente para um melhor suporte a uma manutenção simplificada do Windows quando a largura de banda da rede é limitada. Para mais detalhes, consulte o Gestor de Configuração e a Manutenção Simplificada do [Windows em sistemas operativos](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)de nível inferior .

#### <a name="to-configure-the-content-size-field"></a>Para configurar o campo tamanho do conteúdo
Para configurar o campo Tamanho de **Conteúdo (KB),** vá à página de **Atualizações** de Software no Assistente de Regra de Implementação Automática criar um ADR ou vá ao separador **Deatualizações** de Software nas propriedades para um ADR existente.

![Campo de tamanho de conteúdo](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Melhor funcionalidade para os diálogos de software necessários
Quando um utilizador recebe o software necessário, a partir do **Snooze e lembre-me:** definição, eles podem selecionar a partir da seguinte lista de valores:
- Posteriormente: especifica que as notificações são agendadas com base nas definições de notificação configuradas nas definições do Cliente.
- Tempo fixo: especifica que a notificação será agendada para ser exibida novamente após o tempo selecionado. Por exemplo, se um utilizador selecionar 30 minutos, a notificação será exibida novamente em 30 minutos.

![Página do Agente de Computador estoirar nas definições do Agente Cliente](media/computeragentsettings.png)

O tempo máximo de soneca é sempre baseado nos valores de notificação configurados nas definições do Cliente Agente em cada vez que ao longo da linha temporal de implementação. Por exemplo, se o prazo de **implantação for superior a 24 horas, lembre os utilizadores de que cada definição (horas)** na página do Agente Informático estiver configurada durante 10 horas, e seja mais de 24 horas antes do prazo aquando do lançamento do diálogo, o utilizador será apresentado com um conjunto de opções de soneca até, mas nunca superior a 10 horas. À medida que o prazo se aproxima, o diálogo mostrará menos opções, consistentes com as definições relevantes do Agente cliente para cada componente da linha temporal de implementação.

Além disso, para uma implementação de alto risco, como uma sequência de tarefas que implementa um sistema operativo, a experiência de notificação do utilizador final é agora mais intrusiva. Em vez de uma notificação transitória da barra de tarefas, cada vez que o utilizador é notificado de que é necessária manutenção crítica do software, uma caixa de diálogo como os seguintes ecrãs no computador do utilizador:

![Diálogo de software obrigatório](media/requiredsoftwaredialog.png)


Para obter mais informações:
- [Configurações para gerir implementações de alto risco](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Como configurar as definições do cliente](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negar pedidos de pedido previamente aprovados

Como administrador, pode agora negar um pedido de pedido previamente aprovado. Uma vez negado, para instalar esta aplicação posteriormente os utilizadores devem reenviar um pedido. A negação não desinstala a aplicação; pelo contrário, força a reprovação de qualquer novo pedido para essa aplicação por parte desse utilizador. Anteriormente, a recusa do pedido de pedido só estava disponível para pedidos de pedido que não tivessem sido aprovados.

#### <a name="try-it-out"></a>Experimente
Para negar um pedido aprovado pelo pedido:

1. Na consola 'Gestor de Configuração', [crie e implemente uma aplicação](../../apps/deploy-use/create-applications.md) que requer aprovação.
2. Num computador cliente, abra o Centro de Software e submeta um pedido para a aplicação.
3. Na consola 'Gestor de Configuração', aprove o pedido de aplicação.
4. Negue o pedido de aplicação aprovado: Na consola do Gestor de Configuração, navegue na Visão**Geral** > da **Biblioteca** > de Software Pedidos de**Aprovação** > de**Gestão** de Aplicações e selecione o pedido de aplicação que pretende negar.  Na fita, clique em **Negar**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Excluir clientes da atualização automática
A Pré-visualização Técnica 1610 introduz uma nova definição que pode utilizar para excluir uma coleção de clientes de instalar automaticamente versões de clientes atualizadas.  Isto aplica-se à atualização automática, bem como a outros métodos, tais como atualização baseada em atualizações de software, scripts de logon e política de grupo. Isto pode ser usado para uma coleção de computadores que precisam de maior cuidado ao atualizar o cliente. Um cliente que se encontra numa coleção excluída ignora os pedidos para instalar software de cliente atualizado.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurar a exclusão da atualização automática
Para configurar exclusões de atualização automática:
1. Na consola de Configuração, abra **as Definições da Hierarquia** sob a **configuração do site > administração, > Sites,** e, em seguida, selecione o separador **de atualização** do cliente.
2. Selecione a caixa de verificação para **Excluir clientes especificados da atualização**, e depois para **a recolha exclusão,** selecione a coleção que pretende excluir. Só é possível selecionar uma única coleção para exclusão.
3. Clique **em OK** para fechar e guardar a configuração. Depois, após a atualização da política dos clientes, os clientes da coleção excluída deixarão de instalar automaticamente atualizações para o software do cliente.

   ![Definições para exclusão automática de upgrade](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Embora a interface de utilizador indique que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para anular estas definições. A instalação de impulso do cliente e uma instalação manual do cliente podem ser usadas para anular esta configuração. Para mais detalhes, consulte a secção seguinte.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está numa coleção excluída
Enquanto uma coleção estiver configurada para ser excluída, os membros dessa coleção só podem ter o seu software cliente atualizado por um de dois métodos, que sobrepõem a exclusão:
- **Instalação de Push do Cliente** – Pode utilizar a instalação push do cliente para atualizar um cliente que se encontra numa coleção excluída. Isto é permitido, uma vez que é considerado a intenção do administrador e permite-lhe atualizar os clientes sem remover toda a coleção da exclusão.       
- **Instalação manual** do cliente – Pode atualizar manualmente os clientes que se encontram numa coleção excluída quando utilizar o seguinte interruptor de linha de comando com ccmsetup: /ignore a atualização de ***skips***

  Se tentar atualizar manualmente um cliente que seja membro da coleção excluída e não utilizar este interruptor, o cliente não instalará o novo software do cliente. Para mais informações consulte [Como instalar os Clientes do Gestor de Configuração manualmente](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Para obter mais informações sobre os métodos de instalação do cliente, consulte [como implementar clientes para computadores Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Definições de configuração do Windows Defender

Agora pode configurar as definições do cliente do Windows Defender em computadores Windows 10 matriculados no Intune utilizando itens de configuração na consola 'Gestor de Configuração'.

Especificamente, pode configurar as seguintes definições do Windows Defender:
- Permitir monitorização em tempo real
- Permitir monitorização de comportamento
- Ativar o Sistema de Inspeção de Rede
- Analisar todas as transferências
- Permitir análise de script
- Monitorizar a atividade dos ficheiros e programas
  - Ficheiros monitorizados
- Dias para controlar o software maligno resolvido
- Permitir o acesso à IU de cliente
- Agendar uma análise do sistema
  - Dia agendado
  - Horário agendado
- Agendar uma análise rápida diária
  - Horário agendado
- Limite a utilização do CPU durante uma varredura de ficheiros de arquivo
- Analisar mensagens de e-mail
- Analisar unidades amovíveis
- Scan mapeado unidades
- Ficheiros de digitalização abertos a partir de ações líquidas
- Intervalo de atualização de assinatura
- Permitir proteção da nuvem
- Solicitar amostras aos utilizadores
- Deteção de Aplicações Potencialmente Indesejadas
- Ficheiros/pastas excluídos
- Extensões de ficheiros excluídas
- Processos excluídos

> [!NOTE]
> Estas definições só podem ser configuradas em computadores clientes que executam o Windows 10 November Update (1511) e acima.

### <a name="try-it-out"></a>Experimente!

1. Na consola do Gestor de Configuração, vá **Assets e Compliance** > **Overview** > **Definições de Configuração**de**Definição** > de Conformidade, e crie um novo item de **configuração**.
2. Introduza um nome e, em seguida, selecione **O Windows 8.1 e Windows 10** em **Definições para dispositivos geridos sem o cliente do Gestor de Configuração** e clique em **Next**.
3. Certifique-se de que **todos os Windows 10 (64 bits)** e **All Windows 10 (32 bits)** são selecionados na página **Plataformas Suportadas** e, em seguida, clique em **Next**.
4. Selecione o grupo de definição **do Windows Defender** e, em seguida, clique em **Next**.
5. Configure as definições desejadas nesta página e, em seguida, clique em **Seguinte**.
6. Conclua o assistente.
7. Adicione este item de configuração a uma linha de base de configuração e implemente esta linha de base para computadores que executam o Windows 10 November Update (1511) ou acima.

> [!NOTE]
> Lembre-se de verificar a caixa de verificação de **definições não conformes** ao implementar a linha de base de configuração.

## <a name="request-policy-sync-from-administrator-console"></a>Solicitar sincronização de política da consola de administrador

Agora pode solicitar uma sincronização de política para um dispositivo móvel a partir da consola Do Gestor de Configuração, em vez de precisar de solicitar uma sincronização do próprio dispositivo. As informações do estado do pedido de sincronização estão disponíveis como uma nova coluna nas vistas do dispositivo, chamada **Remote Sync State**. O Estado também aparece na secção de **dados Discovery** do diálogo **Properties** para cada dispositivo móvel.

### <a name="try-it-out"></a>Experimente!

1. Na consola de Configuração Manager, vá **Assets e Compliance** > **Overview** > Dispositivos.
2. No menu "Ações de **Dispositivoremoto Remoto",** selecione **Enviar Pedido de Sincronização**.

Sincronização pode levar de 5 a 10 minutos. Quaisquer alterações de política estão sincronizadas com o dispositivo. Pode rastrear o estado do pedido de sincronização na coluna **Remote Sync State** na vista **Dispositivos** ou no diálogo **Properties** do dispositivo.

## <a name="additional-security-role-support"></a>Apoio adicional ao papel de segurança

Para além do Administrador Completo, as seguintes funções de segurança incorporadas têm agora acesso total a itens no nó de **Todos os Dispositivos Corporativos,** incluindo **Dispositivos Pré-Declarados,** perfis de **inscrição do iOS**e perfis de **inscrição**do Windows:
- **Gestor do Asset Intelligence**
- **Gestor de Acesso a Recursos da Empresa**

O acesso apenas a leitura a estas áreas da consola Do Gestor de Configuração ainda é concedido ao papel de Analista de **Leitura.**

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Acesso condicional para perfis VPN do Windows 10

Agora pode exigir que os dispositivos Do Windows 10 matriculados no Diretório Ativo do Azure sejam compatíveis de forma a ter acesso VPN através de perfis VPN do Windows 10 criados na consola 'Gestor de Configuração'. Isto é possível através do novo acesso condicional Enable para esta caixa de verificação de **ligação VPN** na página Método de **Autenticação** na página do assistente de perfil VPN e propriedades de perfil VPN para perfis VPN do Windows 10. Também pode especificar um certificado separado para autenticação única se permitir o acesso condicional ao perfil.

## <a name="see-also"></a>Veja também
[Pré-visualização técnica para gestor de configuração](../../core/get-started/technical-preview.md)
