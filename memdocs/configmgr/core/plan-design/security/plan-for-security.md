---
title: Planear a segurança
titleSuffix: Configuration Manager
description: Obtenha as melhores práticas e outras informações sobre segurança no Gestor de Configuração.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53a30f376bd288e8d50d88ea8f33af37f3cd599e
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110156"
---
# <a name="plan-for-security-in-configuration-manager"></a>Plano de segurança no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve os conceitos a considerar ao planear a segurança com a implementação do seu Gestor de Configuração. Inclui as seguintes secções:  

- [Plano de certificados (auto-assinado e PKI)](#BKMK_PlanningForCertificates)  
  - [Criptografia: Certificados de próxima geração (GNC)](#bkmk_plan-cng)  
  - [HTTP melhorado](#bkmk_plan-ehttp)  
  - [Certificados para CMG e CDP](#bkmk_plan-cmgcdp)  
  - [O certificado de assinatura do servidor do site (auto-assinado)](#bkmk_plansitesign)  
  - [Revogação do certificado PKI](#BKMK_PlanningForCRLs)  
  - [Os certificados de raiz fidedignos do PKI e os emitentes de certificados](#BKMK_PlanningForRootCAs)  
  - [Seleção de certificados de cliente PKI](#BKMK_PlanningForClientCertificateSelection)  
  - [Uma estratégia de transição para certificados PKI e gestão de clientes baseadona na Internet](#BKMK_PlanningForPKITransition)  

- [Plano para a chave raiz de confiança](#BKMK_PlanningForRTK)  

- [Plano de assinatura e encriptação](#BKMK_PlanningForSigningEncryption)  

- [Plano para a administração baseada em funções](#BKMK_PlanningForRBA)  

- [Plano para O Diretório Ativo Azure](#bkmk_planazuread)  

- [Plano para autenticação do Fornecedor SMS](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a>Plano de certificados (auto-assinado e PKI)  

O Gestor de Configuração utiliza uma combinação de certificados auto-assinados e certificados de infraestrutura de chaves públicas (PKI).  

Utilize os certificados PKI sempre que possível. Para mais informações, consulte os requisitos do [certificado PKI](../network/pki-certificate-requirements.md). Quando o Gestor de Configuração solicitar certificados PKI durante a inscrição para dispositivos móveis, deve utilizar os Serviços de Domínio de Diretório Ativo e uma autoridade de certificação empresarial. Para todos os outros certificados PKI, desloque-os e gerencie-os independentemente do Gestor de Configuração. 

Os certificados PKI são necessários quando os computadores clientes se ligam aos sistemas de sites baseados na Internet. Alguns cenários com o gateway de gestão de nuvem e o ponto de distribuição de nuvem também requerem certificados PKI. Para mais informações, consulte [Gerir clientes na internet.](../../clients/manage/manage-clients-internet.md)

Quando utiliza um PKI, também pode utilizar o IPsec para ajudar a proteger a comunicação servidor-servidor entre sistemas de site num site, entre sites e para outras transferências de dados entre computadores. A implementação do IPsec é independente do Gestor de Configuração.  

Quando os certificados PKI não estão disponíveis, o Gestor de Configuração gera automaticamente certificados auto-assinados. Alguns certificados em 'Gestor de Configuração' são sempre auto-assinados. Na maioria dos casos, o Gestor de Configuração gere automaticamente os certificados auto-assinados, e não precisa de tomar medidas adicionais. Um exemplo é o certificado de assinatura do servidor do site. Este certificado é sempre auto-assinado. Certifica-se de que as políticas que os clientes descarregam do ponto de gestão foram enviadas do servidor do site e não foram adulteradas.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a>Criptografia: Certificados de próxima geração (GNC)  

O Gestor de Configuração suporta a Criptografia: Certificados de Próxima Geração (CNG). Os clientes do Gestor de Configuração podem utilizar o certificado de autenticação do cliente PKI com chave privada no Fornecedor de Armazenamento de Chaves CNG (KSP). Com suporte kSP, os clientes do Gestor de Configuração suportam a chave privada baseada em hardware, como tPM KSP para certificados de autenticação de clientes PKI. Para mais informações, consulte a visão geral dos [certificados de CNG](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a>HTTP melhorado  

A utilização da comunicação HTTPS é recomendada para todos os caminhos de comunicação do Gestor de Configuração, mas é um desafio para alguns clientes devido à sobrecarga de gestão de certificados PKI. A introdução da integração do Azure Ative Directory (Azure AD) reduz alguns, mas não todos os requisitos de certificado. A partir da versão 1806, pode ativar o site a utilizar **http melhorado**. Esta configuração suporta HTTPS nos sistemas do site utilizando uma combinação de certificados auto-assinados e AD Azure. Não requer PKI. Para mais informações, consulte [O HTTP Melhorado](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a>Certificados para CMG e CDP

Gerir clientes na internet através do gateway de gestão de nuvem (CMG) e do ponto de distribuição na nuvem (CDP) requer a utilização de certificados. O número e o tipo de certificados variam consoante os seus cenários específicos. Para obter mais informações, veja os artigos seguintes:
- [Certificados para o gateway de gestão de nuvem](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certificados para o ponto de distribuição em nuvem](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a>Plano para o certificado de assinatura do servidor do site (auto-assinado)  

Os clientes podem obter de forma segura uma cópia do certificado de assinatura do servidor do site dos Serviços de Domínio do Diretório Ativo e da instalação push do cliente. Se os clientes não conseguirem obter uma cópia deste certificado por um destes mecanismos, instale-o quando instalar o cliente. Este processo é especialmente importante se a primeira comunicação do cliente com o site for com um ponto de gestão baseado na Internet. Como este servidor está ligado a uma rede não confiável, é mais vulnerável a ataques. Se não der este passo adicional, os clientes descarregam automaticamente uma cópia do certificado de assinatura do servidor do site a partir do ponto de gestão.  

Os clientes não podem obter uma cópia segura do certificado do servidor do site nos seguintes cenários:  

- Não instala o cliente usando o impulso do cliente, e:  

  - Não estendeu o esquema de Diretório Ativo para Diretor de Configuração.  

  - Não publicou o site do cliente para os Serviços de Domínio de Diretório Ativo.  

  - O cliente pertence a uma floresta ou um grupo de trabalho não fidedigno.  

- Estáa usar a gestão de clientes baseada na Internet e instala o cliente quando está na internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Para instalar clientes com uma cópia do certificado de assinatura do servidor do site  

1.  Localize o certificado de assinatura do servidor do site no servidor principal do site. O certificado está armazenado na loja de certificados **SMS** do Windows. Tem o **servidor** do site de nome sujeito e o nome amigável, Certificado de Assinatura do Servidor do **Site**.  

2.  Exportar o certificado sem a chave privada, armazenar o ficheiro de forma segura e acede-o apenas a partir de um canal seguro.  

3.  Instale o cliente utilizando a seguinte propriedade cliente.msi:`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a>Plano de revogação do certificado PKI  

Quando utilizar certificados PKI com Gestor de Configuração, planeie a utilização de uma lista de revogação de certificados (CRL). Os dispositivos utilizam o CRL para verificar o certificado no computador de ligação. O CRL é um ficheiro que uma autoridade de certificados (CA) cria e assina. Tem uma lista de certificados que a AC emitiu, mas revogado. Quando um administrador de certificado revoga os certificados, a sua impressão digital é adicionada ao LCR. Por exemplo, se um certificado emitido for conhecido ou se suspeitar de ser comprometido.

> [!IMPORTANT]  
> Uma vez que a localização do CRL é adicionada a um certificado quando um CA o emite, certifique-se de que planeia para o CRL antes de implementar quaisquer certificados PKI que o Gestor de Configuração utilize.  

O IIS verifica sempre o CRL para obter certificados de cliente, e não pode alterar esta configuração no Gestor de Configuração. Por padrão, os clientes do Gestor de Configuração verificam sempre o CRL para obter sistemas de site. Desative esta definição especificando uma propriedade do site e especificando uma propriedade CCMSetup.  

Os computadores que usam a verificação da revogação do certificado mas não conseguem localizar o CRL comportam-se como se todos os certificados da cadeia de certificação fossem revogados. Este comportamento deve-se ao facto de não poderem verificar se os certificados estão na lista de revogação do certificado. Neste cenário, todas as ligações falham que requerem certificados e incluem verificação de CRL. Ao validar que o seu CRL está acessível navegando para a sua localização http, é importante notar que o cliente do Gestor de Configuração funciona como SISTEMA LOCAL. Por isso, testar a acessibilidade do CRL com um navegador web em execução sob o contexto do utilizador pode ter sucesso, no entanto a conta de computador pode ser bloqueada ao tentar fazer uma ligação http ao mesmo URL CRL devido à solução interna de filtragem web. Pode ser necessário a listagem de whitelisting do URL CRL em quaisquer soluções de filtragem web nesta situação.

Verificar o CRL sempre que um certificado é usado oferece mais segurança contra o uso de um certificado que é revogado. Embora introduza um atraso de ligação e processamento adicional no cliente. A sua organização pode exigir este controlo de segurança adicional para clientes na internet ou uma rede não confiável.  

Consulte os seus administradores PKI antes de decidir se os clientes do Gestor de Configuração devem verificar o CRL. Em seguida, considere manter esta opção ativada no Gestor de Configuração quando ambas as condições seguintes forem verdadeiras:  

- A sua infraestrutura PKI suporta um CRL, e é publicado onde todos os clientes do Gestor de Configuração podem localizá-lo. Estes clientes podem incluir dispositivos na internet, e em florestas não confiáveis.  

- A obrigação de verificar o CRL para cada ligação a um sistema de site configurado para utilizar um certificado PKI é maior do que os seguintes requisitos:  
  - Ligações mais rápidas  
  - Processamento eficiente no cliente  
  - O risco de os clientes não se ligarem aos servidores se o CRL não puder ser localizado  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a>Plano para os certificados de raiz fidedignos do PKI e a lista de emitentes de certificados  

Se os seus sistemas de site IIS utilizarem certificados de cliente PKI para autenticação de clientes em HTTP, ou para autenticação e encriptação do cliente em HTTPS, poderá ter de importar certificados ca raiz como propriedade do site. Aqui estão os dois cenários:  

- Implementa sistemas operativos utilizando o Gestor de Configuração, e os pontos de gestão só aceitam ligações ao cliente HTTPS.  

- Usa certificados de cliente PKI que não acorrentam a um certificado de raiz que a confiança dos pontos de gestão.  

  > [!NOTE]  
  > Quando emite certificados PKI cliente da mesma hierarquia ca que emite os certificados de servidor que utiliza para pontos de gestão, não precisa especificar este certificado ca raiz. No entanto, se usar várias hierarquias ca e não tiver certeza se eles confiam uns nos outros, importe a raiz ca para a hierarquia ca dos clientes.  

Se tiver de importar certificados ca-raiz para O Gestor de Configuração, exporte-os a partir do CA emissor ou do computador cliente. Se exportar o certificado da AC emissora que também é a raiz da AC, certifique-se de que não exporta a chave privada. Guarde o ficheiro de certificado exportado num local seguro para evitar adulterações. Precisa de acesso ao ficheiro quando configurar o site. Se aceder ao ficheiro através da rede, certifique-se de que a comunicação está protegida contra adulteração utilizando o IPsec.  

Se algum certificado de AC raiz que importa for renovado, deve importar o certificado renovado.  

Estes certificados ca-raiz importados e o certificado de CA raiz de cada ponto de gestão criam a lista de emitentes de certificados que os computadores do Gestor de Configuração utilizam das seguintes formas:  

- Quando os clientes se ligam a pontos de gestão, o ponto de gestão verifica que o certificado de cliente está acorrentado a um certificado de raiz fidedigno na lista de emitentes de certificados do site. Se não o fizer, o certificado é rejeitado e a ligação PKI falha.  

- Quando os clientes selecionam um certificado PKI e têm uma lista de emitentes de certificados, selecionam um certificado que se recorrena a um certificado de raiz fidedigno na lista de emitentes de certificados. Se não houver correspondência, o cliente não seleciona um certificado PKI. Para mais informações, consulte [Plan for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a>Plano para a seleção de certificados de cliente PKI  

Se os sistemas do seu site IIS utilizarem certificados de cliente PKI para autenticação do cliente em HTTP ou para autenticação e encriptação do cliente em HTTPS, planeie como os clientes do Windows selecionam o certificado para utilizar para O Gestor de Configuração.  

> [!NOTE]  
> Alguns dispositivos não suportam um método de seleção de certificados. Em vez disso, selecionam automaticamente o primeiro certificado que preenche os requisitos do certificado. Por exemplo, os clientes em computadores Mac e dispositivos móveis não suportam um método de seleção de certificados.  

Em muitos casos, a configuração padrão e o comportamento são suficientes. O cliente do Gestor de Configuração nos computadores Windows filtra vários certificados utilizando estes critérios nesta ordem:  

1.  A lista de emitentes de certificados: As cadeias de certificados para uma raiz ca que é confiada pelo ponto de gestão.  

2.  O certificado está no arquivo de certificados predefinido **Pessoal**.  

3.  O certificado é válido, não foi revogado e não expirou. O controlo de validade também verifica que a chave privada é acessível.  

4.  O certificado tem capacidade de autenticação do cliente, ou é emitido para o nome do computador.  

5.  O certificado tem o período de validade mais longo.  

Configure os clientes para utilizar a lista de emitentes de certificados utilizando os seguintes mecanismos:  

- Publique-o com informações do site do Gestor de Configuração para Serviços de Domínio de Diretório Ativo.  

- Instale os clientes utilizando o impulso do cliente.  

- Os clientes descarregam-no do ponto de gestão depois de serem designados com sucesso para o seu site.  

- Especifique-o durante a instalação do cliente como um cliente CCMSetup.msi propriedade de CCMCERTISSUERS.  

Os clientes que não têm a lista de emitentes de certificados quando são instalados pela primeira vez e ainda não estão designados para o site ignoram este cheque. Quando os clientes têm a lista de emitentes de certificados e não têm um certificado PKI que se acorrenta a um certificado de raiz fidedigno na lista de emitentes de certificados, a seleção de certificados falha. Os clientes não continuam com os outros critérios de seleção de certificados.  

Na maioria dos casos, o cliente do Gestor de Configuração identifica corretamente um certificado PKI único e apropriado. No entanto, quando este comportamento não for o caso, em vez de selecionar o certificado com base na capacidade de autenticação do cliente, pode configurar dois métodos de seleção alternativos:  

- Uma correspondência parcial de cordas no nome do certificado de cliente. Este método é uma combinação de casos insensíveis. É apropriado se estiver a usar o nome de domínio totalmente qualificado (FQDN) de um computador no campo de assunto e pretender que a seleção do certificado seja baseada no sufixo de domínio, por **exemplo, contoso.com**. No entanto, pode utilizar este método de seleção para identificar qualquer série de caracteres sequenciais no nome do certificado que diferencia o certificado de outros na loja de certificados do cliente.  

  > [!NOTE]
  > Não é possível utilizar a combinação parcial da corda com o nome alternativo do sujeito (SAN) como uma definição do site. Embora possa especificar uma correspondência parcial de cordas para o SAN utilizando ccMSetup, será substituído pelas propriedades do site nos seguintes cenários:  
  > 
  > - Os clientes recuperam informações do site que são publicadas nos Serviços de Domínio de Diretório Ativo.  
  >   - Os clientes são instalados utilizando a instalação push do cliente.  
  > 
  >   Utilize uma correspondência parcial de cordas no SAN apenas quando instalar os clientes manualmente e quando não recuperar informações do site dos Serviços de Domínio do Diretório Ativo. Por exemplo, estas condições aplicam-se a clientes apenas à Internet.  

- Uma correspondência no nome do nome do certificado de cliente ou no nome alternativo do sujeito (SAN) valores de atributo. Este método é uma correspondência sensível a casos. É apropriado se estiver a usar um nome x500 distinto ou identificadores de objetos equivalentes (OIDs) em conformidade com o RFC 3280, e pretende que a seleção do certificado se baseie nos valores do atributo. É possível especificar apenas os atributos e os respetivos valores necessários para identificar ou validar exclusivamente o certificado e distinguir o certificado de outros num arquivo de certificados.  

A tabela seguinte mostra os valores de atributo que o Gestor de Configuração suporta para os critérios de seleção de certificados de cliente.  

|Atributo OID|Atributo de nome único|Definição do atributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente do domínio|  
|1.2.840.113549.1.9.1|E ou E-mail|Endereço de e-mail|  
|2.5.4.3|CN|Nome comum|  
|2.5.4.4|SN|Nome do requerente|  
|2.5.4.5|SERIALNUMBER|Número de série|  
|2.5.4.6|C|Código de país|  
|2.5.4.7|L|Localidade|  
|2.5.4.8|S ou ST|Nome do estado ou distrito|  
|2.5.4.9|STREET|Morada|  
|2.5.4.10|O|Nome da organização|  
|2.5.4.11|OU|Unidade organizacional|  
|2.5.4.12|T ou Title|Título|  
|2.5.4.42|G ou GN ou GivenName|Nome próprio|  
|2.5.4.43|I ou Initials|Iniciais|  
|2.5.29.17|(sem valor)|Nome Alternativo do Requerente|  

Se for em presumido mais de um certificado adequado após a aplicação dos critérios de seleção, pode substituir a configuração predefinida para selecionar o certificado que tem o período de validade mais longo e, em vez disso, especificar que nenhum certificado é selecionado. Neste cenário, o cliente não poderá comunicar com os sistemas do site IIS com um certificado PKI. O cliente envia uma mensagem de erro para o seu ponto de recuo atribuído para alertá-lo para a falha de seleção de certificados para que possa alterar ou aperfeiçoar os critérios de seleção do certificado. Em seguida, o comportamento do cliente depende se a falha de ligação falha através de HTTPS ou HTTP:  

- Se a ligação falhada tiver terminado HTTPS: O cliente tenta ligar-se ao HTTP e utiliza o certificado auto-assinado do cliente.  

- Se a ligação falhada foi sobre http: O cliente tenta ligar-se novamente ao HTTP utilizando o certificado de cliente auto-assinado.  

Para ajudar a identificar um certificado único de cliente PKI, também pode especificar uma loja personalizada que não seja o padrão de **Personal** na loja **de computador.** No entanto, deve criar esta loja independentemente do Gestor de Configuração. Deve ser capaz de enviar certificados para esta loja personalizada e renová-los antes que o prazo de validade expire.  

Para mais informações, consulte [as definições de Configuração para os certificados PKI do cliente](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a>Planeie uma estratégia de transição para certificados PKI e gestão de clientes baseadona na Internet  

As opções de configuração flexíveis no Gestor de Configuração permitem-lhe transitar gradualmente os clientes e o site para utilizar certificados PKI para ajudar a garantir pontos finais do cliente. Os certificados PKI proporcionam uma melhor segurança e permitem-lhe gerir os clientes da Internet.  

Devido ao número de opções de configuração e escolhas no Gestor de Configuração, não há uma única forma de transitar um site para que todos os clientes utilizem ligações HTTPS. No entanto, pode seguir estes passos como orientação:  

1. Instale o site do Gestor de Configuração e configure-o de modo a que os sistemas do site aceitem as ligações do cliente em HTTPS e HTTP.  

2. Configure o separador de **comunicação** do cliente nas propriedades do site de modo a que as **Definições** do Sistema do Site seja **HTTP ou HTTPS,** e selecione Use o certificado de **cliente PKI (capacidade de autenticação do cliente) quando disponível**.  Para mais informações, consulte [as definições de Configuração para os certificados PKI do cliente](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > A partir da versão 1906, este separador chama-se Segurança da **Comunicação.**<!-- SCCMDocs#1645 -->  

3. Efetue uma implementação PKI para os certificados de cliente. Por exemplo, implementação, consulte [Implementar o certificado de cliente para computadores Windows](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Instale clientes utilizando o método de instalação push do cliente. Para mais informações, consulte o [Como instalar clientes do Gestor de Configuração utilizando o impulso](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)do cliente .  

5. Monitorize a implementação e o estado do cliente utilizando os relatórios e informações na consola Do Gestor de Configuração.  

6. Verifique quantos clientes estão a utilizar um certificado PKI de cliente visualizando a coluna **Certificado de Cliente** na área de trabalho **Ativos e Compatibilidade** , nó **Dispositivos** .  

    Também pode implementar a Ferramenta de Avaliação de Prontidão HTTPS **(cmHttpsReadiness.exe)** para computadores. Em seguida, utilize os relatórios para ver quantos computadores podem usar um certificado PKI cliente com ' Configuração Manager.  

   > [!NOTE]
   >  Quando instala o cliente Do Gestor de Configuração, instala a `%windir%\CCM` ferramenta **CMHttpsReadiness.exe** na pasta. As seguintes opções de linha de comando estão disponíveis quando executa esta ferramenta:  
   > 
   > - `/Store:<name>`: Esta opção é a mesma que o imóvel **CCMCERTSTORE** client.msi  
   > - `/Issuers:<list>`: Esta opção é a mesma que o **imóvel CCMCERTISSUERS** client.msi    
   > - `/Criteria:<criteria>`: Esta opção é a mesma que o imóvel **CCMCERTSEL** client.msi    
   > - `/SelectFirstCert`: Esta opção é a mesma que o imóvel **CCMFIRSTCERT** client.msi    
   > 
   >   Para mais informações, consulte sobre as propriedades de [instalação do cliente.](../../clients/deploy/about-client-installation-properties.md)  

7. Quando estiver confiante de que clientes suficientes estão a utilizar com sucesso o certificado PKI do seu cliente para autenticação em HTTP, siga estes passos:  

   1.  Implemente um certificado de servidor web PKI para um servidor membro que execute um ponto de gestão adicional para o site, e configure esse certificado no IIS. Para obter mais informações, consulte [A implementação do certificado de servidor web para sistemas de site que executam o IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Instale a função do ponto de gestão neste servidor e configure a opção **Ligações de cliente** nas propriedades do ponto de gestão para **HTTPS**.  

8. Monitorize e certifique-se de que os clientes que tenham um certificado PKI utilizam o novo ponto de gestão utilizando HTTPS. Pode utilizar contadores de registo iIS ou de desempenho para verificar.  

9. Reconfigure as outras funções do sistema de site para utilizar ligações de cliente HTTPS. Se quiser gerir os clientes na internet, certifique-se de que os sistemas de sites têm uma FQDN de internet. Configure pontos de gestão individuais e pontos de distribuição para aceitar ligações de clientes a partir da internet.  

    > [!IMPORTANT]  
    > Antes de configurar funções do sistema do site para aceitar ligações a partir da internet, reveja as informações de planeamento e os pré-requisitos para a gestão de clientes baseados na Internet. Para mais informações, consulte [comunicações entre pontos finais](../hierarchy/communications-between-endpoints.md).  

10. Alargar o lançamento do certificado PKI para clientes e para sistemas de sites que executam o IIS. Configurar as funções do sistema do site para ligações ao cliente HTTPS e ligações à Internet, conforme necessário.  

11. Para a maior segurança: Quando estiver confiante de que todos os clientes estão a usar um certificado PKI cliente para autenticação e encriptação, altere as propriedades do site para utilizar apenas HTTPS.  

    Este plano introduz primeiro certificados PKI para autenticação apenas em HTTP, e depois para autenticação e encriptação em HTTPS. Ao seguir este plano para introduzir gradualmente estes certificados, reduz-se o risco de os clientes ficarem desgeridos. Também beneficiará da mais alta segurança que o Gestor de Configuração suporta.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a>Plano para a chave raiz de confiança  

A chave de raiz fidedigna do Gestor de Configuração fornece um mecanismo para os clientes do Gestor de Configuração verificarem que os sistemas de site pertencem à sua hierarquia. Cada servidor de site gera uma chave de troca de site para comunicar com outros sites. A chave de troca de site do site de nível superior na hierarquia chama-se chave de raiz fidedigna.  

A função da chave raiz fidedigna no Gestor de Configuração assemelha-se a um certificado de raiz numa infraestrutura de chave pública. Tudo o que assinado pela chave privada da chave de raiz de confiança é confiado mais abaixo na hierarquia. Os clientes armazenam uma cópia da chave raiz fidedigna do site no espaço de nome wMI **root\ccm\locationservices.** 

Por exemplo, o site emite um certificado para o ponto de gestão, que assina com a chave privada da chave raiz de confiança. O site partilha com os clientes a chave pública da sua chave de raiz de confiança. Depois, os clientes podem diferenciar entre pontos de gestão que estão na sua hierarquia e pontos de gestão que não estão na sua hierarquia.   

Os clientes recuperam automaticamente a cópia pública da chave raiz fidedigna utilizando dois mecanismos:  

- Você estende o esquema de Diretório Ativo para Gestor de Configuração, e publica o site para Ative Directory Domain Services. Em seguida, os clientes recuperam a informação deste site a partir de um servidor de catálogo global. Para mais informações, consulte Prepare o [Diretório Ativo para a publicação](../network/extend-the-active-directory-schema.md)do site.  

- Quando instala clientes utilizando o método de instalação push do cliente. Para mais informações, consulte a [instalação do impulso do Cliente.](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)  

Se os clientes não conseguem recuperar a chave de raiz fidedigna usando um destes mecanismos, confiam na chave de raiz de confiança que é fornecida pelo primeiro ponto de gestão com que comunicam. Neste cenário, um cliente pode ser mal direcionado para o ponto de gestão de um intruso onde receberia a política do ponto de gestão fraudulento. Esta ação requer um agressor sofisticado. Este ataque é limitado ao curto espaço de tempo antes de o cliente recuperar a chave raiz de confiança de um ponto de gestão válido. Para reduzir este risco de um intruso que direciona os clientes para um ponto de gestão fraudulento, preforre os clientes com a chave raiz de confiança.  

Utilize os seguintes procedimentos para pré-fornecer e verificar a chave raiz fidedigna para um cliente do Gestor de Configuração:  

- [Pré-fornecer um cliente com a chave raiz de confiança usando um ficheiro](#bkmk_trk-provision-file)  

- [Pré-fornecer um cliente com a chave raiz de confiança sem usar um ficheiro](#bkmk_trk-provision-nofile)  

- [Verifique a chave de raiz de confiança num cliente](#bkmk_trk-verify)  

- [Remova ou substitua a chave raiz fidedigna](#bkmk_trk-reset)  

  > [!NOTE]  
  > Se os clientes conseguirem obter a chave raiz de confiança dos Serviços de Domínio do Diretório Ativo ou do impulso do cliente, não tem de a preprovisionar. 
  > 
  > Quando os clientes utilizam a comunicação HTTPS para pontos de gestão, não é preciso prever a chave raiz fidedigna. Estabelecem confiança nos certificados PKI.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a>Pré-fornecer um cliente com a chave raiz de confiança usando um ficheiro  

1.  No servidor do site, abra o seguinte ficheiro num editor de texto:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada, **SMSPublicRootKey=**. Copie a tecla dessa linha e feche o ficheiro sem alterações.  

3.  Crie um novo ficheiro de texto e colhe a informação chave que copiou do ficheiro mobileclient.tcf.  

4.  Guarde o ficheiro num local onde todos os computadores possam aceder ao mesmo, mas onde o ficheiro está a salvo de adulteração.  

5.  Instale o cliente utilizando qualquer método de instalação que aceite propriedades cliente.msi. Especifique o seguinte imóvel:`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > Quando especificar a chave raiz fidedigna durante a instalação do cliente, especifique também o código do site. Utilize a seguinte propriedade cliente.msi:`SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a>Pré-fornecer um cliente com a chave raiz de confiança sem usar um ficheiro  

1.  No servidor do site, abra o seguinte ficheiro num editor de texto:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Localize a entrada, **SMSPublicRootKey=**. Copie a tecla dessa linha e feche o ficheiro sem alterações.  

3.  Instale o cliente utilizando qualquer método de instalação que aceite propriedades cliente.msi. Especifique a seguinte propriedade `SMSPublicRootKey=<key>` `<key>` cliente.msi: onde está a corda que copiou de mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quando especificar a chave raiz fidedigna durante a instalação do cliente, especifique também o código do site. Utilize a seguinte propriedade cliente.msi:`SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a>Verifique a chave de raiz de confiança num cliente  

1. Abra uma consola Windows PowerShell como administrador.  

2. Execute o seguinte comando:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

A corda devolvida é a chave de raiz de confiança. Verifique se corresponde ao valor **SMSPublicRootKey** no ficheiro mobileclient.tcf no servidor do site.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a>Remova ou substitua a chave raiz fidedigna  

Remova a chave de raiz fidedigna de um cliente utilizando a propriedade cliente.msi, **RESETKEYINFORMATION = TRUE**. 

Para substituir a chave de raiz fidedigna, volte a instalar o cliente juntamente com a nova chave raiz fidedigna. Por exemplo, utilize o impulso do cliente ou especifique a propriedade cliente.msi **SMSPublicRootKey**.  

Para obter mais informações sobre estas propriedades de instalação, consulte sobre os parâmetros e propriedades de [instalação do cliente.](../../clients/deploy/about-client-installation-properties.md)



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a>Plano de assinatura e encriptação  
 
Quando utiliza certificados PKI para todas as comunicações do cliente, não tem de planear a assinatura e encriptação para ajudar a garantir a comunicação de dados do cliente. Se configurar quaisquer sistemas de site que executem o IIS para permitir ligações ao cliente HTTP, decida como ajudar a garantir a comunicação do cliente para o site.  

Para ajudar a proteger os dados que os clientes enviam para pontos de gestão, pode exigir que os clientes assinem os dados. Também pode exigir o algoritmo SHA-256 para assinar. Esta configuração é mais segura, mas não requer SHA-256 a menos que todos os clientes a suportem. Muitos sistemas operativos suportam de forma nativa este algoritmo, mas os sistemas operativos mais antigos podem necessitar de uma atualização ou hotfix. 

Ao assinar ajuda a proteger os dados de adulteração, a encriptação ajuda a proteger os dados da divulgação de informação. Pode ativar a encriptação 3DES para os dados de inventário e as mensagens de estado que os clientes enviam para os pontos de gestão do site. Não é preciso instalar nenhuma atualização nos clientes para suportar esta opção. Os clientes e os pontos de gestão requerem uma utilização adicional do CPU para encriptação e desencriptação.  

Para obter mais informações sobre como configurar as definições para a assinatura e encriptação, consulte a [assinatura e encriptação do Configure](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a>Plano para a administração baseada em funções  

Para obter mais informações, consulte os [fundamentos da administração baseada no papel.](../../understand/fundamentals-of-role-based-administration.md)  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a>Plano para O Diretório Ativo Azure

O Gestor de Configuração integra-se com o Azure Ative Directory (Azure AD) para permitir que o site e os clientes utilizem a autenticação moderna. No embarque no seu site com a AD Azure suporta os seguintes cenários do Gestor de Configuração:

**Cliente**  

- [Gerir clientes na internet através de gateway de gestão de nuvem](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Gerir dispositivos unidos pelo domínio em nuvem](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Cogestão](../../../comanage/overview.md)  

- [Implementar aplicações disponíveis para utilizadores](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Microsoft Store para aplicações online business](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Reduzir os requisitos de infraestrutura. Por exemplo, [Software Center utilizando o ponto de gestão](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) em vez do catálogo de aplicações  

- [Gerir aplicativos Microsoft 365 para empresa](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Servidor**  

- [Análise de Computadores](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Centro Comunitário](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Ponto de distribuição em nuvem](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Descoberta do utilizador](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Para obter mais informações sobre a ligação do seu site ao Azure AD, consulte os [serviços do Configure Azure](../../servers/deploy/configure/azure-services-wizard.md).


Para mais informações sobre o Azure AD, consulte [a documentação do Diretório Ativo do Azure.](https://docs.microsoft.com/azure/active-directory/)



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a>Plano para autenticação do Fornecedor SMS
<!--1357013--> 

A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. Aplica-se a todos os componentes que acedem ao Fornecedor de SMS. Por exemplo, a consola do Gestor de Configuração, os métodos SDK e os cmdlets do Windows PowerShell. 

Esta configuração é um cenário de hierarquia. Antes de alterar esta definição, certifique-se de que todos os administradores do 'Gestor de Configuração' podem iniciar sessão no Windows com o nível de autenticação exigido. 

Estão disponíveis os seguintes níveis:

- **Autenticação do Windows**: Exigir autenticação com credenciais de domínio de Diretório Ativo.   

- **Autenticação do certificado**: Exigir autenticação com um certificado válido emitido por uma autoridade de certificados PKI fidedigna.  

- **Windows Hello for Business authentication**: Requerer a autenticação com autenticação forte de dois fatores que esteja ligada a um dispositivo e utilize biometria ou PIN.  

Para mais informações, consulte [Plan for the SMS Provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Consulte também
- [Segurança e privacidade para clientes do Gestor de Configuração](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configurar a segurança](configure-security.md)  

- [Comunicação entre pontos finais](../hierarchy/communications-between-endpoints.md)  

- [Referência técnica de controlos criptográficos](cryptographic-controls-technical-reference.md)  

- [Requisitos do certificado PKI](../network/pki-certificate-requirements.md)  

