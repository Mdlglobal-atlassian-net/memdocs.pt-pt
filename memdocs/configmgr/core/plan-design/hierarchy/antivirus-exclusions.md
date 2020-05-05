---
title: Exclusões antivírus
titleSuffix: Configuration Manager
description: Aprenda sobre exclusões antivírus recomendadas para uso quando resolver problemas possíveis.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720297"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Exclusões antivírus recomendadas para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo contém recomendações que podem ajudar um administrador a determinar a causa de uma potencial instabilidade num computador que está a executar uma versão suportada de servidores de site do Gestor de Configuração, sistemas de sites e clientes quando é usado juntamente com software antivírus.

> [!IMPORTANT]
>
> - Recomendamos que aplique temporariamente estes procedimentos para avaliar um sistema. Se o desempenho ou estabilidade do seu sistema for melhorado pelas recomendações que são feitas neste artigo, contacte o seu fornecedor de software antivírus para obter instruções ou para obter uma versão atualizada do software antivírus.
> - Este artigo contém informações que mostram como ajudar a baixar as definições de segurança ou como desligar temporariamente as funcionalidades de segurança num computador. Pode fazer estas alterações para entender a natureza de um problema específico. Antes de fazer estas alterações, recomendamos que avalie os riscos associados à implementação desta salção em seu ambiente particular.

## <a name="possible-symptoms"></a>Possíveis sintomas 

A proteção antivírus em tempo real pode causar muitos problemas em servidores de site do Gestor de Configuração, sistemas de site e clientes.

Segue-se uma lista não completa de possíveis sintomas:

- Os componentes do sistema de localização remota não estão instalados. SiteComp.log, Distmgr.log, hman.log ou outros ficheiros de registo do Gestor de Configuração podem conter erros como erro 80070005.
- O cliente do Gestor de Configuração não pode ser instalado utilizando o Client Push.
- A informação do inventário do cliente é imprecisa, em falta ou desatualizada.
- Os atrasos ocorrem nas pastas *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes.
- O Software Center não é povoado por software implantado em sistemas de clientes, ou não começa. Além disso, o ficheiro CCMRepair.log pode conter erros que se assemelham ao seguinte exemplo:

  > A verificação da base de dados falhou com o resultado: 0x80004005 mas DB: C:\Windows\CCM\filename.sdf pode ser aberto, ignorando a reparação de DB.

- O software que é implantado para clientes não pode ser instalado.
- Os dados de conformidade para implementações de software são imprecisos.

## <a name="exclusions"></a>Exclusões

Para evitar tais problemas, recomendamos que adicione as seguintes exclusões de proteção em tempo real:

### <a name="default-installation-folders"></a>Pastas de instalação predefinidas

|  |  |
| - | - |
|*Pasta de Instalação ConfigMgr*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*Pasta de Instalação mp*  |%ProgramFiles%\SMS_CCM  |  
|*Pasta de Instalação de Clientes*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Exclusões de pastas para servidores do site

- Pasta de *Instalação ConfigMgr*\Caixas de entrada
- Pasta de *Instalação ConfigMgr*\Logs
- Pasta de *Instalação ConfigMgr*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Exclusões de pastas para sistemas de sites

- Pontos de gestão
  - *PMp pasta de instalação*\ServiceData
  - Um dos seguintes:
    - Pasta de *instalação ConfigMgr*\MP\OUTBOXES
    - *Unidade de instalação*\SMS\MP\OUTBOXES
- Pontos de distribuição
  - *Pasta de instalação de clientes*\ServiceData
  - *ContentLib_Drive*SMS_DP$
  - *ContentLib_Drive*Drive_Letter \SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- Servidores de base de dados de sites
  - [Como escolher o software antivírus para funcionar em computadores que estão a executar o SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Exclusões de pastas para clientes

- *Pasta de*\\\*Instalação do Cliente .sdf
- *Pasta de Instalação de Clientes*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Pasta de Instalação de Clientes*\Logs

### <a name="file-exclusions-for-mps"></a>Exclusões de ficheiros para deputados

- POL00000.pol em
  - *PP Pasta de Instalação*\PolReqStaging

### <a name="process-exclusions"></a>Exclusões de processos

As exclusões de processos só são necessárias se os programas antivírus agressivos considerarem os ficheiros do programa Do Gestor de Configuração (ficheiros.exe) como processos de alto risco.

- Pasta de *Instalação ConfigMgr*\bin\64\Smsexec.exe
- Qualquer um dos seguintes processos:
  - *Pasta de Instalação de Clientes*\Ccmexec.exe
  - *PMp Pasta*de Instalação \Ccmexec.exe
- *Pasta de Instalação do Cliente*\CmRcService.exe (lado do cliente)
- Pasta de *Instalação ConfigMgr*\bin\64\Sitecomp.exe
- Pasta de *Instalação ConfigMgr*\bin\64\Smswriter.exe
- Pasta de *Instalação ConfigMgr*\bin\64\Smssqlbkup.exe, ou SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- Pasta de *Instalação ConfigMgr*\bin\64\Cmupdate.exe
- *Pasta de Instalação do Cliente*\Ccmrepair.exe (lado do cliente)
- %*windir*%\CCMSetup\Ccmsetup.exe (lado cliente)

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre exclusões antivírus, consulte os seguintes artigos:

[Gestor de configuração Exclusões antivírus do ramo atual -System Center Premier Field Engineer Blog](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[Atualizado System Center 2012 Configuração Manager Antivirus Exclusions com mais detalhes sobre ASD e Boot Images](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[Como escolher o software antivírus para funcionar em computadores que estão a executar o SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Recomendações de digitalização de vírus para computadores Da empresa que estão a executar versões suportadas atualmente do Windows](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
