---
title: Cogestão para os dispositivos com Windows 10
titleSuffix: Configuration Manager
description: Saiba como gerir simultaneamente os dispositivos do Windows 10 utilizando tanto o Gestor de Configuração como o Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e06dc0d40eb6359d11ef31045989d7ed398b3687
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711323"
---
# <a name="what-is-co-management"></a>O que é a cogestão?

<!-- 1350871 -->
A cogestão é uma das principais formas de anexar a implementação do seu Gestor de Configuração existente à nuvem Microsoft 365. Ajuda-o a desbloquear capacidades adicionais alimentadas por nuvem, como acesso condicional.

A cogestão permite-lhe fazer a gestão de dispositivos com o Windows 10 ao utilizar simultaneamente o Configuration Manager e o Microsoft Intune. Permite anexar o seu investimento em Configuração, adicionando uma nova funcionalidade. Ao utilizar a cogestão, tem a flexibilidade para utilizar a solução tecnológica que funciona melhor para a sua organização.

Quando um dispositivo Windows 10 tem o cliente do Gestor de Configuração e está matriculado no Intune, obtém-se os benefícios de ambos os serviços. Controla quais as cargas de trabalho, se houver, muda a autoridade do Gestor de Configuração para Intune. O Gestor de Configuração continua a gerir todas as outras cargas de trabalho, incluindo as cargas de trabalho que não muda para Intune, e todas as outras funcionalidades do Gestor de Configuração que a cogestão não suporta.

Também é capaz de pilotar uma carga de trabalho com uma coleção separada de dispositivos. A pilotagem permite-lhe testar a funcionalidade Intune com um subconjunto de dispositivos antes de mudar um grupo maior.

![Diagrama de visão geral da cogestão](media/co-management-overview.svg)

[Ver o diagrama em tamanho real](media/co-management-overview.svg)

> [!Note]  
> Quando gere simultaneamente dispositivos Do Windows 10 com o Gestor de Configuração e o Microsoft Intune, esta configuração *chama-se cogestão*. Quando gere dispositivos com Gestor de Configuração e se inscreva num serviço DE MDM de terceiros, esta configuração chama-se *coexistência*. Ter duas autoridades de gestão para um único dispositivo pode ser um desafio se não devidamente orquestrado entre os dois. Com cogestão, Configuração Manager e Intune equilibram as [cargas de trabalho](#workloads) para garantir que não há conflitos. Esta interação não existe com serviços de terceiros, pelo que existem limitações com as capacidades de gestão da coexistência. Para mais informações, consulte a [coexistência de MDM de terceiros com o Gestor de Configuração](coexistence.md).

## <a name="paths-to-co-management"></a>Caminhos para a cogestão

Há dois caminhos principais a alcançar para a cogestão:  

- Clientes de Gestor de **Configuração existentes:** Tem dispositivos Windows 10 que já são clientes do Gestor de Configuração. Criaste o Azure AD híbrido e inscreve-os no Intune.  

- **Novos dispositivos baseados na Internet:** Tem novos dispositivos Windows 10 que se juntam ao Azure AD e se inscrevem automaticamente no Intune. Instala o cliente do Gestor de Configuração para chegar a um estado de cogestão.  

Para obter mais informações sobre os caminhos, consulte [Caminhos para a cogestão.](quickstart-paths.md)

## <a name="benefits"></a>Benefícios

Ao inscrever os clientes do Gestor de Configuração existentes em cogestão, ganha o seguinte valor imediato:  

- Acesso condicional com conformidade do dispositivo  

- Ações remotas baseadas em intune, por exemplo: reiniciar, telecomando ou repor fábrica

- Visibilidade centralizada da saúde do dispositivo  

- Link utilizadores, dispositivos e aplicações com Diretório Ativo Azure (Azure AD)  

- Fornecimento moderno com Windows Autopilot  

- Ações remotas

Para obter mais informações sobre este valor imediato da cogestão, consulte a série quickstarts para [cloud connect with co-management](quickstarts.md).

A cogestão também permite orquestrar com intune para várias cargas de trabalho. Para mais informações, consulte a secção [Cargas de Trabalho.](#workloads)

## <a name="prerequisites"></a>Pré-requisitos

A cogestão tem estes pré-requisitos nas seguintes áreas:

- [Licensing](#licensing)  
- [Gestor de configuração](#configuration-manager)  
- [Diretório Ativo Azure](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Permissões e funções](#permissions-and-roles)  

### <a name="licensing"></a>Licenciamento

- Azure AD Premium

    > [!Note]  
    > Uma subscrição de Mobilidade Empresarial + Segurança (EMS) inclui tanto o Azure Ative Directory Premium como o Microsoft Intune.

- Pelo menos uma licença Intune para si como administrador para aceder ao portal Intune.

    > [!Tip]
    > Certifique-se de atribuir uma licença Intune à conta que usa para iniciar sessão com o seu inquilino. Caso contrário, o sessão falha com a mensagem de erro "Utilizador não reconhecido".
    >
    > Já não precisa de adquirir e atribuir licenças individuais intune ou EMS aos seus utilizadores. Para mais informações, consulte o [Produto e licenciando as FAQ.](../core/understand/product-and-licensing-faq.md#bkmk_mem)

### <a name="configuration-manager"></a>Gestor de configuração

A cogestão requer a versão 1710 do Gestor de Configuração ou mais tarde.

Começando na versão 1806 do Gestor de Configuração, pode ligar várias instâncias do Gestor de Configuração a um único inquilino Intune. <!--1357944-->  

Permitir a cogestão em si não requer que você embarque no seu site com a Azure AD. Para o segundo cenário de [caminho,](#paths-to-co-management)os clientes do Gestor de Configuração baseadona na Internet requerem o gateway de [gestão](../core/clients/manage/cmg/plan-cloud-management-gateway.md) da nuvem (CMG). O CMG requer que o site esteja [a bordo da Azure AD para gestão de nuvens.](../core/servers/deploy/configure/azure-services-wizard.md)

### <a name="azure-ad"></a>Azure AD

- Os dispositivos Windows 10 devem ser unidos ao Azure AD. Podem ser um dos seguintes tipos:  

  - [Hybrid Azure-joined AD,](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)onde o dispositivo está unido ao seu Diretório Ativo no local e se juntou ao seu Diretório Ativo Azure.  

  - [Azure AD só se juntou.](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) (Este tipo é por vezes referido como "cloud domínio-joined")<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Configurar o Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Ativar a inscrição automática de dispositivos Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Atualize os seus dispositivos para o Windows 10, versão 1709 ou mais tarde. Para mais informações, consulte [a Adoção do Windows como um serviço](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Os dispositivos móveis do Windows 10 não suportam a cogestão.

### <a name="permissions-and-roles"></a>Permissões e funções

<!--SCCMDocs issue #667-->
| Ação | Papel necessário |
|----|----|
| Criar um gateway de gestão de nuvem no Gestor de Configuração | Gestor **de Subscrição** Azure |
| Criar aplicativos Azure AD a partir de Configuração Manager | **Administrador Global** da Azure AD |
| Import Azure aplicações em Gestor de Configuração | Administrador **completo** do Gestor de Configuração<br>Não são necessárias funções adicionais do Azure |
| Ativar a cogestão no Gestor de Configuração | Um utilizador de Anúncios Azure<br>Gestor de Configuração **Administrador Completo** com **Todos os** direitos de âmbito.<!--SCCMDoc issue 626--> |

Para obter mais informações sobre os papéis do Azure, consulte [Compreender os diferentes papéis.](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)

Para obter mais informações sobre as funções do Gestor de Configuração, consulte [os fundamentos da administração baseada em papéis.](../core/understand/fundamentals-of-role-based-administration.md)

## <a name="workloads"></a>Cargas de trabalho

Não tens de mudar as cargas de trabalho, ou podes fazê-las individualmente quando estiveres pronta. O Gestor de Configuração continua a gerir todas as outras cargas de trabalho, incluindo as cargas de trabalho que não muda para Intune, e todas as outras funcionalidades do Gestor de Configuração que a cogestão não suporta.

A cogestão suporta as seguintes cargas de trabalho:

- Políticas de conformidade  

- Políticas de Atualização do Windows  

- Políticas de acesso a recursos  

- Endpoint Protection  

- Configuração do dispositivo  

- Aplicativos click-to-run do Office  

- Aplicações do cliente  

Para mais informações, consulte [Cargas de Trabalho](workloads.md).

## <a name="monitor-co-management"></a>Monitorizar a cogestão

O painel de cogestão ajuda-o a rever máquinas cogeridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que possam precisar de atenção.

![Screenshot do painel de cogestão](media/co-management-dashboard.png)

Para mais informações, consulte [Como monitorizar a cogestão.](how-to-monitor.md)

## <a name="next-steps"></a>Passos seguintes

- [Saiba mais sobre o valor imediato e começar com a cogestão](quickstarts.md)  

- [Tutorial: Ativar a cogestão dos clientes existentes do Gestor de Configuração](tutorial-co-manage-clients.md)  
