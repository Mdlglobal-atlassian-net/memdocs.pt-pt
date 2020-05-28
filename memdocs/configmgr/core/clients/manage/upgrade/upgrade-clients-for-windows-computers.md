---
title: Atualizar clientes no Windows
titleSuffix: Configuration Manager
description: Atualize os clientes em computadores Windows em 'Gestor de Configuração'.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3849f360b2f22f2f48bbe49159b610399158b29
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427768"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Como atualizar clientes para computadores Windows em 'Gestor de Configuração'

*Aplica-se a: Gestor de Configuração (ramo atual)*

Atualize o cliente do Gestor de Configuração em computadores Windows utilizando métodos de instalação do cliente ou a funcionalidade de atualização automática do cliente. Os seguintes métodos de instalação de cliente são formas válidas de atualizar o software de cliente em computadores Windows:  

- Instalação da política de grupo  

- Instalação do script de início de sessão  

- Instalação manual  

- Instalação de atualização  

Para mais informações, consulte [como implementar clientes para computadores Windows](../../deploy/deploy-clients-to-windows-computers.md).

Exclua os clientes da atualização especificando uma coleção de exclusão. Para mais informações, consulte [Como excluir os clientes da atualização](exclude-clients-windows.md). Os clientes excluídos ainda descarregam e executam o CCMSETUP, mas não atualizam.

> [!TIP]  
> Se atualizar a sua infraestrutura de servidor a partir de uma versão anterior do 'Gestor de Configuração', complete as atualizações do servidor antes de atualizar os clientes do Gestor de Configuração. Este processo inclui a instalação de todas as atualizações de filiais atuais. A mais recente atualização do ramo atual contém a versão mais recente do cliente. Atualize os clientes depois de ter instalado todas as atualizações do Gestor de Configuração.

> [!NOTE]
> Se pretender reatribuir o site aos clientes durante a atualização, especifique o novo site utilizando a `SMSSITECODE` propriedade cliente.msi. Se utilizar o valor do `AUTO` `SMSSITECODE` , também especifique `SITEREASSIGN=TRUE` . Esta propriedade permite a reatribuição automática do site durante a atualização. Para mais informações, consulte as propriedades de [instalação do Cliente - SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a>Sobre a atualização automática do cliente

Configure o site para atualizar automaticamente os clientes para a versão mais recente do Gestor de Configuração. Quando o Gestor de Configuração identifica a versão de um cliente atribuído é mais cedo do que a versão hierárquica, atualiza automaticamente o cliente. Este cenário inclui a atualização do cliente para a versão mais recente quando tenta atribuir a um site do Gestor de Configuração.  

Um cliente pode fazer upgrade automaticamente nos seguintes cenários:  

- A versão do cliente é mais antiga do que a versão usada na hierarquia.  

- O cliente no site da administração central (CAS) tem um pacote de idiomas instalado e o cliente existente não.  

- Um pré-requisito de cliente na hierarquia tem uma versão diferente da instalada no cliente.  

- Um ou mais dos ficheiros de instalação de cliente têm uma versão diferente.  

> [!NOTE]  
> Para identificar as diferentes versões do cliente do Gestor de Configuração na sua hierarquia, utilize o relatório **Contagem dos clientes do Gestor de Configuração por versões de clientes** no site da pasta de relatório - **Informação**do Cliente .  

O Gestor de Configuração cria um pacote de atualização por padrão. Envia automaticamente o pacote para todos os pontos de distribuição da hierarquia. Se fizer alterações no pacote de clientes no CAS, o Gestor de Configuração atualiza automaticamente o pacote e redistribui-o. Uma mudança de exemplo é quando adiciona um pacote de linguagem cliente. Se ativar a atualização automática do cliente, cada cliente instala automaticamente o novo pacote de linguagem cliente.

> [!NOTE]  
> O Gestor de Configuração não envia automaticamente o pacote de atualização do cliente para pontos de distribuição baseados na nuvem do Gestor de Configuração.  

Ative a atualização automática do cliente em toda a sua hierarquia. Esta configuração mantém os seus clientes atualizados com menos esforço.  

Se também gere os sistemas de site do Gestor de Configuração como clientes, determine se os inclui como parte do processo de upgrade automático. Pode excluir todos os servidores ou uma recolha específica da atualização do cliente. Algumas funções de site do Gestor de Configuração partilham o quadro do cliente. Por exemplo, o ponto de gestão e o ponto de distribuição de puxar. Estas funções atualizam-se quando atualiza o site, pelo que a versão do cliente nestes servidores atualiza ao mesmo tempo.

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a>Configurar atualização automática do cliente

Utilize o seguinte procedimento para configurar a atualização automática do cliente no CAS. Esta configuração aplica-se a todos os clientes da sua hierarquia.  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó **de Sites.**  

1. No separador **Home** da fita, no grupo **Sites,** selecione **Definições de Hierarquia**.  

1. Mude para o separador **De atualização** do cliente. Reveja a versão e a data do cliente de produção. Certifique-se de que é a versão que pretende utilizar para atualizar os seus clientes. Se não for a versão cliente que espera, poderá ter de promover o cliente de pré-produção à produção. Para mais informações, consulte como testar as atualizações dos [clientes numa coleção pré-produção.](test-client-upgrades.md)  

1. Selecione **Atualizar todos os clientes da hierarquia utilizando o cliente de produção.** Selecione **OK** para confirmar.  

1. Se não quiser que as atualizações dos clientes se apliquem aos servidores, selecione **Não atualize servidores**.  

1. Especifique o número de dias em que os dispositivos devem atualizar o cliente. Após o dispositivo receber a política, atualiza o cliente num intervalo aleatório dentro deste número de dias. Este comportamento impede um grande número de clientes simultaneamente a atualizar.

    > [!NOTE]
    > Um computador deve estar a funcionar para atualizar o cliente. Se um computador não estiver a funcionar quando está programado para receber a atualização, a atualização não ocorre. Quando o computador liga e recebe a política, marca a atualização por um tempo aleatório dentro do número permitido de dias. Se isto ocorrer após o número de dias para atualizar ter expirado, ele marca a atualização num prazo aleatório dentro de 24 horas após o computador ter sido ligado.
    >
    > Devido a este comportamento, os computadores que são desligados rotineiramente podem demorar mais tempo a atualizar do que o esperado se o tempo de upgrade programado aleatoriamente não estiver dentro do horário normal de trabalho.

1. Para excluir os clientes da atualização, selecione **Excluir clientes especificados da atualização**, e especificar a recolha para excluir. Para mais informações, consulte [Excluir os clientes da atualização](exclude-clients-windows.md).

1. Se pretender que o site copie o pacote de instalação do cliente para pontos de distribuição que tenha ativado para [conteúdo pré-encenado,](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent)selecione a opção de distribuir automaticamente o pacote de instalação do cliente para pontos de **distribuição que estão habilitados para conteúdo pré-encenado**.  

1. Selecione **OK** para guardar as definições e fechar as definições da hierarquia Propriedades.

Os clientes receberão estas definições da próxima vez que transferirem a política.

> [!NOTE]
> As atualizações do cliente honram quaisquer janelas de manutenção do Gestor de Configuração que configuraste. O fio execmgr só executa o programa de armadilhas de configuração do cliente (ccmsetup.exe) durante uma janela de manutenção. Se o dispositivo executa uma edição do Windows com um filtro de escrita, o ccmsetup tenta descarregar e instalar ao mesmo tempo. Caso contrário, o ccmsetup aleatoriamente aleatoriamente um tempo para descarregar conteúdo. Depois de descarregar conteúdo e compilar a política local, o execmgr programa a atualização do cliente durante a próxima janela de manutenção.<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>Próximos passos

Para métodos alternativos de atualização dos clientes, consulte [como implementar clientes para computadores Windows](../../deploy/deploy-clients-to-windows-computers.md).

Excluir clientes específicos da atualização automática. Para mais informações, consulte [Como excluir os clientes da atualização](exclude-clients-windows.md).
