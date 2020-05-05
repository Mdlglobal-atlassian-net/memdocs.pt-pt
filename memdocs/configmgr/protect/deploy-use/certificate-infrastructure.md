---
title: Configurar a infraestrutura de certificados
titleSuffix: Configuration Manager
description: Saiba como configurar a inscrição de certificado sintetizar no Gestor de Configuração.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 590c6fd336ec19949b5f5b99b25b3104524a52d6
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210116"
---
# <a name="configure-certificate-infrastructure"></a>Configurar a infraestrutura de certificados

*Aplica-se a: Gestor de Configuração (ramo atual)*

Aprenda a configurar a infraestrutura de certificados no Gestor de Configuração. Antes de começar, verifique se existem pré-requisitos listados nos [pré-requisitos para perfis](../../protect/plan-design/prerequisites-for-certificate-profiles.md)de certificados .  

Utilize estes passos para configurar a sua infraestrutura para certificados SCEP ou PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Passo 1 - Instalar e Configurar o Serviço de Inscrição e Dependências do Dispositivo de Rede (apenas para certificados SCEP)

 Tem de instalar e configurar o serviço de função Serviço de Inscrição de Dispositivos de Rede para Serviços de Certificados do Active Directory (AD CS), alterar as permissões de segurança nos modelos de certificados, implementar um certificado de cliente de infraestrutura de chave pública (PKI) e editar o registo para aumentar o limite do tamanho predefinido do URL do IIS (Serviços de Informação Internet). Se necessário, também tem de configurar a autoridade de certificação (AC) emissora para permitir um período de validade personalizado.  

> [!IMPORTANT]  
>  Antes de configurar o Gestor de Configuração para trabalhar com o Serviço de Inscrição de Dispositivos de Rede, verifique a instalação e configuração do Serviço de Inscrição do Dispositivo de Rede. Se estas dependências não estiverem a funcionar corretamente, terá dificuldades em resolver a inscrição de certificados através do Gestor de Configuração.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Para instalar e configurar o Serviço de Inscrição de Dispositivos de Rede e dependências  

1. Num servidor que esteja a executar o Windows Server 2012 R2, instale e configure o serviço de função Serviço de Inscrição de Dispositivos de Rede para a função de servidor Serviços de Certificados do Active Directory. Para mais informações, consulte [a Orientação](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\))do Serviço de Inscrição de Dispositivos de Rede .

2. Verifique e, se necessário, modifique as permissões de segurança para os modelos de certificados que o Serviço de Inscrição de Dispositivos de Rede está a utilizar:  

   -   Para a conta que executa a consola Do Gestor de Configuração: **Leia** a permissão.  

        Esta permissão é necessária. Assim, quando executa o Assistente para Criar Perfil de Certificado, pode procurar para selecionar o modelo de certificado que pretende utilizar quando cria um perfil de definições de SCEP. A seleção de um modelo de certificado é sinónimo de que algumas definições no assistente são automaticamente preenchidas. Logo, há menos para si para configurar e é menor o risco de escolha de definições que não são compatíveis com os modelos de certificados que o Serviço de Inscrição de Dispositivos de Rede está a utilizar.  

   -   Para a conta do Serviço SCEP que o conjunto aplicacional do Serviço de Inscrição de Dispositivos de Rede utiliza: permissões de **Leitura** e **Inscrição**.  

        Este requisito não é específico do Gestor de Configuração, mas faz parte da configuração do Serviço de Inscrição de Dispositivos de Rede. Para mais informações, consulte [a Orientação](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\))do Serviço de Inscrição de Dispositivos de Rede .  

   > [!TIP]  
   >  Para identificar os modelos de certificados que o Serviço de Inscrição de Dispositivos de Rede está a utilizar, veja a seguinte chave de registo no servidor que está a executar o Serviço de Inscrição de Dispositivos de Rede: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Estas são as permissões de segurança predefinidas que serão convenientes para a maior parte dos ambientes. No entanto, pode utilizar uma configuração de segurança alternativa. Para mais informações, consulte [O Planeamento para obter permissões](../../protect/plan-design/planning-for-certificate-template-permissions.md)de modelo de certificado para perfis de certificado .  

3. Implemente neste servidor um certificado PKI que suporta a autenticação de cliente. É possível que já disponha de um certificado adequado instalado no computador que pode utilizar ou poderá ter de (ou preferir) implementar um certificado especificamente para esta finalidade. Para obter mais informações sobre os requisitos deste certificado, consulte os detalhes para servidores que executam o Módulo de Política de Gestor de Configuração com o serviço de função de serviço de inscrição de dispositivos de rede na secção **de Certificados PKI para Servidores** no tópico de certificado PKI para o tópico do Gestor de [Configuração.](../../core/plan-design/network/pki-certificate-requirements.md)  

   > [!TIP]
   >  Se precisar de ajuda para a implementação deste certificado, pode utilizar as instruções para a implementação do Certificado de [Cliente para Pontos de Distribuição,](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)porque os requisitos do certificado são os mesmos com uma exceção:  
   > 
   > - Não selecione a caixa de verificação **Permitir que a chave privada seja exportada** no separador **Processamento de Pedidos** das propriedades para o modelo de certificado.  
   > 
   >   Não tem de exportar este certificado com a chave privada porque poderá navegar na loja de computadores local e selecioná-lo quando configurar o Módulo de Política do Gestor de Configuração.  

4. Localize o certificado de raiz ao qual o certificado de autenticação de cliente está encadeado. Em seguida, exporte este certificado da AC de raiz para um ficheiro de certificados (. cer). Guarde este ficheiro numa localização segura à qual pode aceder em segurança quando, posteriormente, instalar e configurar o servidor do sistema de sites para o ponto de registo de certificados.  

5. No mesmo servidor, utilize o editor de registo para aumentar o limite do tamanho predefinido do URL do IIS, definindo os seguintes valores DWORD de chaves de registo em HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Defina a chave **MaxFieldLength** como **65534**.  

   - Defina a chave **MaxRequestBytes** como **16777216**.  

     Para mais informações, consulte o artigo [820129 do Microsoft Support: Definições de registo http.sys para Windows](https://support.microsoft.com/help/820129).

6. No mesmo servidor, no Gestor de Serviços de Informação Internet (IIS), modifique as definições de filtragem de pedidos para a aplicação de /certsrv/mscep e, em seguida, reinicie o servidor. Na caixa de diálogo **Editar Definições de Filtragem de Pedidos**, as definições de **Limites do Pedido** devem ser as seguintes:  

   - **Comprimento máximo de conteúdo permitido (Bytes)**: **30000000**  

   - **Comprimento máximo do URL (Bytes)**: **65534**  

   - **Cadeia de consulta máxima (Bytes)**: **65534**  

     Para obter mais informações sobre estas definições e como configurá-las, consulte os limites dos [pedidos do IIS](https://docs.microsoft.com/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Se pretender poder pedir um certificado que tenha um período de validade inferior ao modelo de certificado que está a utilizar: esta configuração está desativada por predefinição para uma AC empresarial. Para ativar esta opção numa AC empresarial, utilize a ferramenta da linha de comandos Certutil e, em seguida, pare e reinicie o serviço de certificados utilizando os seguintes comandos:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Para mais informações, consulte [as ferramentas e configurações dos serviços de certificado.](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\))

8. Verifique se o Serviço de Inscrição do Dispositivo de `https://server.contoso.com/certsrv/mscep/mscep.dll`Rede está a funcionar utilizando o seguinte link como exemplo: . Deverá ver a página Web incorporada do Serviço de Inscrição de Dispositivos de Rede. Esta página Web explica o que o serviço é e explica que os dispositivos de rede utilizam o URL para submeter pedidos de certificados.  

   Agora que o Serviço de Inscrição de Dispositivos de Rede e dependências estão configurados, está pronto para instalar e configurar o ponto de registo de certificados.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Passo 2 - Instale e configure o ponto de registo do certificado.

Deve instalar e configurar pelo menos um ponto de registo de certificado na hierarquia do Gestor de Configuração, podendo instalar este papel de sistema de site no site da administração central ou num local primário.  

> [!IMPORTANT]  
>  Antes de instalar o ponto de registo do certificado, consulte a secção **Requisitos** do Sistema do Site na secção de [Configurações Suportadas para O Tópico de Gestor de Configuração](../../core/plan-design/configs/supported-configurations.md) para os requisitos e dependências do sistema operativo para o ponto de registo do certificado.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Para instalar e configurar o ponto de registo de certificados  

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração**, expanda **Configuração do Site**, clique em **Servidores e Funções de Sistema de Sites** e selecione o servidor que pretende utilizar para o ponto de registo de certificados.  

3. No separador **Home Page** , no grupo **Servidor** , clique em **Adicionar Funções do Sistema de Sites**.  

4. Na página **Geral** , especifique as definições gerais do sistema de sites e clique em **Seguinte**.  

5. Na página de **Proxy**, clique em **Seguinte**. O ponto de registo de certificados não utiliza as definições de proxy de Internet.  

6. Na página **Seleção da Função do Sistema**, selecione o **Ponto de registo de certificados** na lista de funções disponíveis e clique em **Seguinte**. 

7. Na página do Modo de Registo de **Certificados,** selecione se deseja este ponto de registo de certificado para pedidos de **certificado SCEP processando**ou **processando pedidos**de certificado PFX . Um ponto de registo de certificado não pode processar ambos os tipos de pedidos, mas pode criar vários pontos de registo de certificados se estiver a trabalhar com ambos os tipos de certificados.

   Se processar certificados PFX, terá de escolher uma autoridade de certificado, seja a Microsoft ou a Entrust.

8. A página de **Definições** de Ponto de Registo do Certificado varia de acordo com o tipo de certificado:
   - Se selecionou pedidos de **certificado SCEP process,** então configure o seguinte:
     -   **Nome do site,** número de **porta HTTPS**e nome de **aplicação virtual** para o ponto de registo do certificado. Estes campos são preenchidos automaticamente com valores predefinidos. 
     -   URL para o Serviço de Inscrição do Dispositivo de Rede e certificado CA raiz - Clique em **Adicionar,** em seguida, na caixa de diálogo **Add URL e Root CA Certificate,** especifique o seguinte: **URL for the Network Device Enrollment Service and root CA certificate**
         - **URL do Serviço de Inscrição de Dispositivos de Rede**: especifique o URL no seguinte formato: https://*<server_FQDN>*/certsrv/mscep/mscep.dll. Por exemplo, se o FQDN do seu servidor que está `https://server1.contoso.com/certsrv/mscep/mscep.dll`a executar o Serviço de Inscrição do Dispositivo de Rede for server1.contoso.com, escreva .
         - **Certificado da AC de Raiz**: procure e selecione o ficheiro de certificado (.cer) criado e guardado no **Passo 1: Instalar e configurar o Serviço de Inscrição de Dispositivos de Rede e dependências**. Este certificado CA raiz permite que o ponto de registo do certificado valide o certificado de autenticação do cliente que o Módulo de Política do Gestor de Configuração utilizará.  

   - Se selecionou pedidos de **certificado saquepto sacana,** configura os detalhes de ligação e credenciais para a autoridade de certificados selecionada.

     - Para utilizar a Microsoft como autoridade de certificados, clique em **Adicionar** uma caixa de diálogo de **Autoridade de Certificados e Conta,** especifique o seguinte:
         - Nome do servidor da **Autoridade de Certificados** - Introduza o nome do seu servidor de autoridade de certificados.
         - **Conta de Autoridade de Certificados** - Clique em **Definir** para selecionar ou criar a conta que tem permissões para se inscrever em modelos na autoridade de certificação.
         - Conta de **ligação** ao ponto de registo do certificado - Selecione ou crie a conta que liga o ponto de registo do certificado à base de dados do Gestor de Configuração. Alterativamente, pode utilizar a conta de computador local do computador que acolhe o ponto de registo do certificado.
         - Conta de Publicação de **Certificado de Diretório Ativo** - Selecione uma conta ou crie uma nova conta que será usada para publicar certificados a objetos de utilizador em Diretório Ativo.

         - No URL para a caixa de diálogo de inscrição do dispositivo de **rede e raiz ca,** especifique o seguinte e, em seguida, clique **OK:**  

     - Para utilizar a Entrust como autoridade de certificado, especifique:

       - O URL do **serviço web mdm**
       - O nome de utilizador e as credenciais de senha para o URL.

         Ao utilizar a API do MDM para definir o URL do serviço web Entrust, certifique-se de que utiliza pelo menos a versão 9 da API, como mostra a seguinte amostra:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Versões anteriores da API não apoiam a Entrust.

9. Clique em **Seguinte** e conclua o assistente.  

10. Aguarde alguns minutos para deixar a instalação chegar ao fim e, em seguida, verifique se o ponto de registo de certificados foi instalado com êxito através de qualquer um dos seguintes métodos:  

    -   Na área de trabalho **Monitorização**, expanda **Estado do Sistema**, clique em **Estado do Componente** e procure mensagens de estado no componente **SMS_CERTIFICATE_REGISTRATION_POINT**.  

    -   No servidor do sistema de sites, utilize o ficheiro *<ConfigMgr Installation Path\>* \Logs\crpsetup.log e o ficheiro *<ConfigMgr Installation Path\>* \Logs\crpmsi.log. Uma instalação com êxito irá devolver um código de saída igual a 0.  

    -   Ao utilizar um browser, verifique se pode ligar-se ao URL do ponto de registo do certificado. Por exemplo, `https://server1.contoso.com/CMCertificateRegistration`. Deverá ver uma página **Erro de Servidor** para o nome da aplicação, com uma descrição de HTTP 404.  

11. Localize o ficheiro de certificado exportado para a AC de raiz que o ponto de registo de certificados criou automaticamente na seguinte pasta no computador do servidor do site primário: *<ConfigMgr Installation Path\>* \inboxes\certmgr.box. Guarde este ficheiro para um local seguro a que poderá aceder de forma segura quando instalar mais tarde o Módulo de Política de Gestor de Configuração no servidor que está a executar o Serviço de Inscrição do Dispositivo de Rede.  

    > [!TIP]  
    >  Este certificado não está imediatamente disponível nesta pasta. Pode ter de esperar um pouco (por exemplo, meia hora) antes de o Gestor de Configuração fazer cópias do ficheiro para este local.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Passo 3 - Instale o Módulo de Política do Gestor de Configuração (apenas para certificados SCEP).

Tem de instalar e configurar o Módulo de Política do Gestor de Configuração em cada servidor que especificou no **Passo 2: Instale e configure o ponto** de registo do certificado como URL para o Serviço de Inscrição de **Dispositivos** de Rede nas propriedades para o ponto de registo do certificado.  

##### <a name="to-install-the-policy-module"></a>Para instalar o Módulo de Política  

1. No servidor que executa o Serviço de Inscrição de Dispositivos de Rede, inicie sessão como administrador de domínio e copie os seguintes ficheiros do <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 no suporte de instalação do Gestor de Configuração para uma pasta temporária:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Além disso, se tiver uma pasta LanguagePack no suporte de dados de instalação, copie esta pasta e respetivo conteúdo.  

2. A partir da pasta temporária, executar PolicyModuleSetup.exe para iniciar o assistente de configuração do módulo de configuração.  

3. Na página inicial do assistente, clique em **Seguinte**, aceite os termos de licenciamento e clique em **Seguinte**.  

4. Na página **Pasta de Instalação**, aceite a pasta de instalação predefinida para o módulo de política ou especifique uma pasta alternativa e clique em **Seguinte**.  

5. Na página **Ponto de Registo de Certificados**, especifique o URL do ponto de registo de certificados utilizando o FQDN do servidor do sistema de sites e o nome da aplicação virtual que é especificado nas propriedades para o ponto de registo de certificados. O nome de aplicação virtual predefinido é CMCertificateRegistration. Por exemplo, se o servidor do sistema do site tiver um FQDN de server1.contoso.com e tiver usado o nome de aplicação virtual predefinido, especifique `https://server1.contoso.com/CMCertificateRegistration`.

6. Aceite a porta predefinida **443** ou especifique o número da porta alternativa que o ponto de registo de certificados está a utilizar e clique em **Seguinte**.  

7. Na página **Certificado de Cliente do Módulo de Política**, procure e especifique o certificado de autenticação de cliente que implementou no **Passo 1: Instalar e configurar o Serviço de Inscrição de Dispositivos de Rede e dependências** e clique em **Seguinte**.  

8. Na página **Certificado do Ponto de Registo de Certificados**, clique em **Procurar** para selecionar o ficheiro de certificado exportado para a AC de raiz que localizou e guardou no final do **Passo 2: Instalar e configurar o ponto de registo de certificados**.  

   > [!NOTE]  
   >  Se não tiver guardado anteriormente este ficheiro de certificado, o mesmo está localizado em <ConfigMgr Installation Path\>\inboxes\certmgr.box no computador do servidor do site.  

9. Clique em **Seguinte** e conclua o assistente.  

   Se pretender desinstalar o Módulo de Política do Gestor de Configuração, utilize **programas e funcionalidades** no Painel de Controlo. 

 
Agora que completou os passos de configuração, está pronto para implementar certificados para utilizadores e dispositivos, criando e implementando perfis de certificados. Para obter mais informações sobre como criar perfis de certificado, consulte [Como criar perfis de certificado](../../protect/deploy-use/create-certificate-profiles.md).  
