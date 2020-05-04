---
title: Segurança e privacidade para apps
titleSuffix: Configuration Manager
description: Orientações e recomendações para segurança e privacidade na gestão de aplicações no Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709958"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Segurança e privacidade para gestão de aplicações em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

## <a name="security-guidance-for-application-management"></a>Orientação de segurança para gestão de aplicações  

### <a name="use-the-software-center-without-the-application-catalog"></a>Utilize o Centro de Software sem o catálogo de aplicações

<!--1358309-->

A experiência de utilizador silverlight do catálogo de aplicações não é suportada a partir da versão atual do ramo 1806. Esta configuração ajuda-o a reduzir a infraestrutura do servidor necessária para entregar aplicações aos utilizadores.

A partir da versão 1906, os clientes atualizados utilizam automaticamente o ponto de gestão para implementações de aplicações disponíveis pelo utilizador. Também não pode instalar novas funções de catálogo de aplicações. O suporte termina para as funções de catálogo de aplicações com a versão 1910. A redução da infraestrutura do servidor também reduz a superfície de ataque.

Para proporcionar uma experiência de aplicação consistente e segura para clientes baseados na Internet, utilize o Azure Ative Directory e o portal de gestão de nuvem.

Para mais informações, consulte [Configure Software Center](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Utilizar HTTPS com o catálogo de aplicações

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Configure o ponto do site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações para aceitar ligações HTTPS. Com esta configuração, o servidor é autenticado para os utilizadores. Os dados transmitidos estão protegidos contra adulteração e visualização.

Ajude a prevenir ataques de engenharia social educando os utilizadores a penas que se conectam apenas a sites fidedignos. Educar os utilizadores sobre os perigos de sites maliciosos.

Quando não utilizar HTTPS, não utilize as opções de configuração da marca. Estas configurações mostram o nome da sua organização no catálogo de aplicações como prova de identidade.  


### <a name="use-role-separation"></a>Usar a separação de papéis

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Instale o ponto de site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações em servidores separados. Se o ponto do site estiver comprometido, é separado do ponto de serviço web. Este design ajuda a proteger os clientes e infraestruturas do Gestor de Configuração. Esta configuração é especialmente importante se o ponto do site aceitar as ligações do cliente a partir da internet. Torna o servidor mais vulnerável a ataques.  

### <a name="close-browser-windows"></a>Feche as janelas do navegador

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Instrua os utilizadores a fecharem a janela do navegador quando terminarem a utilização do catálogo de aplicações. Se os utilizadores navegarem para um website externo na mesma janela do navegador que utilizaram para o catálogo de aplicações, o navegador continua a utilizar as definições de segurança que são adequadas para sites fidedignos na intranet.  

### <a name="centrally-specify-user-device-affinity"></a>Especificar centralmente a finção do dispositivo do utilizador

Especifique manualmente a afinidade do dispositivo do utilizador em vez de permitir que os utilizadores identifiquem o seu dispositivo principal. Não ative a configuração baseada no uso.

Não considere que a informação recolhida dos utilizadores ou do dispositivo seja autoritária. Se implementar software utilizando a afinidade do dispositivo de utilizador que um administrador de confiança não especifica, o software poderá ser instalado em computadores e utilizadores que não estejam autorizados a receber esse software.  

### <a name="dont-run-deployments-from-distribution-points"></a>Não faça implantações a partir de pontos de distribuição

Configure sempre as implementações para transferirem conteúdo a partir de pontos de distribuição em vez de executarem a partir destes. Quando configura as implementações para descarregar conteúdo a partir de um ponto de distribuição e executar localmente, o cliente do Gestor de Configuração verifica o hash do pacote depois de descarregar o conteúdo. O cliente descarta o pacote se o hash não corresponder ao hash na apólice.

Se configurar a implementação para funcionar diretamente a partir de um ponto de distribuição, o cliente do Gestor de Configuração não verifica o hash do pacote. Este comportamento significa que o cliente do Gestor de Configuração pode instalar software que tenha sido adulterado.

Se tiver de executar as implementações diretamente a partir de pontos de distribuição, utilize menos permissões NTFS nos pacotes nos pontos de distribuição. Utilize também a segurança do protocolo de internet (IPsec) para proteger o canal entre o cliente e os pontos de distribuição, e entre os pontos de distribuição e o servidor do site.

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a>Não deixe que os utilizadores interajam com processos elevados
  
Se ativar as opções de **Executar com direitos administrativos** ou **instalar para o sistema,** não deixe que os utilizadores interajam com essas aplicações. Quando configurar uma aplicação, pode definir a opção de **permitir que os utilizadores vejam e interajam com a instalação do programa.** Esta definição permite que os utilizadores respondam a quaisquer solicitações necessárias na interface do utilizador. Se configurar também a aplicação para **Executar com direitos administrativos**, ou começar na versão 1802 **Instalar para sistema**, um intruso no computador que executa o programa poderia usar a interface do utilizador para aumentar privilégios no computador cliente.

Utilize programas que utilizem o Instalador do Windows para configuração e privilégios elevados por utilizador para implementações de software que requerem credenciais administrativas. A configuração deve ser executada no contexto de um utilizador que não tenha credenciais administrativas. Os privilégios elevados do Instalador do Windows por utilizador fornecem a forma mais segura de implementar aplicações que tenham este requisito.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Restringir se os utilizadores podem instalar software interativamente

Configure a definição de cliente de **instalações** no grupo **Agente Informático.** Esta definição restringe os tipos de utilizadores que podem instalar software no Software Center.

Por exemplo, crie uma definição personalizada de cliente com **Permissões de instalação** definida como **Apenas administradores**. Aplique esta definição de cliente numa coleção de servidores. Esta configuração impede os utilizadores sem permissões administrativas de instalarem software nesses servidores.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>Em dispositivos móveis, implemente apenas aplicações assinadas.

Implementar aplicações de dispositivos móveis apenas se forem assinadas por código por uma autoridade de certificação (CA) em que o dispositivo móvel confia.

Por exemplo:

- Uma aplicação de um fornecedor, que é assinada por um conhecido CA como VeriSign.  

- Uma aplicação interna que assine independentemente do Gestor de Configuração utilizando o seu CA interno.  

- Uma aplicação interna que assina utilizando o Gestor de Configuração quando cria o tipo de aplicação e utiliza um certificado de assinatura.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Garantir a localização do certificado de assinatura de aplicação de dispositivo móvel

Se assinar aplicações de dispositivomóvel utilizando o **Assistente de Aplicação Criar** no Gestor de Configuração, proteja a localização do ficheiro de certificado de assinatura e proteja o canal de comunicação. Para ajudar a proteger contra a elevação de privilégios e contra ataques man-in-the-middle, guarde o ficheiro de certificado de assinatura numa pasta segura.

Utilize iPsec entre os seguintes computadores:

- O computador que executa a consola Do Gestor de Configuração
- O computador que armazena o ficheiro de assinatura de certificado
- O computador que armazena os ficheiros de origem da aplicação

Em alternativa, assine a aplicação independente do Gestor de Configuração e antes de executar o Assistente de **Aplicação Criar**.

### <a name="implement-access-controls"></a>Implementar controlos de acesso

Para proteger computadores de referência, implemente os controlos de acesso. Quando configurar o método de deteção num tipo de implementação navegando para um computador de referência, certifique-se de que o computador não está comprometido.

### <a name="restrict-and-monitor-administrative-users"></a>Restringir e monitorizar os utilizadores administrativos

Restringir e monitorizar os utilizadores administrativos que concede as seguintes funções de segurança baseadas em funções de gestão de aplicações:

- **Administrador de Aplicações**
- **Autor da Aplicação**
- **Gestor de Implementação de Aplicações**

Mesmo quando configura a administração baseada em funções, os utilizadores administrativos que criem e implementem aplicações poderão ter mais permissões do que pensa. Por exemplo, os utilizadores administrativos que criam ou alteram uma aplicação podem selecionar aplicações dependentes que não estejam no seu âmbito de segurança.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Configure aplicações App-V em ambientes virtuais com o mesmo nível de confiança

Quando configurar ambientes virtuais de virtualização de aplicações da Microsoft (App-V), selecione aplicações que tenham o mesmo nível de confiança no ambiente virtual. Como as aplicações num ambiente virtual App-V podem partilhar recursos, como a área de clipboard, configurar o ambiente virtual para que as aplicações selecionadas tenham o mesmo nível de confiança.

Para mais informações, consulte [Create App-V ambientes virtuais](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Certifique-se de que as aplicações macOS são de uma fonte confiável

Se implementar aplicações para dispositivos macOS, certifique-se de que os ficheiros de origem são de uma fonte de confiança. A ferramenta CMAppUtil não valida a assinatura do pacote de origem. Certifique-se de que o pacote vem de uma fonte em que confia. A ferramenta CMAppUtil não consegue detetar se os ficheiros foram adulterados.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Proteja o ficheiro cmmac para aplicações macos

Se implementar aplicações para computadores macOS, proteja a localização do ficheiro **.cmmac.** A ferramenta CMAppUtil gera este ficheiro e, em seguida, importa-o para O Gestor de Configuração. Este ficheiro não está assinado ou validado.

Proteja o canal de comunicação quando importar este ficheiro para O Gestor de Configuração. Para ajudar a evitar a adulteração deste ficheiro, guarde-o numa pasta segura. Utilize iPsec entre os seguintes computadores:

- O computador que executa a consola Do Gestor de Configuração  
- O computador que armazena o ficheiro **.cmmac**  

### <a name="use-https-for-web-applications"></a>Utilizar HTTPS para aplicações web

Se configurar um tipo de implementação de aplicação web, utilize HTTPS para proteger a ligação. Se implementar uma aplicação web utilizando uma ligação HTTP em vez de uma ligação HTTPS, o dispositivo poderá ser redirecionado para um servidor fraudulento. Os dados que são transferidos entre o dispositivo e o servidor podem ser adulterados.


## <a name="security-issues-for-application-management"></a>Problemas de segurança da gestão de aplicações  

- Os utilizadores com direitos restritos podem copiar ficheiros da cache do cliente no computador cliente.  

     Os utilizadores podem ler a cache do cliente, mas não podem escrever para ele. Com permissões de leitura, um utilizador pode copiar ficheiros de instalação de aplicações de um computador para outro.  

- Os utilizadores de baixos direitos podem alterar ficheiros que registam o histórico de implementação de software no computador cliente.  

     Como a informação do histórico da aplicação não está protegida, um utilizador pode alterar ficheiros que reportem se uma aplicação está instalada.  

- Os pacotes de Aplicação-V não estão assinados.  

     Os pacotes App-V no Gestor de Configuração não suportam a assinatura. As assinaturas digitais verificam que o conteúdo é de uma fonte de confiança e não foi alterado em trânsito. Não há atenuação para esta questão de segurança. Siga as melhores práticas de segurança para descarregar o conteúdo de uma fonte fidedigna e de um local seguro.  

- As aplicações de App-V publicadas podem ser instaladas por todos os utilizadores do computador.  

     Quando uma aplicação App-V é publicada num computador, todos os utilizadores que iniciarem sessão nesse computador podem instalar a aplicação. Não é possível restringir os utilizadores que podem instalar a aplicação após a sua publicação.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a>Certificados para Microsoft Silverlight 5 e modo de confiança elevado necessário para o catálogo de aplicações  

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Os clientes do Gestor de Configuração versão 1710 e anteriormente requerem o Microsoft Silverlight 5, que deve funcionar em modo de confiança elevado para os utilizadores instalarem software a partir do catálogo da aplicação. Por predefinição, as aplicações Silverlight são executadas no modo de confiança parcial para impedir que acedam aos dados do utilizador. Se ainda não estiver instalado, o Gestor de Configuração instala automaticamente o Microsoft Silverlight 5 nos clientes. Por predefinição, o Gestor de Configuração define o Agente de Computador **permitir que as aplicações Silverlight executem em** definição elevada do cliente do modo de confiança para **Sim**. Esta definição permite que aplicações silverlight assinadas e fidedignas solicitem um modo de confiança elevado.  

Ao instalar a função do site de pontos do site do catálogo de aplicações, o cliente também instala um certificado de assinatura da Microsoft na loja de certificados de computador Trust Publishers em cada computador cliente do Gestor de Configuração. As aplicações Silverlight assinadas por este certificado funcionam no modo de confiança elevado, que os computadores exigem para instalar software a partir do catálogo de aplicações. O Gestor de Configuração gere automaticamente este certificado de assinatura. Para aumentar a continuidade do serviço, não apague manualmente ou desloque este certificado de assinatura da Microsoft.  

> [!WARNING]  
> Quando ativadas, as aplicações Permitir que as **aplicações Silverlight sejam executadas em modo** de confiança elevado, a definição de cliente permite que todas as aplicações Silverlight, assinadas por certificados na loja de certificados Trust Publishers, na loja de computadores ou na loja de utilizadores, sejam executadas em modo de confiança elevado. A definição do cliente não pode ativar o modo de confiança elevado especificamente para o catálogo de aplicações do Gestor de Configuração ou para a loja de certificados Trust Publishers na loja de computadores. Se o malware adicionar um certificado fraudulento na loja Trusted Publishers, o malware que utiliza a sua própria aplicação Silverlight pode agora também ser executado em modo de confiança elevado.  

Se definir as aplicações Permitir que as **aplicações De Prata executem em** modo de confiança elevado para **Não**, os clientes não removem o certificado de assinatura da Microsoft.  

Para mais informações sobre aplicações fidedignas em Silverlight, consulte [Aplicações Fidedignas](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a> Informações de privacidade da gestão de aplicações  

A gestão de aplicações permite-lhe executar qualquer aplicação, programa ou script em qualquer cliente da hierarquia. O Gestor de Configuração não tem controlo sobre os tipos de aplicações, programas ou scripts que executa ou o tipo de informação que transmitem. Durante o processo de implementação da aplicação, o Gestor de Configuração poderá transmitir informações que identifiquem o dispositivo e as contas de login entre clientes e servidores.  

O Gestor de Configuração mantém informações sobre o estado sobre o processo de implementação do software. As informações sobre o estado de implementação de software não são encriptadas durante a transmissão, a menos que o cliente comunique utilizando HTTPS. A informação do estado não é armazenada de forma encriptada na base de dados.  

A utilização da instalação de aplicações do Gestor de Configuração para instalar remotamente, interactivamente ou silenciosamente software nos clientes pode estar sujeita a termos de licença de software para esse software. Esta utilização é separada dos Termos de Licença de Software para Gestor de Configuração. Reveja sempre e concorde com os Termos de Licenciamento de Software antes de implementar o software utilizando o Gestor de Configuração.  

O Gestor de Configuração recolhe dados de diagnóstico e utilização sobre aplicações, que são utilizados pela Microsoft para melhorar futuras versões. Para mais informações, consulte [Diagnósticos e dados de utilização](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

A implementação da aplicação não acontece por padrão e requer vários passos de configuração.  

As seguintes funcionalidades ajudam a uma implementação eficiente do software:

- **A finção do dispositivo** de utilizador mapeia um utilizador para dispositivos. Um administrador do Gestor de Configuração implementa software para um utilizador. O cliente instala automaticamente o software num ou mais computadores que o utilizador utiliza com mais frequência.  

- **O Centro** de Software é instalado automaticamente num dispositivo quando instala o cliente do Gestor de Configuração. Os utilizadores mudam as definições, navegam e instalam software a partir do Software Center.  

- O catálogo de **aplicações** é um site que permite que os utilizadores solicitem software para instalar.  

    > [!Important]  
    > O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a>Informação sobre privacidade da afinidade do dispositivo do utilizador

- O Gestor de Configuração pode transmitir informações entre clientes e sistemas de site de pontos de gestão. A informação pode identificar o computador e a conta de inscrição e o uso resumido para contas de inscrição.  

- A informação transmitida entre o cliente e o servidor não é encriptada, a menos que o ponto de gestão esteja configurado para exigir que os clientes se comuniquem usando HTTPS.  

- A informação de utilização do computador e da conta de entrada, que é usada para mapear um utilizador para um dispositivo, é armazenada em computadores clientes, enviada para pontos de gestão e depois armazenada na base de dados do Gestor de Configuração. Por predefinição, as informações antigas são eliminadas da base de dados após 90 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Afinidade Dispositivo/Utilizador Desatualizados** .  

- O Gestor de Configuração mantém informações sobre o estado sobre a afinidade do dispositivo do utilizador. A informação de estado não é encriptada durante a transmissão, a menos que os clientes estejam configurados para comunicar com pontos de gestão utilizando HTTPS. A informação sobre o estado não é armazenada de forma encriptada na base de dados.  

- As informações de utilização do computador e do sessão que são utilizadas para estabelecer a afinidade do utilizador e do dispositivo estão sempre ativadas. Os utilizadores e utilizadores administrativos podem fornecer informações sobre afinidade do utilizador.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a>Informações de privacidade do Centro de Software

- O Software Center permite que o administrador do Gestor de Configuração publique qualquer aplicação ou programa ou script para os utilizadores executarem. O Gestor de Configuração não tem controlo sobre os tipos de programas ou scripts que são publicados no catálogo ou o tipo de informação que transmitem.  

- O Gestor de Configuração pode transmitir informações entre os clientes e o ponto de gestão. A informação pode identificar o computador e as contas de inscrição. A informação transmitida entre o cliente e os servidores não é encriptada, a menos que configure o ponto de gestão para exigir que os clientes se conectem utilizando HTTPS.  

- As informações sobre o pedido de aprovação da aplicação estão armazenadas na base de dados do Gestor de Configuração. Os pedidos que são cancelados ou negados e as entradas correspondentes do histórico de pedidos são eliminadas por defeito após 30 dias. O comportamento de eliminação é configurável através da definição da tarefa de manutenção do site **Eliminar Dados de Pedidos de Aplicação Desatualizados** . Os pedidos de aprovação de pedidos que se encontram em estados aprovados e pendentes nunca são eliminados.  

- O Centro de Software é instalado automaticamente quando instala o cliente Do Gestor de Configuração num dispositivo.  

### <a name="application-catalog-privacy-information"></a>Informações de privacidade do catálogo de aplicações

> [!Important]  
> O suporte termina para as funções de catálogo de aplicações com a versão 1910. Para mais informações, consulte [Remova o catálogo de aplicações](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- O catálogo de aplicações não é instalado por defeito. Esta instalação requer vários passos de configuração.  

- O catálogo de aplicações permite que o administrador do Gestor de Configuração publique qualquer aplicação ou programa ou script para os utilizadores executarem. O Gestor de Configuração não tem controlo sobre os tipos de programas ou scripts que são publicados no catálogo ou o tipo de informação que transmitem.  

- O Gestor de Configuração pode transmitir informações entre os clientes e as funções do sistema do site do catálogo de aplicações. A informação pode identificar o computador e as contas de inscrição. A informação transmitida entre o cliente e os servidores não é encriptada, a menos que estas funções do sistema do site estejam configuradas para exigir que os clientes se conectem utilizando HTTPS.  
