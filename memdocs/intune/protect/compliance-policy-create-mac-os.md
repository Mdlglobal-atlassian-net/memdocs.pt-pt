---
title: Definições de conformidade de dispositivos macOS no Microsoft Intune – Azure | Microsoft Docs
description: Veja uma lista de todas as definições que pode utilizar quando define a conformidade para os seus dispositivos macOS no Microsoft Intune. Exija a proteção de integridade do sistema da Apple, defina as restrições de palavra-passe, exija uma firewall, permita o controlador de chamadas e muito mais.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/04/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04063cf519c9dcb4a10e7acfa0e51181b3bf259a
ms.sourcegitcommit: 99a6e83219978433ec5a91d09beeaf69acbeb522
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82782247"
---
# <a name="macos-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Definições do macOS para marcar dispositivos como conformes ou não conformes com o Intune

Este artigo apresenta e descreve as definições de conformidade diferentes que pode configurar em dispositivos macOS no Intune. Como parte da sua solução de gestão de dispositivos móveis (MDM), utilize estas definições para definir uma versão mínima e máxima do SO, definir a data de expiração de palavras-passe e muito mais.

Esta funcionalidade aplica-se a:

- macOS

Enquanto administrador do Intune, utilize estas definições de conformidade para ajudar a proteger os recursos da sua organização. Para saber mais sobre as políticas de conformidade e para o que servem, veja a [introdução à conformidade de dispositivos](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Antes de começar

[Criar uma política](create-compliance-policy.md#create-the-policy)de conformidade. Em **Plataforma**, selecione **macOS**.

## <a name="device-health"></a>Estado de Funcionamento do Dispositivo

- **Requerem uma proteção contra a integridade do sistema**  
  - **Não configurado** *(predefinido)*- Esta definição não é avaliada para conformidade ou incumprimento.
  - **Require** - Exija que os dispositivos macOS tenham [a Proteção contra a Integridade do Sistema](https://support.apple.com/HT204899) (abre o site da Apple) ativado.  

## <a name="device-properties"></a>Propriedades do Dispositivo

- **SO Mínimo obrigatório**  
  Quando um dispositivo não cumpre o requisito de versão mínima do SO, será reportado como não conforme. É apresentada uma hiperligação com informações sobre como atualizar. O utilizador do dispositivo pode optar por atualizar o seu dispositivo. Depois, pode aceder aos recursos da organização.

- **Versão máxima de SO permitida**  
  quando um dispositivo utiliza uma versão do SO posterior à versão na regra, o acesso aos recursos da organização é bloqueado. Pede-se ao utilizador do dispositivo que contacte o seu administrador de TI. O dispositivo não poderá aceder aos recursos da organização, enquanto a regra não for alterada para permitir a versão do SO.

- **Versão mínima de construção de Os**  
  quando a Apple publica atualizações de segurança, o número da compilação é normalmente atualizado, não a versão do SO. Utilize esta funcionalidade para introduzir um número mínimo de compilação permitido no dispositivo.

- **Versão máxima de construção de Os**  
  quando a Apple publica atualizações de segurança, o número da compilação é normalmente atualizado, não a versão do SO. Utilize esta funcionalidade para introduzir um número máximo de compilação permitido no dispositivo.

## <a name="system-security-settings"></a>Definições de segurança do sistema

### <a name="password"></a>Palavra-passe

- **Palavra-passe obrigatória para desbloquear os dispositivos móveis**  
  - **Não configurado** *(predefinido)*
  - **Exigir** Os utilizadores devem introduzir uma palavra-passe antes de poderem aceder ao seu dispositivo.

- **Senhas simples**  
  - **Não configurado** *(predefinido)*- Os utilizadores podem criar senhas simples como **1234** ou **1111**.
  - **Bloco** - Os utilizadores não podem criar senhas simples, tais como **1234** ou **1111**.

- **Comprimento mínimo da palavra-passe**  
  introduza o número mínimo de dígitos ou carateres que a palavra-passe tem de ter.

- **Tipo de palavra-passe**  
  escolha se uma palavra-passe deve ter apenas carateres **Numéricos** ou se deve existir uma combinação de números e de outros carateres (**Alfanuméricos**).

- **Número de carateres não alfanuméricos na palavra-passe**  
  introduza o número mínimo de carateres especiais, como `&`, `#`, `%`, `!` e assim por diante, que têm de existir na palavra-passe.

  Definir um número mais relevado exige que o utilizador crie uma palavra-passe mais complexa.

- **Minutos máximos de inatividade antes da palavra-passe ser necessária**  
  introduza o tempo de inatividade antes de o utilizador ter de reintroduzir a palavra-passe.

- **Expiração da Palavra-passe (dias)**  
  selecione o número de dias antes de a palavra-passe expirar e ser necessário criar uma nova.

- **Número de senhas anteriores para evitar a reutilização**  
  introduza o número de palavras-passe utilizadas anteriormente que não podem ser utilizadas.
> [!IMPORTANT]
> Quando o requisito da palavra-passe é alterado num dispositivo macOS, só entrará em vigor na próxima vez que o utilizador alterar a sua palavra-passe. Por exemplo, se definir uma restrição de comprimento da palavra-passe para oito dígitos e o dispositivo macOS tiver atualmente uma palavra-passe de seis dígitos, o mesmo permanecerá em conformidade até à próxima vez que o utilizador atualizar a palavra-passe no dispositivo.

### <a name="encryption"></a>Encriptação

- **Encriptação do armazenamento de dados num dispositivo**  
  - **Não configurado** *(predefinido)*
  - **Exigir** - Utilizar *o Necessário* para encriptar o armazenamento de dados nos seus dispositivos.

### <a name="device-security"></a>Segurança do Dispositivo

A firewall protege os dispositivos contra o acesso não autorizado à rede. Pode utilizar a firewall para controlar as ligações por aplicação. 

- **Firewall**  
  - **Não configurado** *(predefinido*) - Esta definição deixa a firewall desligada e o tráfego de rede é permitido (não bloqueado).
  - **Ativar** - Utilizar *o Enable* para ajudar a proteger os dispositivos de acesso não autorizado. Ativar esta funcionalidade permite-lhe processar as ligações recebidas da Internet e utilizar o modo furtivo. 

- **Ligações de entrada**  
  - **Não configurado** *(predefinido)*- Permite ligações de entrada e serviços de partilha.
  - **Bloco** - Bloqueie todas as ligações de rede de entrada, exceto as ligações necessárias para serviços básicos de internet, tais como DHCP, Bonjour e IPSec. Esta definição também bloqueia todos os serviços de partilha, incluindo a partilha de ecrã, o acesso remoto, a partilha de música do iTunes, entre outros.  

- **Modo Stealth**  
  - **Não configurado** *(predefinido)*- Esta definição deixa o modo de stealth desligado.
  - **Ativar** - Ligue o modo de stealth para evitar que os dispositivos respondam a pedidos de sondagem, o que pode ser feito aos meus utilizadores maliciosos. Quando ativado, o dispositivo continua a responder a pedidos recebidos de aplicações autorizadas.  

### <a name="gatekeeper"></a>Controlador de chamadas

Para obter mais informações, veja [Controlador de chamadas no macOS](https://support.apple.com/HT202491) (abre o site da Apple).

- **Permitir aplicações descarregadas a partir destes locais**  
  permite a instalação de aplicações suportadas nos seus dispositivos a partir de diferentes localizações. As suas opções de localização:

  - **Não configurado** *(predefinido)*- A opção gatekeeper não tem qualquer impacto no cumprimento ou no incumprimento.  
  - **Mac App Store** - Apenas instale aplicativos para a loja de aplicações Mac. Não é possível instalar aplicações de terceiros nem de programadores identificados. Se um utilizador selecionar o Controlador de Chamadas para instalar aplicações que não sejam da Mac App Store, o dispositivo será considerado não conforme.
  - **Mac App Store e desenvolvedores identificados** - Instale aplicativos para a loja de aplicações Mac e de desenvolvedores identificados. O macOS verifica a identidade dos programadores e faz outras verificações para confirmar a integridade da aplicação. Se um utilizador selecionar o Controlador de Chamadas para instalar aplicações que não estejam abrangidas por estas opções, o dispositivo será considerado não conforme.
  - **Qualquer lugar** - As aplicações podem ser instaladas a partir de qualquer lugar, e por qualquer desenvolvedor. Esta é a opção menos segura.
 

## <a name="next-steps"></a>Passos seguintes

- [Adicionar ações para dispositivos não conformes](actions-for-noncompliance.md) e [utilizar etiquetas de âmbito para filtrar políticas](../fundamentals/scope-tags.md).
- [Monitorizar as políticas de conformidade](compliance-policy-monitor.md).
- Veja as [definições de política de conformidade para dispositivos iOS](compliance-policy-create-ios.md).