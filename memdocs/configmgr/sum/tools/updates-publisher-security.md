---
title: Certificados e segurança
titleSuffix: Configuration Manager
description: Gerir certificados e segurança para System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5f441bc277f9c91cb1a83ce97879bd29b6349481
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718806"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gerir certificados e segurança para Editor de Atualizações

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os seguintes procedimentos podem ajudá-lo a configurar a loja de certificados no servidor de atualizações, configurar um certificado de auto-assinatura no computador cliente e configurar a Política do Grupo para permitir que o Windows Update Agent nos computadores procure atualizações publicadas.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configure a loja de certificados no servidor de atualização
 Atualizações A Editora utiliza um certificado digital para assinar as atualizações nos catálogos que publica. Antes de um catálogo poder ser publicado no servidor de atualizações, esse certificado deve estar na loja de certificados no servidor de atualizações e na loja de certificados do computador Updates Publisher se esse computador estiver afastado do servidor de atualizações.

O procedimento seguinte é um dos vários métodos possíveis para adicionar o certificado à loja de certificados no servidor de atualização.

### <a name="to-configure-the-certificate-store"></a>Para configurar a loja de certificados
1.  Num computador que pode aceder tanto ao computador Updates Publisher como ao servidor de atualizações, clique em **Iniciar,** clique em **Executar,** digite **MMC** na caixa de texto e clique em **OK** para abrir a Consola de Gestão da Microsoft (MMC).

2.  Clique em **Ficheiros,** clique em **Adicionar/Remover o Snap-in,** clique em **Adicionar,** clique em **Certificados,** clique em **Adicionar,** selecione **a conta de computador**e, em seguida, clique em **Next**.

3.  Selecione **Outro computador,** escreva o nome do servidor de atualização ou clique em **Navegar** para encontrar o computador do servidor de atualização, clique em **Terminar,** clique em **Fechar**, e depois clique em **OK**.

4.  Expandir **Certificados (nome do servidor de*atualização)***, expandir **o WSUS,** e clicar em **Certificados**.

5.  No painel de resultados, clique à direita no certificado pretendido, clique em **Todas as Tarefas**, e, em seguida, clique em **Exportar**.

6.  No Assistente de Exportação de Certificado, utilize as definições predefinidas para criar um ficheiro de exportação com o nome e a localização especificados no assistente. Este ficheiro deve estar disponível para o servidor de atualização antes de passar para o próximo passo.

7.  Clique em **Editores Fidedignos,** clique em **Todas as Tarefas,** e clique em **Importar**. Complete o Assistente de Importação de Certificado utilizando o ficheiro exportado a partir do passo 6.

8.  Se for utilizado um certificado auto-assinado, como a **WSUS Publishers Self-signed**, right-click **Trusted Root Certification Authorities**, clique em **Todas as Tarefas**e, em seguida, clique **em Importar**. Complete o Assistente de Importação de Certificado utilizando o ficheiro exportado a partir do passo 6.

9.  Clique certo **Certificados (nome do servidor de*atualização),*** clique **em Ligar para outro computador,** introduza o nome do computador para o computador Updates Publisher e clique em **OK**.

10. Se o Editor de Atualizações estiver afastado do servidor de atualizações, repita os passos 7 a 9 para importar o certificado para a loja de certificados no computador Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configure um certificado de auto-assinatura em computadores clientes
Nos computadores clientes, o Windows Update Agent (WUA) irá digitalizar as atualizações do catálogo. Este processo não instalará atualizações quando o agente não conseguir localizar o certificado digital na loja Trust Publishers no computador local. Se um certificado auto-assinado foi utilizado para a publicação do catálogo de atualizações, como a **WSUS Publishers Self-signed,** o certificado também deve estar na loja de certificados trust Root Certification Authorities no computador local para que o agente possa verificar a validade do certificado.

Pode utilizar um dos vários métodos para configurar certificados em computadores clientes, como usar a Política de Grupo e o Assistente de Importação de **Certificados** ou utilizando a ferramenta Certutil e distribuição de software.

O seguinte é fornecido como um exemplo de como configurar o certificado de assinatura em computadores clientes.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Para configurar um certificado de auto-assinatura em computadores clientes
1. Num computador com acesso ao servidor de atualizações, clique em **Iniciar,** clique em **Executar,** digite **MMC** na caixa de texto e, em seguida, clique em **OK** para abrir a Consola de Gestão da Microsoft (MMC).

2. Clique em **Ficheiros,** clique em **Adicionar/Remover o Snap-in,** clique em **Adicionar,** clique em **Certificados,** clique em **Adicionar,** selecione **a conta de computador**e, em seguida, clique em **Next**.

3. Selecione **Outro computador,** escreva o nome do servidor de atualização ou clique em **Navegar** para encontrar o computador do servidor de atualização, clique em **Terminar,** clique em **Fechar**, e depois clique em **OK**.

4. Expandir **Certificados (nome do servidor de*atualização)***, expandir **o WSUS,** e clicar em **Certificados**.

5. Clique no certificado no painel de resultados, clique em **Todas as Tarefas,** e clique em **Exportar**. Complete o **Assistente de Exportação** do Certificado utilizando as definições predefinidas para criar um ficheiro de certificado de exportação com o nome e a localização especificados no assistente.

6. Utilize um dos seguintes métodos para adicionar o certificado utilizado para assinar o catálogo de atualizações a cada computador cliente que utilizará a WUA para analisar as atualizações no catálogo. Adicione o certificado no computador cliente da seguinte forma:

   -   Para certificados auto-assinados: Adicione o certificado às Autoridades de **Certificação de Raiz fidedigna e** às lojas **de certificados Trust Publishers.**

   -   Para certificados emitidos pela autoridade de certificação (CA): Adicione o certificado à loja de **certificados Trust Publishers.**

   > [!NOTE]
   > A WUA também verifica se o conteúdo assinado allow a partir da localização do grupo de localização do grupo de **atualização intranet microsoft** está ativado no computador local. Esta definição de política tem de estar ativada para que o WUA procure atualizações criadas e publicadas com o Updates Publisher. Para obter mais informações sobre a ativação desta definição de Política de Grupo, consulte [como configurar a Política de Grupo nos Computadores dos Clientes](https://docs.microsoft.com/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configurar a Política de Grupos para permitir que a WUA nos computadores procure atualizações publicadas
Antes de o Windows Update Agent (WUA) nos computadores procurar atualizações que foram criadas e publicadas com o Updates Publisher, uma definição de política deve ser ativada para permitir conteúdo assinado a partir de um local de atualização intranet microsoft. Quando a definição de política estiver ativada, a WUA aceitará atualizações recebidas através de uma localização intranet se as atualizações forem assinadas na loja de **certificados Trust Publishers** no computador local. Existem vários métodos para configurar a Política de Grupo sem computadores no ambiente.

Para computadores que não estejam no domínio, pode ser configurada uma definição de chave de registo que permite conteúdo assinado a partir de uma localização de serviço intranet Microsoft Update.

Os seguintes procedimentos fornecem os passos básicos que podem ser usados para configurar a Política de Grupo para computadores no domínio e um valor-chave de registo em computadores que não estão no domínio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Para configurar a Política de Grupo sondar a WUA para obter atualizações publicadas
1.  Abra o snap-in do Microsoft Management Console (MMC) da Política de Grupo com um utilizador que tenha os direitos de segurança adequados para configurar a Política de Grupo.

2.  Clique em **Navegar** e selecione o domínio, OU ou GPOs ligados ao site onde a Política de Grupo configurada se propagará aos computadores clientes pretendidos. Clique em **OK,** clique em **Terminar,** clique em **Fechar,** e depois clique **em OK**.

3.  Expanda a definição de política selecionada na árvore da consola, expanda a **configuração do computador,** expanda **os modelos administrativos,** expanda **os componentes do Windows**e, em seguida, clique em Windows **Update**.

4.  No painel de resultados, clique à **direita, deixe o conteúdo assinado a partir da localização do serviço de atualização intranet microsoft,** clique em **Propriedades,** clique em **Ativado**e, em seguida, clique EM **OK**.
