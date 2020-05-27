---
title: Configurar a inscrição para dispositivos Windows com o Microsoft Intune
titleSuffix: ''
description: Configure a inscrição para dispositivos Windows.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9104716c469168a5ab2c5c1b49caf14071150db1
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988903"
---
# <a name="set-up-enrollment-for-windows-devices"></a>Configurar a inscrição para dispositivos Windows

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Este artigo ajuda os administradores de TI a simplificar a inscrição de dispositivos Windows para os seus utilizadores. Assim que tiver [configurado o Intune](../fundamentals/setup-steps.md), os utilizadores inscrevem os dispositivos do Windows ao [iniciar sessão](https://docs.microsoft.com/mem/intune/user-help/windows-enrollment-company-portal) na respetiva conta escolar ou profissional.  

Enquanto administrador do Intune, pode simplificar a inscrição das seguintes formas:

- [Ativar a inscrição automática](#enable-windows-10-automatic-enrollment) (Azure AD Premium necessário)
- [Registo CNAME](#simplify-windows-enrollment-without-azure-ad-premium)
- [Ativar a inscrição](windows-bulk-enroll.md) a granel (Azure AD Premium e Windows Configuration Designer necessário)

Dois fatores determinam como pode simplificar a inscrição de dispositivos do Windows:

- **Utiliza o Azure Active Directory Premium?** <br>O [Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) está incluído com o Enterprise Mobility + Security e outros planos de licenciamento.
- **Que versões de clientes do Windows serão inscritas pelos utilizadores?** <br>Os dispositivos Windows 10 podem ser inscritos automaticamente ao adicionar uma conta escolar ou profissional. As versões anteriores têm de ser inscritas através da aplicação Portal da Empresa.

||**Azure AD Premium**|**Outros AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscrição automática](#enable-windows-10-automatic-enrollment) |Inscrição do utilizador|
|**Versões do Windows anteriores**|Inscrição do utilizador|Inscrição do utilizador|

As organizações que podem utilizar a inscrição automática também podem configurar a [inscrição de dispositivos em massa](windows-bulk-enroll.md) com a aplicação Windows Configuration Designer.

## <a name="device-enrollment-prerequisites"></a>Pré-requisitos de inscrição do dispositivo

Antes de um administrador poder inscrever dispositivos para Intune para gestão, as licenças já deveriam ter sido atribuídas à conta do administrador. [Ler sobre a atribuição de licenças para a inscrição de dispositivos](../fundamentals/licenses-assign.md)

## <a name="multi-user-support"></a>Suporte para múltiplos utilizadores

Intune suporta vários utilizadores em dispositivos que ambos:

- executar a atualização do Criador do Windows 10
- são Azure Ative Directory-joined domínio.

Quando os utilizadores padrão iniciam sessão com as suas credenciais do Azure AD, recebem aplicações e políticas atribuídas ao respetivo nome de utilizador. Só o [utilizador principal](../remote-actions/find-primary-user.md) do dispositivo pode utilizar o Portal da Empresa para cenários de self-service como instalar aplicações e executar ações de dispositivo (Remover, Redefinir). Para dispositivos partilhados do Windows 10 que não tenham um utilizador primário atribuído, o Portal da Empresa ainda pode ser utilizado para instalar aplicações disponíveis.

[!INCLUDE [AAD-enrollment](../includes/win10-automatic-enrollment-aad.md)]

## <a name="simplify-windows-enrollment-without-azure-ad-premium"></a>Simplificar a inscrição do Windows sem o Azure AD Premium
Para simplificar a inscrição, crie um alias (tipo de registo CNAME) de servidor de nomes de domínio (DNS) que redirecione os pedidos de inscrição para os servidores do Intune. Caso contrário, os utilizadores que tentem ligar ao Intune terão de introduzir o nome de servidor do Intune durante a inscrição.

**Passo 1: criar o registo CNAME** (opcional)<br>
Crie registos de recursos CNAME DNS para o domínio da sua empresa. Por exemplo, se o website da sua empresa for contoso.com, criaria um CNAME em DNS que redireciona EnterpriseEnrollment.contoso.com para enterpriseenrollment-s.manage.microsoft.com.

Apesar de a criação de entradas DNS CNAME ser opcional, os registos CNAME facilitam a inscrição para os utilizadores. Se não for encontrado nenhum registo CNAME de inscrição, os utilizadores receberão um pedido para introduzir manualmente o nome do servidor MDM, enrollment.manage.microsoft.com.

|Tipo|Nome do anfitrião|Aponta para|TTL|
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.dominio_da_empresa.com|EnterpriseEnrollment-s.manage.microsoft.com| Uma hora|
|CNAME|EnterpriseRegistration.dominio_da_empresa.com|EnterpriseRegistration.windows.net|Uma hora|

Se a empresa utilizar mais do que um sufixo UPN, tem de criar um CNAME para cada nome de domínio e apontar cada um para EnterpriseEnrollment-s.manage.microsoft.com. Por exemplo, os utilizadores na Contoso utilizam os seguintes formatos como e-mail/UPN:

- name@contoso.com
- name@us.contoso.com
- name@eu.contoso.com

Os administradores de DNS da Contoso devem criar os seguintes CNAMEs:

|Tipo|Nome do anfitrião|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|Uma hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|Uma hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| Uma hora|

`EnterpriseEnrollment-s.manage.microsoft.com`– Suporta um redirecionamento para o serviço Intune com reconhecimento de domínio a partir do nome de domínio do e-mail

As alterações aos registos DNS podem demorar até 72 horas a serem propagadas. Não é possível verificar a alteração de DNS no Intune até o registo DNS ser propagado.

## <a name="additional-endpoints-are-used-but-no-longer-supported"></a>São utilizados pontos finais adicionais, mas já não suportados
EnterpriseEnrollment-s.manage.microsoft.com é o FQDN preferido para inscrição. Há dois outros pontos finais que foram usados pelos clientes no passado e ainda funcionam, mas já não são apoiados. EnterpriseEnrollment.manage.microsoft.com (sem o -s) e manage.microsoft.com ambos funcionam como o destino para o servidor de deteção automática, mas o utilizador vai ter de selecionar OK numa mensagem de confirmação. Se apontar para EnterpriseEnrollment-s.manage.microsoft.com, o utilizador não terá de fazer o passo de confirmação adicional, por isso esta é a configuração recomendada

## <a name="alternate-methods-of-redirection-are-not-supported"></a>Não São Suportados Métodos Alternativos de Redirecionamento
Não é suportada a utilização de um método que não seja a configuração do CNAME. Por exemplo, não é suportada a utilização de um servidor proxy para redirecionar enterpriseenrollment.contoso.com/EnrollmentServer/Discovery.svc para enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc ou para manage.microsoft.com/EnrollmentServer/Discovery.svc.

**Passo 2: verificar o CNAME** (opcional)<br>
1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)escolha **dispositivos**  >  **windows**  >  **windows**  >  **inscrição CNAME Validação**.
2. Na caixa **Domínio**, introduza o site da empresa e, em seguida, selecione **Testar**.

## <a name="tell-users-how-to-enroll-windows-devices"></a>Informar os utilizadores sobre como inscrever dispositivos Windows
Informe os seus utilizadores sobre como inscrever os dispositivos Windows e o que esperar após começarem a ser geridos.

> [!NOTE]
> Os utilizadores finais têm de aceder ao site do Portal da Empresa através do Microsoft Edge para verem as aplicações do Windows que atribuiu a versões específicas do Windows. Os outros browsers, incluindo o Google Chrome, o Mozilla Firefox e o Internet Explorer, não suportam este tipo de filtragem.

Para obter instruções de inscrição do utilizador final, veja [Inscrever o seu dispositivo Windows no Intune](../user-help/windows-enrollment-company-portal.md). Também pode dizer aos utilizadores para consultarem [Que informações pode o administrador de TI ver no meu dispositivo](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md).

>[!IMPORTANT]
> Se não tiver a Inscrição automática de MDM ativada, mas tiver dispositivos Windows 10 que foram associados ao Azure AD, serão visíveis dois registos na consola do Intune após a inscrição. Pode detê-lo certificando-se de que os utilizadores com AD Azure se juntam aos dispositivos que vão para **o**trabalho de acesso às contas  >  **ou escola** e o **Connect** utilizando a mesma conta. 

Para obter mais informações sobre as tarefas do utilizador final, consulte [Recursos sobre a experiência do utilizador final com o Microsoft Intune](../fundamentals/end-user-educate.md).

## <a name="registration-and-enrollment-cnames"></a>Inscrições e Inscrições CNAMEs
O Azure Ative Directory tem um CNAME diferente que utiliza para o registo de dispositivos iOS/iPadOS, Android e Windows. O acesso condicional intonizado requer a inscrição de dispositivos, também chamados de "local de trabalho aderido". Se planeia utilizar acesso condicional, deve também configurar o EnterpriseRegistration CNAME para cada nome da empresa que tenha.

| Tipo | Nome do anfitrião | Aponta para | TTL |
| --- | --- | --- | --- |
| NOME | Registo empresarial. company_domain.com | EnterpriseRegistration.windows.net | Uma hora|

Para obter mais informações sobre o registo do dispositivo, consulte Gerir identidades do [dispositivo utilizando o portal Azure](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal)

## <a name="windows-10-auto-enrollment-and-device-registration"></a>Registo de matrículas automáticas e dispositivos do Windows 10

Esta secção aplica-se aos clientes da nuvem do governo dos EUA.

Apesar de a criação de entradas DNS CNAME ser opcional, os registos CNAME facilitam a inscrição para os utilizadores. Se não for encontrado nenhum registo CNAME de inscrição, os utilizadores são solicitados a introduzir manualmente o nome do servidor MDM, enrollment.manage.microsoft.us.

| Tipo | Nome do anfitrião | Aponta para | TTL |
| --- | --- | --- | --- |
| CNAME | EnterpriseEnrollment.dominio_da_empresa.com | EnterpriseEnrollment-s.manage.microsoft.us | Uma hora|
|CNAME | EnterpriseRegistration.dominio_da_empresa.com | EnterpriseRegistration.windows.net | Uma hora |


## <a name="next-steps"></a>Passos seguintes

- [Considerações sobre quando gerir dispositivos Windows com o Intune no Azure](../fundamentals/intune-legacy-pc-client.md).
