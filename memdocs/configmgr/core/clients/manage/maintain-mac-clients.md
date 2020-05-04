---
title: Manutenção de clientes de Mac
titleSuffix: Configuration Manager
description: Tarefas de manutenção para clientes Mac do Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710651"
---
# <a name="maintain-mac-clients"></a>Manutenção de clientes de Mac
*Aplica-se a: Gestor de Configuração (ramo atual)*

Aqui estão os procedimentos para desinstalar clientes Mac e para renovar os seus certificados.

##  <a name="uninstalling-the-mac-client"></a>Uninstalling the Mac client  

1.  Num computador Mac, abra uma janela terminal e navegue para a pasta que contém **macclient.dmg**.  

2.  Navegue para a pasta Ferramentas e introduza a seguinte linha de comandos:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  A propriedade **-c** instrui o cliente desinstalar para remover também registos de acidentes de cliente e ficheiros de registo. Recomendamos isto para evitar confusões se posteriormente reinstalar o cliente.  

3.  Se necessário, retire manualmente o certificado de autenticação do cliente que o Gestor de Configuração estava a usar, ou revogue-o. CMUnistall não remove nem revoga este certificado.  

##  <a name="renewing-the-mac-client-certificate"></a>Renovar o certificado do cliente Mac  
 Utilize um dos seguintes métodos para renovar o certificado do cliente Mac:  

-   [Renovar o assistente de certificado](#renew-certificate-wizard)  

-   [Renovar o certificado manualmente](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Renovar o assistente de certificado  

1. Configure os seguintes valores como *cordas* no ficheiro ccmclient.plist que controla quando o Assistente de Certificado renovar abre:  

   - **RenovaçãoPeriod1** - Especifica, em segundos, o primeiro período de renovação em que os utilizadores podem renovar o certificado. O valor predefinido é de 3 888 000 segundos (45 dias). Não configure um valor inferior a 300, uma vez que o período reverterá para o padrão. 

   - **RenovaçãoPeriod2** - Especifica, em segundos, o segundo período de renovação em que os utilizadores podem renovar o certificado. O valor predefinido é de 259.200 segundos (3 dias). Se este valor estiver configurado e for superior ou igual a 300 segundos e for inferior ou igual a **RenovaçãoPeriod1,** o valor será utilizado. Se o **RenewalPeriod1** for superior a 3 dias, será utilizado um valor de 3 dias para o **RenewalPeriod2**.  Se o **RenewalPeriod1** for inferior a 3 dias, o **RenewalPeriod2** é definido para o mesmo valor que o **RenewalPeriod1**.  

   - **RenovaçãoReminderInterval1** - Especifica, em segundos, a frequência com que o Assistente de Certificado renovado será apresentado aos utilizadores durante o primeiro período de renovação. O valor predefinido é de 86.400 segundos (1 dia). Se **RenewalReminderInterval1** for superior a 300 segundos e inferior ao valor configurado em **RenewalPeriod1**, será utilizado o valor configurado. Caso contrário, será utilizado o valor predefinido de 1 dia.  

   - **RenovaçãoReminderInterval2** - Especifica, em segundos, a frequência com que o Assistente de Certificado renovado será apresentado aos utilizadores durante o segundo período de renovação. O valor predefinido é de 28.800 segundos (8 horas). Se o **RenewalReminderInterval2** for superior a 300 segundos, inferior ou igual ao **RenewalReminderInterval1** e inferior ou igual ao **RenewalPeriod2**, será utilizado o valor configurado. Caso contrário, será utilizado um valor de 8 horas.  

     **Exemplo:** Se os valores forem deixados com as predefinições, 45 dias antes de o certificado expirar o assistente será aberto a cada 24 horas.  3 dias antes de o certificado expirar o assistente será aberto a cada 8 horas.  

     **Exemplo:** Utilize a seguinte linha de comandos, ou um script, para definir o primeiro período de renovação como 20 dias.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Quando o Assistente de Certificado renovar abre, os campos de **nome do utilizador** e do **servidor** serão normalmente pré-povoados e o utilizador pode simplesmente introduzir uma palavra-passe para renovar o certificado.  

   > [!NOTE]  
   >  Se o assistente não for aberto, ou se fechar inadvertidamente o assistente, clique em **Renovar** , na página de preferências do **Configuration Manager** para abrir o assistente.  

###  <a name="renew-certificate-manually"></a>Renovar o certificado manualmente  
 Um período de validade comum para um certificado de cliente Mac é de 1 ano. O Gestor de Configuração não renova automaticamente o certificado de utilizador que solicita durante a inscrição, pelo que deve utilizar o seguinte procedimento para renovar manualmente o certificado.  

> [!IMPORTANT]  
>  Se o certificado expirar, terá de desinstalar, reinstalar e voltar a inscrever o cliente Mac.  

 Este procedimento remove o SMSID, necessário para pedir um novo certificado para o mesmo computador Mac. Quando remove e substitui o Cliente SMSID, qualquer histórico de cliente armazenado, como o inventário, é eliminado depois de eliminar o cliente da consola Do Gestor de Configuração.  

1.  Crie e povoeça uma coleção de dispositivos para os computadores Mac que deve renovar os certificados de utilizador.  

    > [!WARNING]  
    >  O Gestor de Configuração não monitoriza o período de validade do certificado que inscreveu para computadores Mac. Deve monitorizá-lo de forma independente do Gestor de Configuração para identificar os computadores Mac para adicionar a esta recolha.  

2.  Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo:Mac OS X**  

4.  Na página Plataformas **Suportadas,** certifique-se de que todas as versões Mac OS X são selecionadas.  

5.  Na página **Definições,** escolha **Nova** e, em seguida, na caixa de diálogo **Criar Definição,** especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Tipo de definição:Script**  

    -   **Tipo de dados:Cadeia**  

6.  Na caixa de diálogo **Create Setting,** para **script Discovery,** escolha **adicionar script** para especificar um script que descubra computadores Mac com um SMSID configurado.  

7.  Na caixa de diálogo **Editar Script de Deteção** , introduza o seguinte Script de Shell:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Escolha **OK** para fechar a caixa de diálogo **Edit Discovery Script.**  

9. Na caixa de diálogo **Create Setting,** para **script de reparação (opcional),** escolha **adicionar script** para especificar um script que remova o SMSID quando este for encontrado nos computadores Mac.  

10. Na caixa de diálogo **Criar Script de Remediação** , introduza o seguinte Script de Shell:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a caixa de diálogo do **Script de Reparação Create.**  

12. Na página **Regras de Compatibilidade** do assistente, clique em **Novo**e, na caixa de diálogo **Criar Regra** , especifique as seguintes informações:  

    -   **Nome:Remove SMSID for Mac**  

    -   **Definição selecionada:** Escolha **o Browse** e, em seguida, selecione o script de descoberta que especificou anteriormente.  

    -   No campo **os seguintes valores** , introduza **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Ative a opção **Executar o script de remediação especificado quando esta definição é incompatível**.  

13. Conclua o Assistente de Criação de Item de Configuração.  

14. Crie uma linha de base de configuração que contenha o item de configuração que acaba de criar e implemente-o na coleção do dispositivo que criou no passo 1.  

     Para obter mais informações sobre como criar e implementar linhas de base de configuração, consulte como criar linhas de [base de configuração](../../../compliance/deploy-use/create-configuration-baselines.md) e como implementar linhas de base de [configuração](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Em computadores Mac cujo SMSID tenha sido removido, execute o seguinte comando para instalar um novo certificado:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Quando solicitado, forneça a palavra-passe da conta de utilizador super para executar o comando e, em seguida, a palavra-passe da conta de utilizador do Active Directory.  

16. Para limitar o certificado inscrito ao Gestor de Configuração, no computador Mac, abra uma janela de terminal e efaça as seguintes alterações:  

    a.  Insira o comando`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`

    b.  No diálogo **keychain Access,** na secção **Keychains,** escolha **Sistema**, e depois, na secção **categoria,** escolha **Teclas**.  

    c.  Expanda as chaves para ver os certificados do cliente. Depois de identificar o certificado com uma chave privada acabada de instalar, faça duplo clique na chave.  

    d.  No separador Controlo de **Acesso,** escolha Confirmar antes de **permitir o acesso**.  

    e.  Navegue para **/Biblioteca/Suporte de Aplicação/Microsoft/CCM,** selecione **CCMClient**, e depois escolha **Adicionar**.  

    f.  Escolha **Guardar Alterações** e feche a caixa de diálogo de acesso à **corrente de chave.**  

17. Reinicie o computador Mac.  

