---
title: Planejamento da implementação de clientes para computadores Mac
titleSuffix: Configuration Manager
description: Plano para implementação de clientes em computadores Mac em Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713227"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Planeamento para implementação de clientes em computadores Mac em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode instalar o cliente Do Gestor de Configuração em computadores Mac que executam o sistema operativo Mac OS X e utilizar as seguintes capacidades de gestão:  

- **Inventário de Hardware**  

   Pode utilizar o inventário de hardware do Gestor de Configuração para recolher informações sobre o hardware e aplicações instaladas em computadores Mac. Estas informações podem então ser vistas no Resource Explorer na consola Do Gestor de Configuração e usadas para criar coleções, consultas e relatórios. Para mais informações, consulte [Como utilizar o Resource Explorer para visualizar](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)o inventário de hardware .  

   O Gestor de Configuração recolhe as seguintes informações de hardware dos computadores Mac:  

  -   Processador  

  -   Sistema de Computador  

  -   Unidade de Disco  

  -   Partição de Discos  

  -   Adaptador de rede  

  -   Sistema Operativo  

  -   Serviço  

  -   Processo  

  -   Software instalado  

  -   Produto do sistema informático  

  -   Controlador USB  

  -   Dispositivo USB  

  -   Unidade CDROM  

  -   Controlador de vídeo  

  -   Monitor de ambiente de trabalho  

  -   Bateria portátil  

  -   Memória Física  

  -   Impressora  

  > [!IMPORTANT]  
  >  Não é possível alargar as informações de hardware recolhidas dos computadores Mac durante o inventário de hardware.  

- **Definições de conformidade**  

   Pode utilizar as definições de conformidade do Gestor de Configuração para visualizar a conformidade das definições de preferência do Mac OS X (.plist). Por exemplo, pode impor configurações para a página inicial no navegador Safari ou garantir que a firewall da Apple está ativada. Também pode utilizar scripts de concha para monitorizar e remediar as definições no MAC OS X.  

- **Gestão de aplicações**  

   O Gestor de Configuração pode implementar software para computadores Mac. Pode implementar os seguintes formatos de software para computadores Mac:  

  -   Imagem do disco da Apple (. DMG)  

  -   Ficheiro meta pacote (. MPKG)  

  -   Pacote instalador Mac OS X (. PKG)  

  -   Aplicação Mac OS X (. APP)  

  Quando instala o cliente Do Gestor de Configuração em computadores Mac, não pode utilizar as seguintes capacidades de gestão que são suportadas pelo cliente do Gestor de Configuração em computadores baseados no Windows:  

- Instalação push do cliente  

- Implementação do sistema operativo  

- Atualizações de software  

  > [!NOTE]  
  >  Pode utilizar a gestão de aplicações do Gestor de Configuração para implementar atualizações de software Mac OS X necessárias para computadores Mac. Além disso, pode utilizar as definições de conformidade para se certificar de que os computadores têm as atualizações de software necessárias.  

- Janelas de manutenção  

- Controlo remoto  

- Gestão de energia  

- Verificação de cliente do estado do cliente e remediação  

  Para obter mais informações sobre como instalar e configurar o cliente Do Gestor de Configuração Mac, consulte [como implementar clientes para Macs](../../../../core/clients/deploy/deploy-clients-to-macs.md).
