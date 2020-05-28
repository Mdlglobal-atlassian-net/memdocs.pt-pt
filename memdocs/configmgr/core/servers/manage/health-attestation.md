---
title: Atestado de estado de funcionamento
titleSuffix: Configuration Manager
description: Conheça a funcionalidade de Attestation de Saúde do Dispositivo visível na consola Do Gestor de Configuração.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ed155fb61491a273732ed3b974b6ddb5ac29bc89
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904004"
---
# <a name="health-attestation-for-configuration-manager"></a>Atestação de saúde para gerente de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os administradores podem ver o estado do [Atestado de Estado de Funcionamento do Dispositivo Windows 10](https://docs.microsoft.com/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) na consola do Configuration Manager.  O atestado de estado de funcionamento permite ao administrador garantir que os computadores cliente têm as seguintes configurações fidedignas de BIOS, TPM e software de arranque ativadas:  

-   Antimalware de início antecipado - O antimalware de início antecipado (ELAM) protege o computador durante o arranque e antes da inicialização de controladores de terceiros. [Como ativar ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - A Encriptação de Unidade BitLocker do Windows é um software que encripta todos os dados armazenados no volume do sistema operativo do Windows.  [Como ligar o BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Arranque seguro - O arranque seguro é uma norma de segurança desenvolvida por membros do setor de PC para o ajudar a certificar-se de que o computador arranca utilizando apenas o software que seja considerada fidedigno pelo fabricante do PC. [Saiba mais sobre o Arranque Seguro](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Integridade do código - A integridade do código é uma funcionalidade que melhora a segurança do sistema operativo ao validar a integridade de um controlador ou ficheiro de sistema sempre que é carregado na memória. [Saiba mais sobre Integridade do Código](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Esta funcionalidade está disponível para PCs e recursos no local geridos pelo Configuration Manager e para dispositivos móveis geridos com o Microsoft Intune. Os administradores podem especificar se a comunicação é efetuada através da nuvem ou de infraestruturas no local. A monitorização de atestados de saúde do dispositivo no local permite ao administrador monitorizar os Computadores dos Clientes sem acesso à Internet.

## <a name="enable-health-attestation"></a>Ativar atestado de saúde

 **Requisitos:**  

-   Dispositivos clientes que executam a versão 1607 do Windows 1607 ou do Windows Server 2016 com [attestation](https://docs.microsoft.com/windows-server/security/device-health-attestation)de saúde do dispositivo ativado .
-   Dispositivos ativados TPM 1.2 ou TPM 2.
-   Ao utilizar a gestão da nuvem, a comunicação entre o agente cliente do Gestor de Configuração e o ponto de gestão com *has.spserv.microsoft.com* (porta 443) Serviço de Attestation de Saúde (gestão da nuvem). Quando estiver no local, o cliente deve poder comunicar com o ponto de gestão habilitado para a saúde do dispositivo.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento em computadores cliente do Configuration Manager

Utilize este procedimento para permitir a monitorização da atesta ção de atestados de dispositivos que se ligam à internet.

1.  Na consola De Configuração Manager, escolha definições de cliente de visão geral da **administração**  >  **Overview**  >  **Client Settings**.  Selecione o separador das definições **Agente do Computador** .  
2.  Na caixa de diálogo **Predefinições** , selecione **Agente do Computador** e, em seguida, desloque para baixo para **Ativar comunicação com o Health Attestation Service**  
3.  Defina **Ativar comunicação com o Serviço de Atestado de Estado de Funcionamento** para **Sim**e, em seguida, clique em **OK**.  
4. Direcionem as coleções de dispositivos que devem reportar a saúde do dispositivo.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Como ativar a comunicação do serviço de Atestado do Estado de Funcionamento no local em computadores cliente do Configuration Manager
Utilize este procedimento para permitir a monitorização da atesta de saúde do dispositivo para dispositivos no local que não se ligam à internet.

A partir do Configurmanager 1702, o URL do serviço de atestado de saúde do dispositivo no local pode ser configurado no ponto de gestão para apoiar dispositivos clientes sem acesso à Internet.

1. Na consola de Configuração Manager, navegue em sites de configuração de site de visão **Administration**  >  **geral**da  >  **Site Configuration**  >  **Sites**administração.
2. Clique no site primário ou secundário com o ponto de gestão que suporta clientes de atesta de saúde de dispositivos no local e **selecione Configure site components**  >  **Management Point**. A página **Management Point Component Properties** abre.
3. No separador **Opções Avançadas,** selecione **Adicionar** e especificar um URL de serviço de atestado de atestado de dispositivo válido no local. Pode adicionar vários URLs. Se forem especificados vários URLs no local, os clientes recebem o conjunto completo e escolhem aleatoriamente quais usar.
4.  Na consola De Configuração Manager, escolha definições de cliente de visão geral da **administração**  >  **Overview**  >  **Client Settings**.  Selecione o separador das definições **Agente do Computador** .  
5.  Percorra para baixo para ativar a comunicação com o Serviço de **Atestação de Saúde,** e definido para **Sim**.
7.  Clique na opção **Use on-premises Health Attestaion Service** e reserve para **Sim**.
8. Direcionem as coleções de dispositivos que devem reportar a saúde do dispositivo com as definições do agente cliente para permitir o reporte de atestado de saúde do dispositivo.

Também pode **editar** ou **remover** URLs do serviço de atestado de saúde do dispositivo.

> [!NOTE]
> Se usou o atestado de saúde do dispositivo antes da atualização para o Diretor de Configuração 1702, os URLs no local especificados nas definições do agente cliente são pré-povoados nas propriedades do ponto de gestão durante a atualização. Os clientes no local continuarão a utilizar o URL especificado nas definições do agente cliente até serem atualizados. Em seguida, passarão para um dos URLs especificados no ponto de gestão.

## <a name="monitor-device-health-attestation"></a>Atestado de saúde do dispositivo de monitorização

1.  Para visualizar a vista do atestado de estado de funcionamento, na consola do Configuration Manager, vá para a área de trabalho de **Monitorização** , clique no nó **Segurança** e, em seguida, clique em **Atestado de Estado de Funcionamento**.  
2.  O Atestado de Estado de Funcionamento é apresentado.  

O Atestado de Estado de Funcionamento do Dispositivo apresenta o seguinte:  

-   **Atestado do Estado de Funcionamento** - Mostra a partilha de dispositivos com os estados de conformidade, não conformidade, erro e desconhecidos  
-   **Atestado de Estado de Funcionamento de Relatórios de Dispositivos** - Mostra a percentagem de dispositivos que comunicam o estado de Atestado de Estado de Funcionamento  
-   **Dispositivos Não Conformes por Tipo de Cliente** - Mostra a partilha de dispositivos móveis e computadores não compatíveis  
-   **Definições Principais do Atestado de Estado de Funcionamento em Falta** - Mostra o número de dispositivos em falta na definição de atestado de estado de funcionamento, listados por definição
