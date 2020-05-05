---
title: Capacidades na Pré-visualização Técnica 1512
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074508"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1512 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1512. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a>Atestação de Saúde do Dispositivo  
 A partir da Pré-visualização Técnica 1512, os administradores podem visualizar o estado do Atestado de Saúde do Dispositivo Windows 10 na consola do Gestor de Configuração.  Esta funcionalidade está disponível para O Gestor de Configuração e Configuração com o Microsoft Intune. O Device Health Attestation permite ao administrador garantir que os computadores cliente têm configurações fidedignas de BIOS, TPM e software de arranque. Para suportar o atestado de saúde do dispositivo, os dispositivos do cliente devem estar a executar o Win10 com tPM 2 ativado. O Device Health Attestation apresenta o número de dispositivos ativados para cada o seguinte:  

-   Antimalware de início antecipado  

-   BitLocker  

-   Arranque Seguro  

-   Integridade do Código  

A consola também apresenta as definições de atestado de saúde mais altas com o número de dispositivos.  

Para pré-visualizar a vista de atestado de saúde do dispositivo, na consola do Gestor de Configuração vá ao espaço de trabalho de **Monitorização,** clique no nó de **segurança** e, em seguida, clique em **Atestado de Saúde**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a>Monitorização na consola para termos e condições  
A partir da Pré-visualização Técnica 1512, quando integrar o Gestor de Configuração com o Microsoft Intune, pode utilizar a consola Do Gestor de Configuração para ver quais os utilizadores que aceitaram os termos e condições configurados pelo seu departamento de TI, e que os utilizadores não têm.  

**Para ver informações sumárias:**  

-   Na consola do Gestor de Configuração, vá para **monitorizar** > **as implementações** **de visão geral** > e selecione os termos e condições de implementação que pretende ver.  

**Para ver informações detalhadas:**  

1.  Na consola do Gestor de Configuração vai para os**Termos e Condições**de**Overview** > **Conformidade** > de **Segurança e** > Conformidade, e depois seleciona os termos e condições que pretende ver.  

2.  Na parte inferior da consola, selecione o separador **De implantação,** selecione a implementação e, em seguida, clique no **'Ver'.**  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a>Melhorias nas definições da política de proteção de pontos finais  
Na Pré-visualização Técnica de 1512 adicionámos as seguintes novas definições na política antimalware Endpoint Protection:  

-   Proteção em tempo real: **Bloqueie aplicações potencialmente indesejadas no download e antes da instalação**  

    -   PUA (Potential Unwanted Applications) é uma classificação de ameaça baseada em reputação e identificação orientada por pesquisa. Normalmente, trata-se de bundlers de aplicações indesejadas ou das respetivas aplicações agregadas.  

    -   A definição da política de proteção está ativada (definida para "Sim") por defeito. Quando ativada, esta definição bloqueia PUA no momento da transferência e da instalação. No entanto, pode excluir ficheiros ou pastas específicos para atender às necessidades específicas do seu ambiente.  

-   Configurações de digitalização: **Scan mapeado unidades de rede ao executar uma varredura completa**  

    -   Esta definição proporciona uma maior granularidade para o administrador permitir verificações a pedido de ficheiros de rede sem o risco de digitalizar sempre as unidades de rede mapeadas durante uma varredura completa programada.  

    -   A definição de ficheiros da **rede Scan** deve primeiro ser ativada ("sim") para que esta definição esteja disponível para configurar.  

    -   Por predefinição, esta definição é "Não" o que significa que uma varredura completa não acede a unidades de rede mapeadas.  

-   Definições de submissão de ficheiros de amostras automáticas:  

     O motor antimalware pode solicitar que as amostras de ficheiros sejam enviadas para a Microsoft para análise sueste. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: Ativar a submissão de ficheiros de **amostras automáticas para ajudar a Microsoft a determinar se certos itens detetados são maliciosos:** Mude esta definição para "Sim" para permitir a submissão do ficheiro de amostras automáticas. Por predefinição, esta definição é "Não" o que significa que a submissão de ficheiros de amostras automáticas está desativada e os utilizadores serão solicitados antes de enviarem amostras.   (Esta configuração foi introduzida pela primeira vez no System Center 2012 R2 Configuration Manager SP1)  

    -   Avançado: **Permitir que os utilizadores modifiquem as definições de submissão de ficheiros de amostras automáticas**: Esta definição determina se um utilizador com direitos administrativos locais num dispositivo pode alterar a definição de submissão de ficheiros de amostras automáticas na interface do cliente. Por predefinição, esta definição é "Não" o que significa que as definições só podem ser alteradas a partir da consola do Gestor de Configuração, e os administradores locais de um dispositivo não podem alterar esta configuração.  

         Por exemplo, o seguinte mostra a definição do Windows Defender no Windows 10 definida pelo administrador conforme ativado, e o utilizador não está autorizado a modificá-lo:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Além disso, a definição de **ficheiros e pastas existentes** exclui na secção "Definições de Exclusão" da política antimalware de proteção de pontofinal é melhorada para permitir exclusões de dispositivos. Por exemplo, agora pode especificar o seguinte como exclusão: **\device\mvfs** (em Sistema de Ficheiros com Múltiplas Versões). A política não valida o caminho do dispositivo; a política de proteção do ponto final é fornecida ao motor antimalware no cliente, que deve ser capaz de interpretar a cadeia do dispositivo.  

**Pré-requisitos para a utilização de políticas de proteção de pontos finais:**  

Antes de poder utilizar as políticas de Proteção endpoint, tem de instalar e gerir o cliente Endpoint Protection utilizando as definições do cliente endpoint Protection. Isto é feito utilizando o cliente de Proteção de Pontofinal do System Center para windows 7, Windows 8, Windows 8.1 ou gerido O Windows Defender para o Windows 10. Ver [Proteção do Ponto Final](../../protect/deploy-use/endpoint-protection.md).  
