---
title: Windows Autopilot com cogestão
titleSuffix: Configuration Manager
description: Utilize o Windows Autopilot com cogestão no Gestor de Configuração para simplificar a configuração de novos dispositivos Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b97f9bb6be00129e0b88dc3943af1de166a801d4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711288"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot com cogestão

Receber um novo dispositivo Windows 10 é entusiasmante. No entanto, pode levar algum tempo a configurar todas as suas definições e aplicações para que possa ser produtivo. A cogestão resolve este problema de fornecimento de dispositivos com o Windows Autopilot.

O Autopilot proporciona uma experiência simplificada tanto para si como para os seus utilizadores nas seguintes situações:
- Configurar e reconfigurar novos dispositivos do Windows 10  
- Repor, reciclar e recuperar dispositivos existentes  

O piloto automático reduz o tempo, os recursos e a complexidade associados à implantação, gestão e dereforma dos dispositivos. Ao mesmo tempo, a experiência para os seus utilizadores é simplificada e fácil desde a primeira bota.

O Windows Autopilot suporta vários cenários, todos maximizados com a cogestão:

- Os utilizadores podem conduzir as suas próprias implementações de novos dispositivos para o Ative Directory com a adesão híbrida azure AD, ou Azure Ative Directory (Azure AD)  

- Pode configurar novas implementações de dispositivos em Azure AD para dispositivos e quiosques partilhados  

- Com o Windows Autopilot para dispositivos existentes, utilize o Gestor de Configuração para migrar um dispositivo existente do Windows 7 e Diretório Ativo para o Windows 10 e AD Azure  

No vídeo seguinte, o gestor de programas sénior Danny Guillory e o diretor de programas Andrew McMurray discutem e demo Windows Autopilot com cogestão:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Benefícios

Quando utilizar a cogestão e o Autopilot em conjunto, certifique-se de que os novos dispositivos que entram na sua rede acabam no mesmo estado de gestão. Nesta configuração, os dispositivos estão matriculados em Intune e têm um cliente de Gestor de Configuração.  Permite-lhe utilizar o novo modelo de provisionamento do Windows 10 e ajuda-o a eliminar a necessidade de criar, manter e atualizar imagens personalizadas de OS. 

Em todos estes cenários, pode ativar automaticamente a [cogestão](how-to-prepare-Win10.md) pela Intune. Esta automatização ajuda no processo de provisionamento e na gestão contínua do dispositivo.

Com o Autopilot, não precisas de te preocupar com imagens e condutores. Concentre-se no fornecimento de dispositivos através deste processo automatizado utilizando intune e Configuração Manager através da cogestão.


Eis como usar a cogestão e o Autopilot juntos pode ajudá-lo agora:

#### <a name="reduce-time-costs-and-complexity"></a>Reduzir o tempo, os custos e a complexidade
O Windows Autopilot utiliza a versão otimizada do OEM do Windows 10 que está pré-instalada no dispositivo. Esta configuração poupa às organizações o esforço de ter de manter imagens e controladores personalizados para cada modelo de dispositivo em uso. Em vez de reimaginar o dispositivo, transforme a instalação existente do Windows 10 num estado "pronto para o negócio". Aplica definições e políticas, instala apps e altera a edição do Windows 10. Por exemplo, a atualização do Windows 10 Pro para o Windows 10 Enterprise para que possa suportar funcionalidades avançadas.

#### <a name="improve-the-user-experience"></a>Melhorar a experiência do utilizador
A melhor experiência do utilizador causa a menor perturbação e ajuda-os a voltar a concentrarem-se no seu trabalho. O Windows Autopilot oferece uma abordagem simples para ajudar os seus utilizadores a configurarem-se rapidamente com alguns simples cliques e as suas credenciais DeD Azure. Para muitas organizações com um grande campo de funcionários remotos, utilize o Windows Autopilot para enviar novos dispositivos diretamente do fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Utilize o Autopilot e o Gestor de Configuração para migrar os dispositivos existentes do Windows 7 para o Windows 10
Com o Windows Autopilot para dispositivos existentes, cria-se um ficheiro de configuração e implementa-o com uma sequência de tarefas do Gestor de Configuração. Este processo migra facilmente os dispositivos existentes do Windows 7 para o Windows 10. Utiliza uma imagem do Windows 10 de assinatura no 'Configuração Manager' e aplica-a ao dispositivo Windows 7 existente com a configuração Autopilot. Quando o utilizador inicia o dispositivo, utiliza o processo de embarque conduzido pelo utilizador Autopilot.

Aqui estão os passos para o Autopilot para dispositivos existentes:

![Visão geral do processo para o Windows Autopilot para dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implementar a política do grupo para redirecionar pastas conhecidas para o OneDrive
2. Gerar ficheiro de configuração do Piloto Automático
3. Implementar sequência de tarefas para atualizar para o Windows 10
4. Máquina do Windows 10 passa pelo Autopilot na primeira bota

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernização do fornecimento de dispositivos para todos os tipos de trabalhadores
Com o Autopilot, pode agora fornecer uma implementação de SO mãos-livres a dispositivos não tripulados ou dispositivos partilhados utilizando o modo de auto-implantação. Esta configuração satisfaz as necessidades de todos os seus diferentes tipos de trabalhadores. Além disso, a função de Reset do Piloto Automático do Windows garante que o reprovisionamento de um dispositivo a um novo utilizador é simples e fácil. Este processo simplifica o que tradicionalmente tem sido uma tarefa difícil quando se tem trabalhadores sazonais ou contratados. 



## <a name="case-study"></a>Estudo de caso

A empresa alemã de logística e transporte ferroviário DB Shenker utiliza o Autopilot para aumentar a produtividade dos colaboradores e libertar as suas equipas de TI de trabalharem em tarefas de apoio diárias. Shenker afastou-se da imagem tradicional e substituiu-a por provisões através da nuvem. Agora usam a AD-join Azure e intune para obter novos dispositivos em funcionamento rapidamente. 

Em vez de os seus trabalhadores remotos perderem tempo a viajar para um local com serviços de TI, shenker agora usa o Windows Autopilot. Enviam o equipamento dos seus trabalhadores diretamente do fabricante para o seu escritório de campo local. O trabalhador liga o novo dispositivo à internet e assina com as suas credenciais De AD Azure. O dispositivo liga-se então às aplicações e serviços que o departamento de TI de Schenker atribui ao perfil individual do utilizador.

Para mais informações, consulte a empresa global [de logística centraliza as TI, une os colaboradores com](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10)o local de trabalho digital moderno.



## <a name="value-proposition"></a>Proposta de valor

Crie satisfação na sua organização criando uma melhor experiência de utilizador para os seus utilizadores. Utilize o Windows Autopilot para reduzir os custos. Liberte o seu tempo para se concentrar em outros projetos para impulsionar mais valor e impacto para a sua organização.



## <a name="configure"></a>Configurar

Para obter mais informações, veja os artigos seguintes:

[Utilizar Intune para criar perfis do Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

Windows Autopilot para sequência de [tarefas de dispositivos existentes](../osd/deploy-use/windows-autopilot-for-existing-devices.md)

