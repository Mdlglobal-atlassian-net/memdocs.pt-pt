---
title: Utilizar a AD Azure para cogestão
titleSuffix: Configuration Manager
description: Com o Azure AD pode aproveitar a melhoria da produtividade dos seus utilizadores e segurança para os seus recursos, tanto em ambientes cloud como on-prem
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711526"
---
# <a name="use-azure-ad-for-co-management"></a>Utilizar a AD Azure para cogestão

Na nuvem, a identidade é o novo plano de controlo. O Azure Ative Directory (Azure AD) permite ligar os seus utilizadores, dispositivos e aplicações em ambientes de nuvem e no local. Registar os seus dispositivos no Azure AD permite-lhe melhorar a produtividade dos seus utilizadores e a segurança dos seus recursos. Ter dispositivos em Azure AD é a base tanto para a cogestão como para o acesso condicional baseado em dispositivos.

Para obter mais informações sobre o acesso condicional baseado no dispositivo, consulte [Como: Exigir dispositivos geridos para acesso](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices) a aplicações na nuvem com acesso condicional

No vídeo seguinte, o gestor sénior de programas Sandeep Deo e o gestor de marketing de produtos Adam Harbour discutem e demo Azure AD para cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

A Azure AD oferece duas opções para dispositivos da empresa que se adequam às necessidades da sua organização:  

- **Dispositivo ligado ao Azure AD : Junte-se**aos seus dispositivos Windows 10 para a AD Azure sem necessidade de os juntar ao seu Diretório Ativo no local  

  - Suporta o Windows 10

  - Instale-se sem necessidade de qualquer configuração adicional para os seus ambientes no local  

  - Ao permitir algumas definições em AD Azure, pode permitir que os seus utilizadores se juntem a dispositivos ao Azure AD através da experiência de configuração do Windows (OOBE)  

  - Para mais informações, consulte [Como: Planeie a sua adad Azure aderir à implementação](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Dispositivo híbrido azure ad- joined**: Junte-se aos seus dispositivos já existentes unidos pelo domínio para Azure AD  

  - Suporta Windows 10, Windows 8.1 e Windows 7

  - Configurar utilizando reclamações AD FS ou Azure AD Connect  

  - Para o Windows 10 a adesão acontece no contexto da máquina, para que os utilizadores não tenham de tomar medidas adicionais  

  - Para mais informações, consulte [Como planear a sua implementação híbrida Azure Ative Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Ambas as opções fornecem funcionalidades semelhantes para os utilizadores. É flexível para si escolher qualquer um com base nas suas necessidades. Por exemplo, pode aceder aos seus recursos no local a partir de [máquinas](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) ad-joined Azure, mesmo que não estejam unidas ao Ative Directory.

Pode juntar dispositivos ao Azure AD em vários ambientes, independentemente do seu método de [autenticação.](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn) Por exemplo, autenticação federada ou autenticação em nuvem.

Se já tem um Diretório Ativo no local, a configuração de qualquer uma das opções é simples.

## <a name="benefits"></a>Benefícios

A junção de dispositivos à Azure AD proporciona os seguintes benefícios à sua organização:

### <a name="single-sign-on-to-cloud-resources"></a>Inscrição única para os recursos em nuvem

Nos dispositivos associados ao Azure AD, obtém-se uma experiência integrada de acesso a qualquer nuvem ou recursos no local. Assim que iniciar sessão numa máquina do Windows que esteja associada ao Azure AD, obtém um único sessão em todas as aplicações sem qualquer aviso adicional de entrada.  

### <a name="windows-hello-for-business"></a>Windows Hello para empresas

O Windows Hello for Business traz uma autenticação forte sem palavra-passe para o Windows 10. Ao juntar os seus dispositivos ao Azure AD, pode ativar o Windows Hello for Business através da sua base de utilizadores tanto para os recursos em nuvem como no local. O Windows Hello for Business elimina o problema de lembrar palavras-passe complexas ou expô-las inadvertidamente. O seu processo de inscrição é simples e seguro.

Para mais informações, consulte [o Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Acesso condicional baseado no dispositivo

Ative o acesso condicional com base no estado do dispositivo para proteger melhor os dados da sua organização. O acesso condicional baseado no dispositivo requer um dispositivo gerido. Este dispositivo deve ser um dispositivo compatível ou um dispositivo híbrido azure ad-join. Para dispositivos azure ad-join, você precisa de Intune para marcar o dispositivo como conforme. Mas para dispositivos híbridos azure ad-join, o próprio estado do dispositivo é usado para avaliar o acesso condicional. A cogestão proporciona-lhe a vantagem adicional de avaliar a conformidade através do Intune para dispositivos híbridos azure ad-joined. Esta função certifica-se de que a configuração do dispositivo está intacta.

Para obter mais informações sobre o acesso condicional baseado no dispositivo, consulte [Como: Exigir dispositivos geridos para acesso](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)à aplicação na nuvem com acesso condicional .  

### <a name="automatic-device-licensing"></a>Licenciamento automático de dispositivos

Todos os dispositivos do Windows 10 juntos ao Azure AD passam por verificações de licença. Estas verificações permitem atualizá-las automaticamente de Pro para Enterprise através da nuvem microsoft. Ao remover a subscrição relevante do utilizador, o dispositivo diminui automaticamente a sua licença. Esta funcionalidade fornece um único painel de controlo para a gestão das licenças do Windows, sem quaisquer processos complicados ou sistemas no local.

### <a name="self-service-functionality"></a>Funcionalidade de self-service

A funcionalidade de self-service inclui o reset de palavra-passe self-service e a chave de recuperação BitLocker. O Azure AD também lhe fornece opções diretas para redefinir a sua palavra-passe ou aceder às chaves de recuperação bitLocker. Pode utilizar o Azure AD para redefinir a sua palavra-passe diretamente a partir do ecrã de bloqueio do Windows, em vez de ser de um navegador web. Estas funcionalidades reduzem o atrito para os utilizadores e ajudam a reduzir os custos de helpdesk para a sua organização.  

Para mais informações, consulte [Tutorial: Ative os utilizadores a desbloquearem a sua conta ou a redefinirem as palavras-passe utilizando o reset da palavra-passe self-service do Diretório Ativo Do Azure](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Roaming do estado empresarial

Todos os dispositivos unidos ao Azure AD podem sincronizar as suas definições na nuvem. Qualquer dispositivo ao qual um utilizador assina sincroniza todas as suas definições para uma experiência mais produtiva.  

## <a name="value-proposition"></a>Proposta de valor

Juntar os seus dispositivos ao Azure AD através de qualquer um dos métodos acelera a sua transformação digital. Permite mais funcionalidades fornecidas pelo Microsoft 365. Terá melhores experiências e terá maior segurança para os seus dados.

A Azure AD oferece várias opções para aliviar a sua carga de trabalho, por exemplo:

- Gerencie todas as identidades do dispositivo na sua organização a partir de um único lugar  

- Reduza os custos do seu helpdesk permitindo o reset da palavra-passe self-service. Depois, os utilizadores podem redefinir a sua palavra-passe a partir do ecrã de bloqueio do Windows 10 no seu dispositivo a qualquer momento.  

## <a name="configure"></a>Configurar

Se já tem um ambiente de Diretório Ativo no local, e deseja juntar os seus dispositivos unidos ao domínio para o Azure AD, configure dispositivos híbridos ligados ao Azure AD. Para mais informações, [Como: Planeie o seu Diretório Ativo Azure híbrido aderir à implementação](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

O Gestor de Configuração tem uma definição de cliente para [registar automaticamente novos dispositivos ligados ao domínio do Windows 10 com a AD Azure](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Para obter mais informações sobre a configuração das definições do cliente, consulte [como configurar as definições](../core/clients/deploy/configure-client-settings.md)do cliente .

Se pretender configurar a ad-join Azure para os seus dispositivos sem também os juntar ao seu domínio no local, reveja as considerações para a adesão de Azure AD no seu ambiente. Uma vez que decidiu ir com a AD Azure, você tem muitas opções para implementá-lo com base nas necessidades da sua organização. Para obter mais informações, veja os artigos seguintes:

- [Como: Planear a sua adad Azure aderir à implementação](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Compreenda as suas opções de provisionamento](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  
