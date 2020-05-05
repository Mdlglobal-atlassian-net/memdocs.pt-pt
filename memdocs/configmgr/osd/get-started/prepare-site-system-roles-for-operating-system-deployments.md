---
title: Preparar funções do sistema do site para o OSD
titleSuffix: Configuration Manager
description: Configure as funções do sistema do site antes de implementar sistemas operativos no Gestor de Configuração
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1beec2f5ef7b6da9f1f093300ec6c2b239e7396e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724056"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Preparar funções do sistema do site para implementações de OS com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para implementar sistemas operativos no Gestor de Configuração, prepare primeiro as seguintes funções do sistema do site que requerem configurações e considerações específicas.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Pontos de distribuição  

A função do sistema de pontos de distribuição do site acolhe ficheiros de origem para os clientes descarregarem. Este conteúdo destina-se a aplicações, atualizações de software, imagens de SO, imagens de boot e pacotes de controladores. Controlar a distribuição de conteúdos utilizando opções de largura de banda, estrangulamento e agendamento.  

É importante que tenha pontos de distribuição suficientes para suportar a implementação de sistemas operativos em computadores. Também é importante que planeie a colocação destes pontos de distribuição na sua hierarquia. Para mais informações, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) Este artigo inclui algumas considerações adicionais de planeamento para pontos de distribuição específicos da implantação do OS.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a>Considerações adicionais de planeamento para pontos de distribuição  

Os seguintes itens são coisas de planeamento adicionais a considerar para pontos de distribuição:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Como posso evitar implementações de SO indesejadas?  
O Gestor de Configuração não distingue servidores de sites de outros computadores de destino numa coleção. Se implementar uma sequência de tarefas necessária para uma coleção que inclua um servidor de site, executa a sequência de tarefas da mesma forma que qualquer outro computador da coleção. Certifique-se de que a sua implementação de SO utiliza uma coleção que inclui os clientes pretendidos.  

Gerencie o comportamento para implementações de sequências de tarefas de alto risco. Uma implementação de alto risco é automaticamente instalada num cliente e tem o potencial de causar resultados indesejados. Por exemplo, uma sequência de tarefas com um propósito necessário que implementa um Sistema Operativo. Para reduzir o risco de uma implementação indesejada de alto risco, configure as definições de verificação de implementação. Para mais informações, consulte [Definições para gerir implementações de alto risco](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Quantos computadores podem receber uma imagem de OS de uma só vez a partir de um único ponto de distribuição?  
Para estimar quantos pontos de distribuição precisa, considere as seguintes variáveis:  
- A velocidade de processamento do ponto de distribuição
- A velocidade do disco do ponto de distribuição
- A largura de banda disponível na rede
- O tamanho do pacote de imagem   
  
Por exemplo, se não considerar quaisquer outros fatores de recursos do servidor, o número máximo de computadores que podem processar um pacote de imagem de 4 GB em uma hora numa rede Ethernet de 100 megabit/seg é de 11 computadores.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Se tiver de implantar um SISTEMA para um número específico de computadores dentro de um determinado prazo, distribua a imagem para um número adequado de pontos de distribuição.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Posso colocar um Sistema operativo num ponto de distribuição?  
Pode implantar um SISTEMA num ponto de distribuição, mas a imagem de SO deve ser recebida de um ponto de distribuição diferente.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a>Configurar pontos de distribuição para aceitar pedidos de PXE  

Para implementar sistemas operativos para clientes do Gestor de Configuração que fazem pedidos de arranque PXE, configure um ou mais pontos de distribuição para aceitar pedidos de PXE. Uma vez configurado o ponto de distribuição, ele responde aos pedidos de arranque pXE e determina as medidas de implementação apropriadas a tomar. Para mais informações, consulte [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>Personalize o bloco RamDisk TFTP e os tamanhos das janelas em pontos de distribuição ativados por PXE  

Pode personalizar o bloco RamDisk TFTP e os tamanhos das janelas para pontos de distribuição ativados por PXE. Se personalizar a sua rede, um grande bloco ou tamanho da janela pode fazer com que o download da imagem de arranque falhe com um erro de tempo. As personalizações do bloco RamDisk TFTP e do tamanho da janela permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os seus requisitos de rede específicos. Para determinar qual a configuração mais eficiente, teste as definições personalizadas no seu ambiente.  

-   **Tamanho do bloco TFTP**: O tamanho do bloco é do tamanho dos pacotes de dados que o servidor envia para o cliente que está a descarregar o ficheiro. Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, um grande tamanho de bloco leva a pacotes fragmentados, que a maioria das implementações de clientes PXE não suportam.  

-   **Tamanho da janela de TFTP**: o TFTP precisa de um pacote de confirmação (ACK) para cada bloco de dados enviado. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. A janela TFTP permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. Se aumentar este tamanho da janela, reduz o número de atrasos de ida e volta entre o cliente e o servidor, e diminui o tempo necessário para descarregar uma imagem de arranque.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modificar o tamanho da janela RamDisk TFTP  
Para personalizar o tamanho da janela RamDisk TFTP, adicione a seguinte chave de registo nos pontos de distribuição ativados pelo PXE:  

- **Localização:**`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamdisktFTPWindowSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamanho da janela personalizada)  
    - O valor predefinido é **1** (um bloco de dados preenche a janela).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modificar o tamanho do bloco RamDisk TFTP  
Para personalizar o tamanho da janela RamDisk TFTP, adicione a seguinte chave de registo nos pontos de distribuição ativados pelo PXE:  

- **Localização:**`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nome**: RamdiskTFTPBlockSize  
- **Tipo**: REG_DWORD  
- **Valor**: (tamanho de bloco personalizado)  
    - O valor predefinido é **de 4096**.  

> [!Note]  
> Tanto os Serviços de Implementação do Windows como o serviço de resposta PXE do Gestor de Configuração suportam estas configurações TFTP.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a>Configure pontos de distribuição para suportar multicast  

O multicast é um método de otimização de rede. Use-o em pontos de distribuição quando é provável que vários clientes descarreguem a mesma imagem de OS ao mesmo tempo. Quando utiliza multicast, vários computadores podem simultaneamente descarregar a imagem de OS, uma vez que é multicast pelo ponto de distribuição. Sem multicast, o ponto de distribuição envia uma cópia dos dados a cada cliente sobre uma ligação separada. Para mais informações, consulte [Utilizar o Multicast para implementar o Windows sobre a rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Antes de implementar o SISTEMA, configure um ponto de distribuição para suportar o multicast. Para mais informações, consulte [Instalar e configurar pontos](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)de distribuição .



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a>Ponto de migração do Estado  

O ponto de migração do estado armazena dados estatais de utilizador que usmt captura em um computador, e depois restaura em outro computador. No entanto, ao capturar as definições do utilizador para uma implementação de SO no mesmo computador, como uma implementação em que atualização do Windows no computador de destino, pode escolher se armazena os dados no mesmo computador utilizando links rígidos ou utilizando um ponto de migração estatal. Para algumas implementações de computador, quando cria a loja estatal, o Gestor de Configuração cria automaticamente uma associação entre a loja do Estado e o computador de destino. Como planeia para o ponto de migração do Estado, considere os seguintes fatores:    


### <a name="user-state-size"></a>Tamanho do estado do utilizador  

O tamanho do estado do utilizador afeta diretamente o armazenamento em disco no ponto de migração de estado e o desempenho da rede durante a migração. Considere o tamanho do estado do utilizador e o número de computadores a migrar. Considere também as definições a serem migradas do computador. Por exemplo, se a pasta **My Documents** já estiver apoiada num servidor, então talvez não tenha de a migrar como parte da implementação da imagem. Evitar migrações desnecessárias mantém o tamanho global do estado utilizador menor, e diminui o efeito que de outra forma teria no desempenho da rede e no armazenamento de discos no ponto de migração do Estado.  


### <a name="user-state-migration-tool"></a>Ferramenta de migração de estado do utilizador  

Para capturar e restaurar o estado de utilizador durante a implementação dos sistemas operativos, utilize um pacote de Ferramentas de Migração do Estado utilizador (USMT) que aponta para os ficheiros de origem USMT. O Gestor de Configuração cria automaticamente este pacote na consola do Gestor de Configuração em**Pacotes**de**Gestão** > de Aplicações de Biblioteca > de **Software.** O Gestor de Configuração utiliza USMT 10 para capturar o estado de utilizador de um SISTEMA e depois restaurá-lo para outro. O Kit de Avaliação e Implementação do Windows (Windows ADK) para windows 10 inclui USMT 10.

Para obter uma descrição de diferentes cenários de migração para USMT 10, consulte [cenários comuns de migração](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) na documentação do Windows.  


### <a name="retention-policy"></a>Política de retenção  

Quando configurar o ponto de migração do Estado, especifique o tempo de permanência dos dados do estado do utilizador que armazena. O período de tempo para manter os dados no ponto de migração de estado depende de duas considerações:  

-   O efeito que os dados armazenados têm no armazenamento em disco.  

-   A potencial necessidade de manter os dados durante algum tempo para o caso de ser necessária uma nova migração dos dados.  
  
  
A migração do Estado ocorre em duas fases: capturar os dados e restaurar os dados. Quando captura dados, os dados de estado do utilizador são recolhidos e guardados no ponto de migração de estado. Quando restaurar os dados, os dados de estado do utilizador são recuperados a partir do ponto de migração de estado, escritos no computador de destino e, em seguida, o passo da sequência de tarefas **Disponibilizar Armazenamento de Estados** disponibiliza os dados armazenados. Quando os dados são disponibilizados, o temporizador de retenção é iniciado. Se selecionar a opção de eliminar imediatamente os dados migrados, os dados do estado do utilizador são eliminados assim que são lançados. Se selecionar a opção de manter os dados por um determinado período tempo, os dados são eliminados quando decorrer esse período de tempo, após a disponibilização dos dados de estado. Quanto mais tempo definir o período de retenção, mais espaço de disco é provável que precise.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Selecionar a unidade para armazenar dados de migração de estado do utilizador  

Quando configurar o ponto de migração do Estado, especifique a unidade no servidor para armazenar os dados de migração do estado do utilizador. Selecione uma unidade numa lista fixa de unidades. No entanto, algumas destas unidades podem não ser graváveis, como a unidade de CD ou uma unidade de partilha exterior à rede. Algumas cartas de condução podem não ser mapeadas para qualquer unidade no computador. Especifique uma unidade partilhada e réspita quando configurar o ponto de migração do Estado.  


### <a name="configure-a-state-migration-point"></a>Configurar um ponto de migração de estado  

Utilize os seguintes métodos para configurar um ponto de migração estatal para armazenar os dados do Estado do utilizador:  

-   Utilize o **Assistente para Criar Servidor do Sistema de Sites** para criar um novo servidor do sistema de sites para o ponto de migração de estado.  

-   Utilize o **Assistente para Adicionar Funções ao Sistema de Sites** para adicionar um ponto de migração de estado a um servidor existente.  

Quando utiliza estes assistentes, é-lhe solicitado que forneça as seguintes informações para o ponto de migração do Estado:  

-   As pastas em que os dados de estado do utilizador serão armazenados.  

-   O número máximo de clientes que podem armazenar dados no ponto de migração de estado.  

-   O mínimo de espaço livre para que o ponto de migração de estado armazene os dados de estado do utilizador.  

-   A política de eliminação da função. Ou especifica que os dados do estado do utilizador são eliminados imediatamente após a sua restauração num computador, ou após um número específico de dias após a restauração dos dados do utilizador num computador.  

-   Se o ponto de migração de estado responde apenas a pedidos de restauro dos dados de estado do utilizador. Quando ativa esta opção, não pode utilizar o ponto de migração do Estado para armazenar dados do Estado do utilizador.  

Para os passos para instalar uma função do sistema do site, consulte [adicionar funções](../../core/servers/deploy/configure/add-site-system-roles.md)do sistema do site .  
