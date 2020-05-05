---
title: Comunicações entre pontos finais
titleSuffix: Configuration Manager
description: Saiba como os sistemas e componentes do Gestor de Configuração comunicam através de uma rede.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587235"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Comunicações entre pontos finais no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve como os sistemas de site do Gestor de Configuração e os clientes comunicam através da sua rede. Inclui as seguintes secções:  

- [Comunicações entre sistemas de site num site](#Planning_Intra-site_Com)  
  - [Servidor do site para ponto de distribuição](#bkmk_site2dp)  

- [Comunicações de clientes a sistemas e serviços de sites](#Planning_Client_to_Site_System)  
  - [Comunicação de pontode gestão de clientes](#bkmk_client2mp)  
  - [Comunicação de pontode distribuição do cliente](#bkmk_client2dp)  
  - [Considerações para comunicações de clientes da internet ou uma floresta não confiável](#BKMK_clientspan)  

- [Comunicações através das florestas de Diretório Ativo](#Plan_Com_X-Forest)  
  - [Suporte computadores de domínio numa floresta que não é confiável pela floresta do seu servidor de site](#bkmk_noforesttrust)  
  - [Suporte computadores em um grupo de trabalho](#bkmk_workgroup)  
  - [Cenários para apoiar um site ou hierarquia que abrange vários domínios e florestas](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a> Comunicações entre sistemas de sites num site  

Quando os sistemas ou componentes do Site do Gestor de Configuração comunicam através da rede a outros sistemas ou componentes do site, utilizam um dos seguintes protocolos, dependendo da configuração do site:  

- Bloco de mensagem de servidor (SMB)  

- HTTP  

- HTTPS  

Com a exceção da comunicação do servidor do site para um ponto de distribuição, as comunicações servidor-servidor-servidor num site podem ocorrer a qualquer momento. Estas comunicações não utilizam mecanismos para controlar a largura de banda da rede. Uma vez que não consegue controlar a comunicação entre os sistemas do site, certifique-se de que instala servidores do sistema do site em locais que tenham redes rápidas e bem conectadas.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a>Servidor do site para ponto de distribuição

Para ajudá-lo a gerir a transferência de conteúdo do servidor do site para pontos de distribuição, use as seguintes estratégias:  

- Configure o ponto de distribuição para o controlo da largura de banda de rede e o agendamento. Estes controlos assemelham-se às configurações utilizadas por endereços inter-locais. Utilize esta configuração em vez de instalar outro site do Gestor de Configuração quando a transferência de conteúdo para locais de rede remota é a sua principal consideração de largura de banda.  

- Pode instalar um ponto de distribuição como um ponto de distribuição pré-configurado. Um ponto de distribuição pré-configurado permite-lhe utilizar o conteúdo que é manualmente colocado no servidor do ponto de distribuição e remove o requisito de transferir ficheiros de conteúdo através da rede.  

Para obter mais informações, consulte [Gerir a largura de banda da rede para gestão](manage-network-bandwidth.md)de conteúdos .

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a> Comunicações de clientes para sistemas e serviços do site

Os clientes iniciam a comunicação para as funções do sistema do site, Serviços de Domínio de Diretório Ativo e serviços online. Para permitir estas comunicações, as firewalls devem permitir o tráfego de rede entre os clientes e o ponto final das suas comunicações. Para obter mais informações sobre portas e protocolos utilizados pelos clientes quando comunicam a estes pontos finais, consulte [portas utilizadas no Gestor](ports.md)de Configuração .  

Antes de um cliente poder comunicar com uma função do sistema de site, o cliente utiliza a localização do serviço para encontrar uma função que suporte o protocolo do cliente (HTTP ou HTTPS). Por padrão, os clientes usam o método mais seguro que está disponível para eles. Para mais informações, consulte [como os clientes encontram recursos e serviços](understand-how-clients-find-site-resources-and-services.md)do site.  

Para utilizar https, configure uma das seguintes opções:  

- Utilize uma infraestrutura de chaves públicas (PKI) e instale certificados PKI em clientes e servidores. Para obter informações sobre como utilizar certificados, consulte [os requisitos do certificado PKI](../network/pki-certificate-requirements.md).  

- A partir da versão 1806, configure o site para **utilizar os certificados gerados pelo Gestor de Configuração para sistemas de site HTTP**. Para mais informações, consulte [O HTTP Melhorado](enhanced-http.md).  

Ao implementar uma função do sistema de sites que utiliza Serviços de Informação Internet (IIS) e suporta comunicações de clientes, tem de especificar se os clientes ligam ao sistema de sites através de HTTP ou HTTPS. Se utilizar HTTP, também tem de considerar as opções de assinatura e encriptação. Para mais informações, consulte [Planeamento para assinatura e encriptação.](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption)  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a>Comunicação de pontode gestão de clientes

Há duas fases em que um cliente comunica com um ponto de gestão: autenticação (transporte) e autorização (mensagem). Este processo varia consoante os seguintes fatores:

- Configuração do site: https apenas, permite HTTP ou HTTPS, ou permite HTTP ou HTTPS com HTTP melhorado ativado
- Configuração do ponto de gestão: HTTPS ou HTTP
- Identidade do dispositivo para cenários centrados no dispositivo
- Identidade do utilizador para cenários centrados no utilizador

Utilize a tabela seguinte para entender como funciona este processo:  

| Tipo MP  | Autenticação de cliente  | Autorização do cliente<br>Identidade do dispositivo  | Autorização do cliente<br>Identidade do utilizador  |
|----------|---------|---------|---------|
| HTTP     | Anónimo<br>Com o HTTP melhorado, o site verifica o *utilizador* ou ficha do *dispositivo* Azure AD. | Pedido de localização: Anónimo<br>Pacote de cliente: Anónimo<br>Registo, utilizando um dos seguintes métodos para provar a identidade do dispositivo:<br> - Anónimo (aprovação manual)<br> - Autenticação integrada no Windows<br> - Ficha do *dispositivo* Azure AD (HTTP Melhorado)<br>Após o registo, o cliente usa a assinatura de mensagens para provar a identidade do dispositivo | Para cenários centrados no utilizador, utilizando um dos seguintes métodos para provar a identidade do utilizador:<br> - Autenticação integrada no Windows<br> - Ficha do *utilizador* da AD Azure (HTTP Melhorado) |
| HTTPS    | Utilizando um dos seguintes métodos:<br> - Certificado PKI<br> - Autenticação integrada no Windows<br> - Ficha de *utilizador* ou *dispositivo* Azure AD | Pedido de localização: Anónimo<br>Pacote de cliente: Anónimo<br>Registo, utilizando um dos seguintes métodos para provar a identidade do dispositivo:<br> - Anónimo (aprovação manual)<br> - Autenticação integrada no Windows<br> - Certificado PKI<br> - Ficha de *utilizador* ou *dispositivo* Azure AD<br>Após o registo, o cliente usa a assinatura de mensagens para provar a identidade do dispositivo | Para cenários centrados no utilizador, utilizando um dos seguintes métodos para provar a identidade do utilizador:<br> - Autenticação integrada no Windows<br> - Ficha do *utilizador* da AD Azure |

> [!Tip]  
> Para obter mais informações sobre a configuração do ponto de gestão para diferentes tipos de identidade do dispositivo e com o gateway de gestão da nuvem, consulte O ponto de [gestão Enable para HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a>Comunicação de pontode distribuição do cliente

Quando um cliente comunica com um ponto de distribuição, só precisa de autenticar antes de descarregar o conteúdo. Utilize a tabela seguinte para entender como funciona este processo:

| Tipo DP  | Autenticação de cliente  |
|----------|---------|
| HTTP     | - Anónimo, se permitido<br>- Autenticação integrada pelo Windows com conta de computador ou conta de acesso à rede<br> - Ficha de acesso a conteúdos (HTTP melhorado) |
| HTTPS    | - Certificado PKI<br> - Autenticação integrada pelo Windows com conta de computador ou conta de acesso à rede<br> - Ficha de acesso a conteúdos |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>Considerações para comunicações de clientes da internet ou uma floresta não confiável

Para obter mais informações, veja os artigos seguintes:

- [Planear o gateway de gestão na cloud](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [Plano para gestão de clientes baseado na Internet](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a> Comunicação entre florestas do Active Directory  

O Gestor de Configuração suporta sites e hierarquias que abrangem as florestas de Diretório Ativo. Também suporta computadores de domínio que não estão na mesma floresta de Diretório Ativo que o servidor do site, e computadores que estão em grupos de trabalho.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a>Suporte computadores de domínio numa floresta que não é confiável pela floresta do seu servidor de site

- Instalar funções do sistema de sites nessa floresta não fidedigna, com a opção de publicar informações do site nessa floresta do Active Directory  

- Gerencie estes computadores como se fossem computadores de grupo de trabalho  

Quando instala servidores do sistema do site numa floresta de Diretório Ativo não confiável, a comunicação cliente-a-servidor dos clientes dessa floresta é mantida dentro dessa floresta, e o Gestor de Configuração pode autenticar o computador utilizando kerberos. Quando publica informações do site para a floresta do cliente, os clientes beneficiam de recuperar informações do site, como uma lista de pontos de gestão disponíveis, a partir da sua floresta de Diretório Ativo, em vez de descarregar essa informação a partir do ponto de gestão atribuído.  

> [!NOTE]  
> Se pretender gerir dispositivos que estejam na internet, pode instalar funções de sistema de site baseados na Internet na sua rede de perímetro quando os servidores do sistema do site estiverem numa floresta de Diretório Ativo. Este cenário não requer confiança bidirecional entre a rede do perímetro e a floresta do servidor do site.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a>Suporte computadores em um grupo de trabalho  

- Aprovar manualmente os computadores do grupo de trabalho quando utilizam ligações de cliente HTTP para as funções do sistema de sites. O Gestor de Configuração não pode autenticar estes computadores usando kerberos.  

- Configurar a Conta de Acesso à Rede para que estes computadores possam receber conteúdos dos pontos de distribuição.  

- Fornecer um mecanismo alternativo para que os clientes do grupo de trabalho localizem pontos de gestão. Utilize a publicação DNS, WINS ou atribua diretamente um ponto de gestão. Estes clientes não podem recuperar informações do site dos Serviços de Domínio de Diretório Ativo.  

Para obter mais informações, veja os artigos seguintes:  

- [Gerir registos contraditórios](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Conta de acesso à rede](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Como instalar clientes do Gestor de Configuração em computadores de grupo de trabalho](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Cenários para suportar um site ou uma hierarquia que abranja vários domínios e florestas  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Cenário 1: Comunicação entre locais numa hierarquia que abrange florestas

Este cenário requer uma confiança florestal bidirecional que apoie a autenticação kerberos.  Se você não tem um fundo florestal bidirecional que suporta a autenticação Kerberos, então o Gestor de Configuração não suporta um local de criança na floresta remota.  

O Gestor de Configuração suporta a instalação de um local infantil numa floresta remota que tenha a confiança necessária para dois sentidos com a floresta do local dos pais. Por exemplo, você pode colocar um local secundário em uma floresta diferente do seu local principal, desde que a confiança necessária exista.  

> [!NOTE]  
> Um site infantil pode ser um local primário (onde o site da administração central é o local dos pais) ou um local secundário.  

A comunicação intersite no Gestor de Configuração utiliza replicação de base de dados e transferências baseadas em ficheiros. Quando instalar um site, deve especificar uma conta para instalar o site no servidor designado. Esta conta também estabelece e mantém a comunicação entre sites. Depois de o site instalar e iniciar transferências baseadas em ficheiros e replicação de bases de dados, não precisa de configurar mais nada para comunicação ao site.  

Quando existe um fundo florestal bidirecional, o Gestor de Configuração não requer quaisquer passos de configuração adicionais.  

Por predefinição, quando instala um novo site infantil, o Gestor de Configuração configura os seguintes componentes:  

- Uma rota de replicação entre sites, baseada em ficheiros em cada site que utiliza a conta do computador servidor de sites. O Gestor de Configuração adiciona a conta de computador de cada computador ao **grupo&lt;SMS_SiteToSiteConnection_ sitecode\> ** no computador de destino.  

- Replicação de base de dados entre os Servidores SQL em cada site.  

Também definir as seguintes configurações:  

- As firewalls de intervenção e os dispositivos de rede devem permitir os pacotes de rede que o Gestor de Configuração necessita.  

- A resolução de nomes tem de funcionar entre as florestas.  

- Para instalar um site ou função do sistema de sites, terá de especificar uma conta com permissões de administrador local no computador especificado.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Cenário 2: Comunicação num local que abrange florestas

Este cenário não requer uma confiança florestal bidirecional.  

Os sites primários suportam a instalação de funções do sistema de sites em computadores em florestas remotas.  

- O ponto de serviço Web do Catálogo de Aplicações é a única exceção.  Só é suportado na mesma floresta que o servidor do site.  

- Quando uma função do sistema de site aceita ligações da internet, como uma boa prática de segurança, instale as funções do sistema do site num local onde o limite florestal fornece proteção para o servidor do site (por exemplo, numa rede de perímetro).  

Para instalar uma função do sistema de sites num computador numa floresta não fidedigna:  

- Especifique uma Conta de Instalação do **Sistema de Localização,** que o site utiliza para instalar a função do sistema do site. (Esta conta deve ter credenciais administrativas locais para se ligar a.) Em seguida, instale as funções do sistema do site no computador especificado.  

- Selecione a opção do sistema do site **Exigir que o servidor do site inicie ligações a este sistema de site**. Esta definição requer que o servidor do site estabeleça ligações ao servidor do sistema do site para transferir dados. Esta configuração impede que o computador no local não confiável inicie o contacto com o servidor do site que está dentro da sua rede fidedigna. Estas ligações utilizam a **Conta de Instalação do Sistema de Sites**.  

Ao utilizar uma função do sistema de sites que foi instalada numa floresta não fidedigna, as firewalls têm de permitir o tráfego de rede, mesmo quando o servidor do site inicia a transferência dos dados.  

Além disso, as seguintes funções do sistema de sites requerem acesso direto à base de dados do site. Por isso, as firewalls devem permitir o tráfego aplicável da floresta não confiável ao Servidor SQL do site:  

- Ponto de sincronização do Asset Intelligence  

- Ponto de Endpoint Protection  

- Ponto de inscrição  

- Ponto de gestão  

- Ponto do sistema de reporte  

- Ponto de Migração de Estado  

Para mais informações, consulte [as Portas utilizadas no Gestor](ports.md)de Configuração .  

Pode ser necessário configurar o ponto de gestão e o acesso ao ponto de inscrição na base de dados do site.

- Por padrão, quando instala estas funções, o Gestor de Configuração configura a conta de computador do novo servidor do sistema do site como a conta de ligação para a função do sistema do site. Em seguida, adiciona a conta à função de base de dados do SQL Server adequada.  

- Quando instalar estas funções do sistema do site num domínio não confiável, configure a conta de ligação ao sistema do site para permitir que a função do sistema do site obtenha informações a partir da base de dados.  

Se configurar uma conta de utilizador de domínio para ser a conta de ligação para estas funções do sistema do site, certifique-se de que a conta de utilizador de domínio tem acesso adequado à base de dados do Servidor SQL nesse site:  

- Ponto de gestão: **Conta de Ligação à Base de Dados do Ponto de Gestão**  

- Ponto de registo: **Conta de Ligação do Ponto de Registo**  

Ao planear funções do sistema de sites noutras florestas, considere as seguintes informações adicionais:  

- Se executar o Windows Firewall, configure os perfis de firewall aplicáveis para passar comunicações entre o servidor de base de dados do site e computadores que estão instalados com funções de sistema de site remoto.

- Quando o ponto de gestão baseado na Internet confia na floresta que contém as contas dos utilizadores, as políticas dos utilizadores são apoiadas. Se não existir qualquer fidedignidade, só são suportadas políticas de computador.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Cenário 3: Comunicação entre clientes e funções do sistema de site quando os clientes não estão na mesma floresta de Diretório Ativo que o seu servidor de site

O Gestor de Configuração suporta os seguintes cenários para clientes que não estão na mesma floresta que o servidor do site do seu site:  

- Há uma confiança florestal bidirecional entre a floresta do cliente e a floresta do servidor do site.  

- O servidor de funções do sistema de site está localizado na mesma floresta que o cliente.  

- O cliente está num computador de domínio que não tem uma confiança florestal bidirecional com o servidor do site, e as funções do sistema do site não estão instaladas na floresta do cliente.  

- O cliente está num computador de grupo de trabalho.  

Os clientes de um computador ligado ao domínio podem utilizar os Serviços de Domínio do Diretório Ativo para localização de serviço quando o seu site é publicado na sua floresta de Diretório Ativo.  

Para publicar informações do site para outra floresta de Diretório Ativo:  

- Especificar primeiro a floresta, ativando em seguida a publicação nessa floresta no nó **Florestas do Active Directory** da área de trabalho **Administração** .  

- Configurar cada site para publicar os respetivos dados nos Serviços de Domínio do Active Directory. Esta configuração permite aos clientes dessa floresta obter as informações de site e localizar pontos de gestão. Para clientes que não possam utilizar serviços de domínio de diretório ativo para localização de serviço, pode utilizar DNS, WINS ou o ponto de gestão atribuído ao cliente.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a>Cenário 4: Coloque o conector do Servidor de Câmbio numa floresta remota  

Para apoiar este cenário, certifique-se de que a resolução de nomes funciona entre as florestas. Por exemplo, configurar os avançados dNS. Quando configurar o conector do Exchange Server, especifique a intranet FQDN do Servidor de Câmbio. Para mais informações, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="see-also"></a>Consulte também

- [Plano de segurança](../security/plan-for-security.md)  

- [Segurança e privacidade para clientes do Gestor de Configuração](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
