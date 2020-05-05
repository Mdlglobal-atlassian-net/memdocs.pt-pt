---
title: Cenários de instalação
titleSuffix: Configuration Manager
description: Aprenda técnicas para instalar uma nova hierarquia do Gestor de Configuração quando estiver a atualizar ou atualizar um site.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718099"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Cenários para agilizar a sua instalação de Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o lançamento de versões de atualização para o current branch do Configuration Manager, existem novos cenários para agilizar a instalação de uma nova hierarquia para uma versão de atualização (como atualização 1610), e para atualizar a partir do Microsoft System Center 2012 Configuration Manager.

Os cenários suportados incluem:  

**Instale uma nova hierarquia** de ramificação do Gestor de Configuração que execute uma versão de atualização.  

-   Instale apenas o site de topo e, em seguida, instale imediatamente uma atualização para trazer essa corrente do site com a versão de atualização que utilizará. Em seguida, pode instalar sites adicionais diretamente nessa versão de atualização.  
-   Neste cenário, ignora o processo de instalação de sites adicionais para um nível de base e, em seguida, atualiza-os para a versão de atualização que pretende utilizar.  
-   Neste cenário, ignora o processo de instalação de clientes para uma versão de base e, em seguida, reinstale-os quando atualiza para uma versão posterior.  

Atualize uma infraestrutura do **Microsoft System Center 2012** Para uma versão atualizada do Gestor de Configuração.  

-   Atualize manualmente o seu site de administração central e cada site primário para uma versão de base (como a versão 1606) antes de instalar uma versão de atualização (como a versão 1610).  
-   Não atualize os sites secundários do Microsoft System Center 2012 Configuration Manager até que os seus principais sites executem a versão de atualização que utilizará.  
-   Não atualize os clientes do Microsoft System Center 2012 Configuration Manager até que os seus principais sites executem a versão de atualização que utilizará.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Cenário: Instale uma nova hierarquia numa versão de atualização  
Neste cenário de exemplo, instale o primeiro site de uma hierarquia utilizando uma versão de base do Gestor de Configuração, como a versão 1610. Em seguida, instale a atualização 1610 antes de implementar sites ou clientes adicionais.  

-   Como planeia utilizar uma versão de atualização (como a versão 1610) e não permanecer numa versão de base (como a versão 1606), não precisa de instalar sites adicionais e depois atualizá-los. Isto também se aplica aos clientes.  
-   Não instale sites secundários com a versão 1606 e, em seguida, atualize-os para a versão 1610. Em vez disso, instale sites secundários depois de os seus sites primários executarem a versão 1610.  

Siga esta sequência:  

1. **Instale um site de alto nível para a sua nova hierarquia** utilizando os meios de base.  

   -   Só pode utilizar os meios de base para instalar o primeiro local de uma nova hierarquia.  
   -   Por exemplo, instale um site de alto nível utilizando a versão de base de 1606. Para mais informações, consulte [Utilize o Assistente de Configuração para instalar sites](use-the-setup-wizard-to-install-sites.md).  

   Após este passo, o seu site de alto nível executa a versão 1606.  

2. **Utilize atualizações na consola para atualizar o seu site de nível superior para uma versão posterior.**  

   -   Antes de instalar quaisquer sites ou clientes infantis, atualize o seu site de alto nível para a versão de atualização que pretende utilizar.  
   -   Por exemplo, pode atualizar o seu site de alto nível que executa a versão 1606 para a versão 1610. Para mais informações, consulte [Atualizações para Gestor de Configuração](../../../../core/servers/manage/updates.md).  

   Após este passo, o seu site de alto nível executa a versão 1610.  

3. **Instale os novos sites primários subordinados abaixo de um site de administração central.**  

   - Utilize o suporte de dados de instalação a partir da pasta CD.Latest no servidor do site de administração central para instalar sites primários subordinados. Para mais informações, consulte [o CD. Última pasta para Gestor de Configuração](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Este suporte de dados de origem é necessário para assegurar que os novos sites primários subordinados correspondem à versão do site de administração central.  

   Após este passo, os seus novos sites primários para crianças executam a versão 1610.  

4. **Em cada local primário, utilize a opção na consola para instalar novos sites secundários.**  

   -   Como não instalou sites secundários enquanto os sites primários estavam na versão 1606, não precisa de atualizar sites secundários.  
   -   Em vez disso, instale novos sites secundários que executem a versão 1610. Para obter mais informações, veja [Instalar um site secundário](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) no tópico [Utilizar o Assistente de Configuração para instalar sites](use-the-setup-wizard-to-install-sites.md) .  

   Após este passo, novos sites secundários são instalados e executados versão 1610.  

5. **Instale novos clientes no local principal.**  

   -   Como não instalou clientes enquanto os sites primários estavam na versão 1606, não precisa de atualizar os clientes da versão 1606 para a versão 1610.  
   -   Em vez disso, instale novos clientes que executem a versão 1610. Para mais informações, consulte [Os clientes da Deploy](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Após este passo, são instalados novos clientes que executam a versão 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Cenário: Upgrade System Center 2012 Configuration Manager para uma versão atualizada do Gestor de Configuração, ramo atual  

Neste cenário de exemplo, atualize a sua infraestrutura de Gestor de Configuração do System Center 2012 para uma versão atualizada do ramo atual do Gestor de Configuração, como a versão 1610.  

-   O site da administração central e cada site primário devem atualizar para a versão base 1606 antes de instalar a atualização para a versão 1610.  
-   Sites secundários e clientes não atualizam ou instalam a versão 1606. Em vez disso, passam diretamente do System Center 2012 Configuration Manager para a versão atual do Diretor de Configuração 1610.  

Siga esta sequência:  

1. Atualize o site do Gestor de Configuração do System **Center 2012** de nível superior para uma versão de base do ramo atual, utilizando meios de origem para O Gestor de Configuração (como versão 1606). Para mais informações, consulte Upgrade para 'Gestor de [Configuração'.](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)  

   -   Tal como os cenários tradicionais de upgrade, você sempre atualiza o local de alto nível de uma hierarquia primeiro, e depois atualiza sites infantis.  

   Após este passo, o seu site de alto nível executa a versão 1606.  

2. **Atualize cada site primário subordinado na hierarquia** para essa mesma versão de linha de base.  

   -   Ao atualizar a partir do Microsoft System Center 2012 Configuração Manager, tem de atualizar manualmente cada site primário para uma versão de base do ramo atual.  
   -   Não irá atualizar os locais secundários neste momento.  

   Após este passo, cada site primário executa a versão 1606.  

3. **Delineie janelas de manutenção em locais primários para crianças.** Depois de atualizar todos os seus sites primários para a versão de base, planeie configurar janelas de manutenção para controlar quando esses sites instalarem atualizações de infraestruturas. Para mais informações, consulte [Como utilizar as janelas de manutenção](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (As janelas de manutenção são chamadas *de janelas* de serviço na versão 1606.)  

   -   Um site primário subordinado instala automaticamente as mesmas atualizações que o utilizador instala num site de administração central.  
   -   Os sties secundários não instalam automaticamente novas versões. Deve atualizá-los manualmente a partir da consola.  

   Após este passo, quando instalar atualizações no site de administração central, os sites primários subordinados irão instalar apenas essa atualização quando for permitido pela respetiva janela de manutenção.  

4. **Instale a versão de atualização no seu site de alto nível.** Isto atualiza o seu site de alto nível. Depois de um site da administração central instalar a versão de atualização, cada local primário de cada criança instala automaticamente a atualização a menos que a instalação seja bloqueada por uma janela de manutenção.  

   -   Por exemplo, pode atualizar o seu site de alto nível da versão 1606 para a versão 1610. Para mais informações, consulte [Atualizações para Gestor de Configuração](../../../../core/servers/manage/updates.md).  

   Após este passo, o seu site de administração central e cada site primário executa a versão 1610.  

5. **Atualize os sites secundários.** Depois de um site primário instalar a atualização e executar a versão 1610, utilize a opção na consola para atualizar sites secundários.  

   -   Isto atualiza os sites secundários diretamente do Microsoft System Center 2012 Configuration Manager para a versão de atualização que instalou no site principal.  
   -   Para obter informações sobre a atualização de um site secundário, consulte [os sites de upgrade](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) no tópico de Upgrade para 'Gestor de [Configuração'.](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)  

6. **Atualizar clientes.** Para atualizar os clientes, utilize a informação em [Como atualizar os clientes para computadores Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   Isto atualiza os clientes diretamente do Microsoft System Center 2012 Configuration Manager para a versão de atualização que instalou no site principal.  

   Após este passo, os clientes são atualizados para a versão 1610 sem primeiro atualizar para a versão 1606.
