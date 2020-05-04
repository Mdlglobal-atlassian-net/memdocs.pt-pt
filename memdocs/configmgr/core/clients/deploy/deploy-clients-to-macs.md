---
title: Implementar clientes Mac
titleSuffix: Configuration Manager
description: Aprenda a implementar clientes em computadores Mac no Gestor de Configuração.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713444"
---
# <a name="how-to-deploy-clients-to-macs"></a>Como implementar clientes em Macs

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve como implementar e manter o cliente do Gestor de Configuração em computadores Mac. Para saber o que tem de configurar antes de implementar clientes para computadores Mac, consulte [prepare-se para implementar software de cliente para Macs](prepare-to-deploy-mac-clients.md).

Quando instalar um novo cliente para computadores Mac, poderá também ter de instalar atualizações do 'Gestor de Configuração' para refletir as novas informações do cliente na consola do Gestor de Configuração.

Nestes procedimentos, tem duas opções para instalar certificados de cliente. Leia mais sobre os certificados de cliente para Macs in [Prepare para implementar software de cliente para Macs](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Utilize a inscrição do Gestor de Configuração utilizando a [ferramenta CMEnroll](#bkmk_enroll). O processo de inscrição não suporta a renovação automática do certificado. Reinscreva o computador Mac antes de expirar o certificado instalado.    

- [Utilize um método de pedido e instalação de certificado independente do Gestor de Configuração](#bkmk_external).  

> [!IMPORTANT]  
> Para implantar o cliente em dispositivos que executam o macOS Sierra, configure corretamente o **nome do assunto** do certificado de ponto de gestão. Por exemplo, utilize o FQDN do servidor de pontos de gestão.



## <a name="configure-client-settings"></a>Configurar definições do cliente  

Utilize as [definições padrão](about-client-settings.md) do cliente para configurar a inscrição para computadores Mac. Não pode usar as definições personalizadas do cliente. Para solicitar e instalar o certificado, o cliente do Gestor de Configuração para o Mac requer as definições padrão do cliente.  

1. Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Selecione o nó de **Definições** do Cliente e, em seguida, selecione **As Definições padrão do cliente**.  

2. No separador **Casa** da fita, no grupo **Propriedades,** escolha **Propriedades**.  

3. Selecione a secção **de Inscrição** e, em seguida, configure as seguintes definições:  

    1. **Permitir que os utilizadores matriculem dispositivos móveis e computadores Mac**: **Sim**  

    2. **Perfil de inscrição:** Escolha o **perfil de conjunto**.  

4. Na caixa de diálogo de perfil de inscrição de **dispositivomóvel,** escolha **Criar**.  

5. Na caixa de diálogo **Create Registration Profile,** introduza um nome para este perfil de inscrição. Em seguida, configurar o código do **site de gestão**. Selecione o site primário do Gestor de Configuração que contenha os pontos de gestão destes computadores Mac.  

    > [!NOTE]  
    >  Se não conseguir selecionar o site, certifique-se de configurar pelo menos um ponto de gestão no site para suportar dispositivos móveis.  

6. Escolha **Adicionar**.  

7. Na janela **Add Certification Authority for Mobile Devices,** selecione o servidor da autoridade de certificação que emite certificados para computadores Mac.  

8. Na caixa de diálogo **Create Registration Profile,** selecione o modelo de certificado de computador Mac que criou anteriormente.  

9. Selecione **OK** para fechar a caixa de diálogo do **Perfil de Inscrição** e, em seguida, a caixa de diálogo predefinida de **definições do cliente.**  

    > [!TIP]  
    > Se quiser alterar o intervalo da política do cliente, utilize o intervalo de **sondagem da política do Cliente** no grupo de definição de **cliente.**  

Da próxima vez que os dispositivos descarregarem a política do cliente, o Gestor de Configuração aplica estas definições para todos os utilizadores. Para iniciar a recuperação de políticas para um único cliente, consulte [Iniciar a recuperação de políticas para um cliente de Gestor de Configuração](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Além das definições do cliente de inscrição, certifique-se de que configuraas as seguintes definições do dispositivo do cliente:  

- **Inventário de hardware**: Ative e configure esta funcionalidade se quiser recolher o inventário de hardware dos computadores clientes mac e Windows. Para mais informações, consulte [Como alargar o inventário de hardware](../manage/inventory/extend-hardware-inventory.md).  

- **Definições de conformidade**: Ative e configure esta funcionalidade se pretender avaliar e remediar as definições nos computadores clientes Mac e Windows. Para mais informações, consulte [plan para e configure as definições](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)de conformidade .  

Para mais informações, consulte [Como configurar as definições do cliente](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a>Descarregue o cliente para macOS

1. Descarregue o pacote de ficheiros do cliente macOS, [Microsoft Endpoint Configuration Manager - macOS Client (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850). Guarde **a ConfigmgrMacClient.msi** para um computador que executa o Windows. Este ficheiro não está no meio de instalação do Gestor de Configuração.  

2. Executar o instalador no computador Windows. Extraia o pacote de cliente Mac, **Macclient.dmg,** para uma pasta no disco local. O caminho `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`padrão é .  

3. Copie o ficheiro **Macclient.dmg** para uma pasta no computador Mac.  

4. No computador Mac, execute **o Macclient.dmg** para extrair os ficheiros para uma pasta no disco local.  

5. Na pasta, certifique-se de que contém os seguintes ficheiros: 

    - **Ccmsetup**: Instala o cliente do Gestor de Configuração nos seus computadores Mac utilizando **CMClient.pkg**  

    - **CMDiagnostics**: Recolhe informações de diagnóstico relacionadas com o cliente do Gestor de Configuração nos seus computadores Mac  

    - **CMUninstall**: Desinstala o cliente dos seus computadores Mac  

    - **CMAppUtil**: Converte os pacotes de aplicações da Apple num formato que pode implementar como aplicação de Gestor de Configuração  

    - **CMEnroll**: Solicita e instala o certificado de cliente para um computador Mac para que possa instalar o cliente Do Gestor de Configuração  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a>Inscreva o cliente Mac  

Inscreva clientes individuais com o assistente de [inscrição](#enroll-the-client-with-the-mac-computer-enrollment-wizard)do computador Mac .

Para automatizar a inscrição para muitos clientes, utilize a [ferramenta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscreva o cliente com o assistente de inscrição do computador Mac  

1. Depois de instalar o cliente, o assistente de inscrição de computador abre. Para iniciar manualmente o assistente, selecione **Inscrever-se** na página de preferência do Gestor de **Configuração.**  

2. Na segunda página do assistente, forneça as seguintes informações:  

   - **Nome do utilizador**: O nome do utilizador pode estar nos seguintes formatos:  

     - `domain\name`. Por exemplo: `contoso\mnorth`  

     - `user@domain`. Por exemplo: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Quando utiliza um endereço de e-mail para preencher o campo de nome do **Utilizador,** o Gestor de Configuração povoa automaticamente o campo de nome do **Servidor.** Utiliza o nome padrão do servidor de ponto de procuração de inscrição e o nome de domínio do endereço de e-mail. Se estes nomes não corresponderem ao nome do servidor de ponto de procuração de inscrição, corrija o **nome do Servidor** durante a inscrição.  

       O nome do utilizador e a palavra-passe correspondente devem corresponder a uma conta de utilizador do Diretório Ativo que tenha permissões **de Leitura** e **Inscrição** no modelo de certificado de cliente Mac.  

   - **Nome**do servidor : O nome do servidor de ponto de procuração de inscrição.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automação de cliente e certificado com CMEnroll  

Utilize este procedimento para automatização da instalação do cliente e solicitação e inscrição de certificados de cliente com a ferramenta CMEnroll. Para executar a ferramenta, deve ter uma conta de utilizador do Diretório Ativo.

1. No computador Mac, navegue para a pasta onde extraiu o conteúdo do ficheiro **Macclient.dmg.**  

2. Insira o seguinte comando:`sudo ./ccmsetup`  

3. Aguarde até ver a mensagem **Instalação concluída** . Embora o instalador apresente uma mensagem que deve reiniciar agora, não reinicie e continue até ao próximo passo.  

4. A partir da pasta **Ferramentas** no computador Mac, escreva o seguinte comando:`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Após a instalação do cliente, o Assistente para Inscrever um Computador Mac abre para ajudá-lo a inscrever o computador Mac. Para mais informações, consulte Inscrever o cliente utilizando o assistente de [inscrição](#bkmk_enroll)do computador Mac .  

     Exemplo: Se o servidor de ponto de procuração de inscrição for nomeado **server02.contoso.com**, e conceder permissões **contoso\mnorth** para o modelo de certificado de cliente Mac, escreva o seguinte comando:`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Se o nome do utilizador incluir algum dos `<>"+=,`seguintes caracteres, a inscrição falha: . Utilize um certificado fora de banda com um nome de utilizador que não inclua estes caracteres.  
    >  
    > Para uma experiência de utilizador mais perfeita, guie os passos de instalação. Em seguida, os utilizadores apenas têm de fornecer o seu nome de utilizador e senha.  

5. Digite a palavra-passe para a conta de utilizador do Diretório Ativo. Quando introduz este comando, pede duas palavras-passe. A primeira palavra-passe é para a conta do super utilizador executar o comando. O segundo pedido refere-se à conta de utilizador do Active Directory. Os pedidos parecem idênticos, por isso certifique-se de que os especifica pela sequência correta.  

6. Aguarde até ver a mensagem **Inscrito com êxito** .  

7. Para limitar o certificado inscrito ao Gestor de Configuração, no computador Mac, abra uma janela de terminal e efaça as seguintes alterações:  

    1. Insira o comando`sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. Na janela de acesso à **porta-chaves,** na secção **Porta-chaves,** escolha **sistema**. Em seguida, na secção **categoria,** escolha **Chaves**.  

    3. Expanda as chaves para ver os certificados do cliente. Encontre o certificado com uma chave privada que instalou e abra a chave.  

    4. No separador Controlo de **Acesso,** escolha Confirmar antes de **permitir o acesso**.  

    5. Navegue para **/Biblioteca/Suporte de Aplicação/Microsoft/CCM,** selecione **CCMClient**, e depois escolha **Adicionar**.  

    6. Escolha **Guardar Alterações** e feche a caixa de diálogo de acesso à **corrente de chave.**  

8. Reinicie o computador Mac.  

Para verificar se a instalação do cliente é bem sucedida, abra o item do Gestor de **Configuração** nas **Preferências** do Sistema no computador Mac. Atualização e visualiza a coleção **All Systems** na consola 'Gestor de Configuração'. Confirme que o computador Mac aparece nesta coleção como um cliente gerido.  

> [!TIP]  
> Para ajudar a resolver problemas com o cliente Mac, utilize a ferramenta **CMDiagnostics** incluída no pacote de cliente Mac. Utilize-o para recolher as seguintes informações de diagnóstico:  
>   
> - Uma lista dos processos em execução  
> - A versão do sistema operativo Mac OS X  
> - Relatórios de crash mac OS X relativos ao cliente do Gestor de Configuração, incluindo **CCM\*.crash** e **System Preference.crash**.  
> - O ficheiro De Conta de Materiais (BOM) e a lista de propriedades (.plist) criado pela instalação do cliente do Gestor de Configuração.  
> - O conteúdo da pasta **/Biblioteca/Suporte de Aplicação/Microsoft/CCM/Registos**.  
>   
> A informação recolhida pela CmDiagnostics é adicionada a um ficheiro zip que é guardado para o ambiente de trabalho do computador e é nomeado`cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a>Gerir certificados externos ao Gestor de Configuração

Pode utilizar um método de pedido de certificado e de instalação independente do Gestor de Configuração. Utilize o mesmo processo geral, mas inclua os seguintes passos adicionais: 

- Quando instalar o cliente do Gestor de Configuração, utilize as opções de linha de comando **MP** e **SubjectName.** Introduza o `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`seguinte comando: . O nome do sujeito do certificado é sensível a casos, por isso escreva-o exatamente como aparece nos dados do certificado.  

     Exemplo: A Internet FQDN do ponto de gestão é **server03.contoso.com**. O certificado de cliente Mac tem o FQDN de **mac12.contoso.com** como nome comum no sujeito do certificado. Utilize o seguinte comando:`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Se tiver mais de um certificado que contenha o mesmo valor de assunto, especifique o número de série do certificado a utilizar para o cliente do Gestor de Configuração. Utilize o seguinte comando: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Por exemplo: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Renovar o certificado de cliente Mac  

Este procedimento remove o SMSID. O cliente do Gestor de Configuração do Mac requer um novo ID para usar um certificado novo ou renovado.  

> [!IMPORTANT]  
> Depois de substituir o Cliente SMSID, quando eliminar o antigo recurso na consola Do Gestor de Configuração, também elimina qualquer histórico de cliente armazenado. Por exemplo, histórico de inventário de hardware para aquele cliente.  


1. Crie e povoeça uma coleção de dispositivos para os computadores Mac que devem renovar os certificados de computador.  

2. Na área de trabalho **Ativos e Compatibilidade** , inicie o **Assistente de Criação de Item de Configuração**.  

3. Na página **Geral** do assistente, especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Tipo**: **Mac OS X**  

4. Na página **Plataformas Suportadas,** selecione todas as versões Mac OS X.  

5. Na página **Definições**, selecione **Novo**. Na janela **Criar Definição,** especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Tipo de definição**: **Script**  

    - **Tipo de dados**: **Corda**  

6. Na janela **Criar Definição,** para **o script Discovery,** selecione Adicionar **script**. Esta ação especifica um script para descobrir computadores Mac configurados com um SMSID.  

7. Na janela **Edit Discovery Script,** introduza o seguinte script de concha:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Escolha **OK** para fechar a janela **Edit Discovery Script.**  

9. Na janela **Criar Definição,** para **script de reparação (opcional)** escolha **Adicionar script**. Esta ação especifica um script para remover o SMSID quando é encontrado em computadores Mac.  

10. Na janela **'Criar Remediação Script',** introduza o seguinte script de concha:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Escolha **OK** para fechar a janela **Do Script de Reparação De Criação.**  

12. Na página Regras de **Conformidade,** escolha **New**. Em seguida, na janela **Criar** regra, especifique as seguintes informações:  

    - **Nome**: **Remover SMSID para Mac**  

    - **Definição selecionada**: Escolha **navegar** e, em seguida, selecione o script de descoberta que especificou anteriormente.  

    - No **campo dos seguintes valores:** **O domínio/par predefinido de (com.microsoft.ccmclient, SMSID) não existe**.  

    - Ativar a opção de executar o script de **reparação especificado quando esta definição não for conforme**.  

13. Conclua o assistente.  

14. Crie uma linha de base de configuração que contenha este item de configuração. Desloque a linha de base para a recolha do alvo.  

     Para mais informações, consulte Como criar linhas de [base de configuração](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Depois de instalar um novo certificado em computadores Mac que tenham removido o SMSID, execute o seguinte comando para configurar o cliente para utilizar o novo certificado:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Consulte também

[Preparar a implementação de clientes em Macs](prepare-to-deploy-mac-clients.md)

[Manutenção de clientes de Mac](../manage/maintain-mac-clients.md)
