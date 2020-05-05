---
title: Implementação do certificado PKI de exemplo
titleSuffix: Configuration Manager
description: Siga um exemplo passo a passo para aprender a criar e implementar certificados PKI que o Gestor de Configuração utiliza.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 994ee2916020ecc4e6d9d3c35f41fe24d5a31405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718778"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Implementação passo a passo dos certificados PKI para Gestor de Configuração: Autoridade de Certificação Windows Server 2008

*Aplica-se a: Gestor de Configuração (ramo atual)*

Esta implementação passo a passo, que utiliza uma autoridade de certificação do Windows Server 2008 (CA), tem procedimentos que mostram como criar e implementar os certificados de infraestrutura de chaves públicas (PKI) que o Gestor de Configuração utiliza. Estes procedimentos utilizam uma autoridade de certificação (AC) empresarial e modelos de certificado. Os passos são adequados apenas para uma rede de teste, como prova de conceito.  

Como não existe um único método de implantação para os certificados necessários, consulte a documentação específica de implementação do PKI para os procedimentos e as melhores práticas necessárias para implementar os certificados necessários para um ambiente de produção. Para mais informações sobre os requisitos do certificado, consulte [os requisitos do certificado PKI para O Gestor](pki-certificate-requirements.md)de Configuração .  

> [!TIP]
> Pode adaptar as instruções neste tópico para sistemas operativos que não estejam documentados na secção Requisitos da Rede de Teste. No entanto, se estiver a executar o CA emissor no Windows Server 2012, não está solicitado para a versão do modelo de certificado. Em vez disso, especifique-o no separador de **compatibilidade** das propriedades do modelo:  
>
> - **Autoridade de Certificação**: **Windows Server 2003**  
>   - **Destinatário do certificado**: **Windows XP/Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a>Requisitos da rede de teste

As instruções passo a passo têm os seguintes requisitos:  

- A rede de teste está a executar os Serviços de Domínio do Active Directory com o Windows Server 2008 e está instalada como único domínio e única floresta.  

- Tem um servidor membro que executa o Windows Server 2008 Enterprise Edition, que tem a função de Serviços de Certificados de Diretório Ativo instalado seleção no mesmo, e é configurado como uma autoridade de certificação de raiz empresarial (CA).  

- Tem um computador que tem o Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou mais tarde) instalado no mesmo, esse computador é designado como servidor membro, e os Serviços de Informação de Internet (IIS) estão instalados no mesmo. Este computador será o servidor do sistema de configuração do site do Gestor de Configuração que irá configurar com um nome de domínio totalmente qualificado (FQDN) para suportar as ligações do cliente na intranet e um FQDN de internet se tiver de suportar dispositivos móveis que estejam matriculados pelo Gestor de Configuração e clientes na internet.  

- Tem um cliente do Windows Vista que tem o mais recente pacote de serviços instalado, e este computador é configurado com um nome de computador que compreende caracteres ASCII e é unido ao domínio. Este computador será um computador cliente do Gestor de Configuração.  

- Pode iniciar sessão com uma conta de administrador de domínio raiz ou uma conta de administrador de domínio da empresa e utilizar esta conta para todos os procedimentos nesta implementação, exemplo.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a>Visão geral dos certificados

A tabela seguinte lista os tipos de certificados PKI que podem ser necessários para o Gestor de Configuração e descreve como são utilizados.  

|Requisito de Certificado|Descrição do Certificado|  
|-----------------------------|-----------------------------|  
|Certificado de servidor Web para os sistemas de sites que executam o IIS|Este certificado é utilizado para encriptar dados e autenticar o servidor para clientes. Deve ser instalado externamente a partir do Gestor de Configuração nos servidores de sistemas do site que executam os Serviços de Informação da Internet (IIS) e que são configurados no Gestor de Configuração para utilizar HTTPS.<br /><br /> Para que os passos para configurar e instalar este certificado, consulte implementar o certificado do servidor web para sistemas de [site que executam o IIS](#BKMK_webserver2008_cm2012) neste tópico.|  
|Certificado de serviço para clientes que ligam a pontos de distribuição baseados na nuvem|Para os passos para configurar e instalar este certificado, consulte A implantação do certificado de [serviço para pontos de distribuição baseados](#BKMK_clouddp2008_cm2012) na nuvem neste tópico.<br /><br /> **Importante:** este certificado é utilizado em conjunto com o certificado de gestão do Windows Azure. Para mais informações sobre o certificado de gestão, consulte como criar um Certificado de [Gestão](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) e como adicionar um Certificado de [Gestão a uma subscrição](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate) do Windows Azure na secção plataforma Windows Azure da Biblioteca MSDN.|  
|Certificado de cliente para computadores com o Windows|Este certificado é utilizado para autenticar os computadores clientes do Gestor de Configuração para os sistemas de site que são configurados para utilizar https. Também pode ser utilizado para pontos de gestão e pontos de migração do Estado para monitorizar o seu estado operacional quando são criados para utilizar HTTPS. Deve ser instalado externamente a partir do Gestor de Configuração em computadores.<br /><br /> Para as etapas para configurar e instalar este certificado, consulte [Implementar o certificado de cliente para computadores Windows](#BKMK_client2008_cm2012) neste tópico.|  
|Certificado de cliente para pontos de distribuição|Este certificado tem duas finalidades:<br /><br /> O certificado é utilizado para autenticar o ponto de distribuição para um ponto de gestão ativado para HTTPS antes de o ponto de distribuição enviar mensagens de estado.<br /><br /> Quando a opção do ponto de distribuição **Ativar suporte PXE para clientes** está selecionada, o certificado é enviado para computadores com arranque PXE para que liguem a um ponto de gestão ativado para HTTPS durante a implementação do sistema operativo.<br /><br /> Para as etapas para configurar e instalar este certificado, consulte [Implementar o certificado de cliente para pontos](#BKMK_clientdistributionpoint2008_cm2012) de distribuição neste tópico.|  
|Certificado de inscrição para dispositivos móveis|Este certificado é utilizado para autenticar clientes de dispositivos móveis do Gestor de Configuração para sistemas de localização que estão configurados para utilizar HTTPS. Deve ser instalado como parte da inscrição de dispositivos móveis no ConfigurManager, e escolhe o modelo de certificado configurado como uma definição de cliente de dispositivo móvel.<br /><br /> Para as etapas de configuração deste certificado, consulte A implantação do certificado de [inscrição para dispositivos móveis](#BKMK_mobiledevices2008_cm2012) neste tópico.|  
|Certificado de cliente para computadores Mac|Pode solicitar e instalar este certificado a partir de um computador Mac quando utilizar a inscrição do Gestor de Configuração e escolher o modelo de certificado configurado como uma definição de cliente de dispositivo móvel.<br /><br /> Para os passos para configurar este certificado, consulte [Implementar o certificado de cliente para computadores Mac](#BKMK_MacClient_SP1) neste tópico.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a>Implemente o certificado de servidor web para sistemas de site que executam o IIS

Esta implementação de certificados possui os seguintes procedimentos:  

- Criar e emitir o modelo de certificado de servidor web na autoridade de certificação  

- Solicite o certificado de servidor web  

- Configure o IIS para utilizar o certificado de servidor web  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a>Criar e emitir o modelo de certificado de servidor web na autoridade de certificação

Este procedimento cria um modelo de certificado para sistemas de site do Gestor de Configuração e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de servidor Web na autoridade de certificação

1.  Crie um grupo de segurança chamado **ConfigMgr IIS Servers** que tenha os servidores membros para instalar sistemas de site do Gestor de Configuração que irão executar o IIS.  

2.  No servidor membro que tem Serviços de Certificado instalados, na consola da Autoridade de Certificação, os **modelos** de certificado de clique direito e, em seguida, escolha **Gerir** para carregar a consola de Modelos de **Certificado.**  

3.  No painel de resultados, clique à direita na entrada que tem **o Servidor Web** na coluna de nome do **modelo** e, em seguida, escolha o **modelo duplicado**.  

4.  Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de **Servidor Web ConfigMgr,** para gerar os certificados web que serão utilizados nos sistemas do site do Gestor de Configuração.  

6.  Escolha o separador **Nome** do Assunto e certifique-se de que **a Oferta no pedido** é selecionada.  

7.  Escolha o separador **De Segurança** e, em seguida, remova a permissão **de inscrição** dos grupos de segurança **Dedomínio E.** **Admins.**  

8.  Escolha **Adicionar,** introduza **os Servidores ConfigMgr IIS** na caixa de texto e, em seguida, escolha **OK**.  

9. Escolha a permissão **de Inscrição** para este grupo e não limpe a permissão **De Ler.**  

10. Escolha **OK**e, em seguida, feche a consola de **modelos**de certificado .  

11. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

12. Na caixa de diálogo **'Modelos de Modelos de Habilitação',** escolha o novo modelo que acabou de criar, **o Certificado de Servidor Web ConfigMgr,** e depois escolha **OK**.  

13. Se não precisar de criar e emitir mais certificados, feche a Autoridade de **Certificação.**  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a>Solicite o certificado de servidor web  
 Este procedimento permite especificar os valores FQDN intranet e internet que serão configurados nas propriedades do servidor do sistema do site e, em seguida, instala o certificado do servidor web no servidor membro que executa o IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Para pedir o certificado de servidor Web  

1.  Reiniciar o servidor membro que executa o IIS para garantir que o computador pode aceder ao modelo de certificado que criou utilizando as permissões **de Leitura** e **Inscrição** que configura.  

2.  Escolha **Iniciar,** escolha **Correr**e, em seguida, digite **mmc.exe.** Na consola vazia, escolha **'Ficheiro',** e depois escolha **Adicionar/Remover o Snap-in**.  

3.  Na caixa de diálogo **Add or Remove Snap-ins,** escolha **Certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **Adicionar**.  

4.  Na caixa de diálogo **snap-in do Certificado,** escolha a **conta de Computador,** e escolha **a Seguinte**.  

5.  Na caixa de diálogo **Select Computer,** certifique-se de que **o computador local: (o computador em que esta consola está a funcionar)** e, em seguida, escolha **Terminar**.  

6.  Na caixa de diálogo **Add or Remove,** escolha **OK**.  

7.  Na consola, expandir **Certificados (Computador Local)** e, em seguida, escolher **Pessoal**.  

8.  Certificados **Certificates**de clique à direita, escolha **todas as tarefas,** e, em seguida, escolha **Solicitar novo Certificado**.  

9. Na página **Antes de Começar,** escolha **A Seguir**.  

10. Se vir a página de Política de Inscrição de **Certificados Selecionados,** escolha **A Seguir**.  

11. Na página **de Certificados** de Pedido, identifique o Certificado de **Servidor Web ConfigMgr** na lista de certificados disponíveis e, em seguida, escolha **Mais informações são necessárias para se inscrever para este certificado. Clique aqui para configurar as definições**.  

12. Na caixa de diálogo **Certificate Properties,** no separador **Assunto,** não faça alterações ao **nome Do Assunto**. Isto significa que a caixa **Valor** para a secção **Nome do requerente** permanece em branco. Em vez disso, a partir da secção de **nome alternativa,** escolha a lista de drop-down **do Tipo** e, em seguida, escolha **DNS**.  

13. Na caixa **Valor,** especifique os valores FQDN que irá especificar nas propriedades do sistema do Site Do Gestor de Configuração e, em seguida, escolha **OK** para fechar a caixa de diálogo **Certificate Properties.**  

     Exemplos:  

    - Se o sistema do site aceitar apenas ligações ao cliente a partir da intranet, e a intranet FQDN do servidor do sistema do site for **server1.internal.contoso.com**, **introduza server1.internal.contoso.com**, e, em seguida, escolha **Adicionar**.  

    - Se o sistema de site aceitar ligações de clientes a partir da intranet e da internet, e a intranet FQDN do servidor do sistema do site for **server1.internal.contoso.com** e o FQDN de internet do servidor do sistema do site é **server.contoso.com:**  

        1.  Introduza **server1.internal.contoso.com**e, em seguida, escolha **Adicionar**.  

        2.  Introduza **server.contoso.com**e, em seguida, escolha **Adicionar**.  

        > [!NOTE]  
        >  Pode especificar as FQDNs para O Gestor de Configuração em qualquer ordem. No entanto, verifique se todos os dispositivos que utilizarem o certificado, tais como dispositivos móveis e servidores web proxy, podem utilizar um nome alternativo (SAN) e vários valores no SAN. Se os dispositivos têm suporte limitado para valores de SAN nos certificados, terá de alterar a ordem dos FQDN ou utilizar em vez disso o valor Requerente.  

14. Na página **de Certificados de Pedido,** escolha o Certificado de **Servidor Web ConfigMgr** na lista de certificados disponíveis e, em seguida, escolha **Inscrever- se**.  

15. Na página resultados de instalação de **certificados,** aguarde até que o certificado seja instalado e, em seguida, escolha **Terminar**.  

16. Feche **Certificados (Computador Local)**.  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a>Configure o IIS para utilizar o certificado de servidor web  
 Este procedimento vincula o certificado instalado ao **Web Site Predefinido**do IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Para configurar o IIS para utilizar o certificado de servidor web  

1. No servidor membro que tem o IIS instalado, escolha **Iniciar,** escolha **Programas,** escolha **Ferramentas Administrativas**e, em seguida, escolha o Gestor de Serviços de Informação de **Internet (IIS).**  

2. Expandir **sites,** clicar no **sítio Web predefinido**do clique direito e, em seguida, escolher **Ligações de Edição**.  

3. Escolha a entrada **em https** e, em seguida, escolha **Editar**.  

4. Na caixa de diálogo de ligação do **site de edição,** selecione o certificado solicitado utilizando o modelo de Certificados de Servidor Web ConfigMgr e, em seguida, escolha **OK**.  

   > [!NOTE]  
   >  Se não tiver a certeza qual é o certificado correto, escolha um e, em seguida, escolha **'Ver**' . Isto permite comparar os dados do certificado selecionados com os certificados do snap-in dos Certificados. Por exemplo, o snap-in dos certificados mostra o modelo de certificado que foi utilizado para solicitar o certificado. Pode então comparar a impressão digital do certificado do certificado que foi solicitado utilizando o modelo de Certificados de Servidor Web ConfigMgr com a impressão digital do certificado do certificado atualmente selecionado na caixa de diálogo de ligação do **site de edição.**  

5. Escolha **OK** na caixa de diálogo de ligação do **site de edição** e, em seguida, escolha **Fechar**.  

6. Feche o **Gestor de Serviços de Informação Internet (IIS)**.  

   O servidor membro é agora configurado com um certificado de servidor web Do Gestor de Configuração.  

> [!IMPORTANT]  
>  Quando instalar o servidor do sistema do Gestor de Configuração neste computador, certifique-se de que especifica as mesmas FQDNs nas propriedades do sistema do site, conforme especificado quando solicitou o certificado.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a>Implementar o certificado de serviço para pontos de distribuição baseados na nuvem  

Esta implementação de certificados possui os seguintes procedimentos:  

- [Criar e emitir um modelo de certificado de servidor web personalizado na autoridade de certificação](#BKMK_clouddpcreating2008)  

- [Solicite o certificado de servidor web personalizado](#BKMK_clouddprequesting2008)  

- [Exportar o certificado de servidor web personalizado para pontos de distribuição baseados na nuvem](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a>Criar e emitir um modelo de certificado de servidor web personalizado na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado que é baseado no modelo de certificado do servidor web. O certificado é para pontos de distribuição baseados na nuvem do Gestor de Configuração e a chave privada deve ser exportável. Após a criação do modelo de certificado, este é adicionado à autoridade de certificação.  

> [!NOTE]
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado do servidor web que criou para sistemas de site que executam o IIS. Embora ambos os certificados exijam capacidade de autenticação do servidor, o certificado para pontos de distribuição baseados na nuvem requer que introduza um valor definido sob medida para o Nome do Assunto e a chave privada deve ser exportada. Como uma boa prática de segurança, não configurar modelos de certificado para que a chave privada possa ser exportada a menos que esta configuração seja necessária. O ponto de distribuição baseado na nuvem requer esta configuração porque você deve importar o certificado como um arquivo, em vez de escolhê-lo no certificado.  
> 
>  Quando criar um novo modelo de certificado para este certificado, pode restringir os computadores que podem solicitar um certificado cuja chave privada pode ser exportada. Numa rede de produção, poderá também considerar adicionar as seguintes alterações para este certificado:  
> 
> - Requerer a aprovação para instalar o certificado para segurança adicional.  
>   - Aumente o período de validade do certificado. Uma vez que deve exportar e importar o certificado cada vez que expira, um aumento do período de validade reduz a frequência com que deve repetir este procedimento. No entanto, um aumento do período de validade também diminui a segurança do certificado porque proporciona mais tempo para um intruso desencriptar a chave privada e roubar o certificado.  
>   - Utilize um valor personalizado no Nome Alternativo do Requerente (SAN) do certificado para ajudar a identificar este certificado entre certificados de servidor Web padrão que utiliza com o IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de servidor web personalizado na autoridade de certificação  

1.  Crie um grupo de segurança chamado **ConfigMgr Site Servers** que tem os servidores membros para instalar servidores de site primários do Gestor de Configuração que irão gerir pontos de distribuição baseados na nuvem.  

2.  No servidor membro que está a executar a consola da Autoridade de Certificação, **modelos**de certificado de clique direito, e, em seguida, escolha **Gerir** para carregar a consola de gestão de modelos de certificado.  

3.  No painel de resultados, clique à direita na entrada que tem **o Servidor Web** na coluna de nome do **modelo** e, em seguida, escolha o **modelo duplicado**.  

4.  Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5.  Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de Ponto de **Distribuição Baseado em Nuvem ConfigMgr,** para gerar o certificado de servidor web para pontos de distribuição baseados na nuvem.  

6.  Escolha o separador **'Manuseamento de Pedidos'** e, em seguida, escolha permitir a **exportação**da chave privada .  

7.  Escolha o separador **Segurança** e, em seguida, remova a permissão **de inscrição** do grupo de segurança **Enterprise Admins.**  

8.  Escolha **Adicionar,** **introduza os Servidores do Site ConfigMgr** na caixa de texto e, em seguida, escolha **OK**.  

9. Selecione a permissão **Inscrever** para este grupo e não desmarque a permissão **Leitura** .  

10. Escolha o separador **Criptografia** e certifique-se de que o **tamanho mínimo** da tecla foi definido para **2048**.

11. Escolha **OK**, e, em seguida, feche a consola de **modelos**de certificado .  

12. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

13. Na caixa de diálogo de modelos de **certificado ativa,** escolha o novo modelo que acabou de criar, O Certificado de Ponto de **Distribuição Baseado em Nuvem ConfigMgr,** e depois escolha **OK**.  

14. Se não tiver de criar e emitir mais certificados, feche a Autoridade de **Certificação.**  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a>Solicite o certificado de servidor web personalizado  
 Este procedimento solicita e, em seguida, instala o certificado de servidor web personalizado no servidor membro que executará o servidor do site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Para pedir o certificado de servidor Web personalizado  

1.  Reiniciar o servidor membro depois de criar e configurar o grupo de segurança **ConfigMgr Site Servers** para garantir que o computador pode aceder ao modelo de certificado que criou utilizando as permissões **de Leitura** e **Inscrição** que configura.  

2.  Escolha **Iniciar,** escolha **Correr**e, em seguida, insira **mmc.exe.** Na consola vazia, escolha **'Ficheiro',** e depois escolha **Adicionar/Remover o Snap-in**.  

3.  Na caixa de diálogo **Add or Remove Snap-ins,** escolha **Certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **Adicionar**.  

4.  Na caixa de diálogo **snap-in do Certificado,** escolha a **conta de Computador,** e escolha **a Seguinte**.  

5.  Na caixa de diálogo **Select Computer,** certifique-se de que **o computador local: (o computador em que esta consola está a funcionar)** e, em seguida, escolha **Terminar**.  

6.  Na caixa de diálogo **Add or Remove,** escolha **OK**.  

7.  Na consola, expandir **Certificados (Computador Local)** e, em seguida, escolher **Pessoal**.  

8.  Certificados **Certificates**de clique à direita, escolha **todas as tarefas,** e, em seguida, escolha **Solicitar novo Certificado**.  

9. Na página **Antes de Começar,** escolha **A Seguir**.  

10. Se vir a página de Política de Inscrição de **Certificados Selecionados,** escolha **A Seguir**.  

11. Na página **de Certificados** de Pedido, identifique o Certificado de Ponto de **Distribuição Baseado em Nuvem ConfigMgr** na lista de certificados disponíveis e, em seguida, escolha **Mais informações são necessárias para se inscrever para este certificado.**  

12. Na caixa de diálogo **Certificate Properties,** no separador **Assunto,** para o **nome Assunto,** escolha **o nome comum** como **Tipo**.  

13. Na caixa **Valor** , especifique a sua escolha de nome de serviço e o nome do domínio utilizando um formato FQDN. Por exemplo: **pdnuvem1.contoso.com**.  

    > [!NOTE]  
    >  Torne o nome de serviço único no seu espaço de nome. Irá utilizar DNS para criar um alias (registo CNAME) para mapear este nome de serviço para um identificador (GUID) gerado automaticamente e um endereço IP do Windows Azure.  

14. Escolha **Adicionar**e, em seguida, escolha **OK** para fechar a caixa de diálogo **Certificate Properties.**  

15. Na página **de Certificados** de Pedido, escolha o Certificado de Ponto de **Distribuição Baseado em Nuvem ConfigMgr** na lista de certificados disponíveis e, em seguida, escolha **Inscrever.**  

16. Na página resultados de instalação de **certificados,** aguarde até que o certificado seja instalado e, em seguida, escolha **Terminar**.  

17. Feche **Certificados (Computador Local)**.  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a>Exportar o certificado de servidor web personalizado para pontos de distribuição baseados na nuvem  
 Este procedimento exporta o certificado de servidor Web personalizado para um ficheiro para que possa ser importado quando criar o ponto de distribuição baseado na nuvem.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Para exportar o certificado de servidor Web personalizado para pontos de distribuição baseados na nuvem  

1. Na consola **Certificates (Computador Local),** clique no certificado que acabou de instalar, escolha **Todas as Tarefas**e, em seguida, escolha **exportação**.  

2. No Certificados, o Assistente de Exportação, escolha **O Próximo**.  

3. Na página **Chave Privada de Exportação,** escolha **Sim, exporte a chave privada,** e depois escolha **a Seguinte**.  

   > [!NOTE]  
   >  Se esta opção não estiver disponível, o certificado foi criado sem a opção para exportar a chave privada. Neste cenário, não é possível exportar o certificado no formato necessário. Deve configurar o modelo de certificado para que a chave privada possa ser exportada e, em seguida, solicitar o certificado novamente.  

4. Na página formato de formato de **ficheiros de exportação,** certifique-se de que a Troca de **Informações Pessoais - PKCS #12 (. A** opção PFX) é selecionada.  

5. Na página **Password,** especifique uma palavra-passe forte para proteger o certificado exportado com a sua chave privada e, em seguida, escolha **A Seguinte**.  

6. Na página **De Registo para Exportação,** especifique o nome do ficheiro que pretende exportar e, em seguida, escolha **O Seguinte**.  

7. Para fechar o assistente, escolha **Terminar** na página do Assistente de Exportação de **Certificados** e, em seguida, escolha **OK** na caixa de diálogo de confirmação.  

8. Feche **Certificados (Computador Local)**.  

9. Guarde o ficheiro de forma segura e certifique-se de que pode aceder-lhe a partir da consola 'Gestor de Configuração'.  

   O certificado está agora pronto para ser importado quando criar um ponto de distribuição baseado na nuvem.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a>Implementar o certificado de cliente para computadores Windows  
 Esta implementação de certificados possui os seguintes procedimentos:  

- Criar e emitir o modelo de certificado de autenticação da estação de trabalho na autoridade de certificação  

- Configure a inscrição automática do modelo de autenticação da estação de trabalho utilizando a Política de Grupo  

- Inscreva automaticamente o certificado de autenticação da estação de trabalho e verifique a sua instalação em computadores  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a>Criar e emitir o modelo de certificado de autenticação da estação de trabalho na autoridade de certificação  
 Este procedimento cria um modelo de certificado para computadores clientes do Gestor de Configuração e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de Autenticação de Estação de Trabalho na autoridade de certificação  

1.  No servidor membro que está a executar a consola da Autoridade de Certificação, **modelos**de certificado de clique direito, e, em seguida, escolha **Gerir** para carregar a consola de gestão de modelos de certificado.  

2.  No painel de resultados, clique à direita na entrada que tem **autenticação** de estação de trabalho na coluna nome do **modelo** e, em seguida, escolha **modelo duplicado**.  

3.  Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de **Cliente ConfigMgr,** para gerar os certificados de cliente que serão utilizados nos computadores clientes do Gestor de Configuração.  

5.  Escolha o separador **Segurança,** selecione o grupo **Domain Computers** e, em seguida, selecione as permissões adicionais de **Read** and **Autoenroll**. Não desmarque **Inscrever**.  

6.  Escolha **OK**, e, em seguida, feche a consola de **modelos**de certificado .  

7.  Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

8.  Na caixa de diálogo **'Modelos de Certificado habilitar',** escolha o novo modelo que acabou de criar, Certificado de **Cliente ConfigMgr,** e depois escolha **OK**.  

9. Se não precisar de criar e emitir mais certificados, feche a Autoridade de **Certificação.**  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a>Configure a inscrição automática do modelo de autenticação da estação de trabalho utilizando a Política de Grupo  
 Este procedimento estabelece a Política de Grupo para auto-inscrever o certificado de cliente em computadores.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Para configurar a inscrição automática do modelo de autenticação da estação de trabalho utilizando a Política de Grupo  

1.  No controlador de domínio, escolha **Iniciar,** escolha **Ferramentas Administrativas,** e, em seguida, escolha **Gestão de Políticas de Grupo**.  

2.  Vá ao seu domínio, clique no domínio e, em seguida, escolha **Criar um GPO neste domínio, e link-o aqui**.  

    > [!NOTE]  
    >  Este passo utiliza a melhor prática de criar uma nova Política de Grupo para definições personalizadas, em vez de editar a Política de Domínios Predefinida que é instalada com os Serviços de Domínio do Active Directory. Ao atribuir esta Política de Grupo ao nível do domínio, irá aplicá-la a todos os computadores do domínio. Num ambiente de produção, pode restringir a inscrição automática para que se inscreva apenas em computadores selecionados. Pode atribuir a Política de Grupo a nível de unidade organizacional, ou pode filtrar a Política do Grupo de Domínio com um grupo de segurança para que se aplique apenas aos computadores do grupo. Se restringir a inscrição automática, lembre-se de incluir o servidor que é configurado como o ponto de gestão.  

3.  Na caixa de diálogo **New GPO,** introduza um nome, como Certificados de **Inscrição Automática,** para a nova Política de Grupo, e depois escolha **OK**.  

4.  No painel de resultados, no separador **Objetos de Política do Grupo Linked,** clique à direita na nova Política de Grupo e, em seguida, escolha **Editar**.  

5.  No Editor de **Gestão de Políticas**do Grupo, expandir **políticas** sob **configuração de computador,** e depois ir para as **Definições** / de Segurança do Windows**Definições** / **Políticas de Chave Pública**.  

6.  Clique no tipo de objeto chamado Cliente de Serviços de **Certificado - Inscrição automática,** e, em seguida, escolha **Propriedades**.  

7.  Da lista de abandono do Modelo de **Configuração,** escolha **Habilitado,** escolha **Renovar certificados expirados, atualizar certificados pendentes, remover certificados revogados,** escolher **certificados de atualização que utilizem modelos**de certificados, e depois escolher **OK**.  

8.  Feche a **Gestão de Políticas de Grupo**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a>Inscreva automaticamente o certificado de autenticação da estação de trabalho e verifique a sua instalação em computadores  
 Este procedimento instala o certificado de cliente nos computadores e verifica a instalação.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Para inscrever automaticamente o certificado de autenticação da estação de trabalho e verificar a sua instalação no computador cliente  

1. Reinicie o computador da estação de trabalho e espere alguns minutos antes de iniciar sessão.  

   > [!NOTE]  
   >  Reiniciar um computador é o método mais fiável de garantir o sucesso da inscrição automática de certificados.  

2. Assine com uma conta que tenha privilégios administrativos.  

3. Na caixa de pesquisa, introduza **mmc.exe.** **Enter**  

4. Na consola de gestão vazia, escolha **File**, e, em seguida, escolha **Adicionar/Remover o Snap-in**.  

5. Na caixa de diálogo **Add or Remove Snap-ins,** escolha **Certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **Adicionar**.  

6. Na caixa de diálogo **snap-in do Certificado,** escolha a **conta de Computador,** e escolha **a Seguinte**.  

7. Na caixa de diálogo **Select Computer,** certifique-se de que **o computador local: (o computador em que esta consola está a funcionar)** e, em seguida, escolha **Terminar**.  

8. Na caixa de diálogo **Add or Remove,** escolha **OK**.  

9. Na consola, expandir **Certificados (Computador Local)**, expandir **Pessoal,** e depois escolher **Certificados**.  

10. No painel de resultados, confirme que um certificado tem **autenticação do cliente** na coluna **"Propósito Pretendido",** e que o Certificado de **Cliente ConfigMgr** está na coluna Modelo de **Certificado.**  

11. Feche **Certificados (Computador Local)**.  

12. Repita os passos 1 a 11 para o servidor membro verificar se o servidor que será configurado como o ponto de gestão também tem um certificado de cliente.  

    O computador está agora configurado com um certificado de cliente do Gestor de Configuração.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a>Implementar o certificado de cliente para pontos de distribuição  

> [!NOTE]  
>  Este certificado também pode ser utilizado para imagens de suportes de dados que não utilizem o arranque PXE, uma vez que os requisitos de certificados são os mesmos.  

 Esta implementação de certificados possui os seguintes procedimentos:  

- Criar e emitir um modelo de certificado de autenticação de estação de trabalho personalizado na autoridade de certificação  

- Solicite o certificado de autenticação personalizado da Estação de Trabalho  

- Exportar o certificado de cliente para pontos de distribuição  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a>Criar e emitir um modelo de certificado de autenticação de estação de trabalho personalizado na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para pontos de distribuição do Gestor de Configuração para que a chave privada possa ser exportada e adiciona o modelo de certificado à autoridade de certificação.  

> [!NOTE]
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado que criou para computadores clientes. Embora ambos os certificados exijam capacidade de autenticação do cliente, o certificado para pontos de distribuição requer que a chave privada seja exportada. Como uma boa prática de segurança, não configurar modelos de certificado para que a chave privada possa ser exportada a menos que esta configuração seja necessária. O ponto de distribuição requer esta configuração porque deve importar o certificado como um ficheiro em vez de o escolher no certificado.  
> 
>  Quando criar um novo modelo de certificado para este certificado, pode restringir os computadores que podem solicitar um certificado cuja chave privada pode ser exportada. Na nossa implementação de exemplo, este será o grupo de segurança que criou anteriormente para servidores de sistema de configuração do gestor que executam o IIS. Numa rede de produção que distribua as funções de sistema de sites do IIS, considere criar um novo grupo de segurança para os servidores que executam pontos de distribuição para poder restringir o certificado apenas a estes servidores do sistema de sites. Também poderá considerar adicionar as seguintes alterações a este certificado:  
> 
> - Requerer a aprovação para instalar o certificado para segurança adicional.  
>   - Aumente o período de validade do certificado. Uma vez que deve exportar e importar o certificado cada vez que expira, um aumento do período de validade reduz a frequência com que deve repetir este procedimento. No entanto, um aumento do período de validade também diminui a segurança do certificado porque proporciona mais tempo para um intruso desencriptar a chave privada e roubar o certificado.  
>   - Utilize um valor personalizado no campo Requerente ou Nome Alternativo do Requerente (SAN) do certificado para ajudar a identificar este certificado entre os certificados de cliente padrão. Isto pode ser particularmente útil se pretender utilizar o mesmo certificado para vários pontos de distribuição.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de Autenticação de Estação de Trabalho personalizado na autoridade de certificação  

1.  No servidor membro que está a executar a consola da Autoridade de Certificação, **modelos**de certificado de clique direito, e, em seguida, escolha **Gerir** para carregar a consola de gestão de modelos de certificado.  

2.  No painel de resultados, clique à direita na entrada que tem **autenticação** de estação de trabalho na coluna nome do **modelo** e, em seguida, escolha **modelo duplicado**.  

3.  Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

    > [!IMPORTANT]  
    >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

4.  Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de Ponto de Distribuição de **Clientes ConfigMgr,** para gerar o certificado de autenticação do cliente para pontos de distribuição.  

5.  Escolha o separador **'Manuseamento de Pedidos'** e, em seguida, escolha permitir a **exportação**da chave privada .  

6.  Escolha o separador **Segurança** e, em seguida, remova a permissão **de inscrição** do grupo de segurança **Enterprise Admins.**  

7.  Escolha **Adicionar,** introduza **os Servidores ConfigMgr IIS** na caixa de texto e, em seguida, escolha **OK**.  

8.  Selecione a permissão **Inscrever** para este grupo e não desmarque a permissão **Leitura** .  

9. Escolha **OK**, e, em seguida, feche a consola de **modelos**de certificado .  

10. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

11. Na caixa de diálogo **'Modelos de Certificado habilitar',** escolha o novo modelo que acabou de criar, Certificado de Ponto de Distribuição de **Cliente ConfigMgr,** e depois escolha **OK**.  

12. Se não tiver de criar e emitir mais certificados, feche a Autoridade de **Certificação.**  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a>Solicite o certificado de autenticação personalizado da Estação de Trabalho  
 Este procedimento solicita e, em seguida, instala o certificado de cliente personalizado no servidor membro que executa o IIS e que será configurado como um ponto de distribuição.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Para pedir o certificado de Autenticação de Estação de Trabalho personalizado  

1.  Escolha **Iniciar,** escolha **Correr**e, em seguida, insira **mmc.exe.** Na consola vazia, escolha **'Ficheiro',** e depois escolha **Adicionar/Remover o Snap-in**.  

2.  Na caixa de diálogo **Add or Remove Snap-ins,** escolha **Certificados** da lista de **snap-ins disponíveis**e, em seguida, escolha **Adicionar**.  

3.  Na caixa de diálogo **snap-in do Certificado,** escolha a **conta de Computador,** e escolha **a Seguinte**.  

4.  Na caixa de diálogo **Select Computer,** certifique-se de que **o computador local: (o computador em que esta consola está a funcionar)** e, em seguida, escolha **Terminar**.  

5.  Na caixa de diálogo **Add or Remove,** escolha **OK**.  

6.  Na consola, expandir **Certificados (Computador Local)** e, em seguida, escolher **Pessoal**.  

7.  Certificados **Certificates**de clique à direita, escolha **todas as tarefas,** e, em seguida, escolha **Solicitar novo Certificado**.  

8.  Na página **Antes de Começar,** escolha **A Seguir**.  

9. Se vir a página de Política de Inscrição de **Certificados Selecionados,** escolha **A Seguir**.  

10. Na página **de Certificados de Pedido,** escolha o Certificado de Ponto de Distribuição do **Cliente ConfigMgr** da lista de certificados disponíveis e, em seguida, escolha **Inscrever.**  

11. Na página resultados de instalação de **certificados,** aguarde até que o certificado seja instalado e, em seguida, escolha **Terminar**.  

12. No painel de resultados, confirme que um certificado tem **autenticação do cliente** na coluna **"Propósito Pretendido"** e que o Certificado de Ponto de Distribuição do **Cliente ConfigMgr** está na coluna Modelo de **Certificado.**  

13. Não feche **Certificados (Computador Local)**.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a>Exportar o certificado de cliente para pontos de distribuição  
 Este procedimento exporta o certificado de autenticação de estação de trabalho personalizado para um ficheiro para que possa ser importado nas propriedades do ponto de distribuição.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Para exportar o certificado de cliente para pontos de distribuição  

1. Na consola **Certificates (Computador Local),** clique no certificado que acabou de instalar, escolha **Todas as Tarefas**e, em seguida, escolha **exportação**.  

2. No Certificados, o Assistente de Exportação, escolha **O Próximo**.  

3. Na página **Chave Privada de Exportação,** escolha **Sim, exporte a chave privada,** e depois escolha **a Seguinte**.  

   > [!NOTE]  
   >  Se esta opção não estiver disponível, o certificado foi criado sem a opção para exportar a chave privada. Neste cenário, não é possível exportar o certificado no formato necessário. Deve configurar o modelo de certificado para que a chave privada possa ser exportada e, em seguida, solicitar o certificado novamente.  

4. Na página formato de formato de **ficheiros de exportação,** certifique-se de que a Troca de **Informações Pessoais - PKCS #12 (. A** opção PFX) é selecionada.  

5. Na página **Password,** especifique uma palavra-passe forte para proteger o certificado exportado com a sua chave privada e, em seguida, escolha **A Seguinte**.  

6. Na página **De Registo para Exportação,** especifique o nome do ficheiro que pretende exportar e, em seguida, escolha **O Seguinte**.  

7. Para fechar o assistente, escolha **Terminar** na página do Assistente de **Exportação** do Certificado e escolha **OK** na caixa de diálogo de confirmação.  

8. Feche **Certificados (Computador Local)**.  

9. Guarde o ficheiro de forma segura e certifique-se de que pode aceder-lhe a partir da consola 'Gestor de Configuração'.  

   O certificado está agora pronto para ser importado quando configurar o ponto de distribuição.  

> [!TIP]  
>  Pode utilizar o mesmo ficheiro de certificado quando configura ruminar imagens de meios de comunicação para uma implementação do sistema operativo que não utilize a bota PXE, e a sequência de tarefas para instalar a imagem deve contactar um ponto de gestão que exija ligações ao cliente HTTPS.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a>Implementar o certificado de inscrição para dispositivos móveis  
 Esta implementação de certificado tem um procedimento único para criar e emitir o modelo de certificado de inscrição na autoridade de certificação.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Criar e emitir o modelo de certificado de inscrição na autoridade de certificação  
 Este procedimento cria um modelo de certificado de inscrição para dispositivos móveis Do Gestor de Configuração e adiciona-o à autoridade de certificação.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de inscrição na autoridade de certificação  

1. Crie um grupo de segurança que tenha utilizadores que irão inscrever dispositivos móveis no 'Gestor de Configuração'.  

2. No servidor membro que tem Serviços de Certificado instalados, na consola da Autoridade de Certificação, modelos de **certificados**de clique direito, e depois escolha **Gerir** para carregar a consola de gestão de Modelos de Certificado.  

3. No painel de resultados, clique à direita na entrada que tem **A Autenticação** na coluna nome do **modelo** e, em seguida, escolha modelo **duplicado**.  

4. Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

   > [!IMPORTANT]  
   >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5. Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de Inscrição de **Dispositivos Móveis ConfigMgr,** para gerar os certificados de inscrição para os dispositivos móveis a gerir pelo Gestor de Configuração.  

6. Escolha o separador **Nome do Assunto,** certifique-se de que a **Partir desta informação** do Diretório Ativo é selecionada, selecione o nome **comum** para o **formato de nome do Assunto:**, e, em seguida, limpe o nome principal do **utilizador (UPN)** de **Incluir esta informação em nome de assunto alternativo**.  

7. Escolha o separador **Segurança,** escolha o grupo de segurança que tem utilizadores que tenham dispositivos móveis para se inscreverem e, em seguida, escolha a permissão adicional de **Inscrição**. Não desmarque **Leitura**.  

8. Escolha **OK**, e, em seguida, feche a consola de **modelos**de certificado .  

9. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

10. Na caixa de diálogo **'Modelos de Modelos de Habilitação',** escolha o novo modelo que acabou de criar, o Certificado de Inscrição de **Dispositivos Móveis ConfigMgr,** e depois escolha **OK**.  

11. Se não precisar de criar e emitir mais certificados, feche a consola da Autoridade de Certificação.  

    O modelo de certificado de inscrição de dispositivomóvel está agora pronto para ser selecionado quando configurar um perfil de inscrição de dispositivo móvel nas definições do cliente.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a>Implementar o certificado de cliente para computadores Mac  

Esta implementação de certificado tem um procedimento único para criar e emitir o modelo de certificado de inscrição na autoridade de certificação.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a>Criar e emitir um modelo de certificado de cliente Mac na autoridade de certificação  
 Este procedimento cria um modelo de certificado personalizado para computadores Mac do Gestor de Configuração e adiciona o modelo de certificado à autoridade de certificação.  

> [!NOTE]  
>  Este procedimento utiliza um modelo de certificado diferente do modelo de certificado que pode ter criado para computadores cliente com Windows ou para pontos de distribuição.  
>   
>  Quando criar um novo modelo de certificado para este certificado, pode restringir o pedido de certificado aos utilizadores autorizados.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Para criar e emitir o modelo de certificado de cliente Mac na autoridade de certificação  

1. Crie um grupo de segurança que tenha contas de utilizadores para utilizadores administrativos que matriculem o certificado no computador Mac utilizando o Gestor de Configuração.  

2. No servidor membro que está a executar a consola da Autoridade de Certificação, **modelos**de certificado de clique direito, e, em seguida, escolha **Gerir** para carregar a consola de gestão de modelos de certificado.  

3. No painel de resultados, clique à direita na entrada que apresenta **A Sessão Autenticada** na coluna nome do **modelo** e, em seguida, escolha o **modelo duplicado**.  

4. Na caixa de diálogo **do Modelo Duplicado,** certifique-se de que **o Servidor Windows 2003,** a Enterprise Edition é selecionada e, em seguida, escolha **OK**.  

   > [!IMPORTANT]  
   >  Não selecione **Windows 2008 Server, Enterprise Edition**.  

5. Na caixa de diálogo **Properties of New Template,** no separador **Geral,** introduza um nome de modelo, como o Certificado de **Cliente ConfigMgr Mac,** para gerar o certificado de cliente Mac.  

6. Escolha o separador **Nome do Assunto,** certifique-se de que a **Partir desta informação** do Diretório Ativo é selecionada, escolha o nome **comum** para o **formato de nome do Assunto:**, e, em seguida, limpe o nome principal do **utilizador (UPN)** de **Incluir esta informação em nome de assunto alternativo**.  

7. Escolha o separador **De Segurança** e, em seguida, remova a permissão **de inscrição** dos grupos de segurança **Dedomínio E.** **Admins.**  

8. Escolha **Adicionar**, especifique o grupo de segurança que criou no primeiro passo e, em seguida, escolha **OK**.  

9. Escolha a permissão **de Inscrição** para este grupo e não limpe a permissão **De Ler.**  

10. Escolha **OK**, e, em seguida, feche a consola de **modelos**de certificado .  

11. Na consola da Autoridade de Certificação, os **modelos**de certificado de clique direito, escolha **mato novo**e, em seguida, escolha o modelo de **certificado para emitir**.  

12. Na caixa de diálogo **'Modelos de Certificado habilitar',** escolha o novo modelo que acabou de criar, O Certificado de **Cliente ConfigMgr Mac,** e depois escolha **OK**.  

13. Se não tiver de criar e emitir mais certificados, feche a Autoridade de **Certificação.**  

    O modelo de certificado de cliente Mac está agora pronto para ser selecionado quando configurar as definições do cliente para inscrição.
