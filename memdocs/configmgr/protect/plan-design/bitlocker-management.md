---
title: Planear a gestão do BitLocker
titleSuffix: Configuration Manager
description: Plano para gerir encriptação de unidade BitLocker com gestor de configuração
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 926d1483739b85f787ebc9e2a992ea7ed39633c2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722215"
---
# <a name="plan-for-bitlocker-management"></a>Planear a gestão do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!-- 3601034 -->

A partir da versão 1910, utilize o Gestor de Configuração para gerir a Encriptação bitLocker Drive (BDE) para clientes windows no local. Fornece uma gestão completa do ciclo de vida BitLocker que pode substituir a utilização da Microsoft BitLocker Administration and Monitoring (MBAM).

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Para mais informações, consulte a [visão geral do BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Para gerir a encriptação em dispositivos cogeridos do Windows 10 utilizando o serviço de cloud Do Microsoft Endpoint Manager, altere a carga de trabalho de [ **Proteção de Ponto** ](../../comanage/workloads.md#endpoint-protection) final para Intune. Para obter mais informações sobre a utilização do Intune, consulte a [Encriptação do Windows](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Funcionalidades

O Gestor de Configuração fornece as seguintes capacidades de gestão para encriptação de unidade BitLocker:

### <a name="client-deployment"></a>Implementação de clientes

Implemente o cliente BitLocker para gerir dispositivos Windows que executam o Windows 10 ou Windows 8.1

### <a name="manage-encryption-policies"></a>Gerir políticas de encriptação

- Por exemplo: escolha a encriptação de unidade e a força da cifra, configure a política de isenção do utilizador, as definições de encriptação de unidade de dados fixos.

- Determine os algoritmos com os quais encriptar o dispositivo e os discos que você visa para encriptação.

- Forçar os utilizadores a cumprir em conformidade com novas políticas de segurança antes de utilizar o dispositivo.

- Personalize o perfil de segurança da sua organização por dispositivo.

- Quando um utilizador desbloquear a unidade DES, especifique se desbloqueia apenas uma unidade de SISTEMA ou todas as unidades anexas.

### <a name="compliance-reports"></a>Relatórios de conformidade

Relatórios incorporados para:

- Estado de encriptação por volume ou por dispositivo
- O principal utilizador do dispositivo
- Estado de conformidade
- Razões para o incumprimento

### <a name="administration-and-monitoring-website"></a>Site de administração e monitorização

Permita que outras personalidades na sua organização fora da consola Do Gestor de Configuração ajudem na recuperação da chave, incluindo a rotação da chave e outros suportes relacionados com o BitLocker. Por exemplo, os administradores de mesa de ajuda podem ajudar os utilizadores com a recuperação da chave.

### <a name="user-self-service-portal"></a>Portal de autosserviço do utilizador

Deixe os utilizadores ajudarem-se a si próprios com uma chave de uso único para desbloquear um dispositivo encriptado BitLocker. Uma vez utilizada esta chave, gera uma nova chave para o dispositivo.

## <a name="prerequisites"></a>Pré-requisitos

- Para criar uma política de gestão BitLocker, precisa do papel de **Administrador Completo** no Gestor de Configuração.

- O serviço de recuperação BitLocker requer HTTPS para encriptar as chaves de recuperação através da rede desde o cliente De Configuração Gerir até ao ponto de gestão. Existem duas opções:

  - HTTPS-enable o site do IIS no ponto de gestão que acolhe o serviço de recuperação. Esta opção aplica-se apenas à versão de Configuração Manager 2002.<!-- 5925660 -->

  - Configure o ponto de gestão para HTTPS. Esta opção aplica-se às versões 1910 ou 2002 do Gestor de Configuração.

  Para mais informações, consulte [encriptar dados de recuperação](../deploy-use/bitlocker/encrypt-recovery-data.md).

- Para utilizar os relatórios de gestão bitLocker, instale a função do sistema de pontos de ponto de serviços de reporte. Para mais informações, consulte [o relatório Configure](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > Para que o Relatório de Auditoria de **Recuperação** funcione a partir do site de administração e monitorização, utilize apenas um ponto de serviços de reporte no local principal.

- Para utilizar o portal de self-service ou o site de administração e monitorização, precisa de um servidor Windows que execute o IIS. Pode reutilizar um sistema de site do Gestor de Configuração ou utilizar um servidor web autónomo que tenha conectividade com o servidor de base de dados do site. Utilize uma [versão SISTEMA suportada para servidores](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)do sistema do site .

    > [!NOTE]
    > Instale apenas o portal de auto-atendimento e o site de administração e monitorização com uma base de dados de site primário. Numa hierarquia, instale estes websites para cada local primário.

- No servidor web que irá acolher o portal de self-service, instale o [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4).

- A conta de utilizador que executa o script do instalador do portal necessita de direitos de **sisadmina** SQL no servidor de base de dados do site. Durante o processo de configuração, o script define direitos de função de login, utilizador e SQL para a conta de máquina de servidor web. Pode remover esta conta de utilizador da função de sysadmina após a configuração do portal de autosserviço e do site de administração e monitorização.

- A BitLocker Management não é suportada em máquinas virtuais (VMs). Por esta razão, algumas funcionalidades podem não funcionar como esperado em máquinas virtuais. Por exemplo, a BitLocker Management não iniciará a encriptação em unidades fixas de máquinas virtuais. As unidades fixas adicionais em máquinas virtuais podem mostrar-se conformes, mesmo que não estejam encriptadas.

> [!TIP]
> Por defeito, o passo da sequência de tarefas **Enable BitLocker** apenas encripta o *espaço utilizado* na unidade. A gestão bitLocker utiliza encriptação completa do *disco.* Configure este passo de sequência de tarefas para permitir a opção **de utilizar a encriptação completa do disco**. Para mais informações, consulte os passos da [sequência de tarefas - Enable BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Passos seguintes

[Encriptar dados de recuperação](../deploy-use/bitlocker/encrypt-recovery-data.md) (um pré-requisito opcional antes de implementar a política pela primeira vez)

[Implementar o cliente de gestão BitLocker](../deploy-use/bitlocker/deploy-management-agent.md)
