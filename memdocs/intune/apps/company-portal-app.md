---
title: Como personalizar as aplicações intune Company Portal, site do Portal da Empresa e app Intune
titleSuffix: Microsoft Intune
description: Saiba como pode aplicar a marca específica da empresa às aplicações intune Company Portal, website do Portal da Empresa e aplicação Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dec6f258-ee1b-4824-bf66-29053051a1ae
ms.reviewer: esthermsft
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e584019063c6af7f04f5666ba2c38d8199681c5
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771421"
---
# <a name="how-to-customize-the-intune-company-portal-apps-company-portal-website-and-intune-app"></a>Como personalizar as aplicações intune Company Portal, site do Portal da Empresa e app Intune

As aplicações do Portal da Empresa, o website do Portal da Empresa e a aplicação Intune no Android são onde os utilizadores acedem aos dados da empresa e podem fazer tarefas comuns. A tarefa comum pode incluir a inscrição de dispositivos, a instalação de apps e a localização de informações (como a assistência do seu departamento de TI). Além disso, permitem que os utilizadores acedam de forma segura aos recursos da empresa. A experiência do utilizador final fornece várias páginas diferentes, tais como Detalhes home, apps, app, dispositivos e dispositivos. Para encontrar rapidamente aplicações dentro do Portal da Empresa, pode filtrar as aplicações na página apps.

## <a name="customizing-the-user-experience"></a>Personalizando a experiência do utilizador

Ao personalizar a experiência do utilizador final, irá ajudar a fornecer uma experiência familiar e útil para os seus utilizadores finais. Para isso, navegue para o centro de [administração do Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), e selecione A**Personalização**da **Administração** > de Inquilinos, onde pode editar a política predefinida ou criar até 10 políticas direcionadas para o grupo. Estas configurações aplicar-se-ão às aplicações do Portal da Empresa, ao website do Portal da Empresa e à aplicação Intune no Android.

## <a name="branding"></a>Imagem corporativa

A tabela seguinte fornece os detalhes de personalização da marca para a experiência do utilizador final:

| Nome do campo | Mais informações |
|---|---|---|
| **Nome da organização** | Este nome é apresentado ao longo das mensagens na experiência do utilizador final. Pode ser programado para exibir também em cabeçalhos usando o Show na definição do **cabeçalho.** O comprimento máximo é de 40 caracteres. |
| **Cor** | Escolha **standard** para escolher entre cinco cores padrão. Escolha **o Costume** para selecionar uma cor específica com base num valor de código hex. |
| **Cor do tema** | Dete tede a cor do tema para mostrar através da experiência do utilizador final. Vamos automaticamente definir a cor do texto para preto ou branco para que seja mais visível em cima da sua cor temática selecionada. |
| **Mostrar no cabeçalho** | Selecione se o cabeçalho nas experiências do utilizador final deve exibir o logótipo e o **nome da Empresa,** apenas o **logótipo da Empresa,** ou **apenas**o nome da Empresa . As caixas de pré-visualização abaixo só mostrarão os logótipos, não o nome.  |
| **Carregar logotipo para fundo de cor tema** | Faça upload do logótipo que pretende mostrar em cima da cor temática selecionada. Para a melhor aparência, faça upload de um logotipo com um fundo transparente. Pode ver como isto ficará na caixa de pré-visualização abaixo da definição.<p>Tamanho máximo da imagem: 400 x 400 px<br>Tamanho máximo do ficheiro: 750KB<br>Tipo de ficheiro: PNG, JPG ou JPEG |
| **Carregar logotipo para fundo branco ou claro** | Faça upload do logótipo que pretende mostrar em cima de fundos brancos ou de cor clara. Para a melhor aparência, faça upload de um logotipo com um fundo transparente. Pode ver como isto ficará num fundo branco na caixa de pré-visualização abaixo da definição.<p>Tamanho máximo da imagem: 400 x 400 px<br>Tamanho máximo do ficheiro: 750 KB<br>Tipo de ficheiro: PNG, JPG ou JPEG |
| **Carregar imagem da marca** | Faça upload de uma imagem que reflita a marca da sua organização.<p><ul><li>Largura de imagem recomendada: Superior a 1125 px (necessário para ser pelo menos 650 px)</li><li>Tamanho máximo da imagem: 1,3 MB</li><li>Tipo de ficheiro: PNG, JPG ou JPEG</li><li>É exibido nestes locais:</li><ul><li>portal da empresa iOS/iPadOS: Imagem de fundo na página de perfil do utilizador.</li><li>Website do Portal da Empresa: Imagem de fundo na página de perfil do utilizador.</li><li>Aplicativo Android Intune: Na gaveta e como imagem de fundo na página de perfil do utilizador.</li></ul></ul> |

> [!NOTE]
> Quando um utilizador estiver a instalar uma aplicação iOS/iPadOS a partir do Portal da Empresa, receberá uma solicitação. Isto ocorre quando a aplicação iOS/iPadOS está ligada à loja de aplicações, ligada a um programa de compra de volume (VPP), ou ligada a uma aplicação de linha de negócios (LOB). O pedido permite que os utilizadores aceitem a ação ou permitam a gestão da app. O pedido mostrará o nome da sua empresa, ou quando o nome da sua empresa não estiver disponível, o **Portal da Empresa** será exibido.

### <a name="brand-image-best-practices"></a>As melhores práticas de imagem da marca

A imagem de marca certa pode aumentar a confiança do utilizador apresentando um forte sentido da marca da sua organização. Aqui ficam algumas dicas que talvez deseja considerar para adquirir, escolher e otimizar a imagem para os locais de exibição.

- Entre em contacto com o Departamento de Marketing ou de Artes Gráficas. Estes departamentos podem já ter um conjunto de imagens de marca aprovado. Também poderão ajudá-lo a otimizar as imagens conforme necessário.
- Considere tanto a composição horizontal como a vertical. A imagem deve ter um fundo suficiente, de forma a envolver o ponto focal. A imagem pode ser recortada de forma diferente com base na orientação, no tamanho e na plataforma do dispositivo.
- Evite utilizar uma imagem de stock genérica. A imagem deve refletir a marca da sua organização e sentir-se familiar aos utilizadores. Se não tiver um, é melhor não usar um do que usar um genérico que não tem significado para o seu utilizador.
- Remova os metadados desnecessários. O ficheiro de imagem pode vir com metadados, tais como o perfil da câmara, a geolocalização, o título, a legenda, etc. Utilize uma ferramenta de otimização de imagens para retirar estas informações para manter a qualidade e cumprir o limite de tamanho do ficheiro.

### <a name="brand-image-examples"></a>Exemplos de imagem de marca

A imagem que se segue mostra um exemplo da imagem da marca num iPhone:

<img alt="Screenshot of example iPhone branding image" src="./media/company-portal-app/company-portal-app-01.png" width="250">

O seguinte mostra um exemplo da imagem da marca na aplicação Intune para Android:

<img alt="Screenshot of example #1 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-02.png" width="250">

<img alt="Screenshot of example #2 for Intune app for Android branding image" src="./media/company-portal-app/company-portal-app-03.png" width="250">

## <a name="support-information"></a>Informações de suporte

Insira as informações de apoio da sua organização, para que os colaboradores possam chegar a perguntas. Estas informações de suporte serão exibidas nas páginas de **Suporte**& **Ajuda**e Suporte de **Ajuda** em toda a experiência do utilizador final.

| Nome do campo | Comprimento máximo | Mais informações |
|------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nome do contacto | 40 | Este nome é a quem os utilizadores irão contactar quando contactarem o suporte. |
| Número de telefone | 20 | Este número permite que os utilizadores requisiem o suporte. |
| Endereço de e-mail | 40 | Este endereço de e-mail é onde os utilizadores podem enviar e-mails para suporte. Tem de inserir um endereço de e-mail válido no formato `alias@domainname.com`. |
| Nome do site | 40 | Este é o nome amigável que é exibido em alguns locais para o URL para o site de suporte. Se especificar um URL do site de suporte e nenhum nome amigável, então o URL em si é apresentado nas experiências do utilizador final.  |
| URL do Site | 150 | O site de suporte que os utilizadores devem utilizar. O URL deve estar `https://www.contoso.com`no formato .  |
| Informações adicionais | 120 | Inclua quaisquer mensagens adicionais relacionadas com o suporte para os utilizadores aqui. |

## <a name="configuration"></a>Configuração

A tabela seguinte fornece detalhes adicionais de configuração:

| Nome do campo | Comprimento máximo | Mais informações |
|------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URL de declaração de privacidade | 79 | Detete a declaração de privacidade da sua organização para aparecer quando os utilizadores clicarem em links de privacidade. Tem de introduzir um URL válido no formato `https://www.contoso.com`. |
| Mensagem de privacidade no Portal da Empresa para iOS/iPadOS | 520 | Mantenha o Padrão ou detetete uma mensagem Personalizada para listar os itens que a sua organização pode ou não ver em dispositivos geridos para iOS/iPadOS. Pode usar o markdown para adicionar balas, arrojados, itálicos e ligações. |
| Inscrição de dispositivos | N/D | Especifique se e como os utilizadores devem ser solicitados a inscreverem-se na gestão de dispositivos móveis. Detalhes abaixo. |
| Notificação de propriedade do dispositivo | N/D | Envie uma notificação push aos utilizadores do Portal do Portal do Android e iOS quando o seu tipo de propriedade do dispositivo tiver sido alterado de pessoal para corporativo. Por predefinição, esta notificação push está programada para ser cancelada. Quando a propriedade do dispositivo é definida para a propriedade corporativa, intune tem um maior acesso ao dispositivo, que inclui o inventário completo da aplicação, rotação de chave FileVault, recuperação de númerode telefone e algumas ações remotas selecionadas. Para mais informações, consulte alterar a [propriedade do dispositivo](../enrollment/corporate-identifiers-add.md#change-device-ownership).  |

### <a name="device-enrollment-setting-options"></a>Opções de definição de inscrição do dispositivo

> [!NOTE]
> O suporte para a definição de inscrição do dispositivo requer que os utilizadores finais tenham estas versões do Portal da Empresa:
> - Portal da empresa sobre iOS/iPadOS: versão 4.4 ou posterior
> - Portal da empresa no Android: versão 5.0.4715.0 ou posterior 

|    Opções de inscrição de dispositivos    |    Descrição    |    Solicitações da lista de verificação    |    Notificação    |    Estado dos detalhes do dispositivo    |    Estado dos detalhes da aplicação (de uma app que requer inscrição)    |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------|--------------------|-----------------------------|--------------------------------------------------------------------|
|    Disponível, com solicitações    |    A experiência padrão com solicitações para se inscrever em todos os locais possíveis.    |    Sim    |    Sim    |    Sim    |    Sim    |
|    Disponível, sem solicitações    |    O utilizador pode inscrever-se através do estado dos detalhes do dispositivo para o seu dispositivo atual ou de aplicações que necessitem de inscrição.    |    Não    |    Não    |    Sim    |    Sim    |
|    Indisponível    |    Não há como os utilizadores se inscreverem.    |    Não    |    Não    |    Não    |    Não<sup>(1)</sup>    |

<sup>(1)</sup> **Problema conhecido:** Se definir aplicações para exigir a inscrição para instalação e também definir a inscrição do dispositivo para "Indisponível", a aplicação Portal da Empresa no Android continuará a orientar os utilizadores a inscreverem-se. Isto será removido em breve.

> [!NOTE]
> Se estiver a utilizar o Azure Government, os registos de aplicações estão disponíveis para o utilizador final decidir como pretende partilhar ao iniciar o processo para obter ajuda com um problema. No entanto, caso não esteja a utilizar o Governo do Azure, o Portal da Empresa enviará registos de aplicações diretamente para a Microsoft quando o utilizador iniciar o processo para obter ajuda com um problema. O envio dos registos de aplicações para a Microsoft irá facilitar a resolução dos problemas.

> [!NOTE]
> De acordo com a política da Microsoft e da Apple, não vendemos quaisquer dados recolhidos pelo nosso serviço a terceiros por qualquer motivo.

## <a name="company-portal-derived-credentials-for-iosipados-devices"></a>Empresa Portal derivado de credenciais para dispositivos iOS/iPadOS

Intune apoia a Verificação de Identidade Pessoal (PIV) e o Cartão de Acesso Comum (CAC) Credenciais derivadas em parceria com fornecedores credenciais DISA Purebred, Entrust Datacard e Intercede. Os utilizadores finais passarão por etapas adicionais após a inscrição do seu dispositivo iOS/iPadOS para verificar a sua identidade na aplicação Portal da Empresa. As Credenciais derivadas serão ativadas para os utilizadores, criando primeiro um fornecedor de credenciais para o seu inquilino, direcionando depois um perfil que utiliza credenciais derivadas para utilizadores ou dispositivos.

> [!NOTE]
> O utilizador verá instruções sobre credenciais derivadas com base no link que especificou via Intune.

Para obter mais informações sobre credenciais derivadas para dispositivos iOS/iPadOS, consulte [Utilize credenciais derivadas no Microsoft Intune](../protect/derived-credentials.md).

## <a name="dark-mode-for-iosipados-company-portal"></a>Modo Escuro para portal da empresa iOS/iPadOS

O Modo Escuro está disponível para o portal da empresa iOS/iPadOS. Os utilizadores podem descarregar apps, gerir os seus dispositivos e obter suporte de TI no esquema de cores da sua escolha com base nas definições do dispositivo. O portal da empresa iOS/iPadOS irá corresponder automaticamente às definições do dispositivo do utilizador final para modo escuro ou leve.

## <a name="windows-company-portal-keyboard-shortcuts"></a>Atalhos de teclado do Portal da Empresa do Windows

Os utilizadores finais podem ativar ações de navegação, de aplicação e de dispositivo no Portal da Empresa do Windows com atalhos de teclado.

Os atalhos de teclado seguintes estão disponíveis na aplicação Portal da Empresa do Windows.

| Área | Descrição | Atalho de teclado |
|:------------------:|:--------------:|:-----------------:|
| Menu de navegação | Navegação | Alt+M |
|  | Casa | Alt+H |
|  | Todas as aplicações | Alt+A |
|  | Aplicações instaladas | Alt+I |
|  | Enviar comentários | Alt+F |
|  | O meu perfil | Alt+U |
|  | Definições | Alt+T |
| Base – Mosaico Dispositivo | Mudar o Nome | F2 |
|  | Remover | Ctrl+D ou Delete |
|  | Verificar acesso | Ctrl+M ou F9 |
| Detalhes do dispositivo | Mudar o Nome | F2 |
|  | Remover | Ctrl+D ou Delete |
|  | Verificar acesso | Ctrl+M ou F9 |
| Detalhes da aplicação | Instalar | Ctrl+I |
| Dispositivos | Disponível | Ctrl+D |

Os utilizadores finais também poderão ver os atalhos disponíveis na aplicação Portal da Empresa no Windows.

![Captura de ecrã dos atalhos disponíveis no Portal da Empresa do Windows](./media/company-portal-app/company-portal-app-04.png)

## <a name="user-self-service-device-actions-from-the-company-portal"></a>Ações de dispositivo de self-service do utilizador a partir do Portal da Empresa

Os utilizadores podem realizar ações nos seus dispositivos locais ou remotos através da aplicação ou website do Portal da Empresa ou da aplicação Intune no Android. As ações que um utilizador pode executar variam em função da plataforma e configuração do dispositivo. Em todos os casos, as ações do dispositivo remoto só podem ser executadas pelo Utilizador Primário do dispositivo.

- **Aposentador** – Remove o dispositivo da Intune Management. Na aplicação e website do portal da empresa, isto mostra como **Remover**.
- **Limpeza** – Esta ação inicia um reset do dispositivo. No portal da empresa este é mostrado como **Reset**, ou **Reset de Fábrica** na Aplicação portal iOS/iPadOS Company.
- **Renomear** – Esta ação altera o nome do dispositivo que o utilizador pode ver no Portal da Empresa. Não altera o nome do dispositivo local, apenas a listagem no Portal da Empresa.
- **Sync** – Esta ação inicia um check-in do dispositivo com o serviço Intune. Isto mostra como **Check Status** no Portal da Empresa.
- **Bloqueio remoto** – Este bloqueia o dispositivo, exigindo um PIN para desbloqueá-lo.
- **Redefinir a código de acesso** – Esta ação é utilizada para redefinir a senha do dispositivo. Nos dispositivos iOS/iPadOS, a senha será removida e o utilizador final será obrigado a introduzir um novo código nas definições. Em dispositivos Android suportados, uma nova senha é gerada pela Intune e exibida temporariamente no Portal da Empresa.
- **Recuperação chave** – Esta ação é usada para recuperar uma chave de recuperação pessoal para dispositivos macOS encriptados a partir do website do Portal da Empresa. 

### <a name="self-service-actions"></a>Ações de Self-Service

Algumas plataformas e configurações não permitem ações de dispositivos self-service. Este quadro abaixo fornece mais detalhes sobre as ações de self-service:

|  | Windows 10<sup>(3)</sup> | iOS/iPadOS<sup>(3)</sup> | MacOS<sup>(3)</sup> | Android<sup>(3)</sup> |
|----------------------|--------------------------|-------------------|-----------------------------------|-------------------------|
| Extinguir | Disponível<sup>(1)</sup> | Disponível | Disponível | Disponível<sup>(7)</sup> |
| Eliminação | Disponível | Disponível<sup>(5)</sup> | ND | Disponível<sup>(7)</sup> |
| Renome<sup>(4)</sup> | Disponível | Disponível | Disponível | Disponível |
| Sync | Disponível | Disponível | Disponível | Disponível |
| Bloqueio Remoto | Apenas windows Phone | Disponível | Disponível | Disponível |
| Redefinir código de acesso | Apenas windows Phone | Disponível<sup>(8)</sup> | ND | Disponível<sup>(6)</sup> |
| Recuperação de Chaves | ND | ND | Disponível<sup>(2)</sup> | ND |

<sup>(1)</sup> **A reforma** está sempre bloqueada nos dispositivos Azure AD Joined Windows.<br>
<sup>(2)</sup> **A recuperação da chave** para o MacOS só está disponível através do Portal Web.<br>
<sup>(3)</sup> Todas as ações remotas são desativadas se utilizarem uma inscrição do Gestor de Inscrição do Dispositivo.<br>
<sup>(4)</sup> **O nome de novo** altera apenas o nome do dispositivo na aplicação portal da empresa ou no Portal web, não no dispositivo.<br>
<sup>(5)</sup> **A limpeza** não está disponível nos dispositivos iOS/iPadOS inscritos pelo utilizador.<br>
<sup>(6)</sup> **O Reset Passcode** não é suportado em algumas configurações do Android e Android Enterprise. Para mais informações, consulte [Reset ou remova uma senha do dispositivo no Intune](../remote-actions/device-passcode-reset.md).<br>
<sup>(7)</sup> **A reforma** e a **limpeza** não estão disponíveis nos cenários do Proprietário do Dispositivo Empresarial Android (COPE, COBO, COSU).<br>
<sup>(8)</sup> O código de acesso de **reset** não é suportado nos dispositivos iOS/iPadOS inscritos pelo utilizador.

## <a name="next-steps"></a>Passos seguintes

- [Adicionar aplicativos](apps-add.md)
