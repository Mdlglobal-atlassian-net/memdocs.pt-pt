---
title: HTTP melhorado
titleSuffix: Configuration Manager
description: Utilize a autenticação moderna para garantir a comunicação do cliente sem a necessidade de certificados PKI.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720178"
---
# <a name="enhanced-http"></a>HTTP melhorado

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1356889,1358460-->

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1806 como [uma funcionalidade de pré-lançamento.](../../servers/manage/pre-release-features.md) A partir da versão 1810, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  

A Microsoft recomenda a utilização da comunicação HTTPS para todos os caminhos de comunicação do Gestor de Configuração, mas é um desafio para alguns clientes devido à sobrecarga de gestão de certificados PKI.

A versão 1806 do Gestor de Configuração inclui melhorias na forma como os clientes comunicam com os sistemas do site. Há dois objetivos primários para estas melhorias:  

- Pode garantir uma comunicação sensível do cliente sem a necessidade de certificados de autenticação do servidor PKI.  

- Os clientes podem aceder de forma segura a conteúdos a partir de pontos de distribuição sem a necessidade de uma conta de acesso à rede, certificado PKI cliente e autenticação do Windows.  

Toda a comunicação do cliente está acima de HTTP. O HTTP melhorado não é o mesmo que permitir https para comunicação do cliente ou um sistema de site.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> Os certificados PKI continuam a ser uma opção válida para os clientes com os seguintes requisitos:  
>
> - Toda a comunicação do cliente está sobre HTTPS  
> - Controlo avançado da infraestrutura de assinatura
>
> Além disso, Se já estiver a utilizar o PKI, o certificado PKI ligado ao IIS será utilizado mesmo que o HTTP melhorado seja ligado.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Cenários

Os seguintes cenários beneficiam destas melhorias:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a>Cenário 1: Cliente para ponto de gestão

<!--1356889-->
[Os dispositivos unidos pelo Azure Ative Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) podem comunicar com um ponto de gestão configurado para HTTP. O servidor do site gera um certificado para o ponto de gestão que lhe permite comunicar através de um canal seguro.

> [!Note]  
> Este comportamento é alterado a partir da versão atual do Gerente de Configuração 1802, que requer um ponto de gestão ativado por HTTPS para clientes unidos pela AD azure comunicando através de um gateway de gestão de nuvem. Para mais informações, consulte O ponto de [gestão enable para HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a>Cenário 2: Cliente para ponto de distribuição

<!--1358228-->
Um grupo de trabalho ou um cliente azure ad-join-join pode autenticar e transferir conteúdo em um canal seguro a partir de um ponto de distribuição configurado para HTTP. Este tipo de dispositivos também pode autenticar e descarregar conteúdo a partir de um ponto de distribuição configurado para HTTPS sem necessitar de um certificado PKI no cliente. É um desafio adicionar um certificado de autenticação de cliente a um grupo de trabalho ou cliente azure ad-join.

Este comportamento inclui cenários de implementação de OS com uma sequência de tarefas que funciona a partir de suportes de arranque, PXE ou Software Center. Para mais informações, consulte [a conta](accounts.md#network-access-account)de acesso à Rede .<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a>Cenário 3: Identidade do dispositivo Azure AD

<!--1358460-->
Um [dispositivo Azure Azure AD](/azure/active-directory/devices/concept-azure-ad-join-hybrid) filiado ou híbrido azure sem um utilizador Azure AD assinado pode comunicar com segurança com o seu site atribuído. A identidade do dispositivo baseado na nuvem é agora suficiente para autenticar com o CMG e ponto de gestão para cenários centrados no dispositivo. (Ainda é necessário um sinal de utilizador para cenários centrados no utilizador.)  


## <a name="features"></a>Funcionalidades

O seguinte Gestor de Configuração apresenta suporte ou requer HTTP melhorado:

- [Gateway de gestão da cloud](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Implantação de OS sem conta de acesso à rede](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Ativar a cogestão de novos dispositivos Windows 10 baseados na Internet](../../../comanage/tutorial-co-manage-new-devices.md)
- [Aprovações de aplicativos por e-mail](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Serviço de administração](../../../develop/adminservice/overview.md)
- [Ver consolas recentemente conectadas](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> O ponto de atualização de software e cenários relacionados sempre apoiaram o tráfego http seguro com os clientes, bem como o gateway de gestão de nuvem. Usa um mecanismo com o ponto de gestão diferente da autenticação baseada em certificados ou tokens.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Pré-requisitos  

- Um ponto de gestão configurado para ligações ao cliente HTTP. Descoloque esta opção no separador **Geral** das propriedades do ponto de gestão.  

- Um ponto de distribuição configurado para ligações ao cliente HTTP. Descoloque esta opção no separador **comunicação** das propriedades do ponto de distribuição. Não permita que os **clientes se conectem de forma anónima**.  

- A bordo do site para Azure AD para gestão de nuvens.  

    - Se já preencheu este pré-requisito para o seu site, precisa de atualizar a aplicação Azure AD. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud,** e selecione **Azure Ative Directory Tenants**. Selecione o inquilino Azure AD, selecione a aplicação web no painel **de aplicações** e, em seguida, selecione a definição de **aplicação Update** na fita.  

- *Apenas para o [Cenário 3:](#bkmk_scenario3) *Um cliente que executa a versão 1803 do Windows 10 ou mais tarde, e juntou-se ao Azure AD. O cliente requer esta configuração para autenticação do dispositivo Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Configure o site

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Selecione o site e escolha **Propriedades** na fita.  

2. Mude para o separador comunicação do **computador cliente.**

    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

    Selecione a opção para **HTTPS ou HTTP**. Em seguida, ative a opção de **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**.

> [!Tip]
> Aguarde até 30 minutos para que o ponto de gestão receba e configure o novo certificado a partir do site.

<!--3798957-->
A partir da versão 1902, também pode ativar http melhorado para o site da administração central. Use este mesmo processo e abra as propriedades do site da administração central. Esta ação apenas permite um HTTP reforçado para as funções de Provedor de SMS no site da administração central. Não é um cenário global que se aplica a todos os sites da hierarquia.

Pode ver estes certificados na consola 'Gestor de Configuração'. Vá ao espaço de trabalho da **Administração,** expanda **a Segurança**e selecione o nó de **Certificados.** Procure o certificado raiz de **emissão SMS,** bem como os certificados de função do servidor do site emitidos pela raiz de emissão SMS.

Para obter mais informações sobre como o cliente comunica com o ponto de gestão e ponto de distribuição com esta configuração, consulte [comunicações de clientes para sistemas e serviços do site.](communications-between-endpoints.md#Planning_Client_to_Site_System)


## <a name="see-also"></a>Consulte também

- [Plano de segurança](../security/plan-for-security.md)  

- [Segurança e privacidade para clientes do Gestor de Configuração](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar a segurança](../security/configure-security.md)  

- [Comunicação entre pontos finais](communications-between-endpoints.md)  
