---
title: Utilizar Extensões de Mobilidade Zebra em dispositivos Android no Microsoft Intune – Azure | Microsoft Docs
description: Utilize o Microsoft Intune para gerir e utilizar dispositivos Zebra a executar o Android com Extensões de Mobilidade (MX) Zebra. Fique a conhecer todos os passos, incluindo como instalar a aplicação do Portal da Empresa, fazer sideload da aplicação, atribuir a função de administrador do dispositivo, criar um perfil do StageNow e muito mais.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 077318d4b55c7e1f2a83864aba51e2282630b9fb
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990143"
---
# <a name="use-and-manage-zebra-devices-with-zebra-mobility-extensions-in-microsoft-intune"></a>Utilizar e gerir dispositivos Zebra com as Extensões de Mobilidade Zebra no Microsoft Intune

O Intune inclui um conjunto avançado de funcionalidades, incluindo a gestão de aplicações e a configuração de definições do dispositivo. Estas funcionalidades e configurações incorporadas gerem dispositivos Android fabricados pela Zebra Technologies, também conhecidos como "dispositivos Zebra".

Em dispositivos Android, utilize os perfis de Extensões de Mobilidade da Zebra **(MX)** para personalizar ou adicionar configurações mais específicas da Zebra.

Este artigo mostra-lhe como utilizar as Extensões de Mobilidade (MX) Zebra em dispositivos Zebra no Microsoft Intune.

Esta funcionalidade aplica-se a:

- Android device administrator (Administrador de dispositivos Android)

Para dispositivos Android Enterprise, utilize [o OEMConfig](android-oem-configuration-overview.md).

A sua empresa pode utilizar os dispositivos Zebra na venda a retalho, na fábrica e em muitas outras situações. Por exemplo, é um revendedor e o seu ambiente inclui milhares de dispositivos móveis Zebra utilizados pelos seus assistentes comerciais. O Intune pode ajudar a gerir estes dispositivos como parte da sua solução de gestão de dispositivos móveis (MDM).

Com o Intune, pode inscrever dispositivos Zebra para implementar as aplicações de linha de negócio nos dispositivos. Os perfis de “configuração do dispositivo” permitem criar perfis MX para gerir as definições específicas da Zebra.

> [!NOTE]
> Por predefinição, as APIs Zebra MX não estão bloqueadas nos dispositivos. Antes de um dispositivo se inscrever em Intune, é possível que o dispositivo possa ser comprometido de forma maliciosa. Quando o dispositivo estiver em estado limpo, sugerimos que bloqueie as APIs MX utilizando o Access Manager (AccessMgr). Por exemplo, pode escolher que apenas a aplicação do Portal da Empresa e as aplicações em que confia podem ligar para AFM.
>
> Para mais informações, consulte o bloqueio do [seu dispositivo](https://developer.zebra.com/community/home/blog/2017/04/11/locking-down-your-device) no site da Zebra.

## <a name="before-you-begin"></a>Antes de começar

- Verifique se tem a versão mais recente da aplicação de ambiente de trabalho StageNow da Zebra Technologies.
- Não deixe de ver [Zebra's full MX feature matrix](http://techdocs.zebra.com/mx/compatibility) (Matriz completa de funcionalidades MX da Zebra) (abre o site da Zebra) para confirmar que os perfis que cria são compatíveis com a versão da MX, a versão do SO e o modelo do dispositivo.
- Determinados dispositivos, como os dispositivos TC20/25, não suportam todas as funcionalidades MX disponíveis no StageNow. Não deixe de ver [Zebra's feature matrix](http://techdocs.zebra.com/mx/tc2x/) (Matriz de funcionalidades da Zebra) (abre o site da Zebra) para obter informações de suporte atualizadas.

## <a name="step-1-install-the-latest-company-portal-app"></a>Passo 1: Instale a mais recente app portal da empresa

No dispositivo, abra a loja Google Play. Descarregue e instale a aplicação Intune Company Portal da Microsoft. Quando instalada a partir do Google Play, a aplicação do Portal da Empresa obtém as atualizações e as correções automaticamente.

Se o Google Play não estiver disponível, transfira o [Portal da Empresa do Microsoft Intune para Android](https://www.microsoft.com/download/details.aspx?id=49140) (abre outro site da Microsoft) e [faça o seu sideload](#sideload-the-company-portal-app) (neste artigo). Quando instalada desta maneira, a aplicação não recebe atualizações nem correções automaticamente. Certifique-se de atualizar e remendar a aplicação manualmente.

### <a name="sideload-the-company-portal-app"></a>Fazer sideload da aplicação Portal da Empresa

Recorre ao “sideloading” quando não utiliza o Google Play para instalar uma aplicação. Para fazer sideload da aplicação do Portal da Empresa, utilize o StageNow. 

Os passos seguintes permitem obter uma descrição geral. Para obter detalhes específicos, veja a documentação da Zebra. O artigo [Enroll in an MDM using StageNow](http://techdocs.zebra.com/stagenow/3-1/Profiles/enrollmdm/) (Inscrever-se na MDM com o StageNow) (abre o site da Zebra) pode ser uma boa opção.

1. No StageNow, crie um perfil para se **Inscrever na MDM**.
2. Em **Implementação**, opte por transferir o ficheiro do agente MDM.
3. Defina os passos **Suporte da Aplicação** e **Transferir Configuração** como **Não**.
4. Em **Transferir MDM**, selecione **Transferir/Copiar Ficheiro**. Adicione a origem e o destino do pacote Android do Portal da Empresa (APK).
5. Em **Iniciar MDM**, deixe os valores predefinidos tal como estão. Adicione os seguintes detalhes:

    - **Nome do pacote:**`com.microsoft.windowsintune.companyportal`
    - **Nome da classe:**`com.microsoft.windowsintune.companyportal.views.SplashActivity`

Avance para publicar o perfil e consuma-o com a aplicação StageNow no dispositivo. A aplicação do Portal da Empresa é instalada e aberta no dispositivo.

> [!TIP]
> Para obter mais informações sobre o StageNow e para que serve, veja [StageNow Android device staging](https://www.zebra.com/us/en/products/software/mobile-computers/mobile-app-utilities/stagenow.html) (Transição de dispositivos Android com StageNow) (abre o site da Zebra).

## <a name="step-2-confirm-the-company-portal-app-has-device-administrator-role"></a>Passo 2: Confirmar que a aplicação Portal da Empresa tem função de administrador de dispositivos

A aplicação do Portal da Empresa exige um Administrador de Dispositivos para gerir os dispositivos Android. Para ativar a função de Administrador de Dispositivos, alguns dispositivos Zebra incluem uma interface de utilizador (IU) no dispositivo. Se o dispositivo incluir uma IU, a aplicação do Portal da Empresa avisará o utilizador final para atribuir o Administrador de Dispositivos durante a [inscrição](#step-3-enroll-the-device-in-to-intune) (neste artigo).

Se a interface de utilizador não estiver disponível, utilize o **DevAdmin Manager** no StageNow para criar um perfil que atribui manualmente o Administrador de Dispositivos à aplicação do Portal da Empresa.

Os passos seguintes permitem obter uma descrição geral. Para obter detalhes específicos, veja a documentação da Zebra. 
O artigo [Set battery swap mode as device administrator](https://zebratechnologies.force.com/s/article/Set-Battery-Swap-Mode-as-Device-Administrator-using-StageNow-Tool) (Definir o modo de troca de baterias como administrador de dispositivos) (abre o site da Zebra) pode ser uma boa opção.

1. No StageNow, crie um perfil e selecione **Modo Xpert**.
2. Adicione **DevAdmin Manager** ao perfil.
3. Defina **Ação de Administração de Dispositivos** como **Ativar como Administrador de Dispositivos**.
4. Defina **Nome do Pacote de Administração de Dispositivos** como `com.microsoft.windowsintune.companyportal`.
5. Defina **Nome da Classe de Administração de Dispositivos** como `com.microsoft.omadm.client.PolicyManagerReceiver`.

Avance para publicar o perfil e consuma-o com a aplicação StageNow no dispositivo. É atribuída à aplicação do Portal da Empresa a função de Administrador de Dispositivos.

## <a name="step-3-enroll-the-device-in-to-intune"></a>Passo 3: Inscreva o dispositivo em Intune

Depois de concluir os dois primeiros passos, a aplicação do Portal da Empresa é instalada no dispositivo. O dispositivo está pronto para ser inscrito no Intune.

Veja [Inscrever dispositivos Android](../enrollment/android-enroll.md) para obter os passos. Se tiver muitos dispositivos Zebra, talvez prefira utilizar uma [conta de gestor de inscrição de dispositivos (DEM)](../enrollment/device-enrollment-manager-enroll.md). A utilização de uma conta DEM também remove a opção para anular a inscrição da aplicação do Portal da Empresa, para que os utilizadores não possam anular facilmente a inscrição do dispositivo.

## <a name="step-4-create-a-device-management-profile-in-stagenow"></a>Passo 4: Criar um perfil de gestão de dispositivos no StageNow

Utilize o StageNow para criar um perfil que configura as definições que quer gerir no dispositivo. Para obter detalhes específicos, veja a documentação da Zebra. O artigo [Profiles](http://techdocs.zebra.com/stagenow/3-2/stagingprofiles/) (Perfis) (abre o site da Zebra) pode ser uma boa opção.

Quando cria o perfil no StageNow, no último passo, selecione **Exportar para MDM**. Este passo gera um ficheiro XML. Guarde este ficheiro. Irá precisar delas noutro passo.

- É recomendado testar o perfil antes de o implementar nos dispositivos da sua organização. Para testar, no último passo da criação de perfis com o StageNow no computador, utilize as opções **Testar**. Em seguida, consuma o ficheiro gerado pelo StageNow com a aplicação StageNow no dispositivo.

  A aplicação StageNow no dispositivo mostrará os registos gerados quando testar o perfil. [Utilizar registos do StageNow em dispositivos Zebra com Android no Intune](android-zebra-mx-logs-troubleshoot.md) tem informações sobre como utilizar os registos do StageNow para compreender os erros.

- Se fizer referência a aplicações, atualizar pacotes ou atualizar outros ficheiros no perfil do StageNow, vai querer que o dispositivo obtenha estas atualizações. Para obter as atualizações, o dispositivo tem de ligar ao servidor de implementação do StageNow quando o perfil é aplicado. 

  Em alternativa, pode utilizar as funcionalidades incorporadas no Intune para obter essas alterações, incluindo:

  - As funcionalidades de gestão de aplicações para [adicionar](../apps/apps-add.md), [implementar](../apps/apps-deploy.md), atualizar e [monitorizar](../apps/apps-monitor.md) as aplicações.
  - Gerir as [atualizações do sistema e de aplicações](device-restrictions-android-for-work.md#device-owner-only) nos dispositivos com o Android Enterprise

Depois de testar o ficheiro, o próximo passo é implementar o perfil nos dispositivos com o Intune.

- Pode implantar um ou vários perfis MX num dispositivo.
- Também pode exportar vários perfis StageNow e combinar as definições num único ficheiro XML. Em seguida, faça o upload do ficheiro XML para Intune para ser implantado nos seus dispositivos.

  > [!WARNING]
  > Se vários perfis MX forem direcionados para o mesmo grupo, e configurar a mesma propriedade, haverá conflitos no dispositivo.
  >
  > Se a mesma propriedade for configurada várias vezes num único perfil MX, a última configuração ganha.

## <a name="step-5-create-a-profile-in-intune"></a>Passo 5: Criar um perfil em Intune

No Intune, crie um perfil de configuração de dispositivos:

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione **perfis**de configuração de  >  **dispositivos**  >  **Criar perfil**.
3. Introduza as seguintes propriedades:

    - **Nome**: introduza um nome descritivo para o novo perfil.
    - **Descrição**: Introduza uma descrição para o perfil. Esta definição é opcional, mas recomendada.
    - **Plataforma**: Selecione **administrador de dispositivos Android**.
    - **Tipo de perfil:** Selecione **o perfil MX (apenas zebra)**.

4. Em **Perfil MX no formato .xml**, adicione o ficheiro XML do perfil que [exportou do StageNow](#step-4-create-a-device-management-profile-in-stagenow) (neste artigo).
5. Selecione **OK**  >  **Criar** para guardar as suas alterações. A política é criada e apresentada na lista.

    > [!TIP]
    > Por razões de segurança, não verá o texto xml de perfil depois de o guardar. O texto é encriptado e apenas verá asteriscos (`****`). Para sua referência, é recomendado guardar cópias dos perfis MX antes de os adicionar ao Intune.

O perfil está criado, mas ainda não está ativo. Em seguida, [atribua o perfil](device-profile-assign.md) e [monitorize o estado](device-profile-monitor.md).

Da próxima vez que o dispositivo verificar se existem atualizações de configuração, o perfil MX será implementado no dispositivo. Os dispositivos são sincronizados com o Intune quando são inscritos e, depois, aproximadamente a cada 8 horas. Também pode [forçar uma sincronização no Intune](../remote-actions/device-sync.md). Ou, no dispositivo, abra a **aplicação Do Portal**da Empresa  >  **Definições**  >  **Sync**. 

## <a name="update-a-zebra-mx-configuration-after-its-assigned"></a>Atualizar uma configuração Zebra MX depois de ser atribuído

Para atualizar a configuração específica do MX de um dispositivo Zebra, pode: 

- Crie um ficheiro StageNow XML atualizado, edite o perfil Intune MX existente e carregue o novo ficheiro StageNow XML. Este novo ficheiro substitui a política anterior no perfil e substitui a configuração anterior.
- Crie um novo ficheiro StageNow XML que conecte diferentes configurações, crie um novo perfil Intune MX, carregue o novo ficheiro StageNow XML e atribua-o ao mesmo grupo. Vários perfis estão implantados. Se o novo perfil configurar as definições que já existem nos perfis existentes, ocorrerão conflitos.

## <a name="next-steps"></a>Passos seguintes

- [Atribua o perfil](device-profile-assign.md) e [monitorize o respetivo estado](device-profile-monitor.md).
- [Utilizar registos do StageNow para resolver problemas de dispositivos Zebra](android-zebra-mx-logs-troubleshoot.md).
