---
title: Criar aplicações de servidor Linux e UNIX
titleSuffix: Configuration Manager
description: Veja quais as considerações que deve ter em conta quando cria e implementa aplicações para dispositivos Linux e Unix.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075800"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Criar aplicações de servidor Linux e UNIX com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Tenha em conta as seguintes considerações quando criar e implementar aplicações para computadores que executam o Linux e o UNIX.  

## <a name="general-considerations"></a>Considerações gerais  
 O cliente do Gestor de Configuração do Linux e da UNIX suporta implementações de **software que utilizam pacotes e programas.** Não é possível implementar aplicações do Gestor de Configuração para computadores que executam o Linux e o UNIX.  

 As capacidades de implementação de software Linux e UNIX incluem:  

-   Instalação de software para servidores Linux e UNIX, incluindo as seguintes capacidades:  

    -   Implementação de novo software  

    -   Atualizações de software para programas que já estão num computador  

    -   Patches osso  

-   Comandos Linux nativos e UNIX, e scripts que estão localizados em servidores Linux e UNIX  

-   Implementações que se limitam aos sistemas operativos que especifica quando seleciona a opção do programa **apenas em plataformas de clientes especificadas**

-   Janelas de manutenção para controlar quando o software é instalado

-   Mensagens de estado de implementação para monitorizar as implementações  

-   A opção para o cliente acelerar o uso da rede quando está a descarregar software a partir de um ponto de distribuição  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Diferenças entre a implementação para computadores Linux e UNIX e a implementação para dispositivos Windows
As principais diferenças entre a implementação de pacotes e programas para computadores Linux e UNIX e a implementação de pacotes e programas para dispositivos Windows são as seguintes:  

|Configuração|Detalhes|  
|-------------------|-------------|  
|Utilize apenas configurações destinadas a computadores e não utilize configurações destinadas aos utilizadores.|O cliente do Gestor de Configuração do Linux e da UNIX não suporta configurações que se destinam aos utilizadores.|  
|Configure programas para descarregar software a partir do ponto de distribuição e executar os programas a partir da cache do cliente local.|O cliente do Gestor de Configuração da Linux e da UNIX não suporta o software de funcionamento a partir do ponto de distribuição. Em vez disso, tem de configurar o software para descarregar para o cliente e depois ser instalado.<br /><br /> Por padrão, após o cliente da Linux e da UNIX instalar o software, esse software é eliminado da cache do cliente. No entanto, os pacotes configurados com **conteúdo persistna na cache do cliente** não são eliminados do cliente e permanecem na cache do cliente após a instalação do software.<br /><br /> O cliente da Linux e da UNIX não suporta configurações para a cache do cliente, e o tamanho máximo da cache do cliente é limitado apenas pelo espaço de disco gratuito no computador cliente.|  
|Configurar a Conta de Acesso à Rede para acesso aos pontos de distribuição|Os computadores com Linux e UNIX são concebidos para serem computadores de grupo de trabalho. Para aceder aos pacotes a partir do ponto de distribuição no domínio do servidor do site do Gestor de Configuração, tem de configurar a Conta de Acesso à Rede para o site. Terá de especificar esta conta como uma propriedade do componente de distribuição de software e configurar a conta antes da implementação do software.<br /><br /> Pode configurar várias Contas de Acesso de Rede em cada site. O cliente para Linux e UNIX poderá utilizar cada uma das contas que configurar como Conta de Acesso à Rede.<br /><br /> Para mais informações, consulte os componentes do Site para O Gestor de [Configuração](../../core/servers/deploy/configure/site-components.md).|  

 Poderá implementar pacotes e programas para coleções que contenham apenas clientes Linux ou UNIX ou implementá-los em coleções que contenham uma mistura de tipos de cliente, como a **Coleção Todos os Sistemas**. No entanto, os clientes não-Linux e não-UNIX não instalam o software nem reportam falhas.  

 Quando o cliente do Gestor de Configuração do Linux e da UNIX recebe e executa uma implementação, gera mensagens de estado. Pode visualizar estas mensagens de estado na consola do Gestor de Configuração ou utilizando relatórios para monitorizar o estado de implementação.  

 Para obter informações sobre como usar pacotes e programas, consulte [Pacotes e programas.](../../apps/deploy-use/packages-and-programs.md)  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configure pacotes, programas e implementações para servidores Linux e UNIX  
 Pode criar e implementar pacotes e programas utilizando as opções padrão disponíveis na consola 'Gestor de Configuração'. O cliente não requer configurações únicas.  

 Utilize as informações nas seguintes secções para configurar pacotes e programas e implementações.  

### <a name="packages-and-programs"></a>Pacotes e programas  
 Para criar um pacote e programa para um servidor Linux ou UNIX, utilize o **Create Package e o Program Wizard** da consola 'Gestor de Configuração'. O cliente para Linux e UNIX suporta a maior parte das definições de pacotes e programas. No entanto, várias configurações não são suportadas. Quando criar ou configurar um pacote e programa, considere os seguintes pontos:  

-   Inclua os tipos de ficheiros que são suportados pelos computadores de destino.  

-   Defina as linhas de comando adequadas para utilização no computador de destino.  

-   Tenha em mente que as definições que interagem com os utilizadores não são suportadas.  

A tabela seguinte lista as propriedades para pacotes e programas que não são suportados:  

|Propriedade de pacote e programa|Comportamento|Mais informações|  
|----------------------------------|--------------|----------------------|  
|Definições de partilha de pacote:<br /><br /> - Todas as opções|Um erro é gerado e a instalação do software falha|O cliente não suporta esta configuração. Em vez disso, o cliente terá de transferir o software utilizando HTTP ou HTTPS e executar a linha de comandos a partir da respetiva cache local.|  
|Definições de atualização do pacote:<br /><br /> - Desligar os utilizadores dos pontos de distribuição|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Definições de implementação do sistema operativo:<br /><br /> - Todas as opções|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Relatórios:<br /><br /> - Utilize propriedades de pacote para a correspondência mif do estado<br /><br /> - Utilize estes campos para a correspondência do Estado MIF|As definições são ignoradas|O cliente não suporta o uso de ficheiros MIF de estado.|  
|**Executar:**<br /><br /> - Todas as opções|As definições são ignoradas|O cliente executa sempre os pacotes sem interface do utilizador.<br /><br /> O cliente ignora todas as opções de configuração de Executar.|  
|Após a execução:<br /><br />- Gestor de Configuração reinicia computador<br /><br /> - Os controlos do programa reiniciam<br /><br /> - Gestor de Configuração assina o utilizador|Um erro é gerado e a instalação do software falha|A definição de reinício do sistema e as definições específicas do utilizador não são suportadas.<br /><br /> Quando é utilizada qualquer definição exceto **Não é necessária nenhuma ação** , o cliente gera um erro e continua a instalar o software sem tomar qualquer ação.|  
|Programa pode ser executado:<br /><br /> - Só quando um utilizador é inscrito|Um erro é gerado e a instalação do software falha|As definições específicas do utilizador não são suportadas.<br /><br /> Quando esta opção se encontra configurada, o cliente gera um erro e a instalação do software falha.<br /><br /> As outras opções são ignoradas e a instalação do software continua.|  
|Modo de execução:<br /><br /> - Correr com os direitos do utilizador|As definições são ignoradas|As definições específicas do utilizador não são suportadas.<br /><br /> No entanto, o cliente suporta a configuração em execução com direitos administrativos.<br /><br /> Quando especifica **executar com direitos administrativos,** o cliente do Gestor de Configuração utiliza as suas credenciais de raiz.<br /><br /> Esta definição não gera um erro ou entrada de registo. Em vez disso, a instalação do software falha quando o cliente gera um erro para a configuração pré-requisito do **Programa só pode ser executado** = **quando um utilizador é inscrito em**.|  
|Permitir que os utilizadores vejam e interajam com a instalação do programa|As definições são ignoradas|As definições específicas do utilizador não são suportadas.<br /><br /> Esta configuração é ignorada e a instalação do software continua.|  
|Modo de unidade:<br /><br /> - Todas as opções|As definições são ignoradas|Esta configuração não é suportada porque o conteúdo é sempre descarregado para o cliente e executado localmente.|  
|Executar outro programa primeiro|Um erro é gerado e a instalação do software falha|A instalação do programa recursivo não é suportada.<br /><br /> Quando um programa é configurado para executar outro programa primeiro, a instalação do software falha e a instalação do outro programa não é iniciada.|  
|Quando este programa é atribuído a um computador:<br /><br /> - Corra uma vez para cada utilizador que se inscreve|As definições são ignoradas|As definições específicas do utilizador não são suportadas.<br /><br /> No entanto, o cliente suporta a configuração que funciona uma vez para o computador.<br /><br /> Esta definição não gera um erro ou entrada de registo porque já é criado um erro e uma entrada de registo para a configuração pré-requisito do **Programa só pode ser executado** = **quando um utilizador está ligado**.|  
|Suprimir notificações do programa|As definições são ignoradas|O cliente não implementa uma interface de utilizador.<br /><br /> Quando esta configuração é selecionada, é ignorada e a instalação do software continua.|  
|Desative este programa em computadores onde está implantado|As definições são ignoradas|Esta definição não é suportada e não afeta a instalação de software.|  
|Permitir que este programa seja instalado a partir da sequência de tarefas do Pacote de Instalação sem ser implementado||O cliente não suporta sequências de tarefas.<br /><br /> Esta definição não é suportada e não afeta a instalação de software.|  
|Windows Installer:<br /><br /> - Todas as opções|As definições são ignoradas|O cliente não suporta ficheiros ou definições do Instalador do Windows.|  
|Modo de Manutenção do OpsMgr:<br /><br /> - Todas as opções|As definições são ignoradas|O cliente não suporta esta configuração.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Implementar software para um servidor Linux ou UNIX
 Para implementar software para um servidor Linux ou UNIX utilizando um pacote e programa, pode utilizar o Assistente de **Software de Implementação** a partir da consola Do Gestor de Configuração. A maioria das definições de implementação são suportadas pelo cliente para Linux e UNIX. No entanto, várias configurações não são suportadas. Quando implementar software, considere os seguintes pontos:  

- Forme o pacote em pelo menos um ponto de distribuição que esteja associado a um grupo de limites que está configurado para a localização do conteúdo.  

- O cliente da Linux e da UNIX que recebe esta implementação deve poder aceder a este ponto de distribuição a partir da sua localização de rede.  

- O cliente para Linux e UNIX transfere o pacote a partir do ponto de distribuição e executa o programa no computador local.  

- O cliente da Linux e da UNIX não pode descarregar pacotes de pastas partilhadas. Descarrega pacotes a partir de pontos de distribuição ativados pelo IIS que suportam HTTP ou HTTPS.  

  A tabela seguinte lista propriedades para implementações que não são suportadas:  

|Propriedade de implementação|Comportamento|Mais informações|  
|-------------------------|--------------|----------------------|  
|Definições de implementação - objetivo:<br /><br /> - Disponível<br /><br /> - Obrigatório|As definições são ignoradas|As definições específicas do utilizador não são suportadas.<br /><br /> No entanto, o cliente suporta a definição **necessária**, que aplica o tempo de instalação programado, mas não suporta a instalação manual antes dessa hora programada.|  
|Enviar pacotes de reativação|As definições são ignoradas|O cliente não suporta esta configuração.|  
|Agenda da atribuição:<br /><br /> - assinar<br /><br /> - assinar|Um erro é gerado e a instalação do software falha|As definições específicas do utilizador não são suportadas.<br /><br /> No entanto, o cliente suporta a definição **Logo que possível**.|  
|Definições de notificação:<br /><br /> - Permitir que os utilizadores executem o programa de forma independente das atribuições|As definições são ignoradas|O cliente não implementa uma interface de utilizador.|  
|Quando for atingida a hora agendada da atribuição, permitir a execução das seguintes atividades fora da janela de manutenção:<br /><br /> - Reinício do sistema (se necessário para completar a instalação)|É gerado um erro|O cliente não suporta um reinício do sistema.|  
|Opção de implementação para redes (LAN) rápidas:<br /><br /> - Executar programa a partir do ponto de distribuição|Um erro é gerado e a instalação do software falha|O cliente não pode executar software a partir do ponto de distribuição e, em vez disso, deve descarregar o programa antes de poder executar.|  
|Opção de implementação para uma zona de rede lenta ou pouco fiável ou uma localização de origem de contingência para o conteúdo:<br /><br /> - Permitir que os clientes partilhem conteúdos com outros clientes na mesma subnet|As definições são ignoradas|O cliente não suporta partilhar conteúdo entre pares.|  

 Para obter mais informações sobre a localização do conteúdo, consulte Gerir a infraestrutura de conteúdo e conteúdo para O Gestor de [Configuração](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Para obter mais informações sobre como criar uma implementação, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a> Gerir a largura de banda da rede para transferências de software a partir de pontos de distribuição  
 O cliente Linux e UNIX suporta controlos de largura de banda da rede quando está a descarregar software a partir de um ponto de distribuição.  

 O cliente utiliza as definições de Transferência Inteligente de Fundo (BITS) que configura como configurações do cliente no Gestor de Configuração, mas não implementa BITS. Em vez disso, para otimizar a utilização da largura de banda de rede, o cliente controla o tamanho dos segmentos de pedidos HTTP e o atraso entre segmentos na transferência de software.  

 Para configurar um cliente para utilizar controlos de largura de banda de rede, configure as definições de cliente para **Transferência Inteligente em Segundo Plano** e aplique as definições ao computador cliente. Para utilizar os controlos de largura de banda, o cliente deve receber as definições do cliente para **a Transferência Inteligente de Fundo** com as seguintes definições configuradas como **Sim:**  

- **Limitar a largura de banda de rede máxima para transferências BITS em segundo plano**  

  O cliente suporta as seguintes configurações de Transferência Inteligente em Segundo Plano:  

  -   **Hora de início da janela de limitação**  

  -   **Hora de fim da janela de limitação**  

  -   **Velocidade máxima de transferência durante a janela de limitação (Kbps)**  

  -   **Velocidade máxima de transferência fora da janela de limitação (Kbps)**  

A seguinte configuração de Transferência Inteligente em Segundo Plano não é suportada, sendo ignorada pelo cliente para Linux e UNIX:  

- **Permitir transferências BITS fora da janela de limitação**  

  Se o download de software para o cliente a partir de um ponto de distribuição for interrompido, o cliente da Linux e da UNIX não retoma o download. Em vez disso, reinicia o download de todo o pacote de software.  

##  <a name="configure-operations-for-software-deployments"></a>Configurar operações para implementações de software  
 Da mesma forma que o cliente do Windows, o cliente do Gestor de Configuração do Linux e da UNIX descobre novas implementações de software quando faz sondagens e verifica a nova política. A frequência com que o cliente verifica a existência de novas políticas depende das definições de cliente. Poderá configurar janelas de manutenção para controlar quando ocorrem implementações de software.  

 Poderá configurar as implementações de software em servidores Linux e UNIX utilizando propriedades de pacote, propriedades de programa e propriedades de implementação.  

 Ao receber a política para uma implementação, o cliente submete uma mensagem de estado. Também envia mensagens de estado quando inicia a instalação do software e quando a instalação termina ou falha.  

 Os programas para implementações de software funcionam com as credenciais de raiz com as quais o cliente do Gestor de Configuração para o Linux e uniX funciona. O código de saída do comando do programa é utilizado para determinar o êxito ou falha. O código de saída 0 (zero) é tratado como êxito. Além disso, o **stdout** (sequência de saída padrão) e o **stderr** (sequência de erro padrão) são copiados para o ficheiro de registo quando o nível de registo é definido como INFO ou RASTREIO.  

> [!TIP]  
>  Se o software que pretender implementar estiver localizado numa partilha NFS (Network File System) a que o servidor Linux ou UNIX consiga aceder, não precisará de utilizar um ponto de distribuição para transferir o pacote. Em vez disso, ao criar o pacote, não selecione a caixa de verificação **Este pacote contém ficheiros de origem**. Em seguida, ao configurar o programa, especifique a linha de comandos adequada para aceder diretamente ao pacote no ponto de montagem NFS.  
