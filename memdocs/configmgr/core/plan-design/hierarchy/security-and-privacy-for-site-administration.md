---
title: Segurança e privacidade da administração do site
titleSuffix: Configuration Manager
description: Otimizar a segurança e privacidade para a administração do site em Configuração Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182264"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Segurança e privacidade para administração do site em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo contém informações de segurança e privacidade para sites de Configuração Manager e a hierarquia.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a>Orientação de segurança para a administração do site

Utilize as seguintes orientações para o ajudar a garantir os sites do Gestor de Configuração e a hierarquia.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Executar configuração a partir de uma fonte confiável e comunicação segura

Para ajudar a evitar que alguém adulterar os ficheiros de origem, execute a configuração do Gestor de Configuração a partir de uma fonte fidedigna. Se armazenar os ficheiros na rede, proteja a localização de rede.  

Se executar a configuração a partir de um local de rede, para ajudar a evitar que um intruso adulterar os ficheiros à medida que são transmitidos através da rede, utilize a assinatura IPsec ou SMB entre a localização de origem dos ficheiros de configuração e o servidor do site.  

Se utilizar o Downloader de Configuração para descarregar os ficheiros que são necessários por configuração, certifique-se de que protege a localização onde estes ficheiros estão armazenados. Também proteja o canal de comunicação para este local quando executar a configuração.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Alargar o esquema de Diretório Ativo e publicar sites ao domínio  

As extensões de Schema não são necessárias para executar o Gestor de Configuração, mas criam um ambiente mais seguro. Os clientes e servidores do site podem obter informações de uma fonte fidedigna.  

Se os clientes estiverem num domínio não confiável, implemente as seguintes funções do sistema de site nos domínios dos clientes:  

- Ponto de gestão  

- Ponto de distribuição  

> [!NOTE]  
> Um domínio de confiança para o Gestor de Configuração requer a autenticação kerberos. Se os clientes estão em outra floresta que não tem uma confiança florestal bidirecional com a floresta do servidor do site, estes clientes são considerados como estando num domínio não confiável. Uma confiança externa não é suficiente para este fim.  

### <a name="use-ipsec-to-secure-communications"></a>Use iPsec para garantir comunicações

Embora o Gestor de Configuração proteja a comunicação entre o servidor do site e o computador que executa o Servidor SQL, o Gestor de Configuração não protege as comunicações entre as funções do sistema do site e o Servidor SQL. Só é possível configurar alguns sistemas de site com HTTPS para comunicação intralocal.  

Se não utilizar controlos adicionais para proteger estes canais servidor-a-servidor, os atacantes podem usar vários ataques de falsificação e ataques man-in-the-middle contra sistemas do site. Use a assinatura SMB quando não pode usar IPsec.  

> [!Important]  
> Proteja o canal de comunicação entre o servidor do site e o servidor de origem do pacote. Esta comunicação utiliza SMB. Se não puder utilizar o IPsec para proteger esta comunicação, utilize a assinatura SMB para se certificar de que os ficheiros não são adulterados antes de os clientes os descarregarem e executarem.  

### <a name="dont-change-the-default-security-groups"></a>Não mude os grupos de segurança padrão

Não altere os seguintes grupos de segurança que o Gestor de Configuração cria e gere para a comunicação do sistema do site:

- **código&lt;de site SMS_SiteSystemToSiteServerConnection_MP_\>**  

- **código&lt;de site SMS_SiteSystemToSiteServerConnection_SMSProv_\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

O Gestor de Configuração cria e gere automaticamente estes grupos de segurança. Este comportamento inclui a remoção de contas de computador quando uma função do sistema do site é removida.  

Para garantir a continuidade do serviço e menos privilégios, não edite manualmente estes grupos.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Gerir o processo de fornecimento de raiz de confiança

Se os clientes não puderem consultar o catálogo global de informações do Gestor de Configuração, devem confiar na chave de raiz fidedigna para autenticar pontos de gestão válidos. A chave de raiz de confiança está armazenada no registo do cliente. Pode ser definido utilizando a política de grupo ou a configuração manual.  

Se o cliente não tiver uma cópia da chave raiz de confiança antes de contactar pela primeira vez um ponto de gestão, confia no primeiro ponto de gestão com que comunica. Para reduzir o risco de um atacante direcionar os clientes para um ponto de gestão não autorizado, pode aprovisionar previamente os clientes com a chave de raiz fidedigna. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Utilize números de porta não predefinidos

A utilização de números de porta não predefinidos pode fornecer segurança adicional. Dificultam a exploração do ambiente por parte dos atacantes. Se decidir utilizar portas não predefinidas, planeie-as antes de instalar o 'Gestor de Configuração'. Use-os consistentemente em todos os locais da hierarquia. As portas de pedido do cliente e wake on LAN são exemplos onde você pode usar números de porta não padrão.  

### <a name="use-role-separation-on-site-systems"></a>Utilizar a separação de papéis nos sistemas do local

Embora possa instalar todas as funções do sistema do site num único computador, esta prática raramente é usada em redes de produção. Cria um único ponto de falha.  

### <a name="reduce-the-attack-profile"></a>Reduza o perfil de ataque

Isolar cada função do sistema de site num servidor diferente reduz a hipótese de um ataque contra vulnerabilidades num sistema de site poder ser usado contra um sistema de site diferente. Muitas funções requerem a instalação de Serviços de Informação da Internet (IIS) no sistema de site, o que precisa de aumentar a superfície de ataque. Se tiver de combinar funções para reduzir as despesas de hardware, combine funções IIS apenas com outras funções que exijam IIS.  

> [!IMPORTANT]  
> O papel do ponto de recuo é uma exceção. Uma vez que esta função do sistema de site aceita dados não autenticados dos clientes, não atribui a função de ponto de recuo a qualquer outra função do sistema do Site Do Gestor de Configuração.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Configurar endereços IP estáticos para sistemas de site

Os endereços IP estáticos são mais fáceis de proteger contra ataques de resolução de nomes.  

Os endereços IP estáticos também facilitam a configuração do IPsec. A utilização do IPsec é uma boa prática de segurança para garantir a comunicação entre os sistemas do site no Gestor de Configuração.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Não instale outras aplicações nos servidores do sistema do site

Quando instala outras aplicações nos servidores do sistema do site, aumenta a superfície de ataque para O Gestor de Configuração. Também arrisca problemas de incompatibilidade.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Exigir a assinatura e ativar a encriptação como uma opção do site

Ative as opções de assinatura e encriptação para o site. Certifique-se de que todos os clientes podem suportar o algoritmo de hash SHA-256 e, em seguida, ativar a opção de **Exigir SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Restringir e monitorizar os utilizadores administrativos

Conceda acesso administrativo ao Gestor de Configuração apenas aos utilizadores em quem confia. Em seguida, conceda-lhes permissões mínimas utilizando as funções de segurança incorporadas ou personalizando as funções de segurança. Os utilizadores administrativos que possam criar, modificar e implementar software e configurações podem potencialmente controlar dispositivos na hierarquia do Gestor de Configuração.  

Realize auditorias periódicas às atribuições dos utilizadores administrativos e ao respetivo nível de autorização para verificar as alterações necessárias.  

Para mais informações, consulte a [configuração da administração baseada em papéis](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Backups do Gestor de Configuração Segura

Ao fazer o backup Do Gestor de Configuração, estas informações incluem certificados e outros dados sensíveis que podem ser utilizados por um intruso para personificação.  

Utilize a assinatura SMB ou IPsec quando transferir estes dados através da rede e proteja a localização das cópias de segurança.  

### <a name="secure-locations-for-exported-objects"></a>Locais seguros para objetos exportados

Sempre que exportar ou importar objetos da consola do Gestor de Configuração para um local de rede, proteja a localização e proteja o canal de rede.

Limite quem pode aceder à pasta de rede.  

Para evitar que um intruso adulterar os dados exportados, utilize a assinatura SMB ou o IPsec entre a localização da rede e o servidor do site. Também proteja a comunicação entre o computador que executa a consola do Gestor de Configuração e o servidor do site. Utilize IPsec para encriptar os dados na rede para evitar a divulgação de informações.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Remova manualmente os certificados dos servidores falhados

Se um sistema de site não estiver desinstalado corretamente, ou parar de funcionar e não puder ser restaurado, remova manualmente os certificados do Gestor de Configuração para este servidor de outros servidores do Gestor de Configuração.

Para remover a confiança dos pares que foi originalmente estabelecida com o sistema de site e funções do sistema do site, remova manualmente os certificados do Gestor de Configuração para o servidor falhado na loja de **certificados Pessoas Fidedignas** em outros servidores do sistema do site. Esta ação é importante se reutilizar o servidor sem o reformar.  

Para obter mais informações, consulte [os controlos criptográficos para a comunicação do servidor](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Não configure sistemas de sites baseados na Internet para fazer a ponte entre a rede do perímetro

Não configure os servidores do sistema do site para serem multi-alojados de modo a que se conectem à rede do perímetro e à intranet. Embora esta configuração permita que os sistemas de sites baseados na Internet aceitem ligações de clientes a partir da internet e da intranet, elimina uma fronteira de segurança entre a rede do perímetro e a intranet.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Configure o servidor do site para iniciar ligações às redes de perímetro

Se um sistema de site estiver numa rede não confiável, como uma rede de perímetro, configure o servidor do site para iniciar ligações ao sistema do site.

Por padrão, os sistemas do site iniciam ligações ao servidor do site para transferir dados. Esta configuração pode ser um risco de segurança quando o início da ligação é de uma rede não confiável para a rede fidedigna. Quando os sistemas do site aceitam ligações a partir da internet, ou residem numa floresta não confiável, configure a opção do sistema do site para **exigir que o servidor do site inicie ligações a este sistema de site**. Após a instalação do sistema do site e quaisquer funções, todas as ligações são iniciadas pelo servidor do site a partir da rede fidedigna.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Utilize pontes E terminações SSL com autenticação

Se utilizar um servidor de procuração web para gestão de clientes baseado na Internet, utilize a ponte SSL para o SSL, utilizando a rescisão com autenticação.

Quando configura a rescisão do SSL no servidor web proxy, os pacotes da internet estão sujeitos a inspeção antes de serem encaminhados para a rede interna. O servidor web proxy autentica a ligação do cliente, termina-a e abre uma nova ligação autenticada aos sistemas de sites baseados na Internet.  

Quando os computadores clientes do Gestor de Configuração utilizam um servidor web proxy para se conectarem a sistemas de site baseados na Internet, a identidade do cliente (GUID) está seguramente contida na carga útil do pacote. Então o ponto de gestão não considera o servidor web proxy como o cliente.

Se o seu servidor web proxy não conseguir suportar os requisitos para a ponte SSL, o túnel SSL também é suportado. Esta opção é menos segura. Os pacotes SSL da internet são encaminhados para os sistemas do site sem rescisão. Então não podem ser inspecionados por conteúdo malicioso.  

> [!WARNING]  
> Os dispositivos móveis que são matriculados pelo Gestor de Configuração não podem utilizar a ponte SSL. Só devem usar túneis SSL.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Configurações a utilizar se configurar o site para acordar computadores para instalar software

- Se utilizar pacotes tradicionais de despertar, utilize transmissões unicast em vez de transmissões dirigidas por sub-rede.  

- Se tiver de utilizar transmissões direcionadas para subredes, configure os routers para permitir transmissões direcionadas apenas a partir do servidor do site e apenas num número de porta não predefinido.  

Para obter mais informações sobre as diferentes tecnologias Wake On LAN, consulte [O Planeamento como acordar os clientes.](../../clients/deploy/plan/plan-wake-up-clients.md)

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Se utilizar a notificação de e-mail, configure o acesso autenticado ao servidor de correio SMTP

Sempre que possível, utilize um servidor de correio que suporte o acesso autenticado. Utilize a conta de computador do servidor do site para autenticação. Se tiver de especificar uma conta de utilizador para autenticação, utilize uma conta que tenha privilégios mínimos. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>Impor a ligação do canal LDAP e a assinatura lDAP

A segurança dos controladores de domínio do Diretório Ativo pode ser melhorada configurando o servidor para rejeitar ligações LDAP de Autenticação Simples e Camada de Segurança (SASL) que não solicitam a assinatura ou rejeitam ligações simples LDAP que são realizadas numa ligação de texto clara. A partir da versão 1910, o Gestor de Configuração suporta a aplicação da ligação do canal LDAP e a assinatura lDAP. Para mais informações, consulte os requisitos de [ligação do canal LDAP 2020 e os requisitos de assinatura LDAP para windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a>Orientação de segurança para o servidor do site

Utilize as seguintes orientações para o ajudar a proteger o servidor do site do Gestor de Configuração.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Instale o Gestor de Configuração num servidor membro em vez de um controlador de domínio

O servidor do site do Gestor de Configuração e os sistemas de site não requerem instalação num controlador de domínio. Os controladores de domínio não têm uma base de dados local de Gestão de Contas de Segurança (SAM) que não seja a base de dados de domínio. Quando instala o Gestor de Configuração num servidor membro, pode manter as contas do Gestor de Configuração na base de dados Local SAM e não na base de dados de domínio.  

Esta prática também reduz a superfície de ataque nos controladores de domínio.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Instale sites secundários sem copiar os ficheiros sobre a rede

Quando executar a configuração e criar um site secundário, não selecione a opção de copiar os ficheiros do site principal para o site secundário. Também não utilize uma localização de origem de rede. Quando copias ficheiros sobre a rede, um intruso especializado pode sequestrar o pacote de instalação do local secundário e adulterar os ficheiros antes de serem instalados. Cronometrar este ataque seria difícil. Este ataque pode ser atenuado utilizando IPsec ou SMB quando transferir os ficheiros.  

Em vez de copiar os ficheiros sobre a rede, no servidor de site secundário, copie os ficheiros de origem da pasta dos media para uma pasta local. Em seguida, quando executar a configuração para criar um site secundário, na página De Ficheiros fonte de **instalação,** selecione **Utilize os ficheiros de origem no seguinte local no computador do site secundário (mais seguro)** e especifique esta pasta.  

Para mais informações, consulte [Instale um site secundário](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>Instalação de funções do local herda permissões da raiz de unidade

<!-- SCCMDocs#1380 -->
Certifique-se de configurar corretamente as permissões de acionamento do sistema antes de instalar a primeira função do sistema do site em qualquer servidor. Por exemplo, `C:\SMS_CCM` herda `C:\`permissões de . Se a raiz da unidade não estiver devidamente protegida, os utilizadores de baixos direitos poderão aceder ou modificar conteúdo na pasta 'Gestor de Configuração'.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a>Orientação de segurança para O Servidor SQL

O Gestor de Configuração utiliza o SQL Server como base de dados de back-end. Se a base de dados estiver comprometida, os atacantes podem contornar o Diretor de Configuração. Se acederem diretamente ao SQL Server, podem lançar ataques através do 'Gestor de Configuração'. Considere os ataques contra o SQL Server como de alto risco e atenuar adequadamente.  

Utilize as seguintes orientações de segurança para ajudá-lo a garantir o Servidor SQL para O Gestor de Configuração.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Não utilize o servidor de base de dados do Site Do Gestor de Configuração para executar outras aplicações do SQL Server

Ao aumentar o acesso ao servidor de base de dados do Site Do Gestor de Configuração, esta ação aumenta o risco para os dados do seu Gestor de Configuração. Se a base de dados do site do Gestor de Configuração estiver comprometida, outras aplicações no mesmo computador SQL Server também são colocadas em risco.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Configure o Servidor SQL para utilizar a autenticação do Windows

Embora o Gestor de Configuração aceda à base de dados do site utilizando uma conta Windows e a autenticação do Windows, ainda é possível configurar o Servidor SQL para utilizar o modo misto do Servidor SQL. O modo misto Do Servidor SQL permite que os sign-ins SQL adicionais acedam à base de dados. Esta configuração não é necessária e aumenta a superfície de ataque.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Atualizar O SQL Server Express em sites secundários

Quando instala um site primário, o Gestor de Configuração descarrega o SQL Server Express do Microsoft Download Center. Em seguida, copia os ficheiros para o servidor do site principal. Quando instala um site secundário e seleciona a opção que instala o SQL Server Express, o Gestor de Configuração instala a versão previamente descarregada. Não verifica se existem novas versões disponíveis. Para se certificar de que o site secundário tem as versões mais recentes, faça uma das seguintes tarefas:  

- Depois de instalar o site secundário, execute o Windows Update no servidor do site secundário.  

- Antes de instalar o site secundário, instale manualmente o SQL Server Express no servidor de site secundário. Certifique-se de que instala a versão mais recente e quaisquer atualizações de software. Em seguida, instale o site secundário e selecione a opção de utilizar uma instância de Servidor SQL existente.  

Executa periodicamente o Windows Update para todas as versões instaladas do Servidor SQL. Esta prática garante que têm as mais recentes atualizações de software.  

### <a name="follow-general-guidance-for-sql-server"></a>Siga as orientações gerais para o Servidor SQL

Identifique e siga a orientação geral para a sua versão do Servidor SQL. No entanto, tome em consideração os seguintes requisitos para o Gestor de Configuração:  

- A conta de computador do servidor do site tem de ser membro do grupo Administradores no computador que executa o SQL Server. Se seguir a recomendação do SQL Server de "administradores de prestação explicitamente", a conta que utiliza para executar a configuração no servidor do site deve ser um membro do grupo de Utilizadores SQL.  

- Se instalar o SQL Server utilizando uma conta de utilizador de domínio, certifique-se de que a conta de computador do servidor do site está configurada para um Nome Principal de Serviço (SPN) que é publicado nos Serviços de Domínio do Diretório Ativo. Sem o SPN, a autenticação Kerberos falha e a configuração do Gestor de Configuração falha.  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a>Orientação de segurança para sistemas de sites que executam o IIS

Várias funções do sistema de site no Gestor de Configuração requerem IIS. O processo de segurança do IIS permite ao Gestor de Configuração funcionar corretamente e reduz o risco de ataques de segurança. Quando prático, minimize o número de servidores que requerem IIS. Por exemplo, executar apenas o número de pontos de gestão que você precisa para apoiar a sua base de clientes, tendo em consideração alta disponibilidade e isolamento de rede para gestão de clientes baseadona na Internet.  

Utilize as seguintes orientações para o ajudar a proteger os sistemas de site que executam o IIS.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Desative as funções IIS que não precisa

Instale apenas as funcionalidades mínimas do IIS para a função de sistema de sites que instalar. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../configs/site-and-site-system-prerequisites.md).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Configure as funções do sistema do site para exigir HTTPS

Quando os clientes se ligam a um sistema de site utilizando HTTP e não utilizando HTTPS, utilizam a autenticação do Windows. Este comportamento pode voltar a usar a autenticação NTLM em vez da autenticação Kerberos. Quando é utilizada a autenticação NTLM, os clientes podem ligar a um servidor não autorizado.  

A exceção a esta orientação pode ser pontos de distribuição. As contas de acesso ao pacote não funcionam quando o ponto de distribuição está configurado para HTTPS. As contas de acesso a pacotes fornecem autorização para o conteúdo, para que possa restringir os utilizadores que podem aceder ao conteúdo. Para mais informações, consulte [as melhores práticas de segurança para a gestão de conteúdos.](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement)  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Configure uma lista de fidedignidade de certificados (CTL) no IIS para funções do sistema de site

Funções do sistema de sites:  

- Um ponto de distribuição que configura para HTTPS  

- Um ponto de gestão que configura para HTTPS e permite suportar dispositivos móveis

A CTL é uma lista definida de autoridades de certificação de raiz fidedignas (A). Quando utiliza um CTL com uma política de grupo e uma implantação de infraestruturas de chave pública (PKI), um CTL permite-lhe complementar os CAs de raiz fidedigno existentes que estão configurados na sua rede. Por exemplo, Os CAs que são automaticamente instalados com o Microsoft Windows ou adicionados através de CAs raiz de empresa do Windows. Quando um CTL é configurado no IIS, define um subconjunto daqueles CAs de raiz de confiança.  

Este subconjunto proporciona-lhe mais controlo sobre a segurança. O CTL restringe os certificados de cliente que são aceites apenas aos certificados emitidos a partir da lista de CAs no CTL. Por exemplo, o Windows vem com uma série de certificados CA conhecidos e de terceiros, tais como VeriSign e Thawte.

Por padrão, o computador que executa o IIS confia em certificados que acorrentam a estes conhecidos CAs. Quando não configura o IIS com um CTL para as funções do sistema de site listado, o site aceita como um cliente válido qualquer dispositivo que tenha um certificado emitido destes CAs. Se configurar o IIS com um CTL que não incluiu estes CAs, o site recusa ligações ao cliente, se as cadeias de certificados para estes CAs. Para que os clientes do Gestor de Configuração sejam aceites para as funções do sistema de site listado, deve configurar o IIS com um CTL que especifica os CAs que são utilizados pelos clientes do Gestor de Configuração.  

> [!NOTE]  
> Apenas as funções do sistema de site listadas exigem que configure um CTL no IIS. A lista de emitentes de certificados que o Gestor de Configuração utiliza para pontos de gestão fornece a mesma funcionalidade para computadores clientes quando se conectam a pontos de gestão HTTPS.  

Para obter mais informações sobre como configurar uma lista de CAs fidedignos no IIS, consulte a documentação do IIS.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Não coloque o servidor do site num computador com iIS

A separação de funções ajuda a reduzir o perfil de ataques e a melhorar a capacidade de recuperação. A conta de computador do servidor do site normalmente tem privilégios administrativos em todas as funções do sistema do site. Também pode ter estes privilégios em clientes do Gestor de Configuração, se utilizar a instalação push do cliente.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Utilize servidores IIS dedicados para O Gestor de Configuração

Embora possa hospedar várias aplicações baseadas na Web nos servidores IIS que também são utilizados pelo Gestor de Configuração, esta prática pode aumentar significativamente a sua superfície de ataque. Uma aplicação mal configurada poderia permitir que um intruso ganhasse o controlo de um sistema de site do Gestor de Configuração. Esta violação pode permitir que um intruso ganhe o controlo da hierarquia.  

Se tiver de executar outras aplicações baseadas na Web nos sistemas de site do Gestor de Configuração, crie um web site personalizado para sistemas de site do Gestor de Configuração.  

### <a name="use-a-custom-website"></a>Use um site personalizado

Para sistemas de site que executam o IIS, configure o Gestor de Configuração para usar um website personalizado em vez do website predefinido. Se tiver de executar outras aplicações web no sistema do site, deve utilizar um website personalizado. Esta definição é uma configuração em todo o site e não uma definição para um sistema de site específico.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Quando utilizar websites personalizados, remova os diretórios virtuais predefinidos

Quando muda de usar o website padrão para usar um website personalizado, o Gestor de Configuração não remove os antigos diretórios virtuais. Remova os diretórios virtuais que o Gestor de Configuração originalmente criou no site predefinido.  

Por exemplo, remova os seguintes diretórios virtuais para um ponto de distribuição:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Siga a orientação de segurança do IIS Server

Identifique e siga a orientação geral para a sua versão do IIS Server. Tenha em consideração quaisquer requisitos que o Gestor de Configuração tenha para funções específicas do sistema do site. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../configs/site-and-site-system-prerequisites.md).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a>Orientação de segurança para o ponto de gestão

Os pontos de gestão são a interface principal entre dispositivos e Gestor de Configuração. Considere os ataques contra o ponto de gestão e o servidor em que corre para ser de alto risco, e atenuar adequadamente. Aplique todas as orientações de segurança adequadas e monitor para atividades incomuns.  

Utilize as seguintes orientações para ajudar a garantir um ponto de gestão no Gestor de Configuração.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Atribuir o cliente num ponto de gestão para o mesmo site

Evite o cenário em que atribua o cliente do Gestor de Configuração que se situa num ponto de gestão para um site diferente do site do ponto de gestão.  

Se migrar de uma versão anterior para a filial atual do Gestor de Configuração, emigra o cliente no ponto de gestão para o novo site o mais rapidamente possível.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a>Orientação de segurança para o ponto de estado de recuo

Se instalar um ponto de estado de recuo no Gestor de Configuração, utilize as seguintes orientações de segurança:

Para obter mais informações sobre as considerações de segurança quando instalar um ponto de estado de recuo, consulte [Determine se necessita de um ponto](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)de estado de recuo .  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Não execute outros papéis no mesmo sistema de site

O ponto de estado de recuo foi concebido para aceitar comunicações não autenticadas de qualquer computador. Se executar esta função do sistema do site com outras funções ou um controlador de domínio, o risco para esse servidor aumenta muito.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Instale o ponto de estado de recuo antes de instalar clientes com certificados PKI

Se os sistemas de site do Gestor de Configuração não aceitarem a comunicação do cliente HTTP, pode não saber que os clientes não são geridos devido a problemas de certificadorelacionados com o PKI. Se atribuir clientes a um ponto de estado de recuo, eles reportam estas emissões de certificados através do ponto de estado de recuo.  

Por razões de segurança, não pode atribuir um ponto de recuo aos clientes depois de instalados. Só pode atribuir esta função durante a instalação do cliente.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Evite utilizar o ponto de estado de recuo na rede do perímetro

Por predefinição, o ponto de estado de contingência aceita dados a partir de qualquer cliente. Embora um ponto de estado de recuo na rede de perímetro possa ajudá-lo a resolver os problemas com clientes baseados na Internet, equilibre os benefícios de resolução de problemas com o risco de um sistema de site que aceite dados não autenticados numa rede acessível ao público.  

Se instalar o ponto de estado de recuo na rede do perímetro ou qualquer rede não fidedigna, configure o servidor do site para iniciar transferências de dados. Não utilize a definição predefinida que permite que o ponto de estado de recuo inicie uma ligação ao servidor do site.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>Questões de segurança para a administração do site

Reveja os seguintes problemas de segurança para O Gestor de Configuração:  

- O Gestor de Configuração não tem defesa contra um utilizador administrativo autorizado que usa o Gestor de Configuração para atacar a rede. Os utilizadores administrativos não autorizados são um alto risco de segurança. Podem lançar muitos ataques, que incluem as seguintes estratégias:  

    - Utilize a implementação de software para instalar e executar automaticamente software malicioso em todos os computadores clientes do Gestor de Configuração da organização.  

    - Controle remotamente um cliente do Gestor de Configuração sem permissão do cliente.  

    - Configure intervalos de sondagens rápidos e quantidades extremas de inventário. Esta ação cria ataques de negação de serviço contra clientes e servidores.  

    - Utilizar um site na hierarquia para escrever dados nos dados do Active Directory de outro site.  

    A hierarquia do local é o limite de segurança. Considere os sites apenas como limites de gestão.  

    Audite todas as atividades do utilizador administrativo e reveja regularmente os registos de auditoria. Exija que todos os utilizadores administrativos do Gestor de Configuração sejam submetidos a uma verificação de antecedentes antes de serem contratados. Exigir reverificação periódica como condição de trabalho.  

- Se o ponto de inscrição estiver comprometido, um intruso pode obter certificados para autenticação. Podem roubar as credenciais dos utilizadores que matriculam os seus dispositivos móveis.  

    O ponto de inscrição comunica com um CA. Pode criar, modificar e eliminar objetos de Diretório Ativo. Nunca instale o ponto de inscrição na rede do perímetro. Monitorize sempre para atividades incomuns.  

- Se permitir políticas de utilizador para gestão de clientes baseadas na Internet, aumenta o seu perfil de ataque.  

    Além de utilizar em certificados PKI para ligações cliente-a-servidor, estas configurações requerem autenticação do Windows. Podem voltar a usar a autenticação NTLM em vez de Kerberos. A autenticação NTLM é vulnerável a ataques de representação e repetição. Para autenticar com sucesso um utilizador na internet, é necessário permitir uma ligação do sistema de site baseado na Internet a um controlador de domínio.  

- A parte **Do Admin$** é necessária nos servidores do sistema do site.  

    O servidor do site Do Gestor de Configuração utiliza a parte Do Admin$ para ligar e fazer operações de serviço nos sistemas do site. Não desative ou remova esta parte.  

- O Gestor de Configuração utiliza serviços de resolução de nomes para se ligar a outros computadores. Estes serviços são difíceis de assegurar contra os seguintes ataques de segurança:
    - Spoofing
    - Adulteração
    - Repúdio
    - Divulgação de informação
    - Denial of service
    - Elevação do privilégio

    Identifique e siga qualquer orientação de segurança para a versão do DNS que utiliza para resolução de nomes.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a>Informações de privacidade para descoberta

A Discovery cria registos de recursos de rede e armazena-os na base de dados do Gestor de Configuração. Os registos de dados da Discovery contêm informações de computador, tais como endereços IP, versões DE EE e nomes de computador. Também pode configurar métodos de descoberta de Diretório Ativo para devolver qualquer informação que a sua organização armazene em Ative Directory Domain Services.  

O único método de descoberta que o Gestor de Configuração permite por padrão é a Descoberta do Batimento Cardíaco. Este método apenas descobre computadores que já têm o software cliente do Gestor de Configuração instalado.  

A informação da Discovery não é enviada diretamente para a Microsoft. Está guardado na base de dados do Diretor de Configuração. O Gestor de Configuração retém informação na base de dados até que apague os dados. Este processo acontece a cada 90 dias pela tarefa de manutenção do site **Eliminar Dados de DescobertaS Envelhecidas**.  
