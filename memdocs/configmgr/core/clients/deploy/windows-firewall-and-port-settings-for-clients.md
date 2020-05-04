---
title: Definições de firewall e porta do cliente do Windows
titleSuffix: Configuration Manager
description: Selecione as definições de Firewall do Windows e porta para clientes no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713969"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Windows Firewall e definições de porta para clientes em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os computadores clientes do Configurmanager que executam o Windows Firewall muitas vezes exigem que configure exceções para permitir a comunicação com o seu site. As exceções que deve configurar dependem das funcionalidades de gestão que utiliza com o cliente do Gestor de Configuração.  

 Utilize as secções seguintes para identificar estas funcionalidades de gestão e para mais informações sobre como configurar a Firewall do Windows para estas exceções.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Modificar as Portas e Programas Permitidos pela Firewall do Windows  
 Utilize o seguinte procedimento para modificar as portas e programas no Windows Firewall para o cliente do Gestor de Configuração.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Para modificar as portas e programas permitidos pela Firewall do Windows  

1.  No computador que executa a Firewall do Windows, abra o Painel de Controlo.  

2.  Clique com o botão direito do rato em **Firewall do Windows**e, em seguida, clique em **Abrir**.  

3.  Configure as exceções necessárias e as portas e programas personalizados de que necessita.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programas e Portas Requeridos pelo Configuration Manager  
 As seguintes funcionalidades do Gestor de Configuração requerem exceções na Firewall do Windows:  

### <a name="queries"></a>Consultas  
 Se executar a consola Do Gestor de Configuração num computador que executa o Windows Firewall, as consultas falham na primeira vez que são executadas e o sistema operativo apresenta uma caixa de diálogo a perguntar se pretende desbloquear statview.exe. Se desbloquear statview.exe, as consultas posteriores serão executadas sem erros. Também pode adicionar manualmente Statview.exe à lista de programas e serviços no separador **Exceções** da Firewall do Windows antes de executar uma consulta.  

### <a name="client-push-installation"></a>Instalação Push do Cliente  
 Para utilizar o impulso do cliente para instalar o cliente Do Gestor de Configuração, adicione o seguinte como exceções ao Firewall do Windows:  

-   Saída e entrada: **Partilha de Ficheiros e Impressoras**  

-   Entrada: **Windows Management Instrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Instalação de Cliente Utilizando a Política de Grupo  
 Para utilizar a Política de Grupo para instalar o cliente do Gestor de Configuração, adicione a Partilha de **Ficheiros e Impressoras** como exceção ao Firewall do Windows.  

### <a name="client-requests"></a>Pedidos de Cliente  
 Para que os computadores clientes se comuniquem com os sistemas de site do Gestor de Configuração, adicione o seguinte como exceções ao Firewall do Windows:  

 Saída: Porta TCP **80** (para comunicação HTTP)  

 Saída: Porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Estes são os números de porta padrão que podem ser alterados no Gestor de Configuração. Para mais informações, consulte Como configurar as portas de [comunicação do cliente](../../../core/clients/deploy/configure-client-communication-ports.md). Se os valores predefinidos destas portas tiverem sido alterados, também deve configurar exceções correspondentes na Firewall do Windows.  

### <a name="client-notification"></a>Notificação de cliente  
 Para o ponto de gestão notificar os computadores clientes sobre uma ação que deve tomar quando um utilizador administrativo seleciona uma ação do cliente na consola Do Gestor de Configuração, como descarregamento de política de computador ou iniciar uma varredura de malware, adicione o seguinte como uma exceção ao Firewall do Windows:  

 Saída: Porta TCP **10123**  

 Se esta comunicação não for bem sucedida, o Gestor de Configuração volta automaticamente a utilizar a porta de comunicação de pontos cliente-gestão existente de HTTP, ou HTTPS:  

 Saída: Porta TCP **80** (para comunicação HTTP)  

 Saída: Porta TCP **443** (para comunicação HTTPS)  

> [!IMPORTANT]  
>  Estes são os números de porta padrão que podem ser alterados no Gestor de Configuração. Para mais informações, consulte [Como configurar as portas](../../../core/clients/deploy/configure-client-communication-ports.md)de comunicação dos clientes . Se os valores predefinidos destas portas tiverem sido alterados, também deve configurar exceções correspondentes na Firewall do Windows.  

### <a name="remote-control"></a>Controlo Remoto  
 Para utilizar o controlo remoto do Gestor de Configuração, permita a seguinte porta:  

-   Entrada: Porta TCP **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Assistência Remota e Ambiente de Trabalho Remoto  
 Para iniciar a Assistência Remota a partir da consola Do Gestor de Configuração, adicione o programa personalizado **Helpsvc.exe** e a porta personalizada TCP **135** à lista de programas e serviços permitidos no Windows Firewall no computador cliente. Deve também permitir **Assistência Remota** e **Ambiente de Trabalho Remoto**. Se iniciar a Assistência Remota a partir do computador cliente, a Firewall do Windows configura e permite automaticamente **Assistência Remota** e **Ambiente de Trabalho Remoto**.  

### <a name="wake-up-proxy"></a>Proxy de Reativação  
 Se ativar a definição de cliente do proxy de reativação, um novo serviço com a designação Proxy de Reativação do ConfigMgr utiliza um protocolo ponto a ponto para verificar se outros computadores estão ativos na sub-rede e ativa-os se for necessário. Esta comunicação utiliza as seguintes portas:  

 Saída: Porta UDP **25536**  

 Saída: Porta UDP **9**  

 Estes são os números de porta padrão que podem ser alterados no Gestor de Configuração utilizando as definições dos clientes de **Gestão** de Energia do número de porta de **procuração Wake-up (UDP)** e do número de **porta Wake On LAN (UDP)**. Se especificar a definição de cliente **Gestão de Energia**: **Exceção da Firewall do Windows para proxy de reativação** , estas portas são configuradas automaticamente na Firewall do Windows para clientes. No entanto, se os clientes executarem uma firewall diferente, tem de configurar manualmente as exceções para estes números de porta.  

 Além destas portas, o proxy de reativação também utiliza mensagens de pedido de eco de ICMP (Internet Control Message Protocol) de um computador cliente para outro computador cliente. Esta comunicação é utilizada para confirmar se o outro computador cliente está ativo na rede. Por vezes, o ICMP é também referido como comandos ping de TCP/IP.  

 Para mais informações sobre o wake-up proxy, consulte [Plan como acordar os clientes](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Visualizador de Eventos do Windows, Monitor de Desempenho do Windows e Diagnóstico do Windows  
 Para aceder ao Windows Event Viewer, Windows Performance Monitor e Windows Diagnostics da consola 'Gestor de Configuração', ativa a partilha de **ficheiros e impressoras** como exceção no Windows Firewall.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Portas Utilizadas Durante a Implementação do Cliente do Configuration Manager  
 As tabelas seguintes listam as portas que são utilizadas durante o processo de instalação do cliente.  

> [!IMPORTANT]  
>  Se existir uma firewall entre os servidores do sistema de sites e o computador cliente, confirme se a firewall permite tráfego para as portas que são necessárias para o método de instalação do cliente que selecionou. Por exemplo, as firewalls impedem frequentemente que a instalação push seja bem sucedida porque bloqueiam o Bloco de Mensagem de Servidor (SMB) e as Chamadas de Procedimento Remoto (RPC). Neste cenário, utilize um método diferente de instalação do cliente, tal como a instalação manual (com CCMSetup.exe) ou a instalação do cliente baseada na Política de Grupo. Estes métodos alternativos de instalação do cliente não necessitam de SMB ou RPC.  

 Para obter informações sobre como configurar a Firewall do Windows no computador cliente, consulte [Modificar as Portas e Programas Permitidos pela Firewall do Windows](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Portas que são utilizadas para todos os métodos de instalação  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de estado de contingência, quando está atribuído um ponto de estado de contingência ao cliente.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Portas que são utilizadas com a instalação push do cliente  
 Além das portas listadas na tabela a seguir, a instalação push do cliente também utiliza mensagens de pedido de eco ICMP (Internet Control Message Protocol) do servidor do site para o computador cliente para confirmar se este está disponível na rede. Por vezes, o ICMP é também referido como comandos ping de TCP/IP. O ICMP não tem um número de protocolo UDP ou TCP e, por isso, não está listado na tabela a seguir. No entanto, quaisquer dispositivos de rede intervenientes, tais como firewalls, devem permitir tráfego ICMP para que a instalação push do cliente seja bem sucedida.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o servidor do site e o computador cliente.|--|445|  
|Mapeador de pontos finais RPC entre o servidor do site e o computador cliente.|135|135|  
|Portas dinâmicas RPC entre o servidor do site e o computador cliente.|--|DINÂMICO|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Portas que são utilizadas com a instalação baseada em ponto de atualização de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para o ponto de atualização de software.|--|80 ou 8530 (Ver nota 2, **Windows Server Update Services**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para o ponto de atualização de software.|--|443 ou 8531 (Ver nota 2, **Windows Server Update Services**)|  
|Bloco de Mensagens do Servidor (SMB) entre o servidor de origem e o computador cliente quando especifica a propriedade /fonte da linha de comando CCMSetup/ **fonte:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Portas que são utilizadas com a instalação baseada na Política de Grupo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de gestão quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Bloco de Mensagens do Servidor (SMB) entre o servidor de origem e o computador cliente quando especifica a propriedade /fonte da linha de comando CCMSetup/ **fonte:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Portas que são utilizadas com a instalação manual e com a instalação baseada em scripts de início de sessão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o computador cliente e uma partilha de rede a partir da qual o CCMSetup.exe é executado.<br /><br /> Quando instala o Gestor de Configuração, os ficheiros de * &lt;\>* origem de instalação do cliente são copiados e automaticamente partilhados a partir da pasta InstallationPath \Client em pontos de gestão. No entanto, pode copiar esses ficheiros e criar uma nova partilha em qualquer computador na rede. Em alternativa, pode eliminar este tráfego de rede executando o CCMSetup.exe localmente, por exemplo, utilizando um suporte de dados amovível.|--|445|  
|Protocolo de Transferência de Hipertextos (HTTP) do computador cliente para um ponto de gestão quando a ligação está sobre http, e não especifica a **propriedade/fonte&lt;\>** da linha de comando CCMSetup: Caminho .|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Secure Hypertext Transfer Protocol (HTTPS) do computador cliente para um ponto de gestão quando a ligação está acima DE HTTPS, e não especifica a **propriedade/fonte&lt;\>** da linha de comando CCMSetup: Caminho .|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Bloco de Mensagens do Servidor (SMB) entre o servidor de origem e o computador cliente quando especifica a propriedade /fonte da linha de comando CCMSetup/ **fonte:&lt;Caminho\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Portas que são utilizadas com a instalação baseada em distribuição de software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB) entre o ponto de distribuição e o computador cliente.|--|445|  
|Protocolo HTTP (Hypertext Transfer Protocol) do computador cliente para um ponto de distribuição quando a ligação é efetuada através de HTTP.|--|80 (Ver nota 1, **Porta Alternativa Disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol) do computador cliente para um ponto de distribuição quando a ligação é efetuada através de HTTPS.|--|443 (Ver nota 1, **Porta Alternativa Disponível**)|  

## <a name="notes"></a>Notas  
 **1 Porta Alternativa Disponível** No Gestor de Configuração, pode definir uma porta alternativa para este valor. Se tiver sido definida uma porta personalizada, substitua-a quando definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

 **2 Windows Server Update Services** É possível instalar o Windows Server Update Service (WSUS) no Web site predefinido (porta 80) ou num Web site personalizado (porta 8530).  

 Após a instalação, é possível alterar a porta. Não é necessário utilizar o mesmo número de porta ao longo da hierarquia do site.  

 Se a porta HTTP for 80, a porta HTTPS tem de ser 443.  

 Se a porta HTTP for outra coisa, a porta HTTPS deve ser 1 mais alta. Por exemplo, 8530 e 8531.
