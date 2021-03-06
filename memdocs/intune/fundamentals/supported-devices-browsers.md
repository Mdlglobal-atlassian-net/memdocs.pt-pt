---
title: Sistemas operativos e browsers suportados pelo Microsoft Intune
titleSuffix: ''
description: Apresenta uma lista de plataformas de dispositivos e browsers suportados para a gestão de dispositivos no Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9622a89b8b689dab7ea2d6d332d1d29c38f5668
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80085744"
---
# <a name="supported-operating-systems-and-browsers-in-intune"></a>Sistemas operativos e navegadores suportados em Intune

Antes de configurar o Microsoft Intune, reveja os sistemas operativos e browsers suportados.

Para ajudar a instalar o Intune no seu dispositivo, consulte [a utilização de dispositivos geridos para fazer o trabalho](https://docs.microsoft.com/mem/intune/user-help/use-managed-devices-to-get-work-done) e a utilização da largura de banda da rede [Intune](network-bandwidth-use.md).

Para obter mais informações sobre o suporte do prestador de serviços de configuração, visite a referência do prestador de serviços de [configuração](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

> [!NOTE]
> Intune agora requer Android 5.x (Lollipop) ou mais para aplicações e dispositivos para aceder aos recursos da empresa através da aplicação Portal da Empresa para Android e do Intune App SDK para Android. Este requisito NÃO se aplica aos dispositivos Polycom Android Teams com 4.4. Estes dispositivos continuarão a ser suportados. 

## <a name="intune-supported-operating-systems"></a>Sistemas operativos suportados pelo Intune

Pode gerir dispositivos com os seguintes sistemas operativos:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

### <a name="supported-samsung-knox-standard-devices"></a>Dispositivos Samsung Knox Standard suportados

Para evitar erros de ativação do Knox que impedem a inscrição MDM, a aplicação Portal da Empresa só tentará ativar o Samsung Knox durante a inscrição MDM se o dispositivo estiver na [lista de dispositivos Knox suportados](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Os dispositivos que não suportam a ativação do Samsung Knox são inscritos como dispositivos Android padrão. Um dispositivo Samsung pode ter alguns números de modelo que suportem o Knox, enquanto outros não. Verifique a compatibilidade com o Knox junto do revendedor do seu dispositivo antes da compra e implementação de dispositivos Samsung.

> [!NOTE]
> A inscrição de dispositivos Samsung Knox poderá exigir a [ativação do acesso aos servidores Samsung](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers).

Segue-se uma lista de modelos de dispositivos Samsung que não suportam o Knox. São inscritos como dispositivos Android nativos pela aplicação Portal da Empresa para Android:

| **Nome do dispositivo** | **Números de Modelo do Dispositivo** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110H |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM-T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

### <a name="windows-pc-software-client"></a>Software cliente em PC com Windows

Um [software cliente do Intune](manage-windows-pcs-with-microsoft-intune.md) pode ser implementado e instalado em PCs com Windows como um método alternativo de inscrição. Esta funcionalidade está apenas disponível com o portal clássico do Intune. Pode utilizar o cliente de software Intune para gerir 10 e posteriores PCs, com exceção da edição Home do Windows 10.

> [!Note]
> A Microsoft anunciou que o suporte do Windows 7 termina a 14 de Janeiro de 2020. Nesta data, o Intune também retira o suporte para dispositivos com o Windows 7.
>
> Para mais informações, consulte o [plano Intune para a mudança: fim do suporte para o Windows 7](whats-new.md#windows-7-ends-extended-support).
>
> A Microsoft Intune vai retirar o suporte para a consola Intune baseada em Silverlight a 15 de outubro de 2020. Esta reforma inclui o suporte final para o cliente de software pc configurado pela consola Silverlight (também conhecido como agente pc).
>
> Para mais informações, consulte o suporte final da [Microsoft Intune para a consola de administração baseada em Silverlight](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Take-Action-Microsoft-Intune-ending-support-for-the-Silverlight/ba-p/916249).

<!--  ### Exchange ActiveSync management

You can manage [Exchange ActiveSync devices](../enrollment/device-enrollment.md#mobile-device-management-with-exchange-activesync-and-intune) from the Intune console. This option provides a limited set of management capabilities when compared to the other methods. See [Capabilities of built-in Mobile Device Management in Office 365](https://support.office.com/article/Capabilities-of-built-in-Mobile-Device-Management-for-Office-365-a1da44e5-7475-4992-be91-9ccec25905b0) for a list of supported devices.  -->

## <a name="intune-supported-web-browsers"></a>Browsers suportados do Intune

As diferentes tarefas administrativas necessitam que utilize um dos seguintes sites administrativos.

- [Microsoft 365 admin center (Centro de administração do Microsoft 365)](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Portal do Azure](https://portal.azure.com/)

Os seguintes browsers são suportados para estes portais:

- Microsoft Edge (versão mais recente)
- Microsoft Internet Explorer 11
- Safari (versão mais recente, apenas Mac)
- Chrome (versão mais recente)
- Firefox (versão mais recente)

### <a name="intune-classic-portal"></a>Portal clássico do Intune

O portal clássico Intune é utilizado apenas para gerir dispositivoshttps://manage.microsoft.com)matriculados com o cliente de software Intune PC ( . O portal clássico do Intune necessita do suporte do browser Silverlight.

Os seguintes browsers Silverlight suportam a consola do Intune:

- Internet Explorer 10 ou posterior
- Google Chrome (versões anteriores à versão 42)
- Mozilla Firefox com Silverlight ativado (versões anteriores à versão 56)

> [!Note]
> O Microsoft Edge e os browsers para dispositivos móveis não são suportados no portal clássico do Intune porque não suportam o [Microsoft Silverlight](https://msdn.microsoft.com/library/cc838158(v=vs.95).aspx).

Apenas os utilizadores com permissões de administrador de serviços ou administradores inquilinos com a função de administrador global podem iniciar sessão neste portal. Para aceder à consola de administração, a sua conta tem de ter uma licença para utilizar o Intune e o estado de início de sessão definido como **Permitido**.
