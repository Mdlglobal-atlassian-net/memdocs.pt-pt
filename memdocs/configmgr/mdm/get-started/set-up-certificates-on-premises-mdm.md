---
title: Certificados para MDM no local
titleSuffix: Configuration Manager
description: Configurar certificados para comunicações fidedignas com gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc63a21970bb522407c86d027690b83894b3cb99
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721830"
---
# <a name="set-up-certificates-for-trusted-communications-with-on-premises-mdm"></a>Configurar certificados para comunicações fidedignas com MDM no local

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração no local a gestão de dispositivos móveis (MDM) requer que configure as funções do sistema do site para comunicações fidedignas com dispositivos geridos. Precisa de dois tipos de certificados:

- Um certificado de **servidor web** no IIS nos servidores que hospedam as funções de sistema de site necessárias. Se um servidor apresentar várias funções do sistema do site, só precisa de um certificado para esse servidor. Se cada função estiver num servidor separado, cada servidor necessita de um certificado separado.

- O **certificado de raiz fidedigno** da autoridade de certificados (CA) que emite os certificados do servidor web. Instale este certificado de raiz em todos os dispositivos que necessitem de se ligar às funções do sistema do site.

Para dispositivos ligados ao domínio, se utilizar serviços de certificados de diretório ativo, pode instalar automaticamente estes certificados em todos os dispositivos. Para dispositivos não unidos pelo domínio, instale o certificado de raiz fidedigno por outros meios.

Para dispositivos matriculados a granel, pode incluir o certificado no pacote de inscrições. Para dispositivos inscritos pelo utilizador, tem de adicionar o certificado através de e-mail, transferência Web ou qualquer outro método.

Se utilizar um CA público conhecido como verisign ou GoDaddy para emitir os certificados do servidor, pode evitar ter de instalar manualmente o certificado de raiz fidedigno em cada dispositivo. A maioria dos dispositivos confia nativamente nestas autoridades públicas. Este método é uma alternativa útil para dispositivos matriculados pelo utilizador, em vez de instalar o certificado através de outros meios.

> [!IMPORTANT]  
> Existem muitas formas de configurar os certificados para comunicações fidedignas entre dispositivos e servidores do sistema de site para MDM no local. A informação neste artigo é um exemplo de uma forma de o fazer. Este método requer serviços de certificados de diretório ativo, com uma autoridade de certificação e a função de inscrição web da autoridade de certificação. Para mais informações, consulte Serviços de [Certificadode Diretório Ativo](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740\(v=ws.11\)).

## <a name="publish-the-crl"></a><a name="bkmk_configCa"></a>Publicar o CRL

Por predefinição, a autoridade de certificação do Diretório Ativo (CA) utiliza listas de revogação de certificados baseadas em LDAP (CRLs). Permite ligações ao CRL para dispositivos ligados ao domínio. Para permitir que dispositivos não unidos pelo domínio confiem nos certificados emitidos a partir da AC, adicione um CRL baseado em HTTP.

1. No servidor que executa a autoridade de certificação para o seu site, vá ao menu **Iniciar,** selecione **Ferramentas Administrativas,** e escolha a Autoridade de **Certificação.**

1. Na consola da Autoridade de Certificação, clique direito **no CertificateAuthority,** e depois selecione **Propriedades**.

1. Nas propriedades da Autoridade de Certificados, mude para o separador **Extensões.** Certifique-se de que a **extensão Select** está definida para o Ponto de **Distribuição CRL (CDP)**.

1. Selecione `http://<ServerDNSName>/CertEnroll/<CAName><CRLNameSuffix><DeltaCRLAllowed>.crl`. Em seguida, selecione as seguintes opções:

    - **Inclua em CRLs. Os clientes usam isto para encontrar localizações delta CRL.**

    - **Incluir na extensão CDP dos certificados emitidos.**

    - **Incluir na extensão IDP das CRLs emitidas**

1. Mude para o separador **'Módulo de** Saída.Selecione **Propriedades'** e, em seguida, selecione Permitir que os **certificados sejam publicados no sistema de ficheiros**. Verá um aviso para reiniciar os Serviços de Certificadode Diretório Ativo.

1. Clique direito **em Certificados Revogados,** selecione **Todas as Tarefas,** e, em seguida, escolha **Publicar**.

1. Na janela Publish CRL, selecione **apenas a Delta CRL**e, em seguida, selecione **OK** para fechar a janela.

## <a name="create-the-certificate-template"></a><a name="bkmk_certTempl"></a>Criar o modelo de certificado

O CA utiliza o modelo de certificado do servidor web para emitir certificados para os servidores que hospedam as funções do sistema do site. Estes servidores serão pontos finais SSL para comunicações fidedignas entre as funções do sistema do site e dispositivos matriculados.

1. Crie um grupo de segurança de domínio chamado **ConfigMgr SERVIDORES MDM**. Adicione ao grupo as contas de computador dos servidores do sistema do site.

1. Na consola da Autoridade de Certificação, clique direito **nos modelos**de certificado, e escolha **Gerir**. Esta ação carrega a consola de modelos de certificado.

1. No painel de resultados, clique à direita na entrada que mostra o **Servidor Web** na coluna de **nome** do modelo e, em seguida, selecione **Modelo Duplicado**.

1. Na janela **Modelo Duplicado,** selecione **Windows 2003 Server, Enterprise Edition** ou Windows **2008 Server, Enterprise Edition**, e, em seguida, selecione **OK**.

    > [!TIP]
    > O Gestor de Configuração suporta os modelos de certificados do Servidor Windows 2008, também conhecidos como V3 ou Cryptography: Next Generation (CNG). Para mais informações, consulte a visão geral dos [certificados de CNG](../../core/plan-design/network/cng-certificates-overview.md).

    Se o seu CA for executado no Windows Server 2012 ou mais tarde, esta janela não mostra a opção para a versão do modelo de certificado. Depois de duplicar o modelo, selecione a versão no separador **compatibilidade** das propriedades do modelo.

1. Nas propriedades da janela **do novo modelo,** no separador **Geral,** introduza um nome de modelo. O CA usa este nome para gerar os certificados web que serão utilizados nos sistemas de site do Gestor de Configuração. Por exemplo, digite **o servidor web DoMD ConfigMgr**.

1. Mude para o separador **Nome do Assunto** e selecione Construir a partir de informações de **Diretório Ativo**. Para o formato de nome do assunto, especifique o **nome DNS**. Se o **Nome Principal do Utilizador (UPN)** for selecionado, desative a opção para um nome de assunto alternativo.

1. Mude para o separador **Segurança.**

    1. Remova a permissão de **inscrição** dos grupos de segurança **Dedomínio Admins** e **Enterprise Admins.**

    1. Selecione **Adicionar**e insira o nome do seu grupo de segurança. Por exemplo, **servidores De MDM ConfigMgr**. Selecione **OK** para fechar a janela.

    1. Selecione a permissão **De Inscrição** para este grupo. Não remova a permissão **de leitura.**

1. Selecione **OK** para guardar as suas alterações e feche a consola de Modelos de Certificado.

1. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, selecionem **Novos,** e depois escolham o Modelo de **Certificado para Emitir**.

1. Na janela **Modelos de Modelos de Certificado ativar,** selecione o novo modelo. Por exemplo, **servidor web ConfigMgr MDM**. Em seguida, selecione **OK** para guardar e fechar a janela.

## <a name="request-the-certificate"></a><a name="bkmk_requestCert"></a>Solicitar o certificado

Este processo descreve como solicitar o certificado de servidor web para iIS. Faça este processo para cada servidor do sistema do site que acolhe uma das funções para o MDM no local.

1. No servidor do sistema do site que acolhe uma das funções, abra um pedido de comando como administrador. Introduza `mmc` para abrir uma consola vazia de gestão da Microsoft.

1. Na janela da consola, vá ao menu **'Ficheiro'** e selecione **Adicionar/Remover o Snap-in**.

    1. Escolha **certificados** da lista de snap-ins disponíveis e selecione **Adicionar**.

    1. Na janela de encaixe dos Certificados, escolha a **conta de computador**. Selecione **Seguinte**, e, em seguida, selecione **Terminar** para gerir o computador local.

    1. Selecione **OK** para sair da janela Adicionar ou remover a janela Snap-in.

1. Expandir **Certificados (Computador Local)** e selecionar a loja **Pessoal.** Vá ao menu **Ação,** selecione **Todas as Tarefas,** e escolha **Solicitar novo Certificado**. Esta ação comunica com os Serviços de Certificado de Diretório Ativo para criar um novo certificado utilizando o modelo que criou anteriormente.

    1. No assistente de inscrição de certificado, na página Antes de Começar, selecione **Next**.

    1. Na página de Política de Inscrição de Certificados Selecionados, selecione **Política de Inscrição de Diretório Ativo,** e, em seguida, selecione **Seguinte**.

    1. Selecione o seu modelo de modelo de servidor web **(ConfigMgr MDM Web Server)** e, em seguida, selecione **Inscrever**.

    1. Depois de solicitar o certificado, selecione **Terminar**.

Cada servidor precisa de um certificado de servidor web único. Repita este processo para cada servidor que acolhe uma das funções necessárias do sistema do site. Se um servidor alojar todas as funções do sistema de sites, apenas terá de pedir um certificado de servidor Web.

## <a name="bind-the-certificate"></a><a name="bkmk_bindCert"></a>Ligue o certificado

O próximo passo é ligar o novo certificado ao servidor web. Siga este processo para cada servidor que acolhe as funções do sistema de site de ponto de *inscrição* e de ponto de *inscrição.* Se um servidor acolhe todas as funções do sistema do site, só precisa de fazer este processo uma vez.

> [!NOTE]
> Não é preciso fazer este processo para as funções do sistema de pontos de distribuição e de ponto de gestão de dispositivos. Recebem automaticamente o certificado exigido durante a inscrição.

1. No servidor que acolhe o ponto de inscrição ou ponto de procuração de inscrição, vá ao menu **Iniciar,** selecione **Ferramentas Administrativas,** e escolha **O Gestor IIS**.

1. Na lista de Ligações, selecione o **Web Site predefinido**e, em seguida, selecione **Edição de Encadernações**.

    1. Na janela De Encadernação do Site, selecione **https**, e, em seguida, selecione **Editar**.

    1. Na janela de ligação do site de edição, selecione o certificado recém-inscrito para o **certificado SSL**. Selecione **OK** para guardar e, em seguida, selecione **Fechar**.

1. Na consola IIS Manager, na lista de Ligações, selecione o servidor web. No painel action do lado direito, selecione **Reiniciar**. Esta ação reinicia o serviço de servidor web.

## <a name="export-the-trusted-root-certificate"></a><a name="bkmk_exportCert"></a>Exportar o certificado de raiz de confiança

Os Serviços de Certificado de Diretório Ativo instalam automaticamente o certificado exigido da AC em todos os dispositivos unidos pelo domínio. Para obter o certificado necessário para que os dispositivos não ligados ao domínio se comuniquem com as funções do sistema do site, exporte-o a partir do certificado ligado ao servidor web.

1. No IIS Manager, selecione o **Web Site predefinido**. No painel action do lado direito, selecione **Encadernações**.

1. Na janela De encadernação do site, selecione **https**, e, em seguida, selecione **Editar**.

1. Selecione o certificado do servidor web e selecione **'Ver**. '

1. Nas propriedades do certificado do servidor web, mude para o separador Caminho de **Certificação.** Selecione a raiz do caminho de certificação e selecione **'Ver Certificado**' .

1. Nas propriedades do certificado raiz, mude para o separador **Detalhes** e, em seguida, selecione **Copy to File**.

1. No Certificado De Saque de Exportação, na página welcome, selecione **Next**.

1. Selecione **DER codificado binário X.509 (. CER)** como formato, e selecione **Next**.

1. Introduza um caminho e nome de ficheiro para identificar este certificado de raiz fidedigno. Para o nome do ficheiro, clique em **Navegar...**, escolha um local para guardar o ficheiro do certificado, nomeie o ficheiro e selecione **Next**.

1. Reveja as definições e selecione **Terminar** para exportar o certificado para arquivar.

Dependendo do design da sua autoridade de certificados, poderá ser necessário exportar certificados de raiz de CA subordinados adicionais. Repita este processo para exportar os outros certificados na via de certificação do certificado do servidor web.

## <a name="next-step"></a>Passo seguinte

> [!div class="nextstepaction"]
> [Configurar a inscrição de dispositivos](set-up-device-enrollment-on-premises-mdm.md)
