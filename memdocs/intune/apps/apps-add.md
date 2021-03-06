---
title: Adicionar aplicações ao Microsoft Intune
titleSuffix: ''
description: Saiba como adicionar aplicações ao Microsoft Intune para poder atribuir aplicações a utilizadores e dispositivos. O Intune suporta uma grande variedade de tipos de aplicações.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: da78e0f80df31f5cb0f6236c4f85f93c05f0320a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989479"
---
# <a name="add-apps-to-microsoft-intune"></a>Adicionar aplicações ao Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Antes de configurar, atribuir, proteger ou monitorizar aplicações, deve adicioná-las ao Microsoft Intune.

Os utilizadores de aplicações e dispositivos na sua empresa (a força de trabalho da empresa) podem ter vários requisitos da aplicação. Antes de adicionar aplicações ao Intune e disponibilizá-las à sua força de trabalho, poderá ser útil avaliar e compreender alguns fundamentos da aplicação. Existem vários tipos de aplicações que estão disponíveis para o Intune. Deve determinar os requisitos da aplicação que são necessários pelos utilizadores da sua empresa, tais como as plataformas e capacidades de que a sua força de trabalho necessita. Tem de determinar se vai utilizar o Intune para gerir os dispositivos (incluindo aplicações) ou se o Intune vai gerir as aplicações sem gerir os dispositivos. Além disso, deve determinar as aplicações e capacidades de que a sua força de trabalho precisa e quem precisa delas. As informações neste artigo ajudam-no a começar.

## <a name="app-types-in-microsoft-intune"></a>Tipos de aplicações no Microsoft Intune

O Intune suporta uma grande variedade de tipos de aplicações. As opções disponíveis diferem para cada tipo de aplicação. O Intune permite-lhe adicionar e atribuir os seguintes tipos de aplicações:

| Tipos de aplicações | Instalação | Atualizações |
|---|---|---|
| Aplicações que estão na loja (aplicações da loja) | O Intune instala a aplicação no dispositivo.  | As atualizações das aplicações são automáticas. |
| Aplicações escritas internamente (linha de negócio) | O Intune instala a aplicação no dispositivo (o ficheiro de instalação é disponibilizado por si). | Tem de atualizar a aplicação. |
| Aplicações que estão incorporadas (aplicações incorporadas) | O Intune instala a aplicação no dispositivo.  | As atualizações das aplicações são automáticas. |
| Aplicações na Web (ligação Web) | O Intune cria um atalho para a aplicação Web no ecrã principal do dispositivo. | As atualizações das aplicações são automáticas. |
| Apps de outros serviços da Microsoft  | Intune cria um atalho para a app no Portal da Empresa. Para mais informações, consulte as opções de [definição de fonte da App](../apps/company-portal-app.md#app-source-setting-options). | As atualizações das aplicações são automáticas. |

### <a name="specific-app-type-details"></a>Detalhes específicos do tipo de aplicação
 
A tabela seguinte apresenta uma lista dos tipos de aplicações específicos e como pode adicioná-los no painel **Adicionar aplicação**:

| **Tipo de aplicação específico** | **Tipo geral** | **Procedimentos específicos da aplicação** |
| --- | --- | --- |
| Aplicações da loja Android  | Aplicação da loja  | Selecione **Android** como o **tipo de aplicação** e introduza o URL da Google Play Store para a aplicação. |
| Aplicações Android Enterprise  | Aplicação da loja  | Selecione **Android** como o **tipo de aplicação** e introduza o URL da loja do Managed Google Play para a aplicação. <sup>1</sup> |
| aplicações para iOS/iPadOS  | Aplicação da loja  | Selecione **iOS** como o **tipo de aplicação**, procure a aplicação e selecione a aplicação no Intune. |
| Aplicações da loja Windows Phone 8.1  | Aplicação da loja  | Selecione **Windows Phone 8.1** como o **tipo de aplicação** e introduza o URL da Microsoft Store para a aplicação. |
| Aplicações da Microsoft Store  | Aplicação da loja  | Selecione **Windows** como o **tipo de aplicação** e introduza o URL da Microsoft Store para a aplicação. |
| Aplicações geridas do Google Play | Aplicação da loja  | Selecione **Managed Google Play** como o **tipo de aplicação**, procure a aplicação e selecione a aplicação no Intune. |
| Aplicações do Office 365 para Windows 10  | Aplicação da loja (Office 365) | Selecione o **Windows 10** no microsoft **365 Apps** como o tipo de **aplicação**, e depois selecione a aplicação Office 365 que pretende instalar.  |
| Aplicações do Office 365 para macOS | Aplicação da loja (Office 365) | Selecione **o macOS** em **aplicações Microsoft 365** como o tipo de **aplicação**, e, em seguida, selecione o conjunto de aplicações Office 365. |
| Microsoft Edge, versão 77 e mais tarde para windows 10 | Aplicação da loja | Selecione **o Windows 10** no **Microsoft Edge, na versão 77 e mais tarde** como tipo de **aplicação**. |
| Microsoft Edge, versão 77 e mais tarde para macOS | Aplicação da loja | Selecione **o macOS** no **Microsoft Edge, versão 77 e posteriormente** como tipo de **aplicação**. |
| Aplicações de linha de negócio (LOB) Android | Aplicação LOB | Selecione **Aplicação de linha de negócio** como o **tipo de aplicação**, selecione o **Ficheiro de pacote de aplicação** e, em seguida, introduza um ficheiro de instalação Android com a extensão **.apk**.  |
| aplicativos iOS/iPadOS LOB | Aplicação LOB | Selecione a aplicação **Line-of-business** como o tipo de **aplicação,** selecione o ficheiro de **pacote**siOs/iPadOS com a extensão **.ipa**.  |
| Aplicações LOB Windows Phone | Aplicação LOB | Selecione **Aplicação de linha de negócio** como o **tipo de aplicação**, selecione o **Ficheiro de pacote de aplicação** e, em seguida, introduza um ficheiro de instalação Windows Phone com a extensão **.xap**.  |
| Aplicação LOB do Windows | Aplicação LOB | Selecione **Aplicação de linha de negócio** como o tipo de aplicação, selecione o **Ficheiro de pacote de aplicação** e, em seguida, introduza um ficheiro de instalação do Windows com a extensão **.msi**, **.appx**, **.appxbundle**, **.msix** e **.msixbundle**. |
| Aplicativo iOS/iPadOS incorporado  | Aplicação incorporada | Selecione **Aplicação incorporada** como o **tipo de aplicação** e, em seguida, selecione a aplicação incorporada da lista de aplicações disponibilizadas.  |
| Aplicação Android incorporada  | Aplicação incorporada | Selecione **Aplicação incorporada** como o **tipo de aplicação** e, em seguida, selecione a aplicação incorporada da lista de aplicações disponibilizadas.  |
| Web Apps  | Aplicação Web  | Selecione **Ligação Web** como o **tipo de aplicação** e, em seguida, introduza um URL válido que aponte para a aplicação Web.  |
| Aplicações do sistema Android Enterprise  | Aplicação da loja  | Selecione a **aplicação do sistema Android Enterprise** como o tipo de **aplicação**, e depois introduza o nome da aplicação, editor e ficheiro de pacotes.  |
| Aplicação do Windows (Win32)  | Aplicação LOB  | Selecione **Aplicação do Windows (Win32)** como o **tipo de aplicação**, selecione o **Ficheiro de pacote de aplicação** e, em seguida, selecione um ficheiro de instalação com a extensão **.intunewin**.  |
| Aplicações LOB macOS | Aplicação LOB  | Selecione **Line-of-business** como o tipo de **aplicação,** selecione o ficheiro de **pacote**app , e, em seguida, selecione um ficheiro de instalação com a extensão **.intunemac**.  |

<sup>1</sup> Para obter mais informações sobre o Android Enterprise e os perfis de trabalho Android, veja [Compreender as aplicações licenciadas](apps-add.md#understanding-licensed-apps) abaixo.

Pode adicionar uma aplicação no Microsoft Intune selecionando **apps**  >  **Todas as aplicações**  >  **Add**. O painel do tipo select o tipo de **aplicação Select** é apresentado e permite-lhe selecionar o **tipo de App**. 

>[!TIP]
> Uma aplicação LOB é uma aplicação que adiciona a partir de um ficheiro de instalação da aplicação. Por exemplo, para instalar uma aplicação iOS/iPadOS LOB, adiciona a aplicação selecionando a **aplicação Line-of-business** como o tipo de **App** no painel do **tipo select.** Em seguida, selecione o ficheiro de pacote de aplicação (extensão .ipa). Normalmente, estes tipos de aplicações são escritos internamente.

## <a name="assess-app-requirements"></a>Avaliar requisitos da aplicação
Enquanto administrador de TI, tem de determinar as aplicações que o seu grupo tem de utilizar e as funcionalidades necessárias para cada grupo e subgrupo. Para cada aplicação, tem de determinar as plataformas necessárias, os grupos de utilizadores que precisam da aplicação, as políticas de configuração a aplicar a esses grupos e as políticas de proteção a aplicar.  

Além disso, tem de determinar se precisa de se focar na Gestão de Dispositivos Móveis (MDM) ou apenas na Gestão de Aplicações Móveis (MAM). 

Utilizar o Intune para gerir o dispositivo com a MDM é útil quando:
- Os utilizadores precisam de um perfil de conectividade empresarial VPN ou Wi-Fi para serem produtivos.
- Os utilizadores precisam que um conjunto de aplicações seja disponibilizado nos respetivos dispositivos.
- A sua organização tem de estar em conformidade com políticas de regulamentação ou outras políticas que precisem de controlos de MDM específicos, tal como segurança ou encriptação.

Utilizar o Intune para gerir aplicações com a MAM sem gerir o dispositivo é útil quando:
- Quiser permitir que os utilizadores utilizem os seus próprios dispositivos (BYOD).
- Quiser disponibilizar uma mensagem de pop-up individual para informar os utilizadores de que as proteções de MAM estão aplicadas, em vez de enviar notificações contínuas ao nível do dispositivo.
- Quiser estar em conformidade com algumas políticas que exigem menos funcionalidades de gestão em dispositivos pessoais. Por exemplo, quer gerir os dados empresariais das aplicações, em vez de gerir os dados empresariais do dispositivo inteiro.

Para obter mais informações, [Comparar MDM e MAM](../fundamentals/byod-technology-decisions.md).

### <a name="determine-who-will-use-the-app"></a>Determinar quem irá utilizar a aplicação

Como está a determinar quais as aplicações de que a sua força de trabalho precisa, considere os vários grupos de utilizadores e as várias aplicações que utilizam. Conhecer estes grupos também é útil depois de ter adicionado uma aplicação. Depois de adicionar uma aplicação, tem de designar um grupo de utilizadores que podem utilizar a aplicação. 

Em primeiro lugar, tem de determinar o grupo adequado que deve ter acesso à aplicação com base na confidencialidade dos dados que a aplicação contém. Poderá ter de incluir ou excluir determinados tipos de funções na sua organização. Por exemplo, podem ser precisas apenas determinadas aplicações LOB para o seu grupo de vendas, enquanto as pessoas focadas em engenharia, finanças, RH ou aspetos jurídicos poderão não precisar de utilizar as aplicações LOB. Além disso, o seu grupo de vendas pode precisar de proteção de dados adicional e acesso a serviços empresariais internos nos respetivos dispositivos móveis. Tem de determinar a forma como este grupo se irá ligar aos recursos com a aplicação. Os dados aos quais a aplicação acede residem na cloud ou no local? Além disso, como é que os utilizadores se irão ligar aos recursos com a aplicação? 

O Intune também suporta permitir o acesso a aplicações cliente que exijam o acesso seguro a dados no local, como servidores de aplicações de linha de negócio. Normalmente, tem de disponibilizar este tipo de acesso através de [certificados geridos pelo Intune](../protect/certificates-configure.md) para controlo de acesso combinado com um proxy ou gateway de VPN padrão no perímetro, como o Proxy de Aplicações do Azure Active Directory. A [Intune App Wrapping Tool e app SDK](../developer/apps-prepare-mobile-application-management.md) podem ajudar a conter os dados acedidos dentro da sua app de linha de negócio, para que não possa passar dados corporativos para aplicações ou serviços de consumo.

Utilize o [Guia de planeamento, estruturação e implementação do Intune](../fundamentals/planning-guide.md) para determinar como identificar os grupos organizacionais associados a cada cenário de aplicação de caso de utilização e caso de subutilização. Para obter mais informações sobre a atribuição de aplicações a grupos, veja [Atribuir aplicações a grupos com o Microsoft Intune](apps-deploy.md).

### <a name="determine-the-type-of-app-for-your-solution"></a>Determinar o tipo de aplicação para a sua solução

Pode selecionar de entre os seguintes tipos de aplicações:
- **Apps da loja**: Apps que foram enviadas para a loja microsoft, a loja iOS/iPadOS ou a loja Android são aplicações de loja. O fornecedor da aplicação da loja encarrega-se da manutenção e disponibiliza atualizações à aplicação. Tem de selecionar a aplicação na lista da loja e adicioná-la com o Intune como uma aplicação disponível para os seus utilizadores.
- **Aplicações escritas internamente (linha de negócio)**: as aplicações criadas internamente são aplicações de linha de negócio (LOB). A funcionalidade deste tipo de aplicações foi criada para uma das plataformas suportadas pelo Intune, como windows, iOS/iPadOS, macOS ou Android. A sua organização cria e fornece atualizações como um ficheiro separado. Tem de fornecer atualizações da aplicação aos utilizadores ao adicionar e implementar as atualizações com o Intune.
- **Aplicações na Web**: são aplicações de servidor de cliente. O servidor proporciona a aplicação Web, que inclui a IU, conteúdos e funcionalidades. Além disso, normalmente as plataformas de alojamento na Web modernas oferecem segurança, balanceamento de carga e outras vantagens. A manutenção deste tipo de aplicação é feita separadamente na Web. Tem de utilizar o Intune para apontar para este tipo de aplicação. Também tem de designar que grupos de utilizadores podem aceder à aplicação. Tenha em atenção que o Android não suporta aplicações Web.
- **Apps de outros serviços da Microsoft**: Apps que tenham sido provenientes de Azure AD ou Office Online. As **aplicações da Azure AD Enterprise** são registadas e atribuídas através do [portal Azure.](https://portal.azure.com) **As aplicações Office Online** são atribuídas utilizando os controlos de licenciamento disponíveis no [Centro de Administração M365.](https://admin.microsoft.com) Pode ocultar ou mostrar aplicações Azure AD Enterprise e Office Online aos utilizadores finais no Portal da Empresa. A partir do centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione a personalização da **administração do Inquilino**para encontrar esta  >  **Customization** definição de configuração. Selecione para **Ocultar** ou **mostrar** **aplicações da Azure AD Enterprise** ou **aplicações Do Office Online** no Portal da Empresa para cada utilizador final. Cada utilizador final verá todo o seu catálogo de aplicações a partir do serviço da Microsoft escolhido. Por predefinição, cada fonte adicional de aplicação será definida para **Ocultar**. Para mais informações, consulte as opções de [definição de fonte da App](../apps/company-portal-app.md#app-source-setting-options). 

Ao determinar as aplicações necessárias para a sua organização, tenha em consideração a forma como estas aplicações se integram com serviços cloud, os dados aos quais as aplicações podem aceder, se as aplicações estão disponíveis para utilizadores BYOD e se as aplicações precisam de acesso à Internet.

Para obter mais informações sobre os tipos de aplicações que a sua organização precisa, veja “Aplicações” na secção “Requisitos de funcionalidades” em [Criar uma estrutura](../fundamentals/planning-guide-design.md#feature-requirements).

### <a name="understanding-app-management-and-protection-policies"></a>Compreender as políticas de proteção e gestão de aplicações
O Intune permite-lhe modificar a funcionalidade das aplicações que implementa para ajudar a ajustá-las às políticas de conformidade e de segurança da sua empresa. Este controlo permite-lhe determinar como os dados da sua empresa são protegidos. As aplicações geridas pelo Intune têm um conjunto avançado de políticas de proteção de aplicações móveis, tal como:

- Restringir funções Copiar e colar e Guardar como.
- Configurar links web para abrir dentro da aplicação Microsoft Edge.
- Permitindo o uso multi-identidade e o acesso condicional ao nível da aplicação.

As aplicações geridas pelo Intune também permitem a proteção de aplicações sem exigir a inscrição, dando-lhe a opção de aplicar políticas de prevenção de perda de dados sem gerir o dispositivo do utilizador. Além disso, pode incorporar a gestão de aplicações móveis nas suas aplicações móveis e de linha de negócio com o SDK da Aplicação Intune e a Ferramenta de Encapsulamento de Aplicações. Para obter mais informações sobre estas ferramentas, veja [Descrição geral do SDK da Aplicação Intune](../developer/app-sdk.md).

### <a name="understanding-licensed-apps"></a>Compreender as aplicações licenciadas
Para além de compreender as aplicações Web, aplicações da loja e aplicações LOB, também deve ter em atenção o destino das aplicações licenciadas e aplicações de programa de compras em volume, tais como: 
- **Apple Volume Purchase Program for Business (iOS)**: A loja de aplicações iOS/iPadOS permite-lhe adquirir várias licenças para uma aplicação que pretende executar na sua empresa. A compra de várias cópias ajuda-o a gerir aplicações na sua empresa de forma eficiente. Para mais informações, consulte [Gerir aplicações adquiridas em volume iOiOS/iPadOSS.](vpp-apps-ios.md)
- **Perfil de trabalho do Android**: a forma como atribui aplicações em dispositivos com perfil de trabalho do Android é diferente em dispositivos Android padrão. Todas as aplicações que instala em dispositivos com perfil de trabalho do Android são provenientes da Google Play Store gerida. Pode utilizar o Intune para procurar as aplicações pretendidas e aprová-las. Em seguida, a aplicação aparece no nó **Aplicações licenciadas** do portal do Azure e pode gerir a atribuição da aplicação como faria com qualquer outra aplicação.
- **Microsoft Store para Empresas (Windows 10)**: a Microsoft Store para Empresas dá-lhe um local para encontrar e comprar aplicações para a sua organização, individualmente ou em volume. Ao ligar a loja ao Microsoft Intune, pode gerir as aplicações compradas em volume no portal do Azure. Para obter mais informações, veja [Gerir aplicações a partir da Microsoft Store para Empresas](windows-store-for-business.md).

    > [!NOTE]
    > As extensões de ficheiros de aplicações do Windows incluem **.msi**, **.appx**, **.appxbundle**, **.msix** e **.msixbundle**.  

## <a name="before-you-add-apps"></a>Antes de adicionar aplicações
Considere os seguintes pontos antes de começar a adicionar e a atribuir as aplicações:

- Quando adicionar e atribuir uma aplicação a partir de uma loja, os seus utilizadores têm de ter uma conta nessa loja para conseguir instalar a aplicação.
- Algumas aplicações ou itens que atribua podem depender de aplicações incorporadas para iOS/iPadOS. Por exemplo, se atribuir um livro na loja iOS/iPadOS, a aplicação iBooks deve estar presente no dispositivo. Se tiver removido a aplicação iBooks incorporada, não poderá utilizar o Intune para a restabelecer.

> [!IMPORTANT]
> Se alterar o nome da aplicação através do portal do Azure no Intune após ter implementado e instalado a aplicação, a mesma deixará de poder ser visada através de comandos.

## <a name="cloud-storage-space"></a>Espaço de armazenamento na nuvem
Todas as aplicações que criar com o tipo de instalação do instalador de software (por exemplo, uma aplicação de linha de negócio) são empacotadas e carregadas para o armazenamento na cloud do Intune. Uma subscrição de avaliação do Intune inclui 2 gigabytes (GB) de armazenamento baseado na nuvem, o qual é utilizado para armazenar aplicações e atualizações geridas. Uma subscrição completa não limita a quantidade de armazenamento total.

Requisitos de espaço de armazenamento na cloud:

- Todos os ficheiros de instalação da aplicação têm de estar na mesma pasta.
- O tamanho máximo para qualquer ficheiro que carregar é 8 GB.

  > [!NOTE]
  > As aplicações Windows Line of business (LOB), incluindo Win32, Windows Universal AppX, Windows Universal AppX bundle, Windows Universal MSI X e Windows Universal MSI X bundle, têm um limite máximo de tamanho de 8 GB por app. Todas as outras aplicações LOB, incluindo aplicações iOS/iPadOS LOB, têm um limite máximo de tamanho de 2 GB por app.

## <a name="create-and-edit-categories-for-apps"></a>Criar e editar categorias para as aplicações

As categorias de aplicações podem ser utilizadas para o ajudar a ordenar as aplicações de modo a serem mais fáceis de encontrar por parte dos utilizadores no portal da empresa. Pode atribuir uma ou mais categorias a uma aplicação, por exemplo, *Aplicações de programador* ou *Aplicações de comunicação*.

Quando adiciona uma aplicação ao Intune, é-lhe dada a opção de selecionar a categoria que quiser. Utilize os tópicos das plataformas específicas para adicionar uma aplicação e atribuir categorias. Para criar e editar as suas próprias categorias, utilize o seguinte procedimento:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecione **Apps**  >  **as categorias**de apps .  
    O painel **Categorias de aplicações** apresenta uma lista de categorias atuais. 
5. Efetue um dos seguintes procedimentos:
    - Para adicionar uma categoria, no painel **Criar categoria**, selecione **Adicionar** e, em seguida, introduza um nome para a categoria.  
    Os nomes podem ser introduzidos em apenas um idioma e não são traduzidos pelo Intune.
    - Para editar uma categoria, selecione as reticências (**...**) junto à categoria e, em seguida, selecione **Afixar ao dashboard** ou **Eliminar**.
6. Selecione **Criar**.

## <a name="apps-that-are-added-automatically-by-intune"></a>Aplicações adicionadas automaticamente pelo Intune

Anteriormente, o Intune continha várias aplicações incorporadas que podia atribuir rapidamente. Com base nos comentários de clientes do Intune, removemos esta lista e as aplicações incorporadas já não são apresentadas. No entanto, se já tiver atribuído aplicações incorporadas, as mesmas continuarão visíveis na lista de aplicações. Pode continuar a atribuir as aplicações conforme necessário.

> [!NOTE]
> Para a instalação de uma aplicação não-Line-of-Business necessária, a Intune tentará instalar a aplicação enviando um comando de instalação sempre que o dispositivo faz o check-in, dado que a aplicação não é detetada e o estado de instalação da aplicação não está *instalado pendente.*

## <a name="installing-updating-or-removing-required-apps"></a>Instalar, atualizar ou remover aplicações necessárias

O Intune irá reinstalar, atualizar ou remover automaticamente uma aplicação necessária no prazo de 24 horas em vez de aguardar o ciclo de reavaliação de 7 dias.

O Intune irá reinstalar, atualizar ou remover automaticamente uma aplicação necessária com base nas seguintes condições:
- Se um utilizador final desinstalar uma aplicação de instalação necessária no respetivo dispositivo, o Intune irá reinstalar automaticamente a aplicação quando este agendamento terminar.
- Se a instalação de uma aplicação necessária falhar ou a aplicação não estiver presente no dispositivo, o Intune irá avaliar a conformidade e reinstalar a aplicação quando este agendamento terminar.  
- Um administrador define uma aplicação como disponível para um grupo de utilizadores e um utilizador final instala a aplicação a partir do portal da empresa no dispositivo. Posteriormente, o administrador atualiza a aplicação da v1 para a v2. O Intune irá atualizar a aplicação quando este agendamento terminar, desde que uma versão anterior da aplicação ainda esteja presente no dispositivo.
- Se o administrador implementar a intenção de desinstalação e a aplicação estiver presente no dispositivo e a desinstalação falhar, o Intune irá avaliar a conformidade e desinstalar a aplicação quando este agendamento terminar.   

## <a name="app-installation-errors"></a>Erros de instalação da aplicação

Para obter detalhes sobre os erros de instalação da aplicação Intune, veja [Erros de instalação da aplicação](troubleshoot-app-install.md).

## <a name="next-steps"></a>Passos seguintes

Para saber como adicionar aplicações para cada plataforma ao Intune, veja:

- [Aplicações da loja Android](store-apps-android.md)
- [Aplicações LOB Android](lob-apps-android.md)
- [Aplicações da loja iOS](store-apps-ios.md)
- [Aplicações LOB iOS](lob-apps-ios.md)
- [Aplicações LOB macOS](lob-apps-macos.md)
- [Aplicações Web (para todas as plataformas)](web-app.md)
- [Aplicações da loja Windows Phone 8.1](store-apps-windows-phone-8-1.md)
- [Aplicações LOB Windows Phone](lob-apps-windows-phone.md)
- [Aplicações da Microsoft Store](store-apps-windows.md)
- [Aplicação LOB do Windows](lob-apps-windows.md)
- [Aplicações do Office 365 para Windows 10](apps-add-office365.md)
- [Aplicações do Office 365 para macOS](apps-add-office365-macos.md)
- [Aplicações geridas do Google Play](apps-add-android-for-work.md)
- [Microsoft Edge para Windows 10](apps-windows-edge.md)
- [Microsoft Edge para macOS](apps-edge-macos.md)
- [Aplicações incorporadas](apps-add-built-in.md)
- [Aplicativo do sistema Android Enterprise](apps-ae-system.md)
- [Aplicações Win32](apps-win32-app-management.md)
