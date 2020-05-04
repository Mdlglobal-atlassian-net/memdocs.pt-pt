---
title: Segurança e privacidade do cliente
titleSuffix: Configuration Manager
description: Conheça a segurança e privacidade dos clientes do Gestor de Configuração.
ms.date: 07/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4922502b49ab2da9ce393fab809e4dc583fd962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714011"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Segurança e privacidade para clientes do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo descreve informações de segurança e privacidade para clientes do Gestor de Configuração. Também inclui informações para dispositivos móveis que são geridos pelo [conector Exchange Server](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-clients"></a><a name="BKMK_Security_Clients"></a>Boas práticas de segurança para clientes  

O site Do Gestor de Configuração aceita dados de dispositivos que executam o cliente do Gestor de Configuração. Este comportamento introduz o risco de os clientes poderem atacar o site. Por exemplo, poderiam enviar inventários incorretos ou tentar sobrecarregar os sistemas do site. Implemente o cliente do Gestor de Configuração apenas para dispositivos em que confie. Além disso, utilize os seguintes procedimentos recomendados para ajudar a proteger o site contra dispositivos não autorizados ou comprometidos:  

### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Utilize certificados de infraestrutura de chaves públicas (PKI) para comunicações de clientes com sistemas de site que executam o IIS  

- Como uma propriedade do site, configure **Definições do sistema de sites** para **Apenas HTTPS**.  

- Instale clientes `UsePKICert` com a propriedade CCMSetup.  

- Utilize uma lista de revogação de certificados (CRL) e certifique-se de que os clientes e servidores em comunicação podem aceder-lhe sempre.  

Os clientes de dispositivos móveis e alguns clientes baseados na Internet requerem estes certificados. A Microsoft recomenda estes certificados para todas as ligações do cliente na intranet.  

Para obter mais informações sobre os requisitos do certificado PKI e como são usados para ajudar a proteger o Gestor de Configuração, consulte os [requisitos do certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Aprovar automaticamente computadores cliente de domínios fidedignos, e verificar e aprovar manualmente outros computadores  

Quando não pode utilizar a autenticação PKI, a aprovação identifica um computador em que confia para ser gerido pelo Gestor de Configuração. A hierarquia tem as seguintes opções para configurar a aprovação do cliente:  

- Manual
- Automático para computadores em domínios fidedignos
- Automático para todos os computadores  

O método de aprovação mais seguro é aprovar automaticamente clientes que sejam membros de domínios fidedignos. Em seguida, verifique manualmente e aprove todos os outros computadores. A aprovação automática de todos os clientes não é recomendada, a menos que tenha outros controlos de acesso para evitar que computadores não confiáveis acedam à sua rede.  

Para obter mais informações sobre como aprovar manualmente computadores, consulte [Gerir os clientes a partir do nó dos dispositivos](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Não confie em bloquear para impedir que os clientes acedam à hierarquia do Gestor de Configuração  

Os clientes bloqueados são rejeitados pela infraestrutura do Gestor de Configuração. Se os clientes estiverem bloqueados, não podem comunicar com os sistemas do site para descarregar a política, carregar dados de inventário ou enviar mensagens de estado ou estado.

O bloqueio foi concebido para os seguintes cenários:

- Bloquear meios de arranque perdidos ou comprometidos quando implementa um Sistema operativo para clientes
- Quando todos os sistemas de site aceitam ligações ao cliente HTTPS

Quando os sistemas do site aceitam ligações ao cliente HTTP, não confie em bloquear para proteger a hierarquia do Gestor de Configuração de computadores não confiáveis. Neste cenário, um cliente bloqueado poderia voltar a integrar o site com um novo certificado auto-assinado e identificação de hardware.

A revogação do certificado é a principal linha de defesa contra certificados potencialmente comprometidos. Uma lista de revogação de certificados (CRL) só está disponível a partir de uma infraestrutura de chave pública apoiada (PKI). Bloquear clientes no Gestor de Configuração oferece uma segunda linha de defesa para proteger a sua hierarquia.  

Para mais informações, consulte [Determinar se bloqueia clientes](determine-whether-to-block-clients.md).  

### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Utilize os métodos de instalação mais seguros do cliente que são práticos para o seu ambiente  

- Para computadores de domínio, os métodos de instalação de cliente de Política de Grupo e de instalação de cliente baseada em atualização de software são mais seguros do que a instalação push de cliente.  

- Se aplicar controlos de acesso e alterar controlos, utilize métodos de imagem e instalação manual.  

- Na versão 1806 ou posterior, utilize a autenticação mútua Kerberos com a instalação de push do cliente.  

De todos os métodos de instalação do cliente, a instalação push do cliente é a menos segura devido às muitas dependências que tem. Estas dependências incluem permissões administrativas locais, a parte do Administrador e exceções à firewall. O número e o tipo destas dependências aumentam a sua superfície de ataque.  

A partir da versão 1806, ao utilizar o impulso do cliente, o site pode exigir a autenticação mútua kerberos, não permitindo o recuo à NTLM antes de estabelecer a ligação. Esta melhoria ajuda a garantir a comunicação entre o servidor e o cliente. Para mais informações, consulte [Como instalar clientes com pressão](../deploy-clients-to-windows-computers.md#BKMK_ClientPush)do cliente .<!--1358204-->  

Para obter mais informações sobre os diferentes métodos de instalação do cliente, consulte os métodos de [instalação do Cliente.](client-installation-methods.md)  

Sempre que possível, selecione um método de instalação do cliente que exija menos permissões de segurança no Gestor de Configuração. Restringir os utilizadores administrativos a que sejam atribuídas funções de segurança com permissões que podem ser usadas para outros fins que não a implementação do cliente. Por exemplo, configurar a atualização automática do cliente requer a função de segurança **do Administrador Completo,** que concede a um utilizador administrativo todas as permissões de segurança.  

Para obter mais informações sobre as dependências e permissões de segurança necessárias para cada método de instalação do cliente, consulte "Dependências do método de instalação" em [pré-requisitos para clientes informáticos](../prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Se tiver de utilizar a instalação push de cliente, tome medidas adicionais para proteger a Conta de Instalação Push do Cliente  

Esta conta deve ser um membro do grupo **de Administradores locais** em cada computador que instala o cliente do Gestor de Configuração. Nunca adicione a Conta de Instalação push do cliente ao grupo **Dedomínio Admins.** Em vez disso, crie um grupo global e, em seguida, adicione esse grupo global ao grupo **de Administradores locais** nos seus clientes. Crie um objeto de política de grupo para adicionar uma definição de Grupo Restrito para adicionar a Conta de Instalação push do cliente ao grupo de **Administradores locais.**  

Para obter segurança adicional, crie várias Contas de Instalação de Push do Cliente, cada uma com acesso administrativo a um número limitado de computadores. Se uma conta estiver comprometida, apenas os computadores clientes a que essa conta tem acesso estão comprometidos.  

### <a name="remove-certificates-before-imaging-clients"></a>Remover certificados antes de imagiologia dos clientes  

Quando implementar clientes utilizando imagens de SO, remova sempre os certificados antes de capturar a imagem. Estes certificados incluem certificados PKI para autenticação de clientes e certificados auto-assinados. Se não remover estes certificados, os clientes podem fazer-se passar por si. Não pode verificar os dados de cada cliente.  

Para obter mais informações, consulte Criar uma sequência de [tarefas para capturar um sistema operativo](../../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).  

### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Certifique-se de que os clientes do computador Do Gestor de Configuração obtêm uma cópia autorizada destes certificados  

#### <a name="the-configuration-manager-trusted-root-key-certificate"></a>O certificado de chave de raiz fidedigna do Gestor de Configuração  

Quando ambas as seguintes declarações são verdadeiras, os clientes confiam na chave raiz fidedigna do Gestor de Configuração para autenticar pontos de gestão válidos:  

- Você não estendeu o esquema de Diretório Ativo para Gerente de Configuração
- Os clientes não usam certificados PKI quando comunicam com pontos de gestão  

Neste cenário, os clientes não têm forma de verificar se o ponto de gestão é confiável para a hierarquia, a menos que utilizem a chave raiz de confiança. Sem a chave de raiz fidedigna, um intruso qualificado pode direcionar clientes para um ponto de gestão não autorizado.  

Quando os clientes não podem descarregar a chave raiz fidedigna do Gestor de Configuração do Catálogo Global ou utilizando certificados PKI, pré-fornecer os clientes com a chave raiz de confiança. Esta ação garante que não podem ser direcionadas para um ponto de gestão desonesto. Para mais informações, consulte [O Planeamento para a chave raiz de confiança](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="the-site-server-signing-certificate"></a>O certificado de assinatura do servidor do site  

Os clientes usam este certificado para verificar se o servidor do site assinou a apólice descarregada a partir de um ponto de gestão. Este certificado é autoassinado pelo servidor do site e publicado nos Serviços de Domínio do Active Directory.  

Quando os clientes não podem descarregar o certificado de assinatura do servidor do site a partir do Catálogo Global, por padrão, eles descarregam-no a partir do ponto de gestão. Se o ponto de gestão for exposto a uma rede não confiável como a internet, instale manualmente o certificado de assinatura do servidor do site nos clientes. Esta ação garante que não podem descarregar as políticas adulteradas dos clientes de um ponto de gestão comprometido.  

Para instalar manualmente o certificado de assinatura do servidor do site, utilize a propriedade CCMSetup client.msi **SMSSIGNCERT**. Para mais informações, consulte sobre as propriedades de [instalação do cliente.](../about-client-installation-properties.md)  

### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Não utilize a atribuição automática do site se o cliente descarregar a chave raiz fidedigna a partir do primeiro ponto de gestão que contacta  

Para evitar o risco de um novo cliente descarregar a chave raiz fidedigna de um ponto de gestão fraudulento, utilize apenas a atribuição automática do site nos seguintes cenários:  

- O cliente pode aceder à informação do site do Gestor de Configuração que é publicada nos Serviços de Domínio do Diretório Ativo.  

- Pré-aprovisione o cliente com a chave de raiz fidedigna.  

- Utilize certificados PKI de uma autoridade de certificação empresarial para estabelecer fidedignidade entre o cliente e o ponto de gestão.  

Para obter mais informações sobre a chave de raiz fidedigna, consulte [O Planeamento para a chave raiz fidedigna](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Instalar computadores cliente com a opção CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS  

O método mais seguro para a localização de serviço para os clientes localizarem sites e pontos de gestão é a utilização dos Serviços de Domínio do Active Directory. Às vezes este método não é possível para alguns ambientes. Por exemplo, porque não pode estender o esquema de Diretório Ativo para O Gestor de Configuração, ou porque os clientes estão numa floresta não confiável ou num grupo de trabalho. Se este método não for possível, utilize a publicação de DNS como um método alternativo de localização de serviço. Se ambos os métodos falharem, e quando o ponto de gestão não estiver configurado para ligações ao cliente HTTPS, os clientes podem voltar a utilizar WINS.  

A publicação para WINS é menos segura do que os outros métodos de publicação. Configure os computadores dos clientes para não voltarem a utilizar WINS especificando **SMSDIRECTORYLOOKUP=NoWINS**. Se tiver de utilizar WINS para a localização do serviço, utilize **SMSDIRECTORYLOOKUP=WINSSECURE**. Esta é a predefinição. Utiliza a chave raiz fidedigna do Gestor de Configuração para validar o certificado auto-assinado do ponto de gestão.  

> [!NOTE]  
> Quando configura o cliente para **SMSDIRECTORYLOOKUP=WINSSECURE** e encontra um ponto de gestão do WINS, o cliente verifica a sua cópia da chave raiz fidedigna do Gestor de Configuração que está no WMI.  
>
> Se a assinatura no certificado de ponto de gestão corresponder à cópia do cliente da chave raiz fidedigna, o certificado é validado. Após a validação do certificado, o cliente começa a comunicar com o ponto de gestão que encontrou através da utilização do WINS.  
>
> Se a assinatura no certificado de ponto de gestão não corresponder à cópia do cliente da chave de raiz fidedigna, o certificado não é válido. Neste cenário, o cliente não comunica com o ponto de gestão que encontrou através da utilização do WINS.  

### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Certifique-se de que as janelas de manutenção são suficientemente abrangentes para implementar atualizações de software críticas  

As janelas de manutenção para recolha seleções de dispositivos restringem as vezes que o Gestor de Configuração pode instalar software nestes dispositivos. Se configurar a janela de manutenção demasiado pequena, o cliente poderá não instalar atualizações críticas de software. Este comportamento deixa o cliente vulnerável a qualquer ataque que a atualização do software atenua.  

### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Tome precauções adicionais de segurança para reduzir a superfície de ataque em dispositivos incorporados pelo Windows com filtros de escrita  

Quando ativa filtros de escrita em dispositivos Windows Embedded, quaisquer instalações ou alterações de software são feitas apenas para a sobreposição. Estas alterações não persistem após o reinício do dispositivo. Se utilizar o 'Configuração Manager' para desativar os filtros de escrita, durante este período o dispositivo incorporado é vulnerável a alterações em todos os volumes. Estes volumes incluem pastas partilhadas.  

O Gestor de Configuração bloqueia o computador durante este período para que apenas os administradores locais possam iniciar sessão. Sempre que possível, tome precauções adicionais de segurança para ajudar a proteger o computador. Por exemplo, ativar restrições adicionais na firewall.  

Se utilizar janelas de manutenção para persistir alterações, planeje cuidadosamente estas janelas. Minimize o tempo que os filtros de escrita são desativados, mas faça-os com tempo suficiente para permitir que instalações de software e reinícios sejam concluídos.  

### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Use a versão mais recente do cliente com instalação de cliente baseada em atualização de software

Se utilizar a instalação de clientes baseada em atualizações de software e instalar uma versão posterior do cliente no site, atualize a atualização de software publicada. Em seguida, os clientes recebem a versão mais recente a partir do ponto de atualização de software.  

Quando atualiza o site, a atualização de software para implementação do cliente que é publicada no ponto de atualização de software não é atualizada automaticamente. Republique o cliente do Gestor de Configuração no ponto de atualização do software e atualize o número da versão.  

Para mais informações, consulte [como instalar clientes do Gestor de Configuração utilizando a instalação baseada em atualizações de software.](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP)  

### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Apenas suspenda a entrada bitLocker PIN em dispositivos de acesso confiável e restrito  

Apenas configure a definição do cliente para suspender a **entrada bitLocker PIN no reinício** **para Sempre** para computadores em que confia e que tenham acesso físico restrito.

Quando definir esta definição de cliente para **Sempre**, O Gestor de Configuração pode completar a instalação do software. Este comportamento ajuda a instalar atualizações críticas de software e a retomar os serviços. Se um intruso intercetar o processo de reinício, podem assumir o controlo do computador. Utilize esta definição apenas quando confia no computador e quando o acesso físico ao computador for restrito. Por exemplo, esta definição pode ser apropriada para servidores num centro de dados.  

Para obter mais informações sobre esta definição de cliente, consulte [as definições do cliente](../about-client-settings.md#suspend-bitlocker-pin-entry-on-restart).  

### <a name="dont-bypass-powershell-execution-policy"></a>Não ignore a política de execução da PowerShell

Se configurar a definição do cliente do Gestor de Configuração para a política de **execução powerShell** para **contornar,** então o Windows permite que os scripts PowerShell não assinados possam ser executados. Este comportamento pode permitir que malware seja executado em computadores clientes. Quando a sua organização necessitar desta opção, utilize uma definição personalizada do cliente. Atribua-o apenas aos computadores clientes que devem executar scripts PowerShell não assinados.  

Para obter mais informações sobre esta definição de cliente, consulte [as definições do cliente](../about-client-settings.md#powershell-execution-policy).  


## <a name="security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a>Boas práticas de segurança para dispositivos móveis  

### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Instale o ponto de procuração de matrículas numa rede de perímetro e o ponto de inscrição na intranet  

Para dispositivos móveis baseados na Internet que se inscreva no Gestor de Configuração, instale o ponto de procuração de inscrição numa rede de perímetro e o ponto de inscrição na intranet. Esta separação de funções ajuda a proteger o ponto de registo contra ataques. Se um intruso comprometer o ponto de inscrição, pode obter certificados para autenticação. Também podem roubar as credenciais dos utilizadores que matriculam os seus dispositivos móveis.  

### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Configure as definições de palavra-passe para ajudar a proteger dispositivos móveis de acesso não autorizado  

*Para dispositivos móveis matriculados pelo Gestor*de Configuração : Utilize um item de configuração de dispositivo móvel para configurar a complexidade da palavra-passe como PIN. Especifique pelo menos o comprimento mínimo de senha por defeito.  

*Para dispositivos móveis que não tenham o cliente do Gestor de Configuração instalado mas que sejam geridos pelo conector Do Servidor de Câmbio*: Configure as Definições de **Palavra-Passe** para o conector do Exchange Server de tal forma que a complexidade da palavra-passe é o PIN. Especifique pelo menos o comprimento mínimo de senha por defeito.  

### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Só permite que as candidaturas sejam executadas que são assinadas por empresas em quem confia  

Ajude a prevenir a adulteração de informações de inventário e informações sobre o estado, permitindo que as aplicações sejam executadas apenas quando são assinadas por empresas em quem confia. Não permita que os dispositivos instalem ficheiros não assinados.  

*Para dispositivos móveis matriculados pelo Diretor*de Configuração : Utilize um item de configuração de dispositivomóvel para configurar as **aplicações não assinadas** de definição de segurança como **proibidas**. Configure as instalações de **ficheiros não assinadas** para ser uma fonte de confiança.  

*Para dispositivos móveis que não tenham o cliente do Gestor de Configuração instalado mas que sejam geridos pelo conector Do Servidor de Câmbio*: Configure as definições de **aplicação** para o conector do Exchange Server de tal forma que a instalação de **ficheiros não assinados** e **as aplicações não assinadas** são **proibidas**.  

### <a name="lock-mobile-devices-when-not-in-use"></a>Bloqueie os dispositivos móveis quando não estiver a ser utilizado  

Ajude a prevenir a elevação de ataques de privilégios bloqueando o dispositivo móvel quando não é utilizado.

*Para dispositivos móveis matriculados pelo Diretor*de Configuração : Utilize um item de configuração de dispositivo móvel para configurar o tempo de regulação da palavra-passe **em minutos antes**do bloqueio do dispositivo móvel .  

*Para dispositivos móveis que não tenham o cliente do Gestor de Configuração instalado mas que sejam geridos pelo conector Do Servidor de Câmbio*: Configure as definições de **palavra-passe** para o conector do Exchange Server para definir o **tempo de inversão em minutos antes**de o dispositivo móvel estar bloqueado .  

### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Restringir os utilizadores que podem inscrever os seus dispositivos móveis  

Ajude a prevenir a elevação dos privilégios restringindo os utilizadores que podem inscrever os seus dispositivos móveis. Utilize uma definição de cliente personalizada em vez de predefinições de cliente, para permitir que apenas utilizadores autorizados possam inscrever os respetivos dispositivos móveis.  

### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Orientação de afinidade do dispositivo do utilizador para dispositivos móveis  

Não implemente aplicações para utilizadores que tenham dispositivos móveis matriculados pelo Configuração Manager ou Microsoft Intune nos seguintes cenários:  

- O dispositivo móvel é utilizado por mais de uma pessoa.  

- O dispositivo é matriculado por um administrador em nome de um utilizador.  

- O dispositivo é transferido para outra pessoa sem se reformar e, em seguida, re-matricular o dispositivo.  

A inscrição no dispositivo cria uma relação de afinidade do dispositivo de utilizador. Esta relação mapeia o utilizador que executa a inscrição no dispositivo móvel. Se outro utilizador utilizar o dispositivo móvel, pode executar as aplicações implementadas para o utilizador original, o que pode resultar numa elevação de privilégios. Da mesma forma, se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não são instaladas no dispositivo móvel. Em vez disso, as aplicações implementadas para o administrador podem ser instaladas.  

Ao contrário da afinidade do dispositivo de utilizador para computadores Windows, não é possível definir manualmente as informações de afinidade do dispositivo de utilizador para dispositivos móveis matriculados pelo Microsoft Intune.  

Se transferir a propriedade de um dispositivo móvel matriculado pela Intune, retire primeiro o dispositivo móvel de Intune. Esta ação remove a relação de afinidade do dispositivo utilizador. Em seguida, peça ao utilizador atual para voltar a inscrever o dispositivo.  

### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Certifique-se de que os utilizadores matriculam os seus próprios dispositivos móveis para o Microsoft Intune  

Uma relação de afinidade do dispositivo de utilizador é criada durante a inscrição. Esta ação mapeia o utilizador que executa a inscrição no dispositivo móvel. Se um administrador inscrever o dispositivo móvel para um utilizador, as aplicações implementadas para o utilizador não são instaladas no dispositivo móvel. Em vez disso, as aplicações implementadas para o administrador podem ser instaladas.  

### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Proteja a ligação entre o servidor do site do Gestor de Configuração e o Servidor de Intercâmbio

Se o Servidor de Câmbio estiver no local, utilize o IPsec. A Bolsa hospedada assegura automaticamente a ligação utilizando o SSL.  

### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Utilize o princípio dos menores privilégios para o conector  

Para obter uma lista dos cmdlets mínimos que o conector do Exchange Server necessita, consulte [Gerir dispositivos móveis com 'Gestor de Configuração' e Troca](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  


## <a name="security-best-practices-for-macs"></a><a name="bkmk_macs"></a>Boas práticas de segurança para Macs  

### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Armazenar e aceder aos ficheiros de origem do cliente a partir de um local seguro  

Antes de instalar ou inscrever o cliente no computador Mac, o Gestor de Configuração não verifica se estes ficheiros de origem do cliente foram adulterados. Descarregue estes ficheiros de uma fonte fidedigna. Armazene e aceda-os de forma segura.  

### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Monitorizar e acompanhar o período de validade do certificado  

Para assegurar a continuidade do negócio, monitorize e controle o período de validade dos certificados que utiliza para computadores Mac. O Gestor de Configuração não suporta a renovação automática deste certificado, nem o avisa que o certificado está prestes a expirar. Um período de validade típico é de um ano.  

Para obter mais informações sobre como renovar o certificado, consulte [Renovar manualmente o certificado de cliente Mac](../deploy-clients-to-macs.md#renew-the-mac-client-certificate).  

### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configure o certificado de raiz fidedigno apenas para SSL  

Para ajudar a proteger contra a elevação de privilégios, configure o certificado para a autoridade de certificadode raiz fidedigna para que só seja confiado para o protocolo SSL.

Quando matricula computadores Mac, um certificado de utilizador para gerir o cliente do Gestor de Configuração é automaticamente instalado. Este certificado de utilizador inclui os certificados de raiz fidedignos na sua cadeia fiducida. Para restringir a confiança deste certificado-raiz apenas ao protocolo SSL, utilize o seguinte procedimento:  

1. No computador Mac, abra uma janela de terminal.  

2. Insira o seguinte comando:`sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3. Na caixa de diálogo **Keychain Access,** na secção **Keychains,** clique no **Sistema**. Em seguida, na secção **Categoria,** clique em **Certificados**.  

4. Localize e clique duas vezes no certificado ca raiz para o certificado de cliente Mac.  

5. Na caixa de diálogo do certificado de AC de raiz, expanda a secção **Confiar** e, em seguida, faça as seguintes alterações:  

    1. **Ao utilizar este certificado**: **Altere** a definição Always Trust para **utilizar as predefinições do sistema**.  

    2. **Camada de tomadas seguras (SSL)**: Não alterar **nenhum valor especificado** para **sempre confiar**.  

6. Feche a caixa de diálogo. Quando solicitado, introduza a palavra-passe do administrador e, em seguida, clique em **Definições de Atualização**.  

Depois de completar este procedimento, o certificado de raiz só é confiável para validar o protocolo SSL. Outros protocolos que agora não são fidedignos com este certificado de raiz incluem O Correio Seguro (S/MIME), Autenticação Extensível (EAP) ou assinatura de código.  

> [!NOTE]  
> Utilize também este procedimento se tiver instalado o certificado de cliente independentemente do Gestor de Configuração.


## <a name="security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a>Problemas de segurança para clientes do Gestor de Configuração  

Os seguintes problemas de segurança não têm nenhuma atenuação:  

### <a name="status-messages-arent-authenticated"></a>As mensagens de estado não são autenticadas

A autenticação não é efetuada nas mensagens de estado. Quando um ponto de gestão aceita ligações de cliente HTTP, qualquer dispositivo pode enviar mensagens de estado para o ponto de gestão. Se o ponto de gestão aceitar apenas ligações ao cliente HTTPS, um dispositivo deve ter um certificado de autenticação de cliente válido, mas também pode enviar qualquer mensagem de estado. O ponto de gestão descarta qualquer mensagem de estado inválida recebida de um cliente.  

Há alguns potenciais ataques contra esta vulnerabilidade:

- Um intruso pode enviar uma mensagem falsa para ganhar a adesão a uma coleção baseada em consultas de mensagens de estado.
- Qualquer cliente poderia iniciar um denial of service contra o ponto de gestão, congestionando-o com mensagens de estado.
- Se as mensagens de estado estão a acionar ações nas regras de filtro de mensagem de estado, um intruso poderia acionar a regra de filtro de mensagens de estado.
- Um intruso poderia enviar uma mensagem de estado que tornaria a informação de reportagem imprecisa.  

### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>As políticas podem ser redirecionadas para os clientes não direcionados  

Existem vários métodos que os atacantes poderiam utilizar para fazer com que uma política direcionada para um cliente fosse aplicada a um cliente completamente diferente. Por exemplo, um intruso de um cliente de confiança poderia enviar informações falsas de inventário ou descoberta para que o computador fosse adicionado a uma coleção à qual não deveria pertencer. Esse cliente recebe então todos os destacamentos dessa coleção.

Existem controlos para ajudar a evitar que os atacantes modifiquem diretamente a política. No entanto, os atacantes poderiam tomar uma política existente que reformata e reimplanta um Sistema operativo e enviá-lo para um computador diferente. Esta política redirecionada poderia criar uma negação de serviço. Este tipo de ataques requereria um tempo preciso e um conhecimento alargado da infraestrutura do Gestor de Configuração.  

### <a name="client-logs-allow-user-access"></a>Os registos de cliente permitem o acesso do utilizador  

Todos os ficheiros de registo do cliente permitem ao grupo **Utilizadores** acesso ao *Read* e ao utilizador especial **Interativo** com acesso *ao Write.* Se ativar o registo verboso, os intrusos podem ler os ficheiros de registo para procurarem informações sobre vulnerabilidades de compatibilidade ou de sistema. Processos como o software que o cliente instala no contexto de um utilizador devem escrever para iniciar sessão com uma conta de utilizador de baixos direitos. Este comportamento significa que um intruso também pode escrever para os registos com uma conta de baixos direitos.  

O risco mais grave é que um intruso possa remover informações nos ficheiros de registo. Um administrador pode precisar desta informação para auditoria e deteção de intrusões.  

### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Um computador poderia ser usado para obter um certificado projetado para a inscrição de dispositivos móveis  

Quando o Gestor de Configuração processa um pedido de inscrição, não pode verificar o pedido originado de um dispositivo móvel e não de um computador. Se o pedido for de um computador, pode instalar um certificado PKI que lhe permite registar-se com o Gestor de Configuração.

Para ajudar a prevenir uma elevação de ataque de privilégio neste cenário, apenas permite que utilizadores de confiança matriculem os seus dispositivos móveis. Monitorize cuidadosamente as atividades de inscrição do dispositivo no site.  

### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Um cliente bloqueado ainda pode enviar mensagens para o ponto de gestão

Quando bloqueia um cliente em que já não confia, mas estabeleceu uma ligação de rede para notificação do cliente, o Gestor de Configuração não desliga a sessão. O cliente bloqueado pode continuar a enviar pacotes para o respetivo ponto de gestão, até o cliente desligar da rede. Estes pacotes são apenas pequenos pacotes de manter vivos. Este cliente não pode ser gerido pelo Gestor de Configuração até que seja desbloqueado.  

### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>Atualização automática do cliente não verifica o ponto de gestão

Quando utiliza a atualização automática do cliente, o cliente pode ser direcionado para um ponto de gestão para descarregar os ficheiros de origem do cliente. Neste cenário, o cliente não verifica o ponto de gestão como uma fonte de confiança.  

### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Quando os utilizadores matriculam os computadores Mac pela primeira vez, estão em risco devido à falsificação de DNS  

Quando o computador Mac se conecta ao ponto de procuração de inscrição durante a inscrição, é improvável que o computador Mac já tenha o certificado ca raiz de confiança. Neste ponto, o computador Mac não confia no servidor, e pede ao utilizador para continuar. Se um servidor DNS fraudulento resolver o nome de domínio totalmente qualificado (FQDN) do ponto de procuração de inscrição, pode direcionar o computador Mac para um ponto de procuração de inscrição fraudulenta para instalar certificados a partir de uma fonte não fidedigna. Para ajudar a reduzir este risco, siga os procedimentos recomendados para evitar o spoofing de DNS no seu ambiente.  

### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>A inscrição no Mac não limita os pedidos de certificados  

Os utilizadores podem inscrever novamente os seus computadores Mac, pedindo de cada vez um novo certificado de cliente. O Gestor de Configuração não verifica vários pedidos nem limita o número de certificados solicitados a partir de um único computador. Um utilizador desonesto pode executar um script que repete o pedido de inscrição da linha de comando. Este ataque pode causar uma negação de serviço na rede ou na autoridade de certificados emissores (CA). Para ajudar a reduzir este risco, monitorize com cuidado a AC emissora para detetar este tipo de comportamento suspeito. Bloqueie imediatamente a hierarquia do Gestor de Configuração qualquer computador que mostre este padrão de comportamento.  

### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Um reconhecimento de limpeza não verifica que o dispositivo foi limpo com sucesso  

Quando inicia uma ação de limpeza para um dispositivo móvel, e o Gestor de Configuração reconhece a limpeza, a verificação é que o Gestor de Configuração *enviou* com sucesso a mensagem. Não confirma que o dispositivo *agiu* no pedido.

Para dispositivos móveis geridos pelo conector Exchange Server, um reconhecimento de limpeza verifica que o comando foi recebido pela Exchange, e não pelo dispositivo.  

### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Se utilizar as opções para cometer alterações nos dispositivos Windows Embedded, as contas podem ser bloqueadas mais cedo do que o esperado  

Se o dispositivo Windows Embedded estiver a executar uma versão OS antes do Windows 7 e um utilizador tentar iniciar sessão enquanto os filtros de escrita são desativados pelo 'Gestor de Configuração', o Windows permite apenas metade do número configurado de tentativas incorretas antes de a conta estar bloqueada.

Por exemplo, configura a política de domínio para o limiar de **bloqueio da Conta** a seis tentativas. Um utilizador desalpede a sua palavra-passe três vezes e a conta está bloqueada. Este comportamento cria efetivamente uma negação de serviço. Se os utilizadores devem iniciar sessão em dispositivos incorporados neste cenário, alerte-os sobre o potencial de um limiar de bloqueio reduzido.  


## <a name="privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Clients"></a>Informações de privacidade para clientes do Gestor de Configuração  

Quando implementa o cliente do Gestor de Configuração, ativa as definições do cliente para as funcionalidades do Gestor de Configuração. As definições que utiliza para configurar as funcionalidades podem aplicar-se a todos os clientes na hierarquia do Gestor de Configuração. Este comportamento é o mesmo se estão diretamente ligados à rede interna, ligados através de uma sessão remota, ou ligados à internet.  

A informação do cliente é armazenada na base de dados do Gestor de Configuração no seu servidor SQL, e não é enviada para a Microsoft. A informação é retida na base de dados até que seja eliminada pelas tarefas de manutenção do site **Eliminar Dados de DescobertaS Envelhecidas** a cada 90 dias. Pode configurar o intervalo de eliminação. 

Alguns diagnósticos resumidos ou agregados e dados de utilização são enviados para a Microsoft. Para mais informações, consulte [Diagnósticos e dados de utilização](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Antes de configurar o cliente do Gestor de Configuração, considere os seus requisitos de privacidade.  

Pode saber mais sobre a recolha e utilização de dados da Microsoft na Declaração de Privacidade da [Microsoft.](https://privacy.microsoft.com/privacystatement)

### <a name="client-status"></a>Estado do cliente  

O Gestor de Configuração monitoriza a atividade dos clientes. Avalia periodicamente o cliente do Gestor de Configuração e pode remediar problemas com o cliente e as suas dependências. O estado do cliente é ativado por defeito. Utiliza métricas do lado do servidor para verificação da atividade do cliente. O estado do cliente utiliza ações do lado do cliente para auto-verificações, reparação e para o envio de informações sobre o estado do cliente para o site. O cliente executa os auto-controlos de acordo com um horário que configura. O cliente envia os resultados dos cheques para o site do Gestor de Configuração. Estas informações são encriptadas durante a transferência.  

As informações sobre o estado do cliente são armazenadas na base de dados do Gestor de Configuração no seu servidor SQL, e não são enviadas para a Microsoft. A informação não é armazenada em formato encriptado na base de dados do site. Esta informação é retida na base de dados até ser eliminada de acordo com o valor configurado para o histórico de estado do **cliente de Reter para o número seguinte de dias** de definição de estado do cliente. O valor predefinido para esta definição é de 31 dias.  

Antes de instalar o cliente do Gestor de Configuração com verificação do estado do cliente, considere os seus requisitos de privacidade.  


## <a name="privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a>Informações de privacidade para dispositivos móveis que são geridos com o Conector do Servidor de Intercâmbio  

O Conector de Servidores de Câmbio encontra e gere dispositivos que se ligam a um servidor de câmbio no local ou hospedado utilizando o protocolo ActiveSync. Os registos encontrados pelo Conector do Servidor de Câmbio são armazenados na base de dados do Gestor de Configuração no seu servidor SQL. A informação é recolhida no Servidor de Câmbio. Não contém nenhuma informação adicional do que os dispositivos móveis enviam para o Exchange Server.  

A informação do dispositivo móvel não é enviada para a Microsoft. As informações do dispositivo móvel são armazenadas na base de dados do Gestor de Configuração no seu servidor SQL. A informação é retida na base de dados até que seja eliminada pela tarefa de manutenção do site Eliminar Dados de **DescobertaS Envelhecidas** a cada 90 dias. Configura o intervalo de eliminação.  

Antes de instalar e configurar o conector do Exchange Server, considere os requisitos de privacidade.  

Pode saber mais sobre a recolha e utilização de dados da Microsoft na Declaração de Privacidade da [Microsoft.](https://privacy.microsoft.com/privacystatement)
