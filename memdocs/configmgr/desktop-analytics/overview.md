---
title: Análise de Computadores
titleSuffix: Configuration Manager
description: Uma visão geral do serviço Desktop Analytics integrado com o Gestor de Configuração.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b280661c4de9282d3907b7d480477fc67f6a8dc5
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824069"
---
# <a name="what-is-desktop-analytics"></a>O que é a Análise de Computadores?

Desktop Analytics é um serviço baseado na nuvem que se integra com o Gestor de Configuração. O serviço fornece informações e inteligência para que tome decisões mais informadas sobre a prontidão da atualização dos seus clientes Windows. Combina dados da sua organização com dados agregados de milhões de dispositivos ligados aos serviços de cloud da Microsoft.

Utilize o Desktop Analytics com o Gestor de Configuração para:  

- Crie um inventário de aplicações em execução na sua organização  

- Avaliar a compatibilidade das aplicações com as mais recentes atualizações de funcionalidades do Windows 10  

- Identifique problemas de compatibilidade e receba sugestões de mitigação com base em insights de dados ativados pela nuvem  

- Criar grupos piloto que representem toda a aplicação e propriedade de motorista em um conjunto mínimo de dispositivos  

- Implementar o Windows 10 para dispositivos piloto e geridos pela produção  

![Screenshot da página inicial do Desktop Analytics no portal Azure](media/portal-home.png)

O vídeo seguinte é uma sessão da Ignite 2019, que inclui mais informações sobre desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Utilizando desktop Analytics e Gestor de Configuração para reduzir o Windows TCO através de insights orientados por dados para gestão, manutenção e suporte](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Salta para as 10:00 para uma demonstração aprofundada.

> [!Note]  
> Desktop Analytics é um sucessor do Windows Analytics, que se reformou a 31 de janeiro de 2020.
>
> As capacidades do Windows Analytics são combinadas no serviço Desktop Analytics. O Desktop Analytics também está mais bem integrado com o Gestor de Configuração. Para mais informações, consulte as [FAQ para clientes Windows Analytics](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Benefícios

Muitos clientes têm desafios em obter e manter-se atuais com o Windows 10. O principal desafio é testar aplicações. Este processo é tipicamente manual. É demorado para administradores de TI e proprietários de aplicações analisarem continuamente as aplicações existentes. Em seguida, remediar quaisquer problemas que surjam.

Desktop Analytics fornece os seguintes benefícios:

- Inventário de **dispositivos e software**: Inventário de fatores-chave como apps e versões do Windows.  

- **Identificação do piloto**: Identificação do conjunto mais pequeno de dispositivos que proporcionam a maior cobertura de fatores. Foca-se nos fatores que são mais importantes para um piloto de atualizações e atualizações do Windows. Certificar-se de que o piloto é mais bem sucedido permite-lhe proceder de forma mais rápida e confiante a amplas implantações na produção.  

- **Identificação de problemas**: Utilizando dados de mercado agregados juntamente com dados do seu ambiente, o serviço prevê potenciais problemas para obter e manter-se atual com o Windows. Em seguida, sugere potenciais atenuações.  

- **Integração do Gestor**de Configuração : A nuvem de serviço permite a sua infraestrutura existente no local. Utilize estes dados e análises para implementar e gerir o Windows nos seus dispositivos.  

## <a name="prerequisites"></a>Pré-requisitos

Para utilizar o Desktop Analytics, certifique-se de que o seu ambiente cumpre os seguintes pré-requisitos.

### <a name="technical"></a>Parte Técnica

- Uma subscrição ativa global do Azure, com permissões [da Global Admin.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) [As Contas](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) Microsoft não são suportadas.  

    > [!Important]  
    > O Desktop Analytics exige atualmente que implemente um serviço office 365 no seu inquilino Azure AD. Isto não será um requisito no futuro.

    - **Permissões** do proprietário do espaço de trabalho para **configurar o seu espaço de trabalho,** e as seguintes funções:  

      - [**Função**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) de Administrador de Análise de Ambiente de Trabalho.

      - [**Log Analytics Contributor**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [**User Access Administrator**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) no grupo de recursos para usar um espaço de trabalho existente ou criar um novo espaço de trabalho num grupo de recursos existente.

      - [**Proprietário**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), ou [**Contribuinte**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e Administrador de [**Acesso ao Utilizador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) permissões na subscrição para criar um espaço de trabalho num novo grupo de recursos.  

    - Para aceder ao portal após o embarque, precisa de:

      - [**Função**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) de Administrador de Análise de Desktop e [**Proprietário,**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)ou Permissões [**do Colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) no grupo de recursos onde o espaço de trabalho foi criado.

- Configuração Manager, versão 1902 com rollup de atualização (4500571) ou mais tarde. Para mais informações, consulte ['Update Configuration Manager'.](connect-configmgr.md#bkmk_hotfix)  

    - [**Papel de Administrador Completo**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) no Gestor de Configuração  

    > [!NOTE]
    > Desktop Analytics suporta várias hierarquias do Gestor de Configuração reportando a um único inquilino azure AD.<!-- 4814075 --> Se tiver várias hierarquias no seu ambiente, tem as seguintes opções:
    >
    > - Use diferentes IDs Comerciais e inquilinos da Azure AD.
    > - Configure ambas as hierarquias para usar o mesmo ID comercial para partilhar o inquilino da AD Azure e a instância desktop Analytics. Utilize [diferentes aplicativos](connect-configmgr.md#bkmk_connect) para ligar cada hierarquia. Pode levar até 30 dias após desligar uma hiearquia para o portal refletir alterações. 

- Dispositivos com windows 7, Windows 8.1 ou Windows 10  

    - Instale as últimas atualizações. Para mais informações, consulte [os dispositivos De atualização](enroll-devices.md#update-devices).  

    - Os dispositivos também precisam de ter o cliente do Gestor de Configuração, versão 1902 com rollup de atualização (4500571) ou mais tarde. Para mais informações, consulte ['Update Configuration Manager'.](connect-configmgr.md#bkmk_hotfix)  

    > [!Note]  
    > O Desktop Analytics não suporta atualizações para o canal de manutenção de longo prazo do Windows 10 (LTSC). Para mais informações, consulte o [Windows como uma visão geral](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)do serviço .
    >
    > O Desktop Analytics foi concebido para melhor suportar o cenário de atualização no local. Se precisar de fazer grandes alterações, como de arquitetura de 32 a 64 bits, use um cenário de imagem. As ideias do Desktop Analytics ainda são valiosas nestes cenários clássicos de implementação do SO, mas pode ignorar a orientação específica de upgrade no local. Para mais informações, consulte [Cenários para implantar sistemas operativos empresariais com o Gestor](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)de Configuração .

- Dados de diagnóstico do Windows. Para obter mais informações, veja os seguintes artigos:  

    - [Níveis de dados de diagnóstico](enable-data-sharing.md#diagnostic-data-levels)  

    - [Privacidade desktop Analytics](privacy.md)  

- Conectividade de rede de dispositivos para a nuvem pública da Microsoft. Para mais informações, consulte [Como permitir a partilha de dados](enable-data-sharing.md)  

> [!Important]
> A Microsoft tem um forte compromisso em fornecer as ferramentas e recursos que o colocam no controlo da sua privacidade. Como resultado, a Microsoft não recolhe os seguintes dados de dispositivos localizados em países europeus (EEE e Suíça):
>
> - Dados de diagnóstico do Windows a partir de dispositivos Windows 8.1
> - Dados de utilização de aplicativos para o Windows 7

### <a name="licensing-and-costs"></a>Licenciamento e custos

- Uma subscrição ativa global do Azure.

    > [!NOTE]
    > A maioria das subscrições equivalentes para O Gestor de Configuração também incluem Azure AD. Por exemplo, consulte [os planos microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) e o [licenciamento de Segurança da Enterprise Mobility +](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security)Security .

- Os dispositivos matriculados no Desktop Analytics precisam de uma licença de Gestor de Configuração válida. Para mais informações, consulte o licenciamento do Gestor de [Configuração.](../core/understand/product-and-licensing-faq.md)

- Os utilizadores do dispositivo precisam de uma das seguintes licenças:

  - Windows 10 Enterprise E3 ou E5 (incluído na Microsoft 365 F3, E3 ou E5)

  - Educação Windows 10 A3 ou A5 (incluído na Microsoft 365 A3 ou A5)

  - Windows Virtual Desktop Access E3 ou E5  

> [!NOTE]
> Para além do custo destas subscrições de licença, não há custos adicionais para a utilização do Desktop Analytics dentro do Azure Log Analytics. Os tipos de dados ingeridos pelo Desktop Analytics estão isentos de quaisquer encargos de ingestão e retenção de dados do Log Analytics. Como tipos de dados não faturados, estes dados também não estão sujeitos a nenhuma tampa de ingestão diária de dados do Log Analytics. Para mais informações, consulte o [uso e os custos do Log Analytics.](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)

## <a name="next-steps"></a>Próximos passos

O seguinte tutorial fornece um guia passo a passo para começar com desktop Analytics e Gestor de Configuração:
  
> [!div class="nextstepaction"]
> [Implementar o Windows 10 para o piloto](tutorial-windows10.md)
