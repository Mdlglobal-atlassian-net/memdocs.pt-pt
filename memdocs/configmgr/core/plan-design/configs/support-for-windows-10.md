---
title: Suporte para o Windows 10
titleSuffix: Configuration Manager
description: Conheça as versões do Windows 10 que são suportadas como clientes ou para OSD com Gestor de Configuração
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709629"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Suporte para Windows 10 no Gestor de Configuração  

*Aplica-se a: Gestor de Configuração (ramo atual)*

Saiba mais sobre as versões do Windows 10 que o Gestor de Configuração suporta, incluindo:

- [Windows 10 como cliente de Gestor de Configuração](#windows-10-as-a-client)
- [O Kit de Avaliação e Implementação do Windows (ADK) para windows 10](#windows-10-adk)

> [!Tip]
> O Windows Server constrói como cliente o mesmo que a versão associada do Windows 10. Por exemplo, o Windows Server 2016 é a mesma versão de construção do Windows 10 LTSB 2016, e a versão 1803 do Windows Server é a mesma versão de construção que a versão 1803 do Windows 10.
>
> Para obter mais informações sobre o Windows Server como um sistema de site, consulte [sistemas operativos suportados para servidores](supported-operating-systems-for-site-system-servers.md#bkmk_core)do sistema do Gestor de Configuração .

## <a name="windows-10-as-a-client"></a>Windows 10 como cliente

O Gestor de Configuração tenta fornecer suporte como cliente para cada nova versão do Windows 10 o mais rapidamente possível após a sua disponibilização. Como os produtos têm horários separados de desenvolvimento e lançamento, o suporte que o Gestor de Configuração fornece depende de quando cada um fica disponível.

Uma versão Do Gestor de Configuração cai da matriz após o [suporte para esta versão](../../servers/manage/current-branch-versions-supported.md) termina. Da mesma forma, o suporte para versões do Windows 10 como o Enterprise 2015 LTSB ou 1511 cai da matriz quando são removidos do suporte.

- A versão mais recente do menu atual do Gestor de Configuração recebe atualizações de segurança e críticas, que podem incluir correções para problemas com versões do Windows 10. Quando a Microsoft lançar uma nova versão do atual ramo do 'Gestor de Configuração', as versões anteriores apenas recebem atualizações de segurança. Para mais informações, consulte as [versões atuais](../../servers/manage/current-branch-versions-supported.md)do Suporte para O Gestor de Configuração .  

    > [!Note]  
    > A melhor maneira de se manter atual com o Windows 10 é manter-se atual com o Gestor de Configuração. Para mais informações, consulte o Gestor de [Configuração e o Windows como um Serviço](../../understand/configuration-manager-and-windows-as-service.md).  

- Esta informação complementa [sistemas operativos suportados para clientes e dispositivos.](supported-operating-systems-for-clients-and-devices.md)  

- Se utilizar o ramo de manutenção a longo prazo do Gestor de Configuração, consulte [configurações suportadas para o ramo](../../understand/supported-configurations-for-ltsb.md)de manutenção a longo prazo .  

A tabela seguinte lista as versões do Windows 10 que pode utilizar como cliente com diferentes versões de 'Gestor de Configuração'.

| Versão do Windows 10 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Para obter mais informações sobre o ciclo de vida do Windows, consulte a [ficha de factos do ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) de vida do Windows

| Chave |
|--|
| ![Apoio](media/green_check.png) = **Apoiado**  |
| ![Não](media/Red_X.png) = **apoiado não apoiado** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a>Notas de suporte ao cliente do Windows 10

- O suporte para versões semestral do Windows 10 inclui as seguintes edições: Enterprise, Pro, Education e Pro Education.  

- A partir da versão 1906, o Gestor de Configuração suporta o Windows 10 Pro para workstation.

- Para o Windows 10, versão 1909, os meios de implementação do OS mostram a versão como 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a>Windows 10 no ARM64

O Gestor de Configuração suporta o cliente nos dispositivos ARM64 do Windows 10. A implantação do OS não é suportada.<!-- 1353704 -->

Começando na versão 2002,<!--5954175--> a plataforma **All Windows 10 (ARM64)** está disponível na lista de versões de OS suportadas em objetos com regras de requisitos ou listas de aplicabilidade.

> [!NOTE]
> Se selecionou anteriormente a plataforma de topo **do Windows 10,** esta ação selecionou automaticamente **tanto o Windows 10 (64-bit)** como **o All Windows 10 (32-bits).** Esta nova plataforma não é selecionada automaticamente. Se quiser adicionar **todos os Windows 10 (ARM64)**, selecione-o manualmente na lista.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a>Suporte para Windows Insider

A partir da versão 1906 do 'Gestor de Configuração', pode atualizar e servir as construções [do Windows Insider.](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) Esta capacidade é fornecida como uma conveniência para os nossos clientes. Embora esta funcionalidade funcione, o suporte para a sua melhor forma é. O Gestor de Configuração pode não emitir um hotfix para esta funcionalidade se deixar de funcionar.  

Para fornecer feedback sobre o Windows Insider, utilize o [Feedback Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Quando implementa sistemas operativos com o Gestor de Configuração, o Windows ADK é uma dependência externa necessária. Para obter mais informações, veja os artigos seguintes:

- [Requisitos de infraestrutura para a implementação do SO](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Transferir o Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > A partir da versão 1809 do Windows 10, o Windows PE é um instalador separado. Caso contrário, não há diferença funcional.
    >
    > Certifique-se de que descarrega tanto o **Windows ADK para windows 10** como o **addon Windows PE para o ADK**.

A tabela seguinte lista as versões do ADK do Windows 10 que pode utilizar com diferentes versões do 'Gestor de Configuração'.

| Versão ADK do Windows 10  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Não suportado](media/Red_X.png)   | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Para trás compatível](media/blue_compat.png) | ![Para trás compatível](media/blue_compat.png) | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Para trás compatível](media/blue_compat.png) | ![Para trás compatível](media/blue_compat.png) | ![Não suportado](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

|Chave|
|--|
| ![Apoio](media/green_check.png) = **Apoiado** <br/> Esta tabela apenas mostra a capacidade de suporte do Windows ADK em relação à versão do 'Gestor de Configuração'. A Microsoft recomenda a utilização do Windows ADK que corresponda à versão do Windows que está a implementar. Utilize a versão Mais recente do Windows ADK ao implementar a versão mais recente do Windows 10. A versão mais recente do Windows ADK poderá suportar a implementação de versões oS mais antigas, como o Windows 8.1.<!-- SCCMDocs issue 1229 --> Para obter mais informações sobre a capacidade de suporte de componentes do Windows ADK, consulte plataformas suportadas pelo [DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatível para](media/blue_compat.png)  = **trás compatível com retrocesso** <br/> Esta combinação não é testada, mas deve funcionar. Documentaremos quaisquer problemas ou ressalvas conhecidas. |
| ![Não](media/Red_X.png) = **apoiado não apoiado** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a>Notas de suporte aDK do Windows 10

- O Gestor de Configuração apenas suporta componentes x86 e amd64 do Windows 10 ADK. Atualmente, não suporta componentes ARM ou ARM64.

- As construções do Windows Server têm o mesmo requisito do Windows ADK que a versão associada do Windows 10. Por exemplo, o Windows Server 2016 é a mesma versão de construção do Windows 10 LTSB 2016.
