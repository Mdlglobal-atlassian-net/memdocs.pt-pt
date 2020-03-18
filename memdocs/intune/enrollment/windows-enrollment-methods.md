---
title: Métodos de inscrição do Intune para dispositivos Windows
titleSuffix: Microsoft Intune
description: Saiba as diferentes formas de inscrever dispositivos Windows em Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/25/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: ''
ms.openlocfilehash: eac0eff9167e46d73dffe1c74ce073ffa68c7070
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332745"
---
# <a name="intune-enrollment-methods-for-windows-devices"></a>Métodos de inscrição do Intune para dispositivos Windows

Para gerir os dispositivos em Intune, os dispositivos devem ser matriculados primeiro no serviço Intune. Tanto os dispositivos de propriedade pessoal como os dispositivos corporativos podem ser matriculados para gestão intune. 

Há duas formas de obter dispositivos matriculados em Intune:
- Os utilizadores podem auto-inscrever os seus Computadores Windows 
- Os administradores podem configurar políticas para forçar a inscrição automática sem qualquer envolvimento do utilizador

## <a name="user-self-enrollment-in-intune"></a>Auto-inscrição do utilizador em Intune

Os utilizadores podem auto-inscrever o seu dispositivo Windows utilizando qualquer um destes métodos:

- [Traga o seu próprio dispositivo (BYOD)](https://docs.microsoft.com/user-help/enroll-windows-10-device): Os utilizadores matriculam os seus dispositivos pessoalmente, optando por ligar uma conta **De Trabalho e Escola** a partir das **Definições** do dispositivo. Este processo:
  - Regista o dispositivo com o Azure Ative Directory para ter acesso a recursos corporativos como e-mail.
  - Inscreve o dispositivo em Intune como um dispositivo pessoal (BYOD).
Se um administrador tiver configurado a inscrição automática (disponível com subscrições premium Azure AD), o utilizador só tem de introduzir as suas credenciais uma vez. Caso contrário, terão de se inscrever separadamente através do MDM apenas através da inscrição do MDM e reintroduzir as suas credenciais.  
- **Apenas a inscrição** no MDM permite que os utilizadores matriculem um workgroup existente, Diretório Ativo ou diretório Azure Ative juntou-se ao PC em Intune. Os utilizadores matriculam-se a partir de Definições no PC do Windows existente. Este método não é recomendado porque não regista o dispositivo no Diretório Ativo Azure. Também impede a utilização de funcionalidades como o Acesso Condicional.
- [Azure Ative Directory (Azure AD) Junta-se](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network) ao dispositivo com o Diretório Ativo Azure e permite que os utilizadores inscrevam-se no Windows com as suas credenciais De AD Azure. Se a inscrição automática estiver ativada, o dispositivo está automaticamente matriculado no Intune. O benefício da inscrição automática é um processo de um passo único para o utilizador. Caso contrário, terão de se inscrever separadamente através do MDM apenas através da inscrição do MDM e reintroduzir as suas credenciais. Os utilizadores matriculam-se desta forma, quer durante o Windows OOBE inicial, quer a partir de Definições. O dispositivo está marcado como um dispositivo corporativo em Intune.
- [Autopilot](enrollment-autopilot.md) - Automatiza AD Join e inscreve novos dispositivos corporativos em Intune. Este método simplifica a experiência fora da caixa e remove a necessidade de aplicar imagens personalizadas do sistema operativo nos dispositivos. Quando os administradores usam o Intune para gerir dispositivos Autopilot, podem gerir políticas, perfis, apps e muito mais depois de estarem matriculados.  Existem quatro tipos de implementação do Autopilot: [Modo de Auto-implantação](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying) (para quiosques, sinalização digital ou um dispositivo partilhado), [Modo Acionado pelo Utilizador](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) (para utilizadores tradicionais), a Luva [Branca](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove) permite aos parceiros ou pessoal de TI pré-fornecer um PC Windows 10 para que esteja totalmente configurado e pronto para o negócio e Autopilot [para dispositivos existentes](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) permite-lhe implementar facilmente a versão mais recente do Windows 10 para os seus dispositivos existentes.

## <a name="administrator-based-enrollment-in-intune"></a>Inscrição baseada em administrador em Intune

Os administradores podem configurar os seguintes métodos de inscrição que não requerem interação do utilizador:

- [A Hybrid Azure AD Join](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) permite aos administradores configurar a política do grupo Ative Directory para inscrever automaticamente dispositivos híbridos Azure AD.
- [A Co-management do Gestor de Configuração](https://docs.microsoft.com/configmgr/comanage/overview) permite que os administradores inscrevam os seus dispositivos geridos pelo Gestor de Configuração existentes no Intune para obter os benefícios duplos do Intune e do Gestor de Configuração.
- [O gestor de inscrição](device-enrollment-manager-enroll.md) de dispositivos (DEM) é uma conta de serviço especial. As contas DEM têm permissões que permitem aos utilizadores autorizados inscreverem-se e gerirem vários dispositivos corporativos. Estes tipos de dispositivo são ideais, por exemplo, para aplicações de utilitários ou ponto de venda, mas não para utilizadores que necessitem de aceder a recursos de e-mail ou da empresa. Este método não permite a utilização de funcionalidades como o Acesso Condicional. 
- [A inscrição](windows-bulk-enroll.md) a granel permite que um utilizador autorizado se junte a um grande número de novos dispositivos corporativos para o Azure Ative Directory e intune. Cria um pacote de provisionamento com a aplicação Windows Configuration Designer (WCD). Em seguida, utilizando suportes USB durante a experiência inicial do Windows OOBE ou a partir do PC do Windows existente, instala o pacote de fornecimento para inscrever automaticamente os dispositivos no Intune. Este método não permite a utilização do Acesso Condicional.
- [A inscrição de dispositivos Windows IoT Core](https://docs.microsoft.com/windows/iot-core/manage-your-device/intunedeviceenrollment) é realizada utilizando o Painel Core Windows IoT para preparar o dispositivo e, em seguida, utilizando o Windows Configuration Designer para criar um pacote de provisionamento. Em seguida, utilizando os meios de cartão SD durante o arranque inicial, instala o pacote de fornecimento para inscrever automaticamente os dispositivos em Intune.

## <a name="next-steps"></a>Próximos passos

[Conheça as capacidades dos métodos de inscrição do Windows](enrollment-method-capab.md)
