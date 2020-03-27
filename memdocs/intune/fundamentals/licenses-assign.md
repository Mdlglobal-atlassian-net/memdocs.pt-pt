---
title: Atribuir licenças do Microsoft Intune
description: Atribuir licenças aos utilizadores para que estes possam inscrever-se no Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/12/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: bb4314ea-88b5-44d3-92ce-4c6aff0587a4
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad0964eafccc5bf007b1569762e4cea4d0ee691a
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326781"
---
# <a name="assign-licenses-to-users-so-they-can-enroll-devices-in-intune"></a>Atribuir licenças aos utilizadores para que estes possam inscrever dispositivos no Intune

Quer adicione utilizadores manualmente ou sincronize a partir do Active Directory no local, tem primeiro de atribuir a cada utilizador uma licença do Intune antes de os utilizadores poderem inscrever os respetivos dispositivos no Intune. Para obter uma lista das licenças, veja [Licenses that include Intune (Licenças que incluem o Intune)](licenses.md).

> [!NOTE]
> Os utilizadores designados pela política de proteção de aplicações Intune e não matricularem os seus dispositivos no Microsoft Intune também exigirão uma licença Intune para receber a política.

## <a name="assign-an-intune-license-microsoft-endpoint-manager-admin-center"></a>Atribuir uma licença Intune Microsoft Endpoint Manager centro de administração

Pode utilizar o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) para adicionar manualmente utilizadores baseados na nuvem e atribuir licenças tanto a contas de utilizadores baseados na nuvem como a contas sincronizadas desde o seu Diretório Ativo no local até à AD Azure.

1. No centro de administração do [Microsoft Endpoint Manager,](https://go.microsoft.com/fwlink/?linkid=2109431)selecione **Utilizadores** > **Todos os Utilizadores** > escolha um utilizador > **Licenças** > **Atribuições**.

2. Escolha a caixa para **Intune** > **Save**.

   ![Screenshot da secção de licenças de produto do centro de administração Microsoft 365.](./media/licenses-assign/mem-assign-license.png)

3. A conta de utilizador tem agora as permissões que são precisas para utilizar o serviço e inscrever os dispositivos para gestão.

> [!NOTE]
> Os utilizadores só aparecerão no portal Classic Intune depois de terem matriculado um dispositivo utilizando o cliente intune PC. Além disso, pode selecionar um grupo de utilizadores para editar ao mesmo tempo, ao selecionar para adicionar ou substituir uma licença para todos os utilizadores selecionados.

## <a name="assign-an-intune-license-by-using-azure-active-directory"></a>Atribuir uma licença do Intune com o Azure Active Directory

Também pode atribuir licenças do Intune aos utilizadores com o Azure Active Directory. Para obter mais informações, veja o artigo [Atribuir licenças aos utilizadores no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-assignment-azure-portal). 

## <a name="use-school-data-sync-to-assign-licenses-to-users-in-intune-for-education"></a>Utilizar o School Data Sync para atribuir licenças aos utilizadores do Intune for Education

Se for uma organização de ensino, poderá utilizar o School Data Sync (SDS) para atribuir licenças do Intune for Education aos utilizadores sincronizados. Basta selecionar a caixa de verificação do Intune for Education quando estiver a configurar o perfil SDS.  

![Captura de ecrã da definição do perfil SDS](./media/licenses-assign/i4e-sds-profile-setup-setting.png)

Quando atribuir uma licença do Intune for Education, confirme se a licença do Intune A Direct também foi atribuída.

![Captura de ecrã da configuração da licença do produto](./media/licenses-assign/i4e-set-licenses.png)

Veja esta [descrição geral do School Data Sync](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91) para saber mais sobre o SDS.

## <a name="how-user-and-device-licenses-affect-access-to-services"></a>Como as licenças de utilizadores e dispositivos afetam o acesso aos serviços

* Cada **utilizador** a quem atribuir uma licença de software de utilizador pode aceder e utilizar os serviços online e software relacionado (incluindo software System Center) para gerir aplicações e até 15 dispositivos MDM. O agente intune PC permite 5 máquinas físicas e 1 virtuais por licença de utilizador.
* Pode adquirir licenças para qualquer dispositivo separadamente das licenças de utilizador. As licenças de dispositivo não têm de ser atribuídas aos dispositivos. Cada dispositivo que aceder a e utilizar os serviços online e outro software relacionado (incluindo software do System Center) tem de ter uma licença de dispositivo.
* Caso um dispositivo seja utilizado por mais de um utilizador, cada um requer uma licença de software de dispositivo ou todos os utilizadores requerem uma licença de software de utilizador.

## <a name="understanding-the-type-of-licenses-you-have-purchased"></a>Compreender o tipo de licenças que adquiriu

A forma como comprou o Intune determina as informações da sua subscrição:

- Se adquiriu o Intune através de um Contrato Enterprise, pode encontrar as informações da sua subscrição no portal de Licenciamento em Volume em **Subscrições**.
- Se adquiriu o Intune através de um Fornecedor de Soluções Cloud, contacte o seu revendedor.
- Se adquiriu o Intune com um número de CC ou uma Fatura, a suas licenças serão baseadas no utilizador.

## <a name="use-powershell-to-selectively-manage-ems-user-licenses"></a>Utilizar o PowerShell para gerir seletivamente licenças de utilizador do EMS
As organizações que utilizam Microsoft Enterprise Mobility + Security (anteriormente denominado Enterprise Mobility Suite) podem ter utilizadores que apenas necessitam do Azure Active Directory Premium ou dos serviços do Intune no pacote EMS. Pode atribuir um ou um subconjunto de serviços através dos [cmdlets do PowerShell do Azure Active Directory](https://msdn.microsoft.com/library/jj151815.aspx).

Para atribuir seletivamente licenças de utilizador para serviços do EMS, abra o PowerShell como administrador num computador com o [Módulo Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/jj151815.aspx#bkmk_installmodule) instalado. Pode instalar o PowerShell num computador local ou num servidor do ADFS.

Tem de criar uma nova definição de SKU de licença que se aplique apenas aos planos de serviço pretendidos. Para isso, desative os planos que não quer aplicar. Por exemplo, pode criar uma definição de SKU de licença que não atribua uma licença do Intune. Para ver uma lista dos serviços disponíveis, escreva:

    (Get-MsolAccountSku | Where {$_.SkuPartNumber -eq "EMS"}).ServiceStatus

Pode executar o comando seguinte para excluir o plano de serviço do Intune. Pode utilizar o mesmo método para expandir para um grupo de segurança completo ou pode utilizar filtros mais granulares.

**Exemplo 1**<br>
Criar um novo utilizador na linha de comandos e atribuir uma licença de EMS sem ativar a parte do Intune da licença:

    Connect-MsolService

    New-MsolUser -DisplayName "Test User" -FirstName FName -LastName LName -UserPrincipalName user@<TenantName>.onmicrosoft.com –Department DName -UsageLocation US

    $CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
    Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -AddLicenses <TenantName>:EMS -LicenseOptions $CustomEMS

Verificar com:

    (Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus

**Exemplo 2**<br>
Desativar a parte do Intune da licença de EMS para um utilizador a quem já foi atribuída uma licença:

    Connect-MsolService

    $CustomEMS = New-MsolLicenseOptions -AccountSkuId "<TenantName>:EMS" -DisabledPlans INTUNE_A
    Set-MsolUserLicense -UserPrincipalName user@<TenantName>.onmicrosoft.com -LicenseOptions $CustomEMS

Verificar com:

    (Get-MsolUser -UserPrincipalName "user@<TenantName>.onmicrosoft.com").Licenses.ServiceStatus

![PoSH-AddLic-Verify](./media/licenses-assign/posh-addlic-verify.png)
