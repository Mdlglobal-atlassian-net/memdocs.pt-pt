---
title: Definições insinadas para a aplicação de sala de aula iOS/iPadOS
titleSuffix: Microsoft Intune
description: Saiba as definições intune que pode utilizar para controlar as definições da aplicação Classroom nos dispositivos iOS/iPadOS.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 1381a5ce-c743-40e9-8a10-4c218085bb5f
ms.reviewer: derriw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf4fc3017ccf3efcf93986544c8a60b60acbf3c8
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076123"
---
# <a name="how-to-configure-intune-settings-for-the-iosipados-classroom-app"></a>Como configurar as definições intune para a aplicação iOS/iPadOS Classroom

> [!NOTE]
> Intune não suporta configurar a aplicação classroom. Este artigo só é aplicável aos utilizadores com perfis de educação iOS/iPadOS existentes no Intune.  

## <a name="introduction"></a>Introdução
A [Sala de Aula](https://itunes.apple.com/app/id1085319084) é uma aplicação que ajuda os professores a orientar a aprendizagem e a controlar os dispositivos dos estudantes numa sala de aula. Por exemplo, através da aplicação os professores podem:

- Abrir aplicações nos dispositivos de estudantes
- Bloquear e desbloquear o ecrã do iPad
- Ver o ecrã do iPad de um estudante
- Navegar nos iPads dos estudantes para abrir um marcador ou um capítulo de um livro
- Apresentar o ecrã do iPad de um aluno numa Apple TV

Para configurar a Sala de Aula no seu dispositivo, terá de criar e configurar um perfil de dispositivo de educação intune iOS/iPadOS.

## <a name="before-you-start"></a>Antes de começar

Antes de começar a configurar estas definições, tenha em atenção o seguinte:

- Os iPads dos professores e dos estudantes têm de estar inscritos no Intune.
- Certifique-se de que instalou a aplicação [Apple Classroom](https://itunes.apple.com/us/app/classroom/id1085319084?mt=8) no dispositivo do professor. Pode instalar a aplicação manualmente ou com a [gestão de aplicações do Intune](../apps/app-management.md).
- É necessário configurar certificados para autenticar ligações entre dispositivos de professor e aluno (ver Passo 2, Criar e atribuir um perfil de educação iOS/iPadOS em Intune).
- Os iPads do professor e dos estudantes têm de estar na mesma rede Wi-Fi e ter o Bluetooth ativado.
- A aplicação Classroom funciona em iPads supervisionados que executam iOS/iPadOS 9.3 ou posteriormente.
- Nesta versão, o Intune suporta a gestão de um cenário 1:1, em que cada estudante tem o seu próprio iPad dedicado.


## <a name="step-1---import-your-school-data-into-azure-active-directory"></a>Passo 1 – Importar os seus dados escolares para o Azure Active Directory

Utilize o School Data Sync (SDS) da Microsoft para importar os registos escolares de um SIS (Sistema de Informações de Estudantes) existente para o Azure Active Directory (Azure AD).
O SDS sincroniza as informações a partir do SIS e armazena-as no Azure AD. O Azure AD é um sistema de gestão da Microsoft que o ajuda a organizar os utilizadores e os dispositivos. Em seguida, pode utilizar estes dados para o ajudar a gerir os seus alunos e turmas. [Saiba mais sobre como implementar o SDS](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91).

### <a name="how-to-import-data-using-sds"></a>Como importar dados através do SDS

Pode importar informações para o SDS através de um dos seguintes métodos:

- [Ficheiros CSV](https://support.office.com/article/Follow-these-steps-71d5fe4a-aa51-4f35-9b53-348898a390a1) – exporte e compile manualmente os ficheiros de valores separados por vírgulas (.csv)
- [API PowerSchool](https://support.office.com/article/Follow-these-steps-851b5edc-558f-43a9-9122-b2d63458cb8f) – um fornecedor SIS que simplifica a sincronização com o Azure AD
- [OneRoster](https://support.office.com/article/Follow-these-steps-f43cbb2a-b502-497d-a8b1-783dc05a57ab) – um formato CSV que pode exportar e converter para se sincronizar com o Azure AD

### <a name="find-out-more"></a>Saiba mais

- [Saiba mais sobre a experiência completa de sincronização de dados escolares no local com o Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)
- [Saiba mais sobre o School Data Sync da Microsoft](https://sds.microsoft.com/)
- [Saiba mais sobre o licenciamento no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-whatis-azure-portal)

## <a name="step-2---create-and-assign-an-iosipados-education-profile-in-intune"></a>Passo 2 - Criar e atribuir um perfil de educação iOS/iPadOS em Intune

### <a name="configure-general-settings"></a>Configurar as definições gerais

1. Inscreva-se em [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. No painel **Intune**, selecione **Configuração do dispositivo**.
2. No painel **Configuração do dispositivo**, na secção **Gerir**, selecione **Perfis**.
5. No painel Perfis, selecione **Criar perfil**.
6. No painel de **perfil Criar,** insira um **Nome** e **Descrição** para o perfil de educação iOS/iPadOS.
7. Na lista pendente **Plataforma**, selecione **iOS**.
8. Na lista pendente **Tipo de perfil**, escolha **Educação**.
9. Escolha**configurar** **definições** > .


Na secção seguinte, vai criar certificados para estabelecer uma relação de confiança entre os iPads do professor e dos estudantes. Os certificados são utilizados para autenticar de forma silenciosa e sem problemas as ligações entre os dispositivos, sem ter de introduzir os nomes de utilizador nem palavras-passe.

>[!IMPORTANT]
>Os certificados de professor e estudante que utiliza têm de ser emitidos por autoridades de certificação (ACs) diferentes. Tem de criar duas ACs subordinadas novas ligadas à sua infraestrutura de certificados existente; uma para os professores e outra para os estudantes.

Os perfis de educação do iOS só suportam certificados PFX. Os certificados SCEP não são suportados.

Os certificados criados têm de suportar a autenticação de servidor e a autenticação de utilizador.

### <a name="configure-teacher-certificates"></a>Configurar os certificados do professor

No painel **Educação**, selecione **Certificados do professor**.

#### <a name="configure-teacher-root-certificate"></a>Configurar o certificado de raiz do professor

Em **Certificado de raiz do professor**, escolha o botão Procurar. Selecione o certificado de raiz com:
- A extensão .cer (codificada em Base64 ou DER) 
- A extensão .P7B (com ou sem cadeia completa)

#### <a name="configure-teacher-pkcs12-certificate"></a>Configurar o certificado do professor PKCS#12

Em **Certificado do professor PKCS#12**, configure os seguintes valores:

- **Formato de nome** do assunto - Insere automaticamente os nomes comuns para os certificados de professor com **o líder**. Os nomes comuns para certificados de Estudantes têm o prefixo **membro**.
- **Autoridade de certificação** – uma Autoridade de Certificação (AC) Empresarial que é executada numa edição Enterprise do Windows Server 2008 R2 ou posterior. Não é suportada uma AC Autónoma. 
- **Nome da autoridade de certificação** – introduza o nome da autoridade de certificação.
- **Nome** do modelo do certificado - Introduza o nome de um modelo de certificado que tenha sido adicionado a um CA emissor. 
- **Limiar de renovação (%)** – Especifique a percentagem da duração do certificado antes de o dispositivo pedir a renovação do certificado.
- **Período de validade do certificado** – especifique o tempo restante até o certificado expirar.
Pode especificar um valor inferior ao período de validade do modelo de certificado especificado, mas não superior. Por exemplo, se o período de validade do certificado no modelo de certificado for dois anos, pode especificar um valor de um ano, mas não um valor de cinco anos. O valor também tem de ser inferior ao período de validade restante do certificado da AC emissora.

Quando concluir a configuração dos certificados, escolha **OK**.

### <a name="configure-student-certificates"></a>Configurar os certificados de estudante

1. No painel **Educação**, selecione **Certificados de estudante**.
2. No painel **Certificados de estudante**, na lista de tipos de **Certificados de dispositivos de estudante**, selecione **1:1**.

#### <a name="configure-student-root-certificate"></a>Configurar o certificado de raiz do estudante

Em **Certificado de raiz do estudante**, escolha o botão Procurar. Selecione o certificado de raiz com:
- A extensão .cer (codificada em Base64 ou DER) 
- A extensão .P7B (com ou sem cadeia completa)

#### <a name="configure-student-pkcs12-certificate"></a>Configurar o certificado PKCS#12 do estudante

Em **Certificado PKCS#12 do estudante**, configure os seguintes valores:

- **Formato de nome** do assunto - Insere automaticamente os nomes comuns para os certificados de professor com **o líder**. Os nomes comuns para certificados de Estudantes têm o prefixo **membro**.
- **Autoridade de certificação** – uma Autoridade de Certificação (AC) Empresarial que é executada numa edição Enterprise do Windows Server 2008 R2 ou posterior. Não é suportada uma AC Autónoma. 
- **Nome da autoridade de certificação** – introduza o nome da autoridade de certificação.
- **Nome** do modelo do certificado - Introduza o nome de um modelo de certificado que tenha sido adicionado a um CA emissor. 
- **Limiar de renovação (%)** – Especifique a percentagem da duração do certificado antes de o dispositivo pedir a renovação do certificado.
- **Período de validade do certificado** – especifique o tempo restante até o certificado expirar.
Pode especificar um valor inferior ao período de validade do modelo de certificado especificado, mas não superior. Por exemplo, se o período de validade do certificado no modelo de certificado for dois anos, pode especificar um valor de um ano, mas não um valor de cinco anos. O valor também tem de ser inferior ao período de validade restante do certificado da AC emissora.

Quando concluir a configuração dos certificados, escolha **OK**.

## <a name="finish-up"></a>Concluir

1. No painel **Educação**, selecione OK.
2. No painel **Criar perfil**, selecione **Criar**.

O perfil é criado e apresentado no painel da lista de perfis.

Atribua o perfil aos dispositivos dos estudantes nos grupos de sala de aula que foram criados quando sincronizou os dados escolares com o Azure AD (veja [Como atribuir perfis de dispositivo](../configuration/device-profile-assign.md).

## <a name="next-steps"></a>Passos seguintes

Agora, quando os professores utilizarem a aplicação Classroom, terão controlo total sobre os dispositivos dos estudantes.

Para obter mais informações sobre a aplicação Sala de Aula, veja [Ajuda de Sala de Aula](https://help.apple.com/classroom/ipad/2.0/) no site da Apple.

Se quiser configurar dispositivos iPad partilhados para os estudantes, veja [Como configurar definições de educação do Intune para dispositivos iPad partilhados](education-settings-configure-ios-shared.md).
