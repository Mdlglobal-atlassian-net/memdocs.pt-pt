---
title: Como obter suporte para o Microsoft Intune
titleSuffix: Microsoft Intune
description: Obtenha suporte online e por telefone para subscrições pagas e de avaliação do Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: crisk
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fbb82123f28c5049a60d60572aadcb3d03777b7
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326946"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>Como obter suporte para o Microsoft Intune

A Microsoft fornece suporte global técnico, de pré-vendas, de faturação e de subscrição para o Microsoft Intune. O suporte está disponível tanto online como por telefone para subscrições pagas ou de avaliação. O suporte técnico online está disponível em inglês e japonês. O suporte por telefone e o suporte de faturação online estão disponíveis em idiomas adicionais.

Enquanto administrador do Intune, pode utilizar a opção **Ajuda e Suporte** para enviar um pedido de suporte online do Intune a partir do portal do Azure. Para criar e gerir um incidente de suporte, a sua conta deve ter uma função de Diretório Ativo Azure (Azure AD) que inclua a *ação* **microsoft.office365.supportTickets**. Para obter informações sobre funções do Microsoft Azure AD e as permissões que são necessários para criar um pedido de suporte, veja as [funções de administrador no Microsoft Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal).

>[!IMPORTANT]
> Para obter suporte técnico para produtos de terceiros que funcionam com o Intune (como a Saaswedo, a Cisco ou a Lookout), contacte primeiro o fornecedor desse produto. Antes de abrir um pedido com o suporte do Intune, certifique-se de que configurou o outro produto corretamente.
>
> Para obter informações sobre a resolução de problemas relacionados com o Microsoft Intune, veja a [secção Resolução de problemas](help-desk-operators.md) da documentação do Intune.

## <a name="help-and-support-experience"></a>Experiência da ajuda e suporte

A experiência de Ajuda e suporte para intune está disponível no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e de todas as lâminas (ou páginas) em Intune no portal Azure.

A experiência *de Ajuda e suporte* é semelhante à experiência vista no centro de administração da Microsoft [365](https://admin.microsoft.com/), e substitui o suporte anterior *da Ajuda +* , que permanece em vigor para outros serviços no Azure.

> [!TIP]
> A partir de 18 de novembro de 2019, uma experiência atualizada e simplificada na consola para obter ajuda e apoio está a ser lançada aos inquilinos. Se esta nova experiência ainda não estiver disponível para si, será em breve.

### <a name="options-to-access-help-and-support"></a>Opções para aceder ajuda e suporte

Quando você usa um inquilino recém-criado para Intune, é possível que *a Ajuda e suporte* não abram e a seguinte mensagem seja devolvida:

- *Encontrámos um problema desconhecido. Por favor, refresque a página mas se o problema persistir, por favor crie uma caixa através do [Centro de Administração M365](https://admin.microsoft.com) e consulte o ID da sessão fornecido.*

Os detalhes do erro incluem um ID de *sessão,* detalhes de *extensão,* e muito mais.

Este problema ocorre quando não autenticou a sua nova conta de inquilinos através do **Centro de Administração M365** em https://admin.microsoft.com, ou do **portal Office 365** em https://portal.office.com. Para resolver este problema, selecione o link para *M365 Admin Center* na mensagem, ou visite https://portal.office.com, e inscreva-se. Após a autenticação em qualquer dos locais, *a Ajuda e suporte* para Intune torna-se acessível.

**Ajuda de acesso e suporte:**

- **No portal Azure**

  - Selecione **Ajuda e suporte** a partir de qualquer lâmina ou página Intune.

  > [!NOTE]  
  > Se o seu caso de Intune é hospedado na nuvem privada para o governo, também conhecido como uma nuvem soberana como o Governo de Azure, veja [o apoio intune para](#intune-support-for-private-cloud-for-government)a nuvem privada para o governo , mais tarde neste artigo. A *intune Help e a* experiência de apoio só estarão disponíveis na nuvem privada para o governo no próximo ano.

- **Do centro de administração do Microsoft Endpoint Manager**

  - De qualquer nó no centro de administração do Microsoft Endpoint Manager, selecione o **?** ícone no canto superior direito do portal e, em seguida, use o drop-down para selecionar o tipo de gestão com o que deseja ajuda. O centro de administração do Microsoft Endpoint Manager suporta os seguintes tipos de gestão, e deve selecionar aquele para quem deseja assistência, como intune:

    - Configure Manager (inclui Desktop Analytics)
    - Intune
    - Cogestão  

    > [!div class="mx-imgBorder"]
    > ![Selecione o seu tipo de gestão](./media/get-support/select-management-type.png)

    Depois de selecionar um tipo de gestão, a página *de ajuda e suporte* abre onde pode especificar detalhes para encontrar [soluções](#find-solutions) para um problema específico. Os detalhes são filtrados com base no tipo de gestão que seleciona.

     Se o tipo de gestão certo não foi selecionado **(1)** clique em Select um tipo de *gestão* **(2)** para voltar ao drop-down da seleção do tipo de gestão:

    > [!div class="mx-imgBorder"]
    > ![Confirme o seu tipo de gestão](./media/get-support/confirm-management-selection.png)

  - Se abrir ajuda e suporte de **Troubleshooting + suporte** > **Ajuda e suporte,** não verá o tipo de gestão que selecionou listado abaixo *Ajuda e suporte*.

  - Se perfurar qualquer outro nó como *Dispositivos,* *Apps,* ou *Utilizadores,* e depois selecionar *Ajuda e suporte,* não terá a oportunidade de selecionar um tipo de gestão nem o tipo abaixo do ecrã *de ajuda e suporte*. Neste caso, *Intune* é assumido. Se não quer que o contexto seja Intune, use **o?** opção para que possa selecionar um tipo de gestão diferente.

### <a name="the-support-experience"></a>A experiência de apoio

  Ao abrir ajuda e suporte, o portal exibe a **janela Need?**

  ![Veja a janela de ajuda necessária](./media/get-support/need-help.png)

  No canto superior esquerdo existem três ícones que pode selecionar para abrir diferentes vidraças da janela *Need Help?* O painel da sua visualização é identificado pelo sublinhado.

  Os clientes com um contrato de suporte **Premier** ou **Unificado** têm [opções adicionais](#premier-and-unified-support-customers) de apoio, e vêem um banner em Need help](./media/get-support/premier-banner.png) *![?*

  *Precisa de ajuda?* abre para o painel *Find Solutions.* No entanto, se tiver um caso de suporte ativo, a janela abre-se para o painel de pedidos do *Serviço* onde pode ver detalhes sobre os seus casos de suporte ativos e fechados.

#### <a name="find-solutions"></a>Encontrar soluções

![Selecione o painel de soluções de encontrar](./media/get-support/find-solutions.png)

No painel *find solutions,* especifique alguns detalhes sobre um problema na caixa de texto fornecida. Com base no texto que fornece sobre um problema, o painel povoa com insights que são potenciais fósforos. Também terá links para artigos recomendados que podem ajudá-lo a resolver o problema.

Quando se encontra uma correspondência forte para os detalhes que descreve, as dicas de resolução de problemas podem aparecer na janela *Need?*

Por exemplo, pode introduzir erros de sincronização de **palavra-passe**. Os resultados incluem orientação de resolução de problemas diretamente no painel, e links para artigos recomendados da nossa biblioteca de documentação.

![Ver insights de resolução de problemas](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>Contacte o suporte

![Selecione o painel de suporte de contacto](./media/get-support/contact-support.png)

A partir do painel de suporte de *contacto,* pode submeter um pedido de assistência. Este painel está disponível depois de fornecer algumas palavras-chave básicas no painel de *soluções de encontrar.*

Ao solicitar assistência, forneça uma descrição do problema com o máximo de detalhes necessário.  Depois de confirmar o seu telefone e informações de contacto por e-mail, selecione o método de contacto que prefere. A janela apresenta um tempo de resposta para cada método de contacto, o que lhe dá uma expectativa de quando será contactado. Antes de submeter o seu pedido, anexe ficheiros como registos ou imagens que possam ajudar a preencher detalhes sobre o problema.

![Formulário de suporte de contato](./media/get-support/contact-support-form.png)

Depois de preencher as informações necessárias, selecione **Contacte-me** para submeter o pedido.

#### <a name="service-requests"></a>Pedidos de serviço

![Selecione o painel de pedidos de serviço](./media/get-support/service-requests.png)

O *Serviço solicita* que o painel mostre o histórico do seu caso. Os casos ativos estão no topo da lista, com questões fechadas também disponíveis para revisão.

![Consulte a sua lista de pedidos de serviço](./media/get-support/service-requests-pane.png)

Se tiver um número de caso de suporte ativo, pode inscrevê-lo aqui para saltar para esse problema, ou pode selecionar qualquer incidente da lista de incidentes ativos e fechados para ver mais informações sobre o mesmo.

Quando terminar de visualizar detalhes para um incidente, selecione a seta esquerda que aparece na parte superior da janela de pedido de serviço logo acima dos ícones para os três ícones de painel *need help?* A seta traseira devolve o ecrã à lista de incidentes de apoio que abriu.

#### <a name="premier-and-unified-support-customers"></a>Clientes de suporte Premier e Unificado

Como cliente com um contrato de suporte **Premier** ou **Unificado,** pode especificar uma gravidade para o seu problema e agendar uma chamada de apoio para uma hora e dia específicos. Estas opções estão disponíveis quando abre ou submete um novo problema e quando edita um caso de suporte ativo.

**Gravidade** - As opções para especificar a gravidade de um problema dependem do seu contrato de apoio:

- *Primeiro-ministro*: Severidade de A, B ou C
- *Unificado*: Crítico ou não crítico

A seleção de uma questão de gravidade **A** ou **Crítica** limita-o a um caso de suporte telefónico, que fornece a opção mais rápida para obter suporte.

**Horário de chamada** - Pode solicitar uma chamada num dia e hora específicos.

## <a name="azure-help--support-experience"></a>Experiência da Ajuda + suporte do Azure

Já não pode utilizar a experiência de suporte Azure *Help +* para obter assistência com intune, a menos que a sua subscrição esteja numa nuvem privada para o governo.
Se o seu caso de Intune não funcionar numa nuvem privada para o governo, navegar através do Azure *Help + o suporte* redireciona-o para a *Intune Help e apoiar* a experiência para criar e gerir incidentes de apoio:

Quando utilizar o painel de navegação esquerdo **Ajuda + suporte,** ou utilize o **?** opção de abrir o painel *de ajuda* e, em seguida, selecionar Ajuda **+ suporte,** abre a página de suporte Azure *Help +.*

A partir desta página selecione **+ Novo pedido** de suporte para abrir o separador *Basics* da Ajuda + suporte + nova página de pedido de *suporte.*

![Ajuda + suporte](./media/get-support/help-plus-support.png)

Nesta página:

- Para *o tipo de problemas,* selecione **Técnico**.
- Para *o Serviço,* selecione **Microsoft Intune**.

  Em seguida, é-lhe apresentado um link que o redireciona para a [página de Ajuda e Suporte Intune](https://aka.ms/intunehelpsupport).
  
  ![Novo pedido de suporte](./media/get-support/new-request.png)

## <a name="intune-support-for-private-cloud-for-government"></a>Apoio insintonizado para nuvem privada para o governo

Quando a sua subscrição Intune foi hospedada na nuvem privada para o governo, que também é conhecida como uma nuvem soberana como o Governo Azure, ainda não tem acesso à mais recente intune Help e à experiência de apoio.  Em vez disso, utilize as seguintes informações para obter suporte para Intune.

### <a name="create-an-online-support-ticket"></a>Criar um pedido de suporte online

>[!IMPORTANT]
> Como *Ajuda e apoio* às transições para um novo sistema que ainda não está disponível para a nuvem privada para o governo, quando se cria um incidente de apoio, o portal identifica um caso de suporte que utiliza um número de identificação de 15 dígitos. Quando a caixa de 15 dígitos é criada, um espelho desse caso é criado para ser usado pelo Microsoft Support. Este caso de espelho é criado num novo sistema de suporte, usa um ID de caso de 8 dígitos, e é usado pelos serviços de suporte para rastrear todo o trabalho e comunicações para o seu incidente de suporte. Pouco depois da criação do seu caso de 15 dígitos, receberá um e-mail que identifica o número de 8 dígitos do caso de suporte espelhado que é usado pelos serviços de suporte.
>
> Apoie o trabalho pessoal e comunique a partir do caso de suporte de 8 dígitos, e utilize apenas o caso de suporte de 8 dígitos para registar comunicações e acompanhar o progresso dos incidentes. Portanto, receberá atualizações de e-mail a partir desse caso de suporte de 8 dígitos que servem como o seu histórico de trabalho de caso. Não há detalhes sobre o incidente de apoio de 15 dígitos. Quando o suporte termina e o caso de suporte de 8 dígitos termina, esse estatuto reflete-se no caso de suporte de 15 dígitos que pode ver dentro do portal azul.  Não devem ser esperadas outras atualizações ou alterações de estado para o caso de suporte de 15 dígitos.
>
> Quando as transições entre ferramentas de suporte terminarem ainda este ano, a experiência de suporte Intune hospedada na nuvem governamental assemelhar-se-á à experiência de *ajuda padrão e suporte* que está atualmente disponível para subscrições intune alojadas na nuvem pública.

1. Inicie sessão no portal do Azure (<https://portal.azure.us>) com as suas credenciais de administrador do Intune, selecione o ícone **?** no canto superior direito do portal e, em seguida, selecione **Ajuda + suporte** para aceder à página [Ajuda + suporte do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

   ![Imagem da ligação de ponto de interrogação com a ligação de Ajuda + suporte realçada](./media/get-support/azure-get-support.png)

2. Na página **Ajuda + suporte** do Azure, selecione **Novo pedido de suporte**.

   ![Imagem da ligação Novo pedido de suporte realçada na página de ajuda e suporte](./media/get-support/azure-support-ticket-link.png)

3. No separador **Básico**, para a maioria dos problemas de suporte técnico do Intune, selecione as seguintes opções:
   - **Tipo de problema**: **técnico**
   - **Subscrição**: <*a sua subscrição*>
   - **Serviço**: **Microsoft Intune**
   - **Tipo**de problema : Escolha o seu tipo de problema a partir do menu suspenso.
   - **Subtipo de problemas**: Escolha o subtipo do problema do menu suspenso.
   - **Assunto**: Descreva brevemente o problema com que pretende ajuda.

   ![Imagem do separador Básico na Ajuda + suporte – Nova página de pedido de suporte](./media/get-support/help-new-support-case-basics.png)

   Escolha **a seguir: Soluções** para continuar.
4. No separador **Soluções**, reveja os passos recomendados que podem ajudá-lo a resolver o seu problema sem enviar um pedido de suporte. Se ainda quiser criar um pedido de suporte depois de ver os passos, clique **em Seguinte: Detalhes**.

   ![Imagem do separador Soluções na Ajuda + suporte – Nova página de pedido de suporte](./media/get-support/help-new-support-case-solutions.png)
5. No separador **Detalhes,** preencha os detalhes para o seu problema, o método de suporte, as informações de contacto e, em seguida, clique **em Seguinte: Rever + criar**.

   ![Imagem do separador Detalhes na Ajuda + suporte – Nova página de pedido de suporte](./media/get-support/help-new-support-case-details.png)
6. Reveja as informações, verifique se estão corretas e escolha **Criar** para submeter o pedido de suporte.

   ![Imagem do separador Rever + criar na página Novo pedido de suporte](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>Se tiver alguma pergunta relacionada com a faturação ou subscrição, poderá criar um processo para obter suporte através do [centro de administração do Microsoft 365](https://admin.microsoft.com/Support/SupportEntry.aspx).

### <a name="view-support-requests"></a>Ver pedidos de suporte  

Pode ver os seus pedidos de apoio dentro do portal Azure. No entanto, há informação limitada disponível.  Para ver os seus incidentes:

1. Inicie sessão no portal do Azure (<https://portal.azure.com>) com as suas credenciais de administrador do Intune, selecione o ícone **?** no canto superior direito do portal e, em seguida, selecione **Ajuda + suporte** para aceder à página [Ajuda + suporte do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

2. Na página **de suporte Ajuda +,** pode ver a lista de pedidos de **suporte recentes**.

   > [!IMPORTANT]  
   > A nuvem privada para clientes do governo só pode ver o número do caso de apoio de 15 dígitos, e o estado do incidente. Todas as comunicações de caso e rastreio do trabalho ou alertas são enviadas por e-mail e referenciam o número do caso de suporte de 8 dígitos que é criado como um espelho do caso de suporte aberto a partir da consola Intune.

## <a name="additional-resources"></a>Recursos adicionais  

- [Suporte de gestão de subscrição e faturação](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [Licenciamento em Volume](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [Resolver problemas do Intune](help-desk-operators.md)
