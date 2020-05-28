---
title: Cargas de trabalho de cogestão
titleSuffix: Configuration Manager
description: Saiba mais sobre as cargas de trabalho que pode mudar de Configuração Manager para Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 928ef8a8ebc90807912f22901743725df9aa67e7
ms.sourcegitcommit: 79fb3b0f0486de1644904be348b7e08048e93b18
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82842228"
---
# <a name="co-management-workloads"></a>Cargas de trabalho de cogestão

Não tens de mudar as cargas de trabalho, ou podes fazê-las individualmente quando estiveres pronta. O Gestor de Configuração continua a gerir todas as outras cargas de trabalho, incluindo as cargas de trabalho que não muda para Intune, e todas as outras funcionalidades do Gestor de Configuração que a cogestão não suporta.

Se mudar uma carga de trabalho para Intune, mas depois mudar de ideia, pode trocá-la de volta para 'Gestor de Configuração'.

A cogestão suporta as seguintes cargas de trabalho:

- [Políticas de conformidade](#compliance-policies)  

- [Políticas de Atualização do Windows](#windows-update-policies)  

- [Políticas de acesso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuração do dispositivo](#device-configuration)  

- [Aplicativos click-to-run do Office](#office-click-to-run-apps)  

- [Aplicações do cliente](#client-apps)  

## <a name="compliance-policies"></a>Políticas de conformidade

As políticas de conformidade definem as regras e configurações que um dispositivo deve cumprir para serem consideradas conformes pelas políticas de acesso condicional. Utilize também políticas de conformidade para monitorizar e remediar problemas de conformidade com dispositivos independentemente do acesso condicional. Começando na versão 1910 do Gestor de Configuração, pode adicionar avaliação das linhas de base de configuração personalizadas como regra de avaliação da política de conformidade. Para mais informações, consulte Incluir as linhas de [base de configuração personalizadas como parte da avaliação da política de conformidade.](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)

Para obter mais informações sobre a funcionalidade Intune, consulte [as políticas](https://docs.microsoft.com/intune/device-compliance-get-started)de conformidade do Dispositivo .  

## <a name="windows-update-policies"></a>Políticas de Atualização do Windows

O Windows Update for Business permite configurar políticas de diferimento para atualizações de funcionalidades do Windows 10 ou atualizações de qualidade para dispositivos Windows 10 geridas diretamente pelo Windows Update for Business.

Para obter mais informações sobre a funcionalidade Intune, consulte [Configure Windows Update para políticas de diferimento de negócios](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Políticas de acesso a recursos

As políticas de acesso a recursos configuram as definições de VPN, Wi-Fi, e-mail e certificado nos dispositivos.

Para obter mais informações sobre a funcionalidade Intune, consulte Implementar perfis de [acesso a recursos](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> A carga de trabalho de acesso ao recurso também faz parte da configuração do dispositivo. Estas políticas são geridas pela Intune quando muda a carga de trabalho de Configuração do [Dispositivo.](#device-configuration)

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

A carga de trabalho endpoint Protection inclui o conjunto Windows Defender de funcionalidades de proteção antimalware:

- Windows Defender Antimalware
- Windows Defender Application Guard  
- Firewall do Windows Defender  
- Windows Defender SmartScreen  
- Encriptação do Windows
- Windows Defender Exploit Guard  
- Controlo de Aplicações do Windows Defender  
- Centro de Segurança do Windows Defender  
- Proteção avançada de ameaças do Windows Defender (agora conhecida como Proteção de Ameaças do Microsoft Defender)

Para obter mais informações sobre a funcionalidade Intune, consulte [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Quando muda esta carga de trabalho, as políticas do Gestor de Configuração permanecem no dispositivo até que as políticas intune as sobressaem. Este comportamento garante que o dispositivo ainda tem políticas de proteção durante a transição.
>
> A carga de trabalho de proteção de pontofinal também faz parte da configuração do dispositivo. O mesmo comportamento aplica-se quando muda a carga de trabalho de configuração do [dispositivo.](#device-configuration)<!-- SCCMDocs.nl-nl issue #4 --> Quando muda a carga de trabalho de configuração do dispositivo, também inclui políticas para a funcionalidade de Proteção de Informação do Windows, que não está incluída na carga de trabalho de proteção de pontofinal.<!-- 4184095 -->
>
> As definições antivírus do Microsoft Defender que fazem parte do tipo de perfil de restrições do Dispositivo para a configuração do Dispositivo Intune não estão incluídas no âmbito do slider de proteção endpoint. Para gerir o Antivírus Do Microsoft Defender para dispositivos cogeridos com o slider de proteção de pontofinal ativado, utilize as novas políticas antivírus no **microsoft Endpoint manager administrador antivírus**  >  **de segurança**  >  **Antivirus**Endpoint . O novo tipo de política tem novas e melhoradas opções disponíveis, e suporta todas as mesmas definições disponíveis no perfil de restrições do Dispositivo. <!--6609171-->
>
> A funcionalidade de encriptação do Windows inclui a gestão bitLocker. Para obter mais informações sobre o comportamento desta funcionalidade com cogestão, consulte a [gestão do Deploy BitLocker](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Configuração do dispositivo

<!--1357903-->

A carga de trabalho de configuração do dispositivo inclui configurações que gere para dispositivos na sua organização. Mudar esta carga de trabalho também move as cargas de trabalho de acesso a **recursos** e proteção de **pontos finais.**

Ainda pode implementar definições do 'Configuração Manager' para dispositivos cogeridos, mesmo que o Intune seja a autoridade de configuração do dispositivo. Esta exceção pode ser usada para configurar configurações que a sua organização necessita, mas ainda não estão disponíveis em Intune. Especifique esta exceção numa linha de base de [configuração do Gestor](../compliance/deploy-use/create-configuration-baselines.md)de Configuração . Ative a opção de **aplicar sempre esta linha de base mesmo para clientes cogeridos** ao criar a linha de base. Pode mudá-lo mais tarde no separador **Geral** das propriedades de uma linha de base existente.  

Para obter mais informações sobre a funcionalidade Intune, consulte Criar um perfil de [dispositivo no Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  

> [!NOTE]
> Quando muda a carga de trabalho de configuração do dispositivo, também inclui políticas para a funcionalidade de Proteção de Informação do Windows, que não está incluída na carga de trabalho de proteção de pontofinal.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Aplicativos click-to-run do Office

<!--1357841-->

Esta carga de trabalho gere as aplicações do Office 365 em dispositivos cogeridos.

- Depois de mover a carga de trabalho, a aplicação aparece no Portal da **Empresa** no dispositivo  

- As atualizações do escritório podem demorar cerca de 24 horas a aparecer no cliente a menos que os dispositivos sejam reiniciados  

- Há uma nova condição global, são as aplicações do **Office 365 geridas pela Intune no dispositivo.** Esta condição é adicionada por defeito como requisito para os novos pedidos do Office 365. Ao transitar esta carga de trabalho, os clientes cogeridos não cumprem o requisito da aplicação. Depois não instalam o Office 365 implantado através do Diretor de Configuração.  

Para obter mais informações sobre a funcionalidade Intune, consulte [as aplicações do Assign Office 365 para dispositivos Windows 10 com](https://docs.microsoft.com/intune/apps-add-office365)o Microsoft Intune .

## <a name="client-apps"></a>Aplicações do cliente

<!--1357892-->

Use o Intune para gerir aplicações de clientes e scripts PowerShell em dispositivos windows 10 cogeridos. Após a transição desta carga de trabalho, todas as aplicações disponíveis implantadas a partir de Intune estão disponíveis no Portal da Empresa. As aplicações que implementa no 'Gestor de Configuração' estão disponíveis no Software Center.

Para obter mais informações sobre a funcionalidade Intune, consulte o que é a gestão de [aplicações da Microsoft Intune?](https://docs.microsoft.com/intune/app-management)

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1806 como [uma funcionalidade de pré-lançamento.](../core/servers/manage/pre-release-features.md) Começando com a versão 2002, já não é uma funcionalidade de pré-lançamento.  
>
> Esta funcionalidade pode aparecer na lista de funcionalidades como **aplicações Móveis para dispositivos cogeridos.**<!-- 5849669 -->

A partir da versão 1910, quando activao Microsoft Connected Cache nos pontos de distribuição do Gestor de Configuração, podem agora servir aplicações Microsoft Intune Win32 a clientes cogeridos. Para mais informações, consulte o [Microsoft Connected Cache no 'Configuração Manager'.](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune)

## <a name="diagram-for-app-workloads"></a>Diagrama para cargas de trabalho de aplicativos

![Diagrama de trabalhos de aplicações de cogestão](media/co-management-apps.svg)

[Ver o diagrama em tamanho real](media/co-management-apps.svg)

## <a name="known-issues"></a>Problemas conhecidos

Quando a carga de trabalho endpoint Protection é transferida para Intune, o cliente ainda pode honrar as políticas definidas pelo Gestor de Configuração e pelo Microsoft Defender. <!--5024559-->

Para resolver este problema, aplique o CleanUpPolicy.xml utilizando configSecurityPolicy.exe após as políticas intune terem sido recebidas pelo cliente usando os passos abaixo:

1. Copie e guarde o texto abaixo como `CleanUpPolicy.xml` .

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. Abra um pedido de comando elevado para `ConfigSecurityPolicy.exe` . Tipicamente, este executável está numa das seguintes diretórios:
   - C:\Programa Ficheiros\Windows Defender
   - C:\Program Files\Microsoft Security Client
1. A partir do pedido de comando, passe no ficheiro xml para limpar a apólice. Por exemplo, `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Próximos passos

[Como mudar as cargas de trabalho](how-to-switch-workloads.md)  
