---
title: Página de Estado do Inquilino Intune da Microsoft
titleSuffix: Microsoft Intune
description: Utilize a página Intune Tenant Status para ver detalhes importantes do inquilino sem sair do portal Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 7954a686-25dc-4fce-b395-324816f46d3b
ms.reviewer: crisk
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4d747a38dd8e2f95cafb25ec5705f83199f4c54
ms.sourcegitcommit: 5dc3545d7f76ce81598f6b1c9734b0ac0a3e9722
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83690686"
---
# <a name="use-the-intune-tenant-status-page"></a>Utilize a página Intune Tenant Status

A página Microsoft Intune Tenant Status é um hub centralizado onde pode ver detalhes atuais e importantes sobre o seu inquilino. Os detalhes incluem disponibilidade e utilização da licença, estado do conector e comunicações importantes sobre o serviço Intune.

> [!TIP]
> Um inquilino é um caso de Azure Ative Directory (Azure AD). A sua subscrição ao Intune é hospedada por um Inquilino AD Azure. Para mais informações, consulte [A configuração de um inquilino](https://docs.microsoft.com/azure/active-directory/develop/quickstart-create-new-tenant) na documentação da AD Azure.

Para ver o dashboard, inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) vá para a **administração do Inquilino**, e, em seguida, selecione O Estatuto do **Inquilino**.

A página é dividida em três separadores:

## <a name="tenant-details"></a>Detalhes do inquilino
Os detalhes do inquilino fornecem informações sobre o seu inquilino. Consulte detalhes como o nome e localização do seu inquilino, a autoridade do MDM e o número de lançamento do serviço de inquilinos. O número de lançamento do serviço é um link que abre o *artigo "O que há de novo no intune"* sobre os docs da Microsoft. No *Que é novo,* pode ler sobre as mais recentes funcionalidades e atualizações para o serviço Intune.  

Neste separador também encontrará informações básicas sobre as suas licenças disponíveis e quantas são atribuídas aos utilizadores. As licenças para dispositivos não são mostradas.

## <a name="connector-status"></a>Estado do conector
O estado do conector é um local de paragem única para rever o estado de todos os conectores disponíveis para Intune.  

Os conectores são:
- **Ligações que configura a serviços externos.** Por exemplo, o serviço *apple volume purchase program* ou o serviço De Piloto Automático *windows.*  O estado deste tipo de conector baseia-se no último tempo de sincronização bem sucedido.
- **Certificados ou credenciais que são necessários para se ligarem a um serviço externo não gerido**, como certificados apple Push Notification *Services* (APNS). O estado deste tipo de conector baseia-se no carimbo de tempo de validade do certificado ou credencial.  

Ao abrir o separador de estado do *Conector,* quaisquer conectores não saudáveis exibem no topo da lista. Seguem-se os conectores com avisos e, em seguida, a lista de conectores saudáveis. Os conectores que ainda não configuraste aparecem em último, uma *vez que não está ativado*.

Quando há mais do que um único conector de qualquer tipo, o estado é um resumo para todos os mesmos conectores. O estado menos saudável de qualquer conector único é usado como saúde para o grupo.  

**Estado do conector:**
- **Insalubre:**
  - O certificado ou credencial expirou
  - A última sincronização foi há três ou mais dias.
- **Aviso:**
  - O certificado ou credencial expirará no prazo de sete dias
  - A última sincronização foi há mais de um dia.
- **Saudável:**
  - O certificado ou credencial não expirará nos próximos sete dias.
  - A última sincronização foi há menos de um dia.  

Ao selecionar um conector da lista, o portal apresenta a página do portal que é relevante para esse conector. Na página dos conectores pode visualizar o estado dos conectores previamente configurados ou selecionar opções para adicionar ou criar um novo conector desse tipo.

Por exemplo, se selecionar o conector **VPP Data expiração,** a página de **Tokens** do programa adquirido em volume do iOS abre onde pode ver mais detalhes sobre esse conector. Também pode criar uma nova configuração ou editar e corrigir problemas com um existente.

## <a name="service-health-dashboard"></a>Painel de saúde de serviço  
No painel de saúde do Serviço pode visualizar detalhes para *incidentes* de Serviço que afetam o seu inquilino, e *notícias Intune* que fornecem informações sobre atualizações e alterações planeadas.

### <a name="intune-service-health-and-message-center"></a>Intune Service Health e centro de mensagens
Consulte detalhes para incidentes e avisos ativos sem ter de navegar para o Microsoft 365 Service Health Dashboard ou para o Message Center, ambos localizados no centro de administração da [Microsoft 365](https://admin.microsoft.com). Só são mostrados incidentes que afetam o seu inquilino.  

Quando seleciona um incidente, os detalhes do incidente são apresentados diretamente na página do Estado do Inquilino. Para ver avisos e incidentes passados, selecione **Ver incidentes/avisos passados**. O centro de administração da Microsoft 365 abre e pode ver avisos e incidentes dos últimos 30 dias para o seu inquilino.  

Para visualizar informações para A *Saúde do Serviço Intune,* a sua conta deve ter o papel de **Administrador Global** ou Suporte de **Serviço** no Diretório Ativo Azure ou no centro de administração da Microsoft 365. Para atribuir estas permissões, inscreva-se no centro de administração da [Microsoft 365](https://admin.microsoft.com) com permissões do Administrador Global. Selecione **Utilizadores > Utilizadores Ativos**e, em seguida, selecione a conta que requer acesso. **Selecione Editar** para Funções, selecione administrador de suporte de *serviço* ou *administrador global,* e em **seguida, Guarde** a sua edição para atribuir as permissões.  

Só é possível configurar as suas preferências de comunicação para a Intune Service Health através do centro de administração da Microsoft 365.

### <a name="intune-message-center"></a>Centro de Mensagens Intune  
Consulte as comunicações informativas da equipa de serviço Intune sem ter de navegar para o Centro de Mensagens do Escritório. As comunicações incluem mensagens sobre alterações que aconteceram recentemente ao serviço Intune, ou que estão a caminho do seu inquilino.  

Por padrão, as 10 mensagens mais recentes e ativas exibem. Para ver mensagens mais antigas, selecione **Ver Mensagens passadas** para abrir o centro de *mensagens* no centro de administração da Microsoft 365.  

Para visualizar informações para Intune News, a sua conta deve ter o papel de administrador de **suporte** global ou de suporte de **serviço** no Diretório Ativo do Azure ou o papel de leitor do **Message Center** no centro de administração da Microsoft 365.  Para atribuir esta permissão, inscreva-se no centro de administração da [Microsoft 365](https://admin.microsoft.com) com permissões de administrador. Selecione **Utilizadores > Utilizadores Ativos**e, em seguida, selecione a conta que requer acesso. **Selecione Editar** para *Funções,* selecione *Teams Communications Administrator*e, em seguida, **Guarde** a sua edição para atribuir as permissões.  

Só é possível configurar as suas preferências de comunicação para o centro de mensagens Intune através do centro de administração da Microsoft 365.
