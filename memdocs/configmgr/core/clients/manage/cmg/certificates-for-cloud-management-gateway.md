---
title: Certificados CMG
titleSuffix: Configuration Manager
description: Conheça os diferentes certificados digitais para usar com o portal de gestão de nuvem.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 33e4ecbac965206ec4043f5adf91d2dbfb9602d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714081"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para o gateway de gestão de nuvem

*Aplica-se a: Gestor de Configuração (ramo atual)*

Dependendo do cenário que utiliza para gerir clientes na internet com o portal de gestão de nuvem (CMG), precisa de um ou mais dos seguintes certificados digitais:  

- [Certificado de autenticação do servidor CMG](#bkmk_serverauth)  
  - [Certificado de raiz fidedigno da CMG aos clientes](#bkmk_cmgroot)  
  - [Certificado de autenticação do servidor emitido por fornecedor público](#bkmk_serverauthpublic)  
  - [Certificado de autenticação do servidor emitido da empresa PKI](#bkmk_serverauthpki)  

- [Certificado de autenticação de cliente](#bkmk_clientauth)  
  - [Certificado de raiz fidedigno do cliente à CMG](#bkmk_clientroot)  

- [Ativar o ponto de gestão para HTTPS](#bkmk_mphttps)  

- [Certificado de gestão Azure](#bkmk_azuremgmt)  

Para obter mais informações sobre os diferentes cenários, consulte o plano para o gateway de gestão de [nuvens.](plan-cloud-management-gateway.md)

## <a name="general-information"></a>Informações gerais

<!--SCCMDocs issue #779-->
Os certificados para o gateway de gestão da nuvem suportam as seguintes configurações:  

- Comprimento da chave de 2048-bit ou 4096 bit

- Principais fornecedores de armazenamento para chaves privadas de certificado. Para mais informações, consulte a visão geral dos [certificados de CNG](../../../plan-design/network/cng-certificates-overview.md).  

- Quando configurar o Windows com a seguinte política: **Criptografia do sistema: Utilize algoritmos compatíveis com FIPS para encriptação, hashing e assinatura**  

- **TLS 1.2**. Para mais informações, consulte [Como ativar o TLS 1.2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a>Certificado de autenticação do servidor CMG

*Este certificado é exigido em todos os cenários.*

Fornece este certificado ao criar o CMG na consola 'Gestor de Configuração'.

A CMG cria um serviço HTTPS ao qual os clientes baseados na Internet se conectam. O servidor requer um certificado de autenticação do servidor para construir o canal seguro. Adquira um certificado para o efeito a um prestador público, ou emita-o a partir da sua infraestrutura de chave pública (PKI). Para mais informações, consulte [o certificado raiz fidedigno da CMG aos clientes.](#bkmk_cmgroot)

> [!NOTE]
> O certificado de autenticação do servidor CMG suporta wildcards. Algumas autoridades de certificados emitem certificados usando um personagem wildcard para o nome de anfitrião. Por exemplo, `*.contoso.com`. Algumas organizações usam certificados wildcard para simplificar o seu PKI e reduzir os custos de manutenção.<!--491233-->  
>
> Para obter mais informações sobre como utilizar um certificado wildcard com um CMG, consulte [Configurar um CMG](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Este certificado requer um nome globalmente único para identificar o serviço em Azure. Antes de solicitar um certificado, confirme que o nome de domínio Azure que deseja é único. Por exemplo, *GraniteFalls.CloudApp.Net.*

1. Inicie sessão no [portal do Azure](https://portal.azure.com).
1. **Selecione todos os recursos**e, em seguida, selecione **Adicionar**.
1. Procure o **serviço Cloud**. Selecione **Criar**.
1. No campo de **nome DNS,** digite o prefixo que desejar, por exemplo *GraniteFalls*. A interface reflete se o nome de domínio está disponível ou já está a ser utilizado por outro serviço.

    > [!Important]  
    > Não crie o serviço no portal, basta utilizar este processo para verificar a disponibilidade do nome.

Se também ativar o CMG para conteúdos, confirme que o nome do serviço CMG é também um nome único da conta de armazenamento Azure. Se o nome de serviço de nuvem CMG for único, mas o nome da conta de armazenamento não for, o Gestor de Configuração não presta o serviço em Azure. Repita o processo acima no portal Azure com as seguintes alterações:

- Pesquisar por **conta de Armazenamento**
- Teste o seu nome no campo de **nome da conta de armazenamento**

O prefixo do nome DNS, por exemplo *GraniteFalls,* deve ter 3 a 24 caracteres de comprimento, e usar apenas caracteres alfanuméricos. Não use caracteres especiais, como`-`um traço .<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a>Certificado de raiz fidedigno da CMG aos clientes

Os clientes devem confiar no certificado de autenticação do servidor CMG. Há dois métodos para realizar esta confiança:

- Utilize um certificado de um fornecedor de certificados de confiança pública e global. Por exemplo, mas não se limitando a, DigiCert, Thawte ou VeriSign. Os clientes windows incluem autoridades de certificados de raiz fidedignas (AE) destes fornecedores. Utilizando um certificado de autenticação de servidor emitido por um destes fornecedores, os seus clientes confiam automaticamente nele.  

- Utilize um certificado emitido por uma empresa CA da sua infraestrutura de chaves públicas (PKI). A maioria das implementações do PKI da empresa adicionam os CAs de raiz confiável aos clientes windows. Por exemplo, utilizar serviços de certificados de diretório ativo com a política do grupo. Se emitir o certificado de autenticação do servidor CMG a partir de uma AC em que os seus clientes não confiam automaticamente, adicione o certificado raiz de confiança da AC aos clientes baseados na Internet.  

  - Também pode utilizar perfis de certificado supor Gerente de Configuração para fornecer certificados aos clientes. Para mais informações, consulte [Introdução aos perfis de certificados](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - Se planeia [instalar o cliente do Gestor de Configuração a partir do Intune,](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)também pode utilizar perfis de certificado intune para fornecer certificados aos clientes. Para mais informações consulte [Configurar um perfil](https://docs.microsoft.com/intune/certificates-configure)de certificado .

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a>Certificado de autenticação do servidor emitido por fornecedor público

Um fornecedor de certificados de terceiros não pode criar um certificado para CloudApp.net, uma vez que esse domínio é propriedade da Microsoft. Só pode obter um certificado emitido para um domínio que possui. A principal razão para adquirir um certificado a um fornecedor de terceiros é que os seus clientes já confiam no certificado raiz desse fornecedor.

Utilize o seguinte processo para criar um pseudónimo DNS:

1. Crie um registo de nome canónico (CNAME) no DNS público da sua organização. Este registo cria um pseudónimo para a CMG para um nome amigável que utiliza na certidão pública.

    Por exemplo, Contoso dá nomes às suas Cataratas **de Granito**CMG . Este nome torna-se **GraniteFalls.CloudApp.Net** em Azure. No dNS público de Contoso contoso.com espaço de nome, o administrador do DNS cria um novo recorde CNAME para **GraniteFalls.Contoso.com** para o nome verdadeiro do anfitrião, **GraniteFalls.CloudApp.net**.  

2. Solicite um certificado de autenticação do servidor a um fornecedor público utilizando o Nome Comum (CN) do pseudónimo CNAME.
Por exemplo, Contoso usa **GraniteFalls.Contoso.com** para o certificado CN.  

3. Crie o CMG na consola 'Gestor de Configuração' utilizando este certificado. Na página **definições** do Assistente de Gateway de Gestão de Nuvem:  

    - Quando adiciona o certificado de servidor para este serviço na nuvem (a partir do **ficheiro Certificado),** o assistente extrai o nome de anfitrião do certificado CN como nome de serviço.  

    - Em seguida, anexa esse nome de anfitrião para **cloudapp.net**, ou **usgovcloudapp.net** para a nuvem do Governo dos EUA Azure, como o Serviço FQDN para criar o serviço em Azure.  

    - Por exemplo, quando o Contoso cria o CMG, o Gestor de Configuração extrai o nome de anfitrião **GraniteFalls** do certificado CN. Azure cria o serviço real como **GraniteFalls.CloudApp.net.**  

Quando cria a instância CMG no Gestor de Configuração, enquanto o certificado tem GraniteFalls.Contoso.com, o Gestor de Configuração extrai apenas o nome de anfitrião, por exemplo: GraniteFalls. Anexa este nome de anfitrião a CloudApp.net, que o Azure necessita na criação de um serviço na nuvem. O pseudónimo CNAME no espaço de nome DNS para o seu domínio, Contoso.com, mapeia juntos estes dois FQDNs. O Gestor de Configuração dá aos clientes uma política de acesso a este CMG, o mapeamento dNS une-o para que possam aceder de forma segura ao serviço em Azure.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a>Certificado de autenticação do servidor emitido da empresa PKI

Crie um certificado SSL personalizado para o CMG o mesmo que para um ponto de distribuição em nuvem. Siga as instruções para [a implementação do certificado de serviço para pontos de distribuição baseados na nuvem,](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) mas faça as seguintes coisas de forma diferente:

- Ao solicitar o certificado de servidor web personalizado, forneça um FQDN para o nome comum do certificado. Este nome pode ser um nome de domínio público que possui ou pode utilizar o domínio cloudapp.net. Se utilizar o seu próprio domínio público, consulte o processo acima para criar um pseudónimo DNS no DNS público da sua organização.  

- Ao utilizar o domínio cloudapp.net público para o certificado de servidor web CMG:  

  - Na nuvem pública de Azure, use um nome que termina em **cloudapp.net**  

  - Use um nome que termina em **usgovcloudapp.net** para a nuvem do Governo dos EUA Azure  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a>Certificado de autenticação do cliente

*Este certificado é necessário para clientes baseados na Internet que executam o Windows 8.1, e os dispositivos Windows 10 não se juntam ao Azure Ative Directory (Azure AD). Também é necessário no ponto de ligação CMG. Não é necessário para clientes do Windows 10 que se juntaram à Azure AD.*

Os clientes usam este certificado para autenticar com a CMG. Os dispositivos Windows 10 que são híbridos ou em nuvem não necessitam deste certificado porque utilizam o Azure AD para autenticar.

Forei este certificado fora do contexto do Gestor de Configuração. Por exemplo, utilize serviços de certificadode diretório ativo e política de grupo para emitir certificados de autenticação de clientes. Para mais informações, consulte [a implementação do certificado de cliente para computadores Windows](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

Para encaminhar de forma segura os pedidos dos clientes, o ponto de ligação CMG requer um certificado de autenticação do cliente que corresponda ao certificado de autenticação do servidor no ponto de gestão HTTPS. Se os clientes utilizarem a autenticação Azure AD, ou configurar o ponto de gestão para O HTTP Melhorado, este certificado não é necessário. Para mais informações, consulte O ponto de [gestão enable para HTTPS](#bkmk_mphttps).

> [!NOTE]
> A Microsoft recomenda a adesão de dispositivos à Azure AD. Os dispositivos baseados na Internet podem usar a AD Azure para autenticar com o Gestor de Configuração. Também permite tanto os cenários do dispositivo como do utilizador, quer o dispositivo esteja na internet ou ligado à rede interna. Para mais informações, consulte [Instalar e registar o cliente utilizando a identidade Azure AD](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Começando na versão 2002,<!--5686290--> O Gestor de Configuração alarga o seu suporte a dispositivos baseados na Internet que muitas vezes não se ligam à rede interna, não conseguem aderir ao Azure Ative Directory (Azure AD), e não têm um método para instalar um certificado emitido pelo PKI. Para mais informações, consulte [a autenticação baseada em Token para CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a>Certificado de raiz fidedigno do cliente à CMG

*Este certificado é exigido quando utilizar certificados de autenticação do cliente. Quando todos os clientes usam a AD Azure para autenticação, este certificado não é necessário.*

Fornece este certificado ao criar o CMG na consola 'Gestor de Configuração'.

A CMG deve confiar nos certificados de autenticação do cliente. Para realizar esta confiança, forneça a cadeia de certificados de raiz fidedigno. Certifique-se de adicionar todos os certificados na cadeia de confiança. Por exemplo, se o certificado de autenticação do cliente for emitido por um CA intermédio, adicione os certificados ca intermédios e de raiz.

> [!Note]  
> Quando cria um CMG, já não é necessário fornecer um certificado de raiz fidedigno na página Definições. Este certificado não é necessário quando se utiliza o Azure Ative Directory (Azure AD) para autenticação do cliente, mas costumava ser exigido no assistente. Se estiver a utilizar certificados de autenticação de clientes PKI, então ainda deve adicionar um certificado de raiz fidedigno à CMG.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> Na versão 1902 e anterior, só pode adicionar dois CAs de raiz de confiança e quatro CAs intermédios (subordinados).

#### <a name="export-the-client-certificates-trusted-root"></a>Exportar a raiz fidedigna do certificado de cliente

Depois de emitir um certificado de autenticação de cliente para um computador, utilize este processo nesse computador para exportar a raiz de confiança.

1. Abra o menu Iniciar. Escreva "corra" para abrir a janela Run. Abra `mmc`.  

2. No menu 'Ficheiro', escolha **Adicionar/Remover o Snap-in...**.  

3. Na caixa de diálogo Add or Remove Snap-ins, selecione **Certificados**e, em seguida, **selecione Adicionar**.  

    1. Na caixa de diálogo snap-in certificates, selecione **a conta de computador**e, em seguida, selecione **Next**.  

    1. Na caixa de diálogo Select Computer, selecione **computador local**e, em seguida, selecione **Terminar**.  

    1. Na caixa de diálogo Add or Remove, selecione **OK**.  

4. Expandir **Certificados,** expandir **Personal,** e selecionar **Certificados.**  

5. Selecione um certificado cujo propósito é autenticação do **cliente.**  

    1. A partir do menu Action, **selecione Open**.  

    1. Vá ao separador Caminho de **Certificação.**  

    1. Selecione o próximo certificado na cadeia e selecione **'Ver Certificado**'.  

6. Nesta nova caixa de diálogo de certificado, vá ao separador **Detalhes.** Selecione **Copiar para Arquivar...**.  

7. Complete o Assistente de Exportação de Certificado utilizando o formato de certificado predefinido, **DER codificado binário X.509 (. CER)**. Tome nota do nome e localização do certificado exportado.  

8. Exportar todos os certificados na via de certificação do certificado de autenticação original do cliente. Tome nota dos certificados exportados que são Ca.C. intermédios e quais são cas de raiz de confiança.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a>Ativar o ponto de gestão para HTTPS

Forei este certificado fora do contexto do Gestor de Configuração. Por exemplo, utilize serviços de certificados de diretório ativo e política de grupo para emitir um certificado de servidor web. Para mais informações, consulte [os requisitos do certificado PKI](../../../plan-design/network/pki-certificate-requirements.md) e [implemente o certificado de servidor web para sistemas de site que executam o IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

Ao utilizar a opção do site para **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP,** o ponto de gestão pode ser HTTP. Para mais informações, consulte [O HTTP Melhorado](../../../plan-design/hierarchy/enhanced-http.md).

> [!Tip]  
> Se não estiver a utilizar o Enhanced HTTP, e o seu ambiente tiver vários pontos de gestão, não tem de os ativar a todos para a CMG. Configure os pontos de gestão ativados pela CMG **apenas**como Internet . Então os seus clientes no local não tentam usá-los.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Certificado HTTP melhorado para pontos de gestão

Quando ativa o Enhanced HTTP, o servidor do site gera um certificado auto-assinado chamado **Certificado SMS Role SSL,** emitido pelo certificado de emissão SMS raiz. O ponto de gestão adiciona este certificado ao Web site iIS Predefinido ligado à porta 443.

### <a name="management-point-client-connection-mode-summary"></a>Resumo do modo de conexão do cliente do ponto de gestão

Estas tabelas resumem se o ponto de gestão requer HTTP ou HTTPS, dependendo do tipo de versão cliente e site.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Para clientes baseados na Internet que comunicam com o portal de gestão de nuvem

Configure um ponto de gestão no local para permitir ligações da CMG com o seguinte modo de ligação ao cliente:

| Tipo de cliente   | Ponto de gestão |
|------------------|------------------|
| Grupo de Trabalho        | Nota E-HTTP<sup>[1,](#bkmk_note1)</sup>HTTPS |
| AD-joined domínio | Nota E-HTTP<sup>[1,](#bkmk_note1)</sup>HTTPS |
| Azure AD-joined  | E-HTTP, HTTPS |
| Híbrido-a-join    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Nota 1**: Esta configuração requer que o cliente tenha um certificado de [autenticação do cliente,](#bkmk_clientauth)e apenas suporta cenários centrados no dispositivo.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Para clientes no local que comunicam com o ponto de gestão no local

Configure um ponto de gestão no local com o seguinte modo de ligação ao cliente:

| Tipo de cliente   | Ponto de gestão |
|------------------|------------------|
| Grupo de Trabalho        | HTTP, HTTPS |
| AD-joined domínio | HTTP, HTTPS |
| Azure AD-joined  | HTTPS       |
| Híbrido-a-join    | HTTP, HTTPS |

> [!NOTE]  
> Os clientes associados ao domínio aD suportam cenários centrados no dispositivo e no utilizador que comunicam com um ponto de gestão HTTP ou HTTPS.  
>
> Os clientes unidos pela AD azure e híbridos podem comunicar via HTTP para cenários centrados no dispositivo, mas precisam de E-HTTP ou HTTPS para permitir cenários centrados no utilizador. Caso contrário, comportam-se da mesma forma que os clientes do grupo de trabalho.  

#### <a name="legend-of-terms"></a>Lenda dos termos

- *Grupo de trabalho*: O dispositivo não está associado a um domínio ou AD Azure, mas tem um certificado de [autenticação de cliente](#bkmk_clientauth)  
- *AD-joined domínio:* Você junta o dispositivo a um domínio de Diretório Ativo no local  
- *Azure AD-joined*: Também conhecido como cloud domínio-joined, você junta-se ao dispositivo a um inquilino azure Ative Diretório  
- *Híbrido-joined*: Você se junta ao dispositivo tanto para um domínio de Diretório Ativo como um inquilino Azure AD  
- *HTTP*: Sobre as propriedades do ponto de gestão, você define as ligações do cliente para **HTTP**  
- *HTTPS*: Sobre as propriedades do ponto de gestão, você define as ligações do cliente para **HTTPS**  
- *E-HTTP*: Nas propriedades do site, separador de comunicação de **computador cliente,** definiu as definições do sistema do site para **HTTPS ou HTTP,** e permite a opção de utilizar certificados gerados pelo Gestor de **Configuração para sistemas de site HTTP**. Configurar o ponto de gestão para HTTP, o ponto de gestão HTTP está pronto para a comunicação HTTP e HTTPS (cenários simbólicos).  
    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a>Certificado de gestão Azure

*Este certificado é necessário para implementações clássicas de serviço. Não é necessário para implementações do Gestor de Recursos Azure.*

> [!Important]  
> A partir da versão 1810, as implementações clássicas de serviço sintetizadas em Azure são depreciadas no Gestor de Configuração. Comece a utilizar implementações do Gestor de Recursos Azure para o gateway de gestão de nuvem. Para mais informações, consulte [Plano para CMG](plan-cloud-management-gateway.md#azure-resource-manager).
>
> Começando na versão 1902 do Gestor de Configuração, o Gestor de Recursos do Azure é o único mecanismo de implementação para novos casos do gateway de gestão de nuvem. Este certificado não é exigido na versão 1902 do Gestor de Configuração.<!-- 3605704 -->

Fornece este certificado no portal Azure e ao criar o CMG na consola 'Gestor de Configuração'.

Para criar o CMG em Azure, o ponto de ligação do Gestor de Configuração precisa de autenticar primeiro a sua subscrição Azure. Ao utilizar uma implantação clássica de serviço, utiliza o certificado de gestão Azure para esta autenticação. Um administrador azure envia este certificado para a sua subscrição. Quando criar o CMG na consola 'Gestor de Configuração', forneça este certificado.

Para obter mais informações e instruções sobre como fazer o upload de um certificado de gestão, consulte os seguintes artigos na documentação do Azure:

- [Serviços em nuvem e certificados de gestão](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Faça upload de um Certificado de Gestão de Serviços Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Certifique-se de copiar o ID de subscrição associado ao certificado de gestão. Usa-o para criar o CMG na consola 'Gestor de Configuração'.

## <a name="next-steps"></a>Passos seguintes

- [Configurar o gateway de gestão na cloud](setup-cloud-management-gateway.md)  

- [Perguntas frequentes sobre o gateway de gestão de nuvens](cloud-management-gateway-faq.md)  

- [Segurança e privacidade para o gateway de gestão na cloud ](security-and-privacy-for-cloud-management-gateway.md)  
