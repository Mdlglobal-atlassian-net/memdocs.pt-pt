---
title: Referência técnica de controlos criptográficos
titleSuffix: Configuration Manager
description: Saiba como a assinatura e encriptação podem ajudar a proteger os ataques de dados de leitura no Gestor de Configuração.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623a8dab52e13c4674b961e825033430d34a8f88
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906551"
---
# <a name="cryptographic-controls-technical-reference"></a>Referência técnica de controlos criptográficos

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração utiliza a assinatura e a encriptação para ajudar a proteger a gestão dos dispositivos na hierarquia do Gestor de Configuração. Com a assinatura, se os dados foram alterados em trânsito, é descartado. A encriptação ajuda a evitar que um intruso leia os dados utilizando um analisador de protocolo de rede.  

 O algoritmo primário de hashing que o Gestor de Configuração usa para assinar é SHA-256. Quando dois sites do Gestor de Configuração comunicam entre si, assinam as suas comunicações com o SHA-256. O algoritmo de encriptação primário implementado no Gestor de Configuração é 3DES. Isto é utilizado para armazenar dados na base de dados do Gestor de Configuração e para a comunicação http do cliente. Quando utiliza a comunicação do cliente sobre HTTPS, pode configurar a sua infraestrutura de chaves públicas (PKI) para utilizar certificados RSA com os algoritmos de hashing máximos e comprimentos-chave que estão documentados nos requisitos de [certificado SKI](../network/pki-certificate-requirements.md).  

 Para a maioria das operações criptográficas para sistemas operativos baseados no Windows, o Gestor de Configuração utiliza algoritmos SHA-2, 3DES e AES e RSA da biblioteca Windows CryptoAPI rsaenh.dll.  

> [!IMPORTANT]  
>  Consulte as informações sobre as alterações recomendadas em resposta às vulnerabilidades SSL em [About SSL Vulnerabilities](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Controlos criptográficos para operações do Gestor de Configuração  
 As informações no Gestor de Configuração podem ser assinadas e encriptadas, quer utilize ou não certificados PKI com 'Gestor de Configuração'.  

### <a name="policy-signing-and-encryption"></a>Assinatura e encriptação de políticas  
 As atribuições de políticas de cliente são assinadas pelo certificado de assinatura autoassinado do servidor do site para ajudar a evitar o risco de segurança que representa o envio de políticas que tenham sido adulteradas por um ponto de gestão comprometido. Isto é importante se estiver a usar a gestão de clientes baseada na Internet porque este ambiente requer um ponto de gestão que esteja exposto à comunicação na Internet.  

 A política é encriptada com 3DES quando contém dados sensíveis. Políticas que contenham dados confidenciais são enviadas apenas para clientes autorizados. Políticas que não tenham dados confidenciais não são encriptadas.  

 Quando a política é armazenada nos clientes, é encriptada com interface de programação de aplicações de Proteção de Dados (DPAPI).  

### <a name="policy-hashing"></a>A política hashing  
 Quando os clientes do Gestor de Configuração solicitam a política, primeiro recebem uma atribuição de política para que saibam quais as políticas que lhes são aplicáveis, e depois solicitam apenas esses órgãos políticos. Cada atribuição de política contém o hash calculado para o corpo da política correspondente. O cliente obtém os corpos de políticas aplicáveis e calcula o hash desses corpos. Se o hash contido no corpo de política transferido não corresponder ao hash na atribuição de política, o cliente rejeita o corpo de política.  

 Os algoritmos hash para políticas são SHA-1 e SHA-256.  

### <a name="content-hashing"></a>Hashing de conteúdo  

O serviço de gestão de distribuição no servidor do site calcula o hash dos ficheiros de conteúdo de todos os pacotes. O fornecedor de política inclui o hash na política de distribuição de software. Quando o cliente do Gestor de Configuração descarrega o conteúdo, o cliente regenera o hash localmente e compara-o com o fornecido na apólice. Se os hashes coincidirem, o conteúdo não foi alterado e o cliente instala-o. Se um único byte do conteúdo tiver sido alterado, os hashes não coincidirão e o software não será instalado. Esta verificação ajuda a garantir que é instalado o software correto, uma vez que o conteúdo real é verificado em relação à política.  

O algoritmo hash predefinido para conteúdo é o SHA-256.

Nem todos os dispositivos suportam hash de conteúdo. As exceções incluem:  

- Clientes Windows, quando transmitem em fluxo conteúdo de App-V.  

- Os clientes do Windows Phone, embora estes clientes verifiquem a assinatura de uma aplicação que é assinada por uma fonte fidedigna.  

- O cliente do Windows RT, embora estes clientes verifiquem a assinatura de uma aplicação assinada por uma fonte fidedigna e também utilizam a validação do nome completo do pacote (PFN).  

- Os clientes executados em versões do Linux e UNIX que não suportam SHA-256. Para mais informações, consulte [Planplan para a implantação de clientes para computadores Linux e UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Assinatura e encriptação de inventário  
 O inventário que os clientes enviam para os pontos de gestão é sempre assinado pelos dispositivos, independentemente de comunicarem com os pontos de gestão por HTTP ou HTTPS. Se utilizarem HTTP, pode optar por encriptar estes dados, que é a melhor prática de segurança.  

### <a name="state-migration-encryption"></a>Encriptação da migração do Estado  
 Os dados armazenados em pontos de migração de estado da implementação de sistemas operativos são sempre encriptados pela Ferramenta de Migração de Estado de Utilizador (USMT) utilizando 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Encriptação para pacotes multicast para implantar sistemas operativos  
 Para cada pacote de implementação de sistema operativo, pode ativar a encriptação quando o pacote for transferido para computadores através da utilização de multicast. A encriptação utiliza a norma AES (Advanced Encryption Standard). Se ativar a encriptação, não é necessária qualquer configuração adicional de certificados. O ponto de distribuição de capacidade multicast gera automaticamente chaves simétricas para encriptar o pacote. Cada pacote tem uma chave de encriptação diferente. A chave é armazenada no ponto de distribuição de capacidade multicast utilizando APIs padrão do Windows. Quando o cliente liga à sessão multicast, a troca de chaves ocorre através de um canal encriptado com o certificado de autenticação de cliente emitido pela PKI (quando o cliente utilizar HTTPS) ou o certificado autoassinado (quando o cliente utilizar HTTP). O cliente armazena a chave na memória apenas durante a sessão multicast.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Encriptação para meios de comunicação para implantar sistemas operativos  
 Quando utiliza suportes de dados para implementar sistemas operativos e especifica uma palavra-passe para proteger os suportes de dados, as variáveis de ambiente são encriptadas utilizando AES (Advanced Encryption Standard). Outros dados existentes no suporte de dados, incluindo pacotes e conteúdo de aplicações, não estão encriptados.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Encriptação para conteúdo que é hospedado em pontos de distribuição baseados na nuvem  
 Começando pelo System Center 2012 Configuração Manager SP1, quando utiliza pontos de distribuição baseados na nuvem, o conteúdo que envia para estes pontos de distribuição é encriptado utilizando o Advanced Encryption Standard (AES) com um tamanho de chave de 256 bits. O conteúdo será novamente encriptado sempre que for atualizado. Quando os clientes transferirem o conteúdo, este será encriptado e protegido pela ligação HTTPS.  

### <a name="signing-in-software-updates"></a>Assinatura em atualizações de software  
 Todas as atualizações de software têm de ser assinadas por um fabricante fidedigno para proteção contra adulteração. Em computadores cliente, o Windows Update Agent (WUA) procura as atualizações no catálogo, mas não instalará uma atualização se não conseguir localizar o certificado digital no arquivo Fabricantes Fidedignos no computador local. Se tiver sido utilizado um certificado autoassinado para publicar as atualizações no catálogo, como o certificado autoassinado WSUS Publishers, este terá de constar também no arquivo de certificados Autoridades de Certificação de Raiz Fidedigna, no computador local, para verificação da validade do certificado. O WUA também verifica se a definição de Política de Grupo **Permitir conteúdo assinado da localização do serviço de atualização da Microsoft na intranet** está ativada no computador local. Esta definição de política tem de estar ativada para que o WUA procure atualizações criadas e publicadas com o Updates Publisher.  

 Quando as atualizações de software são publicadas no System Center Updates Publisher, são assinadas por um certificado digital quando são publicadas ou atualizadas num servidor. Pode especificar um certificado PKI ou configurar o Updates Publisher para gerar um certificado autoassinado para assinar a atualização de software.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Dados de configuração assinados para definições de conformidade  
 Quando importa dados de configuração, o Gestor de Configuração verifica a assinatura digital do ficheiro. Se os dados não tiverem sido assinados ou se a verificação da assinatura digital falhar, será apresentado um aviso e será perguntado se pretende continuar com a importação. Continue a importar os dados de configuração apenas se confiar explicitamente no fabricante e na integridade dos ficheiros.  

### <a name="encryption-and-hashing-for-client-notification"></a>Encriptação e hashing para notificação do cliente  
 Se utilizar notificações de cliente, todas as comunicações utilizarão TLS e a encriptação mais elevada que os sistemas operativos do servidor e do cliente possam negociar. Por exemplo, um computador cliente que executa o Windows 7 e um ponto de gestão que executa o Windows Server 2008 R2 pode suportar encriptação AES de 128 bits, enquanto um computador cliente que executa o Vista para o mesmo ponto de gestão irá negociar até encriptação 3DES. A mesma negociação ocorre para o hash dos pacotes que são transferidos durante a notificação do cliente, que utiliza SHA-1 ou SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificados utilizados pelo Gestor de Configuração  
 Para uma lista dos certificados de infraestrutura de chaves públicas (PKI) que podem ser utilizados pelo Gestor de Configuração, quaisquer requisitos ou limitações especiais, e como os certificados são utilizados, consulte [os requisitos do certificado PKI.](../network/pki-certificate-requirements.md) Esta lista inclui os comprimentos de chaves e algoritmos hash suportados. A maioria dos certificados suporta SHA-256 e chaves de 2048 bits.  

> [!NOTE]  
>  Todos os certificados que o Gestor de Configuração utiliza devem conter apenas caracteres de um único byte no nome do assunto ou nome alternativo do sujeito.  

 Os certificados PKI são necessários para os seguintes cenários:  

- Quando gere os clientes do Gestor de Configuração na Internet.  

- Quando gere os clientes do Gestor de Configuração em dispositivos móveis.  

- Quando gerir computadores Mac.  

- Quando utilizar pontos de distribuição baseados na nuvem.  

  Para a maioria das outras comunicações do Gestor de Configuração que requerem certificados para autenticação, assinatura ou encriptação, o Gestor de Configuração utiliza automaticamente os certificados PKI se estiverem disponíveis. Se não estiverem disponíveis, o Gestor de Configuração gera certificados auto-assinados.  

  O Gestor de Configuração não utiliza certificados PKI quando gere dispositivos móveis utilizando o conector Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Gestão de dispositivos móveis e certificados PKI  
 Se o dispositivo móvel não tiver sido bloqueado pelo operador móvel, pode utilizar o 'Configuração' ou o Microsoft Intune para solicitar e instalar um certificado de cliente. Este certificado fornece autenticação mútua entre o cliente nos sistemas de site do dispositivo móvel e do Gestor de Configuração ou nos serviços Microsoft Intune. Se o seu dispositivo móvel estiver bloqueado, não pode utilizar o 'Gestor de Configuração' ou o Intune para implementar certificados.  

 Se ativar o inventário de hardware para dispositivos móveis, O Gestor de Configuração ou o Intune também inventário os certificados que estão instalados no dispositivo móvel.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Implantação do sistema operativo e certificados PKI  
 Quando utiliza o Gestor de Configuração para implementar sistemas operativos e um ponto de gestão requer ligações ao cliente HTTPS, o computador cliente também deve ter um certificado para comunicar com o ponto de gestão, mesmo estando numa fase transitória, como o arranque de suportes de sequência de tarefas ou um ponto de distribuição ativado por PXE. Para suportar este cenário, deve criar um certificado de autenticação de cliente PKI e exportá-lo com a chave privada e, em seguida, importá-lo para as propriedades do servidor do site e também adicionar o certificado de CA raiz de confiança do ponto de gestão.  

 Se criar suportes de dados de arranque, importa o certificado de autenticação de cliente quando criar o suporte de dados de arranque. Configure uma palavra-passe no suporte de dados de arranque para ajudar a proteger a chave privada e outros dados confidenciais configurados na sequência de tarefas. Os computadores que iniciam a partir do suporte de dados de arranque irão apresentar o mesmo certificado ao ponto de gestão tal como necessário para as funções dos clientes, como o pedido de política de cliente.  

 Se estiver a utilizar o arranque PXE, importará o certificado de autenticação de cliente para o ponto de distribuição ativado com PXE, que utiliza o mesmo certificado para todos os clientes que iniciam a partir de um ponto de distribuição ativado com PXE. Como procedimento recomendado de segurança, solicite aos utilizadores que liguem os computadores a um serviço PXE para fornecer uma palavra-passe que ajude a proteger a chave privada e outros dados confidenciais nas sequências de tarefas.  

 Se algum destes certificados de autenticação de cliente for comprometido, bloqueie os certificados no nó **Certificados** na área de trabalho **Administração** , nó **Segurança** . Para gerir estes certificados, tem de ter a definição **Gerir certificado de implementação do sistema operativo** correta.  

 Após a implementação do sistema operativo e a instalação do Gestor de Configuração, o cliente exigirá o seu próprio certificado de autenticação de cliente PKI para comunicação do cliente HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Soluções de procuração ISV e certificados PKI  
 Os Fornecedores independentes de Software (ISVs) podem criar aplicações que alargam o Gestor de Configuração. Por exemplo, um ISV poderia criar extensões para suportar plataformas de cliente não Windows, tais como computadores Macintosh ou UNIX. No entanto, se os sistemas de sites precisarem de ligações cliente HTTPS, estes clientes têm também de utilizar certificados KPI para a comunicação com o site. O Gestor de Configuração inclui a capacidade de atribuir um certificado ao representante do ISV que permite comunicações entre os clientes proxy isv e o ponto de gestão. Se utilizar extensões que requerem certificados de proxy ISV, consulte a documentação desse produto. Para obter mais informações sobre como criar certificados de procuração ISV, consulte o Kit de Desenvolvedor de Software do Gestor de Configuração (SDK).  

 Se o certificado ISV for comprometido, bloqueie o certificado no nó **Certificados** na área de trabalho **Administração** , nó **Segurança** .  

### <a name="asset-intelligence-and-certificates"></a>Inteligência de ativos e certificados  
 O Gestor de Configuração instala com um certificado X.509 que o ponto de sincronização da Inteligência de Ativos utiliza para ligar à Microsoft. O Gestor de Configuração utiliza este certificado para solicitar um certificado de autenticação do cliente do serviço de certificados da Microsoft. O certificado de autenticação de cliente é instalado no servidor de sistema de site do ponto de sincronização do Asset Intelligence e é utilizado para autenticar o servidor para a Microsoft. O Configuration Manager utiliza o certificado de autenticação de cliente para transferir o catálogo do Asset Intelligence e para carregar os títulos de software.  

 Este certificado tem um comprimento de chave de 1024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Pontos e certificados de distribuição baseados na nuvem  
 Começando pelo System Center 2012 Configuration Manager SP1, os pontos de distribuição baseados na nuvem requerem um certificado de gestão (auto-assinado ou PKI) que você envia para o Microsoft Azure. Este certificado de gestão requer a capacidade de autenticação de servidor e um comprimento de chave do certificado de 2048 bits. Além disso, é necessário configurar um certificado de serviço para cada ponto de distribuição baseado na nuvem, que não pode ser autoassinado mas tem de ter capacidade de autenticação de servidor e um comprimento de chave do certificado mínimo de 2048 bits.  

> [!NOTE]  
>  O certificado de gestão autoassinado destina-se apenas a fins de teste e não se destina a utilização em redes de produção.  

 Os clientes não necessitam de um certificado PKI de cliente para utilizarem pontos de distribuição baseados na nuvem; eles procedem à autenticação para a gestão através da utilização de um certificado autoassinado ou um certificado PKI de cliente. O ponto de gestão emite então um token de acesso ao cliente, que o cliente apresenta ao ponto de distribuição baseado na nuvem. O token é válido durante 8 horas.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>O Conector Intune microsoft e os certificados  
 Quando o Microsoft Intune inscreveu dispositivos móveis, pode gerir estes dispositivos móveis no 'Configuração Manager' criando um conector Microsoft Intune. O conector utiliza um certificado PKI com capacidade de autenticação do cliente para autenticar o Gestor de Configuração para o Microsoft Intune e transferir todas as informações entre eles utilizando o SSL. A chave do certificado tem o tamanho de 2048 bits e utiliza o algoritmo hash SHA-1.  

 Quando o conector é instalado, é criado um certificado de assinatura e armazenado no servidor do site para chaves de sideload e é criado um certificado de encriptação e armazenado no ponto de registo de certificados para encriptar o desafio SCEP (Simple Certificate Enrollment Protocol). Estes certificados também têm um tamanho de chave de 2048 bits e utilizam o algoritmo hash SHA-1.  

 Quando a Intune inscreveu dispositivos móveis, instala um certificado PKI no dispositivo móvel. Este certificado tem capacidade de autenticação de cliente, utiliza um tamanho de chave de 2048 bits e utiliza o algoritmo hash SHA-1.  

 Estes certificados PKI são automaticamente solicitados, gerados e instalados pela Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>CRL verificação de certificados PKI  
 Uma lista de revogação de certificados PKI (CRL) aumenta a sobrecarga administrativa e de processamento, mas apresenta mais segurança. No entanto, se a verificação CRL está ativada, mas a CRL está inacessível, a ligação de PKI falha. Para mais informações, consulte Segurança e privacidade para O Gestor de [Configuração](security-and-privacy.md).  

 A verificação da lista de revogação de certificados (CRL) está ativada por predefinição no IIS, por isso, se estiver a utilizar um CRL com a sua implementação PKI, não há nada adicional para configurar na maioria dos sistemas de site do Gestor de Configuração que executam o IIS. A exceção é para atualizações de software, que requerem um passo manual para ativar a verificação CRL para verificar as assinaturas nos ficheiros de atualização de software.  

 A verificação CRL está ativada por predefinição para computadores cliente quando utilizam ligações de cliente HTTPS. Não é possível desativar a verificação de CRL para clientes em computadores Mac em SP1, gestor de configuração ou posterior.  

 A verificação do CRL não é suportada para as seguintes ligações no Gestor de Configuração:  

-   Ligações de servidor a servidor.  

-   Dispositivos móveis matriculados pelo Gestor de Configuração.  

-   Dispositivos móveis matriculados pela Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Controlos criptográficos para a comunicação do servidor  
 O Gestor de Configuração utiliza os seguintes controlos criptográficos para a comunicação do servidor.  

### <a name="server-communication-within-a-site"></a>Comunicação do servidor dentro de um site  
 Cada servidor do sistema do site utiliza um certificado para transferir dados para outros sistemas de site no mesmo site do Gestor de Configuração. Algumas funções de sistema do site também utilizam certificados para autenticação. Por exemplo, se instalar o ponto proxy de registo num servidor e o ponto de registo noutro servidor, eles podem autenticar-se entre si utilizando este certificado de identidade. Quando o Gestor de Configuração utiliza um certificado para esta comunicação, se houver um certificado PKI disponível que tenha capacidade de autenticação do servidor, o Gestor de Configuração utiliza-o automaticamente; se não, o Gestor de Configuração gera um certificado auto-assinado. Este certificado autoassinado tem capacidade de autenticação de servidor, utiliza SHA-256 e tem um comprimento de chave de 2048 bits. O Gestor de Configuração copia o certificado para a loja Pessoas Fidedignas em outros servidores do sistema de sites que podem precisar de confiar no sistema do site. Os sistemas de sites podem depois confiar um do outro utilizando estes certificados e PeerTrust.  

 Além deste certificado para cada servidor de sistema de site, o Gestor de Configuração gera um certificado auto-assinado para a maioria das funções do sistema do site. Quando existe mais do que uma instância da função de sistema do site no mesmo site, elas partilham o mesmo certificado. Por exemplo, pode ter vários pontos de gestão ou vários pontos de registo no mesmo site. Este certificado autoassinado também utiliza SHA-256 e tem um comprimento de chave de 2048 bits. É também copiado para o Arquivo de Pessoas Fidedignas nos servidores de sistema do site que poderão necessitar de confiar nele. As seguintes funções de sistema do site geram este certificado:  

- Ponto de serviço Web do Catálogo de Aplicações  

- Ponto de Web site do Catálogo de Aplicações  

- Ponto de sincronização do Asset Intelligence  

- Ponto de registo de certificados  

- Ponto de Endpoint Protection  

- Ponto de inscrição  

- Ponto de estado de contingência  

- Ponto de gestão  

- Ponto de distribuição com multicast ativado  

- Ponto do Reporting Services  

- Ponto de atualização de software  

- Ponto de Migração de Estado  

- Conector do Microsoft Intune  

Estes certificados são geridos automaticamente pelo Gestor de Configuração e, se necessário, gerados automaticamente.  

O Gestor de Configuração também utiliza um certificado de autenticação do cliente para enviar mensagens de estado do ponto de distribuição para o ponto de gestão. Quando o ponto de gestão está configurado apenas para ligações de cliente HTTPS, é necessário utilizar um certificado PKI. Se o ponto de gestão aceita ligações HTTP, é possível utilizar um certificado PKI ou selecionar a opção para utilizar um certificado autoassinado que tenha capacidade de autenticação de cliente, utilize SHA-256 e tenha um comprimento de chave de 2048 bits.  

### <a name="server-communication-between-sites"></a>Comunicação do servidor entre sites  
 O Gestor de Configuração transfere dados entre sites utilizando a replicação da base de dados e a replicação baseada em ficheiros. Para mais informações, consulte [comunicações entre pontos finais](../hierarchy/communications-between-endpoints.md).  

 O Gestor de Configuração configura automaticamente a replicação da base de dados entre os sites e utiliza certificados PKI que possuam capacidade de autenticação do servidor se estes estiverem disponíveis; caso contrário, o Gestor de Configuração cria certificados auto-assinados para autenticação do servidor. Em ambos os casos, a autenticação entre sites é estabelecida utilizando os certificados do Arquivo de Pessoas Fidedignas que utilize PeerTrust. Esta loja de certificados é utilizada para garantir que apenas os computadores SQL Server que são utilizados pela hierarquia do Gestor de Configuração participam na replicação site-a-site. Enquanto os sites primários e o site de administração central podem replicar alterações à configuração de todos os sites na hierarquia, os sites secundários podem replicar alterações à configuração apenas do respetivo site principal.  

 Os servidores de site estabelecem comunicação site a site através da utilização de uma troca de chaves segura que ocorre automaticamente. O servidor de site remetente gera um hash e assina-o com a respetiva chave privada. O servidor de site recetor verifica a assinatura, utilizando a chave pública e compara o hash com um valor gerado localmente. Se coincidirem, o site recetor aceita os dados replicados. Se os valores não coincidirem, o Gestor de Configuração rejeita os dados de replicação.  

 A replicação da base de dados no Gestor de Configuração utiliza o Corretor de Serviços de Servidor EsqL para transferir dados entre os sites utilizando os seguintes mecanismos:  

- Ligação SQL Server a SQL Server: esta opção utiliza as credenciais do Windows para autenticação de servidor e certificados autoassinados com 1024 bits, para assinar e encriptar os dados utilizando a norma AES (Advanced Encryption Standard). Se existirem certificados PKI com capacidade de autenticação de servidor disponíveis, serão utilizados. O certificado tem de estar localizado no arquivo Pessoal para o arquivo de certificados de Computador.  

- SQL Service Broker: esta opção utiliza os certificados autoassinados com 2048 bits para assinar e encriptar os dados utilizando a norma AES (Advanced Encryption Standard). O certificado tem de estar localizado na base de dados mestre do SQL Server.  

  A replicação baseada em ficheiros utiliza o protocolo Bloco de Mensagem de Servidor (SMB) e utiliza SHA-256 para assinar estes dados que não estão encriptados mas não contêm dados confidenciais. Se pretender encriptar estes dados, pode utilizar o IPsec e deverá implementá-lo de forma independente a partir do 'Gestor de Configuração'.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Controlos criptográficos para clientes que utilizam comunicação HTTPS para sistemas de sites  
 Quando as funções de sistema do site aceitam ligações de cliente, pode configurá-las para aceitarem ligações HTTPS e HTTP ou apenas ligações HTTPS. As funções de sistema do site que aceitam ligações a partir da Internet só aceitam ligações de cliente através de HTTPS.  

 As ligações de cliente através de HTTPS oferecem um nível mais elevado de segurança, integrando com uma infraestrutura de chaves públicas (PKI), para ajudar a proteger a comunicação cliente-servidor. No entanto, configurar ligações de cliente HTTPS sem conhecimentos abrangentes de planeamento, implementação e operações PKI poderia deixá-lo vulnerável. Por exemplo, se não proteger a AC raiz, as pessoas mal intencionadas poderão comprometer a confiança de toda a sua infraestrutura PKI. Não conseguir implementar e gerir os certificados PKI utilizando processos controlados e seguros poderá ter como resultado clientes não geridos que não recebem atualizações ou pacotes de software críticos.  

> [!IMPORTANT]  
>  Os certificados PKI que são utilizados na comunicação de cliente protegem a comunicação apenas entre o cliente e alguns sistemas de sites. Não protegem o canal de comunicação entre o servidor de site e os sistemas de sites ou entre servidores de site.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Comunicação que não é encriptada quando os clientes usam comunicação HTTPS  
 Quando os clientes comunicam com sistemas de sites utilizando HTTPS, as comunicações são geralmente encriptadas através de SSL. No entanto, nas seguintes situações, os clientes comunicam com sistemas de sites sem utilizar a encriptação:  

- O cliente não consegue efetuar uma ligação HTTPS através da intranet e reverter para a utilização de HTTP quando os sistemas de sites permitem esta configuração  

- Comunicação para as seguintes funções de sistema do site:  

  -   O cliente envia mensagens de estado para o ponto de estado de contingência  

  -   O cliente envia pedidos PXE para um ponto de distribuição com PXE ativado  

  -   O cliente envia dados de notificação para um ponto de gestão  

  Os pontos do Reporting Services estão configurados para utilizar HTTP ou HTTPS independentemente do modo de comunicação do cliente.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Controlos criptográficos para clientes chat usam comunicação HTTP para sistemas de site  
 Quando os clientes utilizam a comunicação HTTP para as funções do sistema de site, podem usar certificados PKI para autenticação do cliente, ou certificados auto-assinados que o Gestor de Configuração gera. Quando o Gestor de Configuração gera certificados auto-assinados, eles têm um identificador de objeto personalizado para a assinatura e encriptação, e estes certificados são usados para identificar exclusivamente o cliente. Para todos os sistemas operativos suportados exceto o Windows Server 2003, estes certificados autoassinados utilizam SHA-256 e têm um comprimento de chave de 2048 bits. Para o Windows Server 2003, é utilizado SHA1 com um comprimento de chave de 1024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Implantação do sistema operativo e certificados auto-assinados  
 Quando utiliza o Gestor de Configuração para implantar sistemas operativos com certificados auto-assinados, um computador cliente também deve ter um certificado para comunicar com o ponto de gestão, mesmo que o computador esteja numa fase de transição, como o arranque de meios de sequência de tarefas ou um ponto de distribuição ativado por PXE. Para suportar este cenário para ligações ao cliente HTTP, o Gestor de Configuração gera certificados auto-assinados que têm um identificador de objeto personalizado para a assinatura e encriptação, e estes certificados são usados para identificar exclusivamente o cliente. Para todos os sistemas operativos suportados exceto o Windows Server 2003, estes certificados autoassinados utilizam SHA-256 e têm um comprimento de chave de 2048 bits. Para o Windows Server 2003, é utilizado SHA1 com um comprimento de chave de 1024 bits. Se estes certificados autoassinados forem comprometidos, para impedir a sua utilização por atacantes para representar clientes fidedignos, bloqueie os certificados no nó **Certificados** da área de trabalho **Administração** , nó **Segurança** .  

### <a name="client-and-server-authentication"></a>Autenticação de cliente e servidor  
 Quando os clientes se ligam ao HTTP, autenticam os pontos de gestão utilizando serviços de domínio de diretório ativo ou utilizando a chave raiz fidedigna do Gestor de Configuração. Os clientes não autenticam outras funções de sistema de sites, como pontos de migração de estado ou pontos de atualização de software.  

 Quando um ponto de gestão autentica pela primeira vez um cliente utilizando o certificado de cliente autoassinado, este mecanismo fornece uma segurança mínima porque qualquer computador pode gerar um certificado autoassinado. Neste cenário, o processo de identificação de clientes tem de ser aumentado mediante aprovação. Apenas computadores fidedignos devem ser aprovados, automaticamente pelo Gestor de Configuração, ou manualmente, por um utilizador administrativo. Para mais informações, consulte a secção de aprovação nas [Comunicações entre pontos finais](../hierarchy/communications-between-endpoints.md).  

## <a name="about-ssl-vulnerabilities"></a>Sobre as vulnerabilidades SSL
Para melhorar a segurança dos seus clientes e servidores do Gestor de Configuração, faça o seguinte:

- Ativar o TLS 1.2

  Para ativar o TLS 1.2 para o Gestor de Configuração, consulte [como ativar o TLS 1.2 para o Gestor](enable-tls-1-2.md)de Configuração .
- Desativar SSL 3.0, TLS 1.0 e TLS 1.1 
- Reencomende as suítes cifrarelacionadas com TLS 

Para mais informações, consulte [Como restringir o uso de certos algoritmos e protocolos criptográficos em Schannel.dll](https://support.microsoft.com/help/245030/) e [Prioritizing Schannel Cipher Suites](https://docs.microsoft.com/windows/win32/secauthn/prioritizing-schannel-cipher-suites). Estes procedimentos não afetam a funcionalidade do Gestor de Configuração.

