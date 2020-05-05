---
title: Configurar classificações e produtos
titleSuffix: Configuration Manager
description: Siga estes passos para configurar classificações e produtos de atualização de software para sincronizar na consola 'Gestor de Configuração'.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 7e2cc1c2dc52a0bb6eb8d0dd143cbb2d005dc6e9
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078469"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Configure classificações e produtos para sincronizar  

*Aplica-se a: Gestor de Configuração (ramo atual)*

O software atualiza os metadados durante o processo de sincronização no Gestor de Configuração com base nas definições que especifica nas propriedades dos componentes do Software Update Point. Depois de sincronizar as atualizações de software pela primeira vez, ou quando forem lançados novos produtos e classificações, deve ir às propriedades para selecionar os novos itens. Utilize o seguinte procedimento para configurar classificações e produtos a sincronizar.  

> [!NOTE]  
> Utilize o procedimento desta secção apenas no site de nível superior.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Para configurar classificações e produtos a sincronizar  

1. Na consola de Gestor de **Configuração,** navegue para**sites**de**configuração** > do site **da administração.** > 

2. Selecione o site da administração central ou o local primário autónomo.  

3. No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.

4. No separador **Classificações** , especifique as classificações de atualização de software para as quais quer sincronizar atualizações de software.  

    Cada atualização de software é definida com uma classificação de atualização que ajuda a organizar os diferentes tipos de atualizações. Durante o processo de sincronização, serão sincronizados os metadados de atualizações de software para as classificações especificadas. O Gestor de Configuração fornece a capacidade de sincronizar atualizações de software com as seguintes classificações de atualização:  

     - **Atualizações Críticas**: Especifica uma correção amplamente lançada para um problema específico que aborda um bug crítico e não relacionado com a segurança.  
     - **Atualizações de Definição**: Especifica uma atualização de software amplamente lançada e frequente que contém adições à base de dados de definição de um produto.  
     - **Pacotes de funcionalidades**: Especifica a nova funcionalidade do produto que é distribuída pela primeira vez fora de um lançamento do produto e que é tipicamente incluída na próxima versão completa do produto.  
     - **Atualizações de Segurança**: Especifica uma correção amplamente lançada para uma vulnerabilidade específica do produto e relacionada com a segurança.  
     - **Pacotes de serviços**: Especifica um conjunto testado e cumulativo de todos os hotfixos, atualizações de segurança, atualizações críticas e atualizações que são aplicadas a um produto. Além disso, os pacotes de serviço podem conter correções adicionais para problemas que são encontrados internamente desde a libertação do produto.  
     - **Ferramentas**: Especifica um utilitário ou funcionalidade que ajuda a completar uma ou mais tarefas.  
     - **Atualização Rollups**: Especifica um conjunto testado e cumulativo de hotfixos, atualizações de segurança, atualizações críticas e atualizações que são embaladas em conjunto para uma fácil implementação. Um rollup de atualização geralmente aborda uma área específica, como um componente de segurança ou produto.  
     - **Atualizações**: Especifica uma correção amplamente lançada para um problema específico. Uma atualização aborda um bug não crítico e não relacionado com a segurança.  
     - **Upgrade**: Especifica uma atualização para funcionalidades e funcionalidades do Windows 10. Os pontos de atualização do software e os seus sites devem executar um mínimo de WSUS 6.2 com o [hotfix 3095113](https://support.microsoft.com/kb/3095113) para obter a classificação **de Upgrade.** Para obter mais informações sobre a instalação desta atualização e outras atualizações para **Atualizações,** consulte [os pré-requisitos para atualizações](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012)de software .

    > [!NOTE]
    > Pode selecionar os **controladores Microsoft Surface e atualizações de firmware** para sincronizar os controladores Microsoft Surface.<!--1098490--> Para mais informações, consulte a secção de atualizações de recortes de ['Surface' do Microsoft e firmware.](#bkmk_Surface)

5. No separador **Produtos** , especifique os produtos para os quais quer sincronizar atualizações de software e, em seguida, clique em **Fechar**.  

    - O Gestor de Configuração armazena uma lista de produtos e famílias de produtos a partir dos quais pode escolher quando instalar pela primeira vez o ponto de atualização do software. Os produtos e famílias de produtos que são lançados após o lançamento do Gestor de Configuração podem não estar disponíveis para selecionar até completar a sincronização das atualizações de software, que atualiza a lista de produtos disponíveis e famílias de produtos a partir das quais pode escolher.  

    - Os metadados para cada atualização de software definem os produtos para os quais a atualização é aplicável. Um produto é uma edição específica de um sistema operativo ou aplicação, como o Windows Server 2012. Uma família de produtos é o sistema operativo base ou a aplicação a partir da qual derivam os produtos individuais. Um exemplo de uma família de produtos é o Windows, do qual o Windows Server 2012 é membro. Pode especificar uma família de produtos ou produtos individuais dentro de uma família de produtos. Quanto mais produtos selecionar, mais tempo demora a sincronizar atualizações de software.  

    - Quando as atualizações de software são aplicáveis a vários produtos, e pelo menos um dos produtos foi selecionado para sincronização, todos os produtos aparecem na consola Do Gestor de Configuração mesmo que alguns produtos não tenham sido selecionados. Por exemplo, se o Windows Server 2012 for o único sistema operativo que selecionou, e se uma atualização de software se aplicar ao Windows 8 e ao Windows Server 2012, ambos os produtos são apresentados na consola 'Gestor de Configuração'.  

    > [!NOTE]  
    > **O Windows 10, a versão 1903 e mais tarde** foi adicionado ao Microsoft Update como seu próprio produto, em vez de fazer parte do produto **do Windows 10** como versões anteriores. Esta alteração fez com que fizesse uma série de passos manuais para garantir que os seus clientes vêem estas atualizações. Ajudamos a reduzir o número de passos manuais que tem de tomar para o novo produto na versão 1906 do Gestor de Configuração. <!--4682946-->
    >
    > Quando atualiza para a versão 1906 do Gestor de Configuração e tem o produto **Windows 10** selecionado para sincronização, as seguintes ações ocorrem automaticamente:
    > - O **Windows 10, a versão 1903 e o** produto posterior são adicionados para sincronização.
    > - As Regras de [Implementação Automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) que contêm o produto Windows **10** serão atualizadas para incluir o **Windows 10, a versão 1903 e mais tarde.**
    > - [Os planos de manutenção](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) são atualizados para incluir o **Windows 10, a versão 1903 e o** produto posterior.

## <a name="include-microsoft-surface-drivers-and-firmware-updates"></a><a name="bkmk_Surface"></a>Inclua os controladores microsoft Surface e as atualizações de firmware

Pode selecionar os **controladores Microsoft Surface e atualizações de firmware** para sincronizar os controladores Microsoft Surface.<!--1098490--> Todos os pontos de atualização de software devem executar o Windows Server 2016 com a atualização cumulativa [KB4025339](https://support.microsoft.com/help/4025339) ou posteriormente instaladopara sincronizar com sucesso os controladores do Surface. Se ativar um ponto de atualização de software num computador que executa o Windows Server 2012 depois de ativar os controladores Surface, os resultados da digitalização das atualizações do controlador não são precisos. Isto resulta em dados de conformidade incorretos apresentados na consola do Gestor de Configuração e nos relatórios do Gestor de Configuração.  

- Esta funcionalidade foi introduzida pela primeira vez na versão 1706 como [uma funcionalidade de pré-lançamento.](../../core/servers/manage/pre-release-features.md) A partir da versão 1710, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  
- O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  
- Os condutores dos dispositivos ARM não são suportados para sincronização.

## <a name="configuring-products-for-versions-of-windows-10"></a>Configurar produtos para versões do Windows 10

### <a name="windows-10-version-1909"></a>Windows 10, versão 1909

O Windows 10, versão 1909, partilha um sistema operativo comum com o Windows 10, versão 1903. Ambas as versões são servida com as mesmas atualizações cumulativas. Para mais informações sobre o Windows 10, versão 1909, consulte o [Windows 10, versão 1909 opções](https://aka.ms/1909mechanics) de entrega post.

Para garantir que tanto a versão 1909 do Windows 10 como o Windows 10, os clientes da versão 1903 instalam atualizações do Gestor de Configuração:

- Aprove as atualizações para as versões de 1909 e 1903 do Windows 10.
  - As atualizações têm diferentes títulos e regras de aplicabilidade para cada versão S.
  - A aprovação de cada atualização por versão e arquitetura do SO mantém o processo normal de aprovação dos administradores.
- Os ficheiros de instalação de atualização cumulativa são os mesmos para as versões de 1909 e 1903 do Windows 10.
  - O Gestor de Configuração só irá descarregar os ficheiros de origem da atualização uma vez.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Atualizações de funcionalidades para windows 10, versão 1909

Quando aprovar atualizações de funcionalidades para o Windows 10, versão 1909, existem algumas opções diferentes que verá:

- O Windows 10, versão 1903 clientes, é oferecido a um [Pacote de Habilitação,](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package)lançado a 12 de novembro de 2019.
  - O pacote de habilitação é um pequeno e rápido ficheiro que ativa o Windows 10, a versão 1909 funcionalidades e reinicia o dispositivo.
  - Os pré-requisitos para o pacote de habilitação incluem:
    - Uma atualização acumulada mínima de [KB4517389,](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389)lançada a 8 de outubro de 2019.
    - Uma atualização mínima de pilha de serviços de [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), lançada a 24 de setembro de 2019.
  - Esta atualização, como qualquer outra Atualização de `https:\\catalog.update.microsoft.com`Funcionalidades, não está disponível para importação a partir de .
  - A atualização sincronizará automaticamente com a WSUS se tiver a **classificação do Windows 10, versão 1903 e posterior** classificação de produto e **upgrades** selecionada para sincronização.
  - Na consola 'Gestor de Configuração', vá ao espaço de trabalho da Biblioteca de **Software,** expanda **a manutenção do Windows 10**e selecione o nó de **Atualizações do Windows 10.** Procure os termos "habilitação" ou "4517245".

    > [!TIP]
    > Uma vez que estas são atualizações de funcionalidades, não estão no nó **All Software Updates.**

- O Windows 10, a versão 1809 e os clientes anteriores são atualizados com uma única atualização de funcionalidades diretas.
  - Isto é como todas as outras instalações anteriores para Atualizações de Funcionalidades que já fez para o Windows 10.

> [!NOTE]
> Tanto o pacote de habilitação como a atualização tradicional da funcionalidade para o Windows 10, a versão 1909 mostrará como "Instalada" em relatórios, independentemente do caminho utilizado para a sua instalação.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, versão 1903 e mais tarde

**O Windows 10, a versão 1903 e mais tarde** foi adicionado ao Microsoft Update como seu próprio produto, em vez de fazer parte do produto **do Windows 10** como versões anteriores. Esta alteração fez com que fizesse uma série de passos manuais para garantir que os seus clientes vêem estas atualizações. Ajudamos a reduzir o número de passos manuais que tem de tomar para o novo produto na versão 1906 do Gestor de Configuração. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, versão 1903 e mais tarde com versão de Configuração Manager 1906
Quando atualiza para a versão 1906 do Gestor de Configuração e tem o produto **Windows 10** selecionado para sincronização, as seguintes ações ocorrem automaticamente:
- O **Windows 10, a versão 1903 e o** produto posterior são adicionados para sincronização.
- As Regras de [Implementação Automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) que contêm o produto Windows **10** serão atualizadas para incluir o **Windows 10, a versão 1903 e mais tarde.**
- [Os planos de manutenção](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) são atualizados para incluir o **Windows 10, a versão 1903 e o** produto posterior.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, versão 1903 e mais tarde com versão de Configuração Manager 1902
Se estiver a utilizar o Gestor de Configuração 1902 com clientes do Windows 10,versão 1903, terá de:
- Selecione o **Windows 10, a versão 1903 e o** produto posterior para sincronização.
- Atualize quaisquer [Regras de Implementação Automática](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) para o Windows 10, versão 1903 clientes.
- Atualizar [os planos de manutenção](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) para o Windows 10, versão 1903 clientes.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a>Programa Insider do Windows
<!--3556023-->
A partir de setembro de 2019, pode ser reparado e atualizado os dispositivos que executam o Windows Insider Preview com o 'Gestor de Configuração'. Esta alteração significa que pode gerir estes dispositivos sem alterar os seus processos normais ou ativar o Windows Update para o Negócios. Pode baixar atualizações de funcionalidades e atualizações cumulativas para o Windows Insider Preview, tal como qualquer outra atualização ou atualização do Windows 10. Para mais informações, consulte as atualizações de [funcionalidades do Windows 10 pré-lançamento](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) para publicação de blog wSUS.

Para obter mais informações sobre o suporte para o Windows Insider no 'Gestor de Configuração', consulte [suporte para windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Pré-requisitos

- Configuração Manager versão 1906 ou superior, configurado para gestão de [atualizações](../plan-design/plan-for-software-updates.md)de software .
- Dispositivos Windows 10 que executam a construção de [pré-visualização do Windows Insider](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- Uma coleção contendo os dispositivos Windows Insider.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Ativar atualizações e atualizações do Windows Insider

É necessário ativar os produtos e classificações para atualizações e atualizações do Windows Insider. Atualizações de funcionalidades, atualizações cumulativas e outras atualizações para o Windows Insider estão na categoria de **produto Pré-Lançamento do Windows Insider.**

1. Na consola de Gestor de **Configuração,** navegue para**sites**de**configuração** > do site **da administração.** > 
2. Selecione o site da administração central ou o local primário autónomo.  
3. No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.
4. No separador **Produtos,** certifique-se de que os seguintes produtos são selecionados para sincronização:
    - Pré-lançamento do Windows Insider
    - Windows 10, versão 1903 e mais tarde
5. No separador **Classificações,** certifique-se de que as seguintes classificações são selecionadas para sincronização:
    - Upgrades
    - Atualizações de Segurança
    - Atualizações (opcional)
6. Clique **em OK** para fechar as propriedades do componente do ponto de **atualização**de software .

### <a name="upgrading-windows-insider-devices"></a>Atualizar dispositivos Insider do Windows

Uma vez sincronizadas as atualizações para Windows Insiders, pode vê-las a partir da **Biblioteca** > de Software**Windows 10 a servicindo** > **todas as atualizações do Windows 10**.

![Windows Insiders apresenta atualizações para manutenção do Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Implemente atualizações de funcionalidades para o Windows Insider na sua recolha de alvos, tal como qualquer outra atualização. No entanto, irá ter em mente os seguintes itens quando estiver a implementar estas Atualizações de Funcionalidades:

- Estas atualizações serão aplicáveis a todos os clientes do Windows 10 1903 ou mais cedo, com arquitetura, edição e linguagem correspondentes.
- Existem termos de licença, a sua implementação deve aceitar os termos para ser instalado.
- Considere utilizar a prioridade da [linha nas definições](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority)do cliente .
- A Dynamic Update instala automaticamente atualizações críticas, incluindo a mais recente Atualização Cumulativa, diretamente a partir do Microsoft Update. Este comportamento começou com as Atualizações de Funcionalidades para a versão 1903 do Windows 1903. 
  - Pode [desativar](../../core/clients/deploy/about-client-settings.md#bkmk_du) explicitamente a Dynamic Update nas definições do cliente ou com um [ficheiro setupconfig.ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Para mais informações, consulte a publicação de blog [do Windows 10 Dynamic Update.](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)

Para obter mais informações sobre como implementar upgrades, consulte [o Manage Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Manter os dispositivos Insider atualizados

As atualizações cumulativas para o Windows Insider estarão disponíveis para o WSUS e por extensão para O Gestor de Configuração. Estas Atualizações Cumulativas serão lançadas numa frequência semelhante às atualizações cumulativas do Windows 10. As atualizações cumulativas do Windows Insider estão na categoria de **pré-lançamento** do Windows Insider e classificadas como **Atualizações** de Segurança ou **Atualizações**. Pode implementar as Atualizações Cumulativas para o Windows Insider utilizando o seu processo regular de atualização de software, como utilizar [regras de implementação automáticas](../deploy-use/automatically-deploy-software-updates.md) ou [implementações faseadas](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Atualizações de segurança estendidas e gestor de configuração

O programa [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) é uma opção de último recurso para os clientes que precisam de executar certos produtos legados da Microsoft após o fim do suporte. Inclui atualizações de segurança críticas e/ou importantes (conforme definido pelo [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)durante um máximo de três anos após a data de fim do suporte alargado do produto.

Os produtos que estão para além do seu ciclo de vida de suporte não são suportados para uso com O Gestor de Configuração. Isto inclui todos os produtos abrangidos pelo programa ESU. Por exemplo, o Windows 7. As atualizações de segurança lançadas no âmbito do programa ESU serão publicadas nos Serviços de Atualização do Servidor do Windows (WSUS). Estas atualizações aparecerão na consola 'Gestor de Configuração'. Embora os produtos abrangidos pelo programa ESU deixem de ser suportados para utilização com o Gestor de Configuração, a [versão mais recente do atual ramo](../../core/servers/manage/updates.md#version-details) do Gestor de Configuração pode ser utilizada para implementar e instalar atualizações de segurança do Windows lançadas no âmbito do programa. A versão mais recente também pode ser utilizada para implementar o Windows 10 para dispositivos que executam o Windows 7.

As funcionalidades de gestão de clientes não relacionadas com a gestão de atualizações de software windows ou a implementação de OS deixarão de ser testadas nos sistemas operativos abrangidos pelo programa ESU e não garantimos que continuarão a funcionar. É altamente recomendado atualizar ou migrar para uma versão atual dos sistemas operativos o mais rapidamente possível para receber apoio de gestão de clientes.


## <a name="next-steps"></a>Passos seguintes

Inicie atualizações de software sincronizando para recuperar atualizações de software com base nos novos critérios. Para mais informações, consulte as atualizações de [software Synchronize](synchronize-software-updates.md).
