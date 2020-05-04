---
title: Cogestão de cargas de trabalho
titleSuffix: Configuration Manager
description: Saiba como mudar as cargas de trabalho atualmente geridas pelo Gestor de Configuração para o Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 4874d12149f213351740c9e5b300bf04fc536571
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711365"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Como mudar as cargas de trabalho do Gestor de Configuração para Intune

Um dos benefícios da cogestão é mudar as cargas de trabalho do Diretor de Configuração para o Microsoft Intune. Quando um dispositivo Windows 10 tem o cliente do Gestor de Configuração e está matriculado no Intune, obtém-se os benefícios de ambos os serviços. Controla quais as cargas de trabalho, se houver, muda a autoridade do Gestor de Configuração para Intune. O Gestor de Configuração continua a gerir todas as outras cargas de trabalho, incluindo as cargas de trabalho que não muda para Intune, e todas as outras funcionalidades do Gestor de Configuração que a cogestão não suporta.

Se mudar uma carga de trabalho para Intune, mas depois mudar de ideia, pode trocá-la de volta para 'Gestor de Configuração'.

Para obter mais informações sobre as cargas de trabalho suportadas, consulte [cargas de trabalho](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Switch cargas de trabalho a partir da versão 1906
<!--3555750 FKA 1357954 -->
A partir da versão 1906, pode configurar diferentes coleções-piloto para cada uma das cargas de trabalho de cogestão. Poder utilizar diferentes coleções piloto permite-lhe ter uma abordagem mais granular ao deslocar cargas de trabalho. Pode trocar cargas de trabalho quando ativa a cogestão, ou mais tarde, quando estiver pronto. Se ainda não permitiu a cogestão, faça-o primeiro. Para mais informações, consulte [Como permitir a cogestão.](how-to-enable.md) Depois de ativar a cogestão, modifique as definições nas propriedades de cogestão.

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.**  
2. Selecione o objeto de cogestão e, em seguida, escolha **propriedades** na fita.  
3. Mude para o separador **Workloads.** Por predefinição, todas as cargas de trabalho estão definidas para a definição do Gestor de **Configuração.** Para mudar uma carga de trabalho, desloque o controlo do slider para a carga de trabalho para a definição desejada.  

    ![Screenshot do separador Workloads na página de propriedades de cogestão](media/3555750-co-management-workloads-tab.png)

    - **Gestor de Configuração**: O Gestor de Configuração continua a gerir esta carga de trabalho.  

    - **Insagamento piloto**: Comute esta carga de trabalho apenas para os dispositivos da recolha de pilotos. Pode alterar as **coleções Pilot** no separador **Encenação** da página de propriedades de cogestão.  

    - **Insintonize:** Alterne esta carga de trabalho para todos os dispositivos do Windows 10 inscritos em cogestão.  

4. Vá ao separador **Staging** e altere a **coleção Pilot** para qualquer uma das cargas de trabalho, se necessário.
  
   ![Screenshot do separador Workloads na página de propriedades de cogestão](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Antes de trocar as cargas de trabalho, certifique-se de configurar corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre geridas por uma das ferramentas de gestão dos seus dispositivos.
> - A partir da versão 1806 do Gestor de Configuração, quando muda uma carga de trabalho de cogestão, os dispositivos cogeridos sincronizam automaticamente a política de MDM da Microsoft Intune. Esta sincronização também acontece quando inicia a ação de Política de Computador de **Descarregamento** a partir de notificações de clientes na consola 'Gestor de Configuração'. Para mais informações, consulte Iniciar a recuperação da [política do cliente através da notificação do cliente](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Switch cargas de trabalho na versão 1902 e anterior

Pode trocar cargas de trabalho quando ativa a cogestão, ou mais tarde, quando estiver pronto. Se ainda não permitiu a cogestão, faça-o primeiro. Para mais informações, consulte [Como permitir a cogestão.](how-to-enable.md) Depois de ativar a cogestão, modifique as definições nas propriedades de cogestão.

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.**  

2. Selecione o objeto de cogestão e, em seguida, escolha **propriedades** na fita.
   - Será solicitado a assinar em Azure AD. O pedido não o impede de atualizar o seu embarque. No entanto, será solicitado cada vez que abrir a página **Propriedades** até iniciar o seu início.

3. Mude para o separador **Workloads.** Por predefinição, todas as cargas de trabalho estão definidas para a definição do Gestor de **Configuração.** Para mudar uma carga de trabalho, desloque o controlo do slider para a carga de trabalho para a definição desejada.  

    ![Screenshot do separador Workloads na página de propriedades de cogestão](media/properties-workloads.png)

    - **Gestor de Configuração**: O Gestor de Configuração continua a gerir esta carga de trabalho.  

    - **Insagamento piloto**: Comute esta carga de trabalho apenas para os dispositivos da recolha de pilotos. Pode alterar a **coleção Pilot** no separador **Encenação** da página de propriedades de cogestão.  

    - **Insintonize:** Alterne esta carga de trabalho para todos os dispositivos do Windows 10 inscritos em cogestão.  

4. No separador **Staging** da página de propriedades de cogestão, altere a **coleção Pilot** para as suas cargas de trabalho, se necessário.

5. Clique em **OK** para guardar e sair propriedades de cogestão.

> [!Important]  
> - Antes de trocar as cargas de trabalho, certifique-se de configurar corretamente e implementar a carga de trabalho correspondente no Intune. Certifique-se de que as cargas de trabalho são sempre geridas por uma das ferramentas de gestão dos seus dispositivos. 
> - A partir da versão 1806 do Gestor de Configuração, quando muda uma carga de trabalho de cogestão, os dispositivos cogeridos sincronizam automaticamente a política de MDM da Microsoft Intune. Esta sincronização também acontece quando inicia a ação de Política de Computador de **Descarregamento** a partir de notificações de clientes na consola 'Gestor de Configuração'. Para mais informações, consulte Iniciar a recuperação da [política do cliente através da notificação do cliente](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Passos seguintes

[Monitorizar a cogestão](how-to-monitor.md)
