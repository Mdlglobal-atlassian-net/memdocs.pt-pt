---
title: Criar perfis de dispositivo no Microsoft Intune – Azure | Microsoft Docs
description: Adicione ou configure um perfil de configuração de dispositivos no Microsoft Intune. Selecione o tipo de plataforma, configure as definições, adicione uma etiqueta de âmbito.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2031ba23b49bda4890d2638272e3b808b4bf5a9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327442"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Criar um perfil de dispositivo no Microsoft Intune

Os perfis de dispositivo permitem-lhe adicionar e configurar definições e, em seguida, enviar essas definições para dispositivos na sua organização. Veja [Aplicar definições e funcionalidades aos dispositivos com perfis de dispositivo](device-profiles.md) para obter mais detalhes, incluindo o que pode fazer.

Este artigo:

- Apresenta os passos para criar um perfil.
- Mostra-lhe como adicionar uma etiqueta de âmbito para “filtrar” o perfil.
- Descreve regras de aplicabilidade em dispositivos Windows 10 e mostra-lhe como criar uma regra.
- Apresenta os tempos de ciclos de atualização de entrada quando os dispositivos recebem perfis e atualizações de perfis.

## <a name="create-the-profile"></a>Criar o perfil

Os perfis são criados no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Neste centro de administração, selecione **Dispositivos**. Existem as seguintes opções:

- **Visão geral**: Lista o estado dos seus perfis e fornece detalhes adicionais sobre os perfis que atribuiu aos utilizadores e dispositivos.
- **Monitor**: Verifique o estado dos seus perfis para obter sucesso ou falha e consulte também os registos nos seus perfis.
- **Por plataforma**: Crie e veja políticas e perfis pela sua plataforma. Esta vista também pode mostrar funcionalidades específicas da plataforma. Por exemplo, selecione **Windows**. Verá funcionalidades específicas do Windows, tais como Os Anéis de **Atualização do Windows 10** e **os scripts PowerShell**.
- **Política**: Criar perfis de dispositivos, carregar [scripts PowerShell personalizados](../apps/intune-management-extension.md) para executar em dispositivos e adicionar planos de dados aos dispositivos que utilizem [eSIM](esim-device-configuration.md).

Quando criar um perfil **(Perfis** > de configuração**Criar perfil),** escolha a sua plataforma:

- **Administrador de dispositivos Android**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 e posterior**
- **Windows 8.1 e posterior**
- **Windows Phone 8.1**

Em seguida, escolha o tipo de perfil. Consoante a plataforma que escolheu, as definições que pode configurar variam. Os seguintes artigos descrevem as definições para os diferentes tipos de perfil:

- [Modelos administrativos (Janelas)](administrative-templates-windows.md)
- [Personalizado](custom-settings-configure.md)
- [Otimização de entrega (Windows)](delivery-optimization-windows.md)
- [Credencial derivada (Android Enterprise, iOS, iPadOS)](../protect/derived-credentials.md)
- [Funcionalidades do dispositivo (macOS, iOS, iPadOS)](device-features-configure.md)
- [Firmware de dispositivos (Windows)](device-firmware-configuration-interface-windows.md)
- [Restrições de dispositivos](device-restrictions-configure.md)
- [A desfiliação do domínio (Windows)](domain-join-configure.md)
- [Upgrade de edição e interruptor de modo (Windows)](edition-upgrade-configure-windows-10.md)
- [Educação (iOS, iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [E-mail](email-settings-configure.md)
- [Proteção endpoint (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Extensões (macOS)](kernel-extensions-overview-macos.md)
- [Proteção de identidade (Windows)](../protect/identity-protection-configure.md)
- [Kiosk](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [Perfil de Extensões de Mobilidade (MX) (administrador de dispositivoandroid)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [Certificado PKCS](../protect/certficates-pfx-configure.md)
- [Certificado PKCS importado](../protect/certificates-imported-pfx-configure.md)
- [Ficheiro preferencial (macOS)](preference-file-settings-macos.md)
- [Certificado SCEP](../protect/certificates-scep-configure.md)
- [Avaliação segura (Educação) (Windows)](education-settings-configure.md)
- [Dispositivo multiutilizador partilhado (Windows)](shared-user-device-settings.md)
- [Despesas de telecomunicações (administrador de dispositivos Android, iOS, iPadOS)](telecom-expenses-monitor.md)
- [Certificado fidedigno](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

Por exemplo, se selecionar **iOS/iPadOS** para a plataforma, as opções do tipo de perfil são semelhantes ao seguinte perfil:

> [!div class="mx-imgBorder"]
> ![Criar perfil iOS/iPadOS em Intune](./media/device-profile-create/create-device-profile.png)

## <a name="scope-tags"></a>Scope tags (Etiquetas de âmbito)

Depois de adicionar as definições, também pode adicionar uma etiqueta de âmbito ao perfil. As etiquetas de âmbito filtram perfis `US-NC IT Team` `JohnGlenn_ITDepartment`para grupos de TI específicos, tais como ou . E são usados em TI distribuídos.

Para obter mais informações sobre etiquetas de âmbito e o que pode fazer, veja [Utilizar RBAC e etiquetas de âmbito para TI distribuídas](../fundamentals/scope-tags.md).

## <a name="applicability-rules"></a>Regras de aplicabilidade

Aplica-se a:

- Windows 10 e posterior

As regras de aplicabilidade permitem que os administradores direcionem dispositivos num grupo que satisfaça critérios específicos. Por exemplo, cria um perfil de restrições de dispositivos que se aplica ao grupo de **dispositivos All Windows 10.** E, só quer o perfil atribuído aos dispositivos que executam o Windows 10 Enterprise.

Para fazer esta tarefa, crie uma regra de **aplicabilidade.** Estas regras são ótimas para os seguintes cenários:

- Utiliza o Windows 10 Education (EDU). No Bellows College, você quer direcionar todos os dispositivos EDU do Windows 10 entre RS3 e RS4.
- Você quer direcionar todos os utilizadores em Recursos Humanos em Contoso, mas apenas quer dispositivos Profissionais ou Empresariais do Windows 10.

Para abordar estes cenários, você:

- Crie um grupo de dispositivos que inclua todos os dispositivos no Bellows College. No perfil, adicione uma regra de aplicabilidade para que se `16299` aplique se `17134`a versão mínima do SO for e a versão máxima for . Atribuir este perfil ao grupo de dispositivos da Escola Bellows.

  Quando é atribuído, o perfil aplica-se a dispositivos entre as versões mínima seleções mínimas e máximas que introduz. Para dispositivos que não estejam entre as versões mínima seleção e o máximo que introduz, o seu estado mostra **que não**é aplicável .

- Crie um grupo de utilizadores que inclua todos os utilizadores em Recursos Humanos (RH) na Contoso. No perfil, adicione uma regra de aplicabilidade para que se aplique a dispositivos que executem o Windows 10 Professional ou Enterprise. Atribuir este perfil ao grupo de utilizadores de RH.

  Quando é atribuído, o perfil aplica-se a dispositivos que executam o Windows 10 Professional ou Enterprise. Para dispositivos que não estejam a executar estas edições, o seu estado mostra **como Não aplicável**.

- Se houver dois perfis com as mesmas definições, então o perfil sem uma regra de aplicabilidade é aplicado. 

  Por exemplo, o ProfileA tem como alvo o grupo de dispositivos Windows 10, permite o BitLocker e não tem uma regra de aplicabilidade. O ProfileB tem como alvo o mesmo grupo de dispositivos Windows 10, permite o BitLocker, e tem uma regra de aplicabilidade para aplicar apenas o perfil ao Windows 10 Enterprise.

  Quando ambos os perfis são atribuídos, o ProfileA é aplicado porque não tem uma regra de aplicabilidade. 

Ao atribuir o perfil aos grupos, as regras de aplicabilidade funcionam como um filtro e apenas visam os dispositivos que cumprem os seus critérios.

### <a name="add-a-rule"></a>Adicionar uma regra

1. Selecione Regras de **Aplicabilidade**. Pode escolher a **regra,** **propriedade**e **edição osso:**

    > [!div class="mx-imgBorder"]
    > ![Adicione uma regra de aplicabilidade a um perfil de configuração do dispositivo no Microsoft Intune](./media/device-profile-create/applicability-rules.png)

2. Regra **Rule**, escolha se pretende incluir ou excluir utilizadores ou grupos. As opções são:

    - **Atribuir perfil se**: Inclui utilizadores ou grupos que satisfaçam os critérios em que entra.
    - **Não designe o perfil se**: Excluir utilizadores ou grupos que satisfaçam os critérios em que insere.

3. Em **Propriedade,** escolha o seu filtro. As opções são: 

    - **Edição OS**: Na lista, consulte as edições do Windows 10 que pretende incluir (ou excluir) na sua regra.
    - **Versão OS**: Introduza os números da versão **min** e **max** Windows 10 que pretende incluir (ou excluir) na sua regra. Ambos os valores são necessários.

      Por exemplo, pode `10.0.16299.0` introduzir (RS3 ou 1709) para versão mínima e `10.0.17134.0` (RS4 ou 1803) para versão máxima. Ou, pode ser mais granular e `10.0.16299.001` `10.0.17134.319` entrar para versão mínima e para versão máxima.

4. Selecione **Adicionar** para guardar as suas alterações.

## <a name="refresh-cycle-times"></a>Tempos de ciclos de atualização

Intune usa diferentes ciclos de atualização para verificar se há atualizações nos perfis de configuração. Se o dispositivo se matriculou recentemente, o check-in funciona com mais frequência. Os ciclos de atualização de políticas e perfis listam os [tempos estimados](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) de atualização.

Em qualquer altura, os utilizadores podem abrir a aplicação do Portal da Empresa e sincronizar o dispositivo para verificarem imediatamente se existem as atualizações de perfis.

## <a name="recommendations"></a>Recomendações

Ao criar perfis, considere as seguintes recomendações:

- Diga o nome das suas políticas para saber o que são e o que fazem. Todas as políticas de [conformidade](../protect/create-compliance-policy.md) e perfis de [configuração](../configuration/device-profile-create.md) têm uma propriedade de **Descrição** opcional. Em **Descrição,** seja específico e inclua informações para que outros saibam o que a política faz.

  Alguns exemplos de perfil de configuração incluem:

  **Nome do perfil**: Modelo de administrador - perfil de configuração OneDrive para todos os utilizadores do Windows 10  
  **Descrição do perfil**: Perfil de modelo de administrador OneDrive que inclui as definições mínimas e base para todos os utilizadores do Windows 10. Criado user@contoso.com para impedir que os utilizadores partilhem dados organizacionais para contas pessoais do OneDrive.

  **Nome do perfil**: Perfil VPN para todos os utilizadores iOS/iPadOS  
  **Descrição do perfil**: Perfil VPN que inclui as definições mínimas e base para todos os utilizadores iOS/iPadOS para ligar à VPN Contoso. Criado user@contoso.com si os utilizadores autenticam automaticamente a VPN, em vez de pedir em que os utilizadores se instem com o seu nome de utilizador e palavra-passe.

- Crie o seu perfil através da sua tarefa, como configurar as definições do Microsoft Edge, ativar as definições antivírus do Microsoft Defender, bloquear dispositivos de jailbroken iOS/iPadOS, e assim por diante.

- Crie perfis que se apliquem a grupos específicos, tais como Marketing, Vendas, Administradores de TI ou por localização ou sistema escolar.

- Separe as políticas de utilizador das políticas do dispositivo.

  Por exemplo, os [modelos administrativos em Intune](administrative-templates-windows.md) têm centenas de configurações ADMX. Estes modelos mostram se uma definição se aplica aos utilizadores ou dispositivos. Ao criar modelos de administração, atribua as definições dos seus utilizadores a um grupo de utilizadores e atribua as definições do seu dispositivo a um grupo de dispositivos.

  A imagem que se segue mostra um exemplo de uma definição que pode aplicar-se aos utilizadores e/ou aplicar-se aos dispositivos:

  > [!div class="mx-imgBorder"]
  > ![Modelo de administração intonizado que se aplica ao utilizador e dispositivos](./media/device-profile-create/setting-applies-to-user-and-device.png)

- Sempre que criar uma política restritiva, comunique esta alteração aos seus utilizadores. Por exemplo, se estiver a alterar o requisito de código de acesso de 4 caracteres para 6 caracteres, informe os seus utilizadores antes de atribuir a apólice.

## <a name="next-steps"></a>Passos seguintes

[Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
