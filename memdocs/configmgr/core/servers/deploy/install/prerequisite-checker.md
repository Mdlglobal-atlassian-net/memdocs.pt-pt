---
title: Verificador de pré-requisitos
titleSuffix: Configuration Manager
description: Aprenda a utilizar um verificador pré-requisito para identificar e corrigir problemas que possam bloquear a instalação de uma função de instalação de função de site ou do sistema do site.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718176"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Verificador pré-requisito para gestor de configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

 Antes de executar a Configuração para instalar ou atualizar um site do Gestor de Configuração, ou antes de instalar uma função de sistema de site num novo servidor, pode utilizar esta aplicação autónoma **(Prereqchk.exe**) a partir da versão do 'Gestor de Configuração' que pretende utilizar para verificar a prontidão do servidor. Utilize o Verificador Pré-Requisito para identificar e corrigir problemas que bloqueiem a instalação de uma função de funcionamento do site ou do sistema do local.  

> [!NOTE]  
>  O Verificador pré-requisito funciona sempre como parte da Configuração.  

Por predefinição, quando o Verificador pré-requisito é executado:  

-   Valida o servidor onde funciona.  
-   O computador local é digitalizado para um servidor de site existente, e apenas as verificações aplicáveis ao site são executadas.  
-   Se não forem detetados sites existentes, todas as regras pré-requisitos são executadas.  
-   Verifica as regras para verificar se o software e as definições necessárias para a configuração são instaladas. É possível que o software necessário exija configurações adicionais ou atualizações de software que não sejam verificadas pelo Verificador Pré-Requisito.  
-   Regista os seus resultados no ficheiro **ConfigMgrPrereq.log** na unidade do sistema do computador. O ficheiro de registo pode conter informações adicionais que não aparecem na interface da aplicação.  

Quando executar o Verificador Pré-Requisito num pedido de comando e especificar opções específicas da linha de comando:  

-   O Verificador pré-requisito executa apenas as verificações associadas ao servidor do site ou aos sistemas do site que especifica na linha de comando.  
-   Para verificar um computador remoto, a sua conta de utilizador deve ter direitos de administrador ao computador remoto.  

Para obter mais informações sobre as verificações que o Verificador pré-requisito executa, consulte [a Lista de verificações pré-requisitos para o Gestor de Configuração](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiar ficheiros de Verificadores pré-requisitos para outro computador  

1.  No Windows Explorer, vá a um dos seguintes locais:  

    -   **&lt;*Meios de instalação do Gestor de Configuração*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Gestor de Configuração*\>\BIN\X64**  

2.  Copie os seguintes ficheiros para a pasta de destino no outro computador:  

    - prereqchk.exe
    - prereqcore.dll
    - prereqchkres.dll
      - Este ficheiro encontra-se na subpasta para o idioma de instalação. Por exemplo, o `00000409` inglês está na subpasta. <!--586808-->
    - basesql.dll
    - basesvr.dll
    - baseutil.dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Executar verificador pré-requisito com verificações por defeito  

1.  No Windows Explorer, vá a um dos seguintes locais:  

    -   **&lt;*Meios de instalação do Gestor de Configuração*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Gestor de Configuração*\>\BIN\X64**  

2.  Executar **prereqchk.exe** para iniciar o Pré-Requisito Checker.   
    O Verificador pré-requisito deteta os locais existentes e, se for encontrado, realiza verificações para a prontidão de upgrade. Se não forem encontrados sites, todos os controlos são realizados. A coluna **Tipo de Site** fornece informações sobre o servidor do site ou o sistema do site com o qual a regra está associada.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Executar verificador pré-requisito a partir de um pedido de comando para todas as verificações predefinidas  

1.  Abra uma janela De Comando E altere os diretórios para um dos seguintes locais:  

    -   **&lt;*Meios de instalação do Gestor de Configuração*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Caminho de instalação do Gestor de Configuração*\>\BIN\X64**  

2.  Introduza **prereqchk.exe /LOCAL** para iniciar o Pré-Requisito Checker e executar todas as verificações pré-requisitos no servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Executar verificador pré-requisito a partir de um pedido de comando para usar opções  

1. Abra uma janela De Comando E altere os diretórios para um dos seguintes locais:  

   -   **&lt;*Meios de instalação do Gestor de Configuração*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Caminho de instalação do Gestor de Configuração*\>\BIN\X64**  

2. Introduza **prereqchk.exe** com a adição de uma ou mais das seguintes opções de linha de comando.  

   Por exemplo, para verificar um local primário, pode utilizar o seguinte:  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN\> do SQL Server /SDK &lt;\> FQDN do SMS Provider [/JOIN &lt;FQDN of central administration site\>] [/MP &lt;FQDN of management point\>] [/DP &lt;FQDN of distribution point\>]**  

   **Servidor de site da administração central:**  

   -   **/NOUI**  

        Não é necessário. Inicia o Verificador Pré-Requisito sem visualizar a interface do utilizador. Deve especificar esta opção antes de qualquer outra opção na linha de comando.  

   -   **/CAS**  

        Necessário. Verifica que o computador local cumpre os requisitos para o site da administração central.  

   -   **&lt; */SQL FQDN do Servidor SQL*>**  

        Necessário. Utilizando o nome de domínio totalmente qualificado (FQDN), verifica que o computador especificado satisfaz os requisitos para o Servidor SQL alojar a base de dados do site do Gestor de Configuração.  

   -   **/SDK &lt; *FQDN do Provedor sms*>**  

        Necessário. Verifica que o computador especificado satisfaz os requisitos para o Provedor de SMS.  

   -   **/Ssbport**  

        Não é necessário. Verifica que uma exceção de firewall está em vigor para permitir a comunicação na porta SQL Server Broker (SSB). A porta SSB padrão é 4022.  

   -   **Instalar &lt;caminho *de instalação do Gestor de Configuração* dir>**  

        Não é necessário. Verifica o espaço mínimo do disco nos requisitos para a instalação do local.  

   **Servidor de site primário:**  

   -   **/NOUI**  

       Não é necessário. Inicia o Verificador Pré-Requisito sem visualizar a interface do utilizador. Deve especificar esta opção antes de qualquer outra opção na linha de comando.  

   -   **/PRI**  

        Necessário. Verifica que o computador local cumpre os requisitos para o local principal.  

   -   **&lt; */SQL FQDN do Servidor SQL*>**  

        Necessário. Verifica que o computador especificado satisfaz os requisitos para que o SQL Server seja o anfitrião da base de dados do site do Gestor de Configuração.  

   -   **/SDK &lt; *FQDN do Provedor sms*>**  

        Necessário. Verifica que o computador especificado satisfaz os requisitos para o Provedor de SMS.  

   -   **/JOIN &lt; *FQDN do site da administração central*>**  

        Não é necessário. Verifica que o computador local cumpre os requisitos para a ligação ao servidor do site da administração central.  

   -   **/MP &lt; *FQDN do ponto de gestão*>**  

        Não é necessário. Verifica que o computador especificado satisfaz os requisitos para a função do sistema do site de pontos de gestão. Esta opção só é suportada quando utiliza a opção **/PRI.**  

   -   **/DP &lt; *FQDN do ponto de distribuição*>**  

        Não é necessário. Verifica que o computador especificado satisfaz os requisitos para a função do sistema do site de pontos de distribuição. Esta opção só é suportada quando utiliza a opção **/PRI.**  

   -   **/Ssbport**  

        Não é necessário. Verifica que existe uma exceção à firewall para permitir a comunicação sobre a porta SSB. A porta SSB padrão é 4022.  

   -   **Instalar &lt;caminho *de instalação do Gestor de Configuração* dir>**  

        Não é necessário. Verifica o espaço mínimo do disco nos requisitos para a instalação do local.  

   **Servidor de site secundário:**  

   -   **/NOUI**  

        Não é necessário. Inicia o Verificador Pré-Requisito sem visualizar a interface do utilizador. Deve especificar esta opção antes de qualquer outra opção na linha de comando.  

   -   **/SEC &lt; *FQDN do servidor de site secundário*>**  

        Necessário. Verifica que o computador especificado satisfaz os requisitos para o local secundário.  

   -   **/INSTALASQLEXPRESS**  

        Não é necessário. Verifica se o SQL Server Express pode ser instalado no computador especificado.  

   -   **/Ssbport**  

        Não é necessário. Verifica que existe uma exceção à firewall para permitir a comunicação da porta SSB. A porta SSB padrão é 4022.  

   -   **/Sqlport**  

        Não é necessário. Verifica que uma exceção de firewall está em vigor para permitir a comunicação para a porta de serviço SQL Server, e que a porta não está a ser utilizada por outra instância nomeada do Servidor SQL. A porta predefinida é 1433.  

   -   **Instalar &lt;caminho *de instalação do Gestor de Configuração* dir>**  

        Não é necessário. Verifica o espaço mínimo do disco nos requisitos para a instalação do local.  

   -   **/SourceDir**  

        Não é necessário. Verifica que a conta de computador do site secundário pode aceder à pasta que acolhe os ficheiros de origem para Configuração.  

   **Consola de Gestor de Configuração:**  

   -   **/Adminui**  

        Necessário. Verifica que o computador local cumpre os requisitos para a instalação do Gestor de Configuração.  

3. Na interface de utilizador pré-requisito do Verificador, o Verificador Pré-Requisito cria uma lista de problemas descobertos na secção de **resultados pré-requisito.**  

   -   Clique num item na lista para obter detalhes sobre como resolver o problema.  
   -   Tem de resolver todos os itens da lista que tenham um estado de **Erro** antes de instalar o servidor do site, o sistema do site ou a consola do Gestor de Configuração.  
   -   Também pode abrir o ficheiro **ConfigMgrPrereq.log** na raiz da unidade do sistema para rever os resultados pré-requisitos do Verificador. O ficheiro de registo pode conter informações adicionais que não são apresentadas na interface de utilizador pré-requisito do Verificador.  
