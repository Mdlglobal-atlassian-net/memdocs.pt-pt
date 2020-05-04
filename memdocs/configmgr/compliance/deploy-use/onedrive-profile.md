---
title: Perfis do OneDrive para Empresas
titleSuffix: Configuration Manager
description: Redirecione as pastas conhecidas do Windows para o OneDrive for Business utilizando um perfil OneDrive para Negócios no Gestor de Configuração.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712240"
---
# <a name="onedrive-for-business-profiles"></a>Perfis do OneDrive para Empresas

A partir da versão 1902 do Gestor de Configuração, pode criar o OneDrive para Perfis de Negócios para mover pastas conhecidas do Windows para o OneDrive for Business. Estas pastas incluem Desktop, Documents e Pictures. Em cada perfil, pode especificar as definições para mover as pastas conhecidas pelo Windows. Para obter mais informações sobre o OneDrive para o Negócio, consulte [Redirecionar e mover as pastas conhecidas do Windows para o OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Pré-requisitos

- [Encontre o seu Escritório 365 ID inquilino](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Implemente a versão do cliente sincronizado OneDrive 18.111.0603.0004 ou posterior. Para mais informações, consulte [implementar aplicações OneDrive utilizando](https://docs.microsoft.com/onedrive/deploy-on-windows)o 'Gestor de Configuração'.  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a>Mover pastas conhecidas do Windows para o OneDrive
<!--3556021-->
Utilize o Gestor de Configuração para mover as pastas conhecidas do Windows para o OneDrive para o Negócios. Estas pastas incluem Desktop, Documents e Pictures. Para simplificar as atualizações do Windows 10, implemente estas definições para os clientes do Windows 7 antes de implementar uma sequência de tarefas. 

1. Na consola De Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione o nó **OneDrive para Perfis de Negócios.**  

   ![Nó oneDrive para perfis de negócio](media/onedrive-for-business-profiles-node.png)
2. Na fita, selecione **Create OneDrive para perfil de negócio**.  

3. Especifique um nome para identificar esta política e selecione **Next**.  

4. Selecione as plataformas que serão aprovisionadas com o perfil OneDrive para Negócios. Quando terminar de selecionar as plataformas, clique em **Next**.

    ![Selecione plataformas para o perfil OneDrive para Negócios](media/onedrive-for-business-profile-select-platforms.png) 

5. Na página **Definições:**

    1. Especifique a sua identificação do inquilino do Escritório 365.  

    2. Selecione uma das seguintes opções para mover as pastas conhecidas para o OneDrive:  

        - **Solicita aos utilizadores que movam as pastas conhecidas**do Windows para o OneDrive : Com esta opção, o utilizador vê um assistente a mover os seus ficheiros. Se optarem por adiar ou recusar mover as suas pastas, o OneDrive recorda-as periodicamente.  

        - **Mover silenciosamente as pastas conhecidas**do Windows para o OneDrive : Quando esta política se aplica ao dispositivo, o cliente OneDrive redireciona automaticamente as pastas conhecidas para o OneDrive for Business.  

            - **Mostre a notificação aos utilizadores depois**de as pastas terem sido redirecionadas : Se ativar esta opção, o cliente OneDrive notifica o utilizador depois de movimentar as suas pastas.  

    3. **Impedir que os utilizadores redirecionem as suas pastas conhecidas**do Windows para o seu PC : Desativa a opção no OneDrive for Business no cliente para que os utilizadores mudem estas pastas para o dispositivo.  

       ![OneDrive para definições de movimento de pasta conhecidas de negócios](media/onedrive-for-business-profile-move-folder-settings.png)

6. Complete o assistente e, em seguida, implemente a apólice.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Implementar o OneDrive para perfil de negócio

1. Na consola De Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione o nó **OneDrive para Perfis de Negócios.**  


2. Selecione o perfil e, em seguida, selecione **Colocar** na fita.

3. Especifique as seguintes definições para a sua implementação:

   1. **Recolha**: Clique em **Navegar...** e, em seguida, selecione a coleção para a qual pretende implementar o perfil.  
   1. **Gerar um alerta:**

      - **Quando o cumprimento é inferior:** Percentagem mínima de conformidade do cliente para manter, caso contrário, um alerta é gerado.
      -  **Data e hora**: A data alerta começar a ser gerada com base na conformidade do perfil.
      - Criar alerta de **Gestor de Operações do Centro**de Sistema : Envie um alerta de conformidade para o Gestor de Operações do Centro de Sistemas.
   1. **Horário:**

      - **Horário simples**: Por padrão, esta definição utiliza um calendário simples para iniciar a avaliação de conformidade de sete em sete dias.
      - **Horário personalizado**: Defina quando executar a avaliação de conformidade. A hora de início baseia-se na hora local do computador que executa a consola Do Gestor de Configuração no momento em que cria a programação ou pode utilizar utc.
 
      ![Implementar o OneDrive para o perfil de negócios](media/onedrive-for-business-deploy-profile.png)

4. Clique em **OK** para implementar o perfil OneDrive para negócios.


## <a name="next-steps"></a>Passos seguintes

[Criar perfis de ligação remota](create-remote-connection-profiles.md)
