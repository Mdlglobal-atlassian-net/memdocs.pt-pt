---
title: Cache de pares de clientes
titleSuffix: Configuration Manager
description: Utilize a cache de pares do cliente para locais de origem ao implementar conteúdo com o Gestor de Configuração.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c302e839c2a41ba27d160db24928f7e202de78dc
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110190"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de pares para clientes do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1101436-->
Utilize cache de pares para ajudar a gerir a implementação de conteúdo para clientes em locais remotos. A cache peer é uma solução de Gestor de Configuração incorporada que permite aos clientes partilhar conteúdo com outros clientes diretamente a partir da sua cache local.   

> [!Note]  
> Na versão 1906, o Gestor de Configuração permite esta funcionalidade por padrão. Na versão 1902 ou anterior, o Gestor de Configuração não permite esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Descrição geral

Definições:  

- **Cliente de cache peer**: Qualquer cliente do Gestor de Configuração que descarrega conteúdo de um par  

- **Fonte de cache peer**: Um cliente de Gestor de Configuração que você habilita para cache de pares, e que tem conteúdo para partilhar com outros clientes  

Utilize as configurações do cliente para permitir que os clientes sejam fontes de cache de pares. Não precisas de ativar clientes de cache de pares. Quando permite que os clientes sejam fontes de cache de pares, o ponto de gestão inclui-os na lista de fontes de localização de conteúdo.<!--510397--> Para mais informações sobre este processo, consulte [Operações](#operations).  

Uma fonte de cache de pares deve ser um membro do atual grupo de fronteira do cliente de cache de pares. O ponto de gestão não inclui fontes de cache de pares de um grupo de fronteira sinuoso na lista de fontes de conteúdo que fornece ao cliente. Só inclui pontos de distribuição de um grupo de fronteiras vizinhos. Para obter mais informações sobre os grupos de fronteira atuais e vizinhos, consulte [os grupos de fronteira](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

O cliente do Gestor de Configuração utiliza cache de pares para servir a outros clientes todos os tipos de conteúdo na cache. Este conteúdo inclui aplicações Microsoft 365 para ficheiros empresariais e ficheiros de instalação expresso.<!--SMS.500850-->  

A cache de pares não substitui o uso de outras soluções como o Windows BranchCache ou a Otimização de Entregas. A cache dos pares funciona juntamente com outras soluções. Estas tecnologias dão-lhe mais opções para alargar as soluções tradicionais de implementação de conteúdos, como pontos de distribuição. A cache dos pares é uma solução personalizada sem dependência da BranchCache. Se não ativar ou utilizar branchCache, a cache dos pares ainda funciona.  

> [!Note]  
> A partir da versão 1802, o Windows BranchCache está sempre ativado nas implementações. A definição para **permitir que os clientes partilhem conteúdos com outros clientes na mesma subnet** é removida.<!--SCCMDocs issue 539--> Se o ponto de distribuição o suporta, e está ativado nas configurações do cliente, os clientes usam branchCache. Para mais informações, consulte [Configure BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Operações

Para permitir a cache dos pares, desloque as [definições](#bkmk_settings) do cliente para uma coleção. Em seguida, os membros dessa coleção funcionam como uma fonte de cache para outros clientes no mesmo grupo de fronteiras.  

- Um cliente que opera como fonte de conteúdo de pares submete uma lista de conteúdos em cache disponíveis ao seu ponto de gestão usando mensagens estatais.

   > [!NOTE]
   > Consulte [as mensagens do Estado no Gestor](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) de Configuração para a lista de mensagens de estado de origem de conteúdo de pares aplicáveis, as mensagens de estado especifiquem as que têm identificações de mensagens estatais de 7200, 7201, 7202 e 7203.

- Outro cliente do mesmo grupo de fronteiras faz um pedido de localização de conteúdo para o ponto de gestão. O servidor devolve a lista de potenciais fontes de conteúdo. Esta lista inclui cada fonte de cache de pares que tem o conteúdo e está online. Inclui também os pontos de distribuição e outras localizações de fonte de conteúdo nesse grupo de fronteira. Para mais informações, consulte [a prioridade da fonte de conteúdo.](fundamental-concepts-for-content-management.md#content-source-priority)  

- Como de costume, o cliente que procura o conteúdo seleciona uma fonte da lista fornecida. O cliente tenta então obter o conteúdo.  

A partir da versão 1806, os grupos de fronteiras incluem configurações adicionais para lhe dar mais controlo sobre a distribuição de conteúdos no seu ambiente. Para mais informações, consulte as opções do [grupo Boundary para downloads de pares](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Se o cliente recuar para um grupo de limites vizinhos para conteúdo, o ponto de gestão não adiciona as fontes de cache dos pares do grupo de fronteira do vizinho à lista de potenciais localizações de fonte de conteúdo.  

Escolha apenas os clientes mais adequados como fontes de cache de pares. Avaliar a adequação do cliente com base em atributos como o tipo de chassis, espaço de disco e conectividade da rede. Para mais informações que o possam ajudar a selecionar os melhores clientes para usar para cache de pares, consulte [este blog por um consultor da Microsoft.](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801)


### <a name="limited-access-to-a-peer-cache-source"></a>Acesso limitado a uma fonte de cache de pares  

Uma fonte de cache de pares rejeita pedidos de conteúdo quando satisfaz qualquer uma das seguintes condições no momento em que um par solicita conteúdo:  

- Modo de bateria baixa  

- Carga do processador ultrapassa os 80%  

- Disco I/O tem um *AvgDiskQueueLength* que ultrapassa 10  

- Não há mais ligações disponíveis para o computador  

> [!Tip]  
> Configure estas definições utilizando a classe WMI do servidor de configuração do cliente para a funcionalidade de origem de pares *(SMS_WinPEPeerCacheConfig*) no SDK do Gestor de Configuração.  

Quando a fonte de cache peer rejeita um pedido para o conteúdo, o cliente de cache de pares continua a procurar conteúdo da sua lista de localizações de fonte de conteúdo.   



## <a name="requirements"></a>Requisitos

- O cache peer suporta todas as versões do Windows listadas como suportadas em [sistemas operativos suportados para clientes e dispositivos](../configs/supported-operating-systems-for-clients-and-devices.md). Os sistemas operativos não Windows não são suportados como fontes de cache de pares ou clientes de cache de pares.  

- Uma fonte de cache de pares deve ser um cliente de Gestor de Configuração associado ao domínio. No entanto, um cliente que não esteja unido ao domínio pode obter conteúdo a partir de uma fonte de cache de pares unida no domínio.  

- Os clientes só podem descarregar conteúdo a partir de fontes de cache de pares no seu atual grupo de fronteiras.  

- Não é necessária uma conta de acesso à [rede](accounts.md#network-access-account) com a seguinte exceção:  

  - Configure uma conta de acesso à rede no site quando um cliente com cache de pares executa uma sequência de tarefas do Centro de Software, e reinicia para uma imagem de arranque. Quando o dispositivo está no Windows PE, utiliza a conta de acesso à rede para obter conteúdo a partir da fonte de cache dos pares.  

  - Quando necessário, a fonte de cache peer usa a conta de acesso à rede para autenticar pedidos de descarregamento de pares. Esta conta requer apenas permissões de utilizador de domínio para este fim.  

- Com a versão 1802 e anterior, a última submissão de descoberta de batimentos cardíacos do cliente determina o limite atual de uma fonte de cache de pares. Um cliente que vagueia por um grupo de fronteiras diferente pode ainda ser membro do seu antigo grupo de fronteiras para fins de cache de pares. Este comportamento resulta em oferecer a um cliente uma fonte de cache de pares que não está na sua localização de rede imediata. Não permita que os clientes de roaming como uma fonte de cache de pares.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > A partir da versão 1806, o Gestor de Configuração é mais eficiente para determinar se uma fonte de cache de pares percorreu outro local. Este comportamento garante que o ponto de gestão o oferece como fonte de conteúdo para os clientes na nova localização e não na localização antiga. Se estiver a utilizar a funcionalidade de cache de pares com fontes de cache de pares de roaming, depois de atualizar o site para a versão 1806, também atualize todas as fontes de cache de pares para a versão mais recente do cliente. O ponto de gestão não inclui estas fontes de cache de pares na lista de locais de conteúdo até que sejam atualizados para pelo menos a versão 1806.<!--SCCMDocs issue 850-->  

- Antes de tentar descarregar conteúdo, o ponto de gestão primeiro valida que a fonte de cache de pares está online.<!--sms.498675--> Esta validação ocorre através do "canal rápido" para a notificação do cliente, que utiliza a porta TCP 10123.<!--511673-->  

> [!Note]  
> Para aproveitar as novas funcionalidades do Gestor de Configuração, os clientes da primeira atualização para a versão mais recente. Embora a nova funcionalidade apareça na consola Do Gestor de Configuração quando atualiza o site e a consola, o cenário completo não é funcional até que a versão do cliente seja também a mais recente.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a>Definições de cliente de cache peer

Para obter mais informações sobre as definições do cliente de cache peer, consulte [as definições](../../clients/deploy/about-client-settings.md#client-cache-settings)de cache do Cliente . 

Para obter mais informações sobre a configuração destas definições, consulte [como configurar as definições](../../clients/deploy/configure-client-settings.md)do cliente .

Em clientes com cache de pares que utilizam o Firewall do Windows, o Gestor de Configuração configura as portas de firewall que especifica nas definições do cliente.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a>Suporte parcial de descarregamento
<!--1357346-->
A partir da versão 1806, as fontes de cache dos pares de clientes podem agora dividir o conteúdo em partes. Estas peças minimizam a transferência de rede para reduzir a utilização de WAN. O ponto de gestão fornece um rastreio mais detalhado das partes de conteúdo. Tenta eliminar mais do que um download do mesmo conteúdo por grupo de fronteiras. 


### <a name="example-scenario"></a>Cenário de exemplo

Contoso tem um único local primário com dois grupos de fronteira: Sede (Sede) e Filial. Há uma relação de 30 minutos entre os grupos de fronteira. O ponto de gestão e ponto de distribuição do site estão apenas no limite do QG. A sucursal não tem ponto de distribuição local. Dois dos quatro clientes da sucursal estão configurados como fontes de cache de pares. 

![Diagrama de configuração de rede como descrito para o cenário de exemplo](media/1357346-peer-cache-source-parts.png)

1. Direciona-se para uma implantação com conteúdo para os quatro clientes da sucursal. Só distribuiu o conteúdo para o ponto de distribuição.  

2. O Cliente3 e o Cliente4 não têm uma fonte local para a implantação. O ponto de gestão instrui os clientes a esperar 30 minutos antes de voltarem ao grupo de fronteira remoto.  

3. O Cliente1 (PCS1) é a primeira fonte de cache de pares a refrescar a política com o ponto de gestão. Como este cliente está habilitado como uma fonte de cache de pares, o ponto de gestão instrui-o a começar imediatamente a descarregar a parte A a partir do ponto de distribuição.  

4. Quando o Cliente2 (PCS2) contacta o ponto de gestão, como parte A já está em andamento, mas ainda não está completo, o ponto de gestão instrui-o a começar imediatamente a descarregar a parte B a partir do ponto de distribuição.  

5. PcS1 termina o download da parte A e imediatamente notifica o ponto de gestão. Como parte B já está em andamento, mas ainda não está completo, o ponto de gestão instrui-o a começar a descarregar a parte C a partir do ponto de distribuição.  

6. PcS2 termina o download da parte B e imediatamente notifica o ponto de gestão. O ponto de gestão instrui-o a começar a descarregar a parte D a partir do ponto de distribuição.  

7. PcS1 termina o download da parte C e imediatamente notifica o ponto de gestão. O ponto de gestão informa que não há mais peças disponíveis a partir do ponto de distribuição remota. O ponto de gestão instrui-o a descarregar a parte B do seu par local, pcS2.  

8. Este processo continua até que ambas as fontes de cache de pares de clientes tenham todas as peças umas das outras. O ponto de gestão prioriza as peças do ponto de distribuição remota antes de instruir as fontes de cache dos pares a descarregar peças de pares locais.  

9. O Cliente3 é o primeiro a atualizar a política após o período de recuo de 30 minutos expirar. Agora, volta a verificar o ponto de gestão, que informa o cliente de novas fontes locais. Em vez de descarregar o conteúdo na íntegra a partir do ponto de distribuição através do WAN, ele descarrega o conteúdo na íntegra a partir de uma das fontes de cache de pares do cliente. Os clientes priorizam fontes de pares locais. 

> [!Note]  
> Se o número de fontes de cache de pares de clientes for maior do que o número de peças de conteúdo, então o ponto de gestão instrui as fontes adicionais de cache de pares a esperar pelo recuo como um cliente normal. 


### <a name="configure-partial-download"></a>Configurar o download parcial

1. Criar [grupos de fronteira](../../servers/deploy/configure/boundary-groups.md) e fontes de cache por normal.  

2. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site,** e selecione **Sites**. Clique em **Definições de Hierarquia** na fita.  

3. No separador **Geral,** ative a opção de **configurar as fontes**de cache dos clientes para dividir o conteúdo em partes .  

4. Criar uma implementação necessária com conteúdo.  

   > [!Note]  
   > Esta funcionalidade só funciona quando o cliente descarrega conteúdo em segundo plano, como por exemplo com uma implementação necessária. Os downloads a pedido, como quando o utilizador instala uma implementação disponível no Software Center, comportam-se como de costume.  

Para vê-los a lidar com o download de conteúdos em partes, examine o **ContentTransferManager.log** na fonte de cache de pares do cliente e o **MP_Location.log** no ponto de gestão.  



## <a name="guidance-for-cache-management"></a>Orientação para a gestão de cache
<!--510645-->
A cache peer baseia-se na cache do cliente do Gestor de Configuração para partilhar conteúdo. Considere os seguintes pontos para gerir a cache do cliente no seu ambiente:  

- A cache do cliente do Gestor de Configuração não é como a biblioteca de conteúdos num ponto de distribuição. Enquanto gere o conteúdo que distribui para um ponto de distribuição, o cliente do Gestor de Configuração gere automaticamente o conteúdo na sua cache. Existem configurações e métodos para ajudar a controlar o conteúdo na cache de uma fonte de cache de pares. Para mais informações, consulte [Configurar o cache do cliente para clientes do Gestor de Configuração](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- O tamanho normal da cache e a manutenção aplicam-se às fontes de cache dos pares. Para mais informações, consulte [configurar](../../clients/deploy/about-client-settings.md#configure-client-cache-size)o tamanho da cache do cliente . Considere o tamanho de conteúdos maiores, como pacotes de atualização de OS ou ficheiros de atualização expressa do Windows 10. Compare a sua necessidade deste conteúdo com o espaço de disco disponível em fontes de cache de pares.  

- O cliente de origem de cache peer atualiza o último tempo referenciado de conteúdo na cache quando um par o descarrega. O cliente usa esta marca de tempo quando mantém automaticamente a sua cache, removendo primeiro o conteúdo mais antigo. Por isso, deve esperar para remover o conteúdo que os clientes de cache de pares descarregam com mais frequência, se é que é.  

- Se necessário, durante uma sequência de tarefas de implementação de OS, utilize a variável **SMSTSPreserveContent** para manter o conteúdo na cache do cliente. Para obter mais informações, consulte variáveis de sequência de [tarefas](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Se necessário, ao criar o seguinte software, utilize a opção de **persistir conteúdo na cache do cliente:**  
  - Aplicações
  - Pacotes
  - Imagens do SO
  - Pacotes de upgrade de OS
  - Imagens de arranque



## <a name="monitoring"></a>Monitorização   

Para ajudá-lo a entender o uso da cache de pares, consulte o dashboard Fontes de Dados do **Cliente.** Para mais informações, consulte o dashboard de [fontes](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)de dados do Cliente .

Utilize também relatórios para visualizar o uso de cache dos pares. Na consola, vá ao espaço de trabalho **de Monitorização,** expanda **reporte**e selecione o nó **reporte.** Todos os seguintes relatórios têm um tipo de Conteúdo de Distribuição de **Software:**  

1.  **Rejeição**do conteúdo da fonte de cache peer : Com que frequência as fontes de cache de pares num grupo de fronteira rejeitam um pedido de conteúdo.  

    > [!Note]  
    > **Edição conhecida**<!--486652-->: Ao aprofundar resultados como *MaxCPULoad* ou *MaxDiskIO,* pode receber um erro que sugira que o relatório ou detalhes não podem ser encontrados. Para contornar esta questão, use os outros dois relatórios que mostram diretamente os resultados.  

2. **Rejeição do conteúdo**da fonte de cache por condição : Mostra detalhes de rejeição para um grupo de limites especificado ou tipo de rejeição. 

    > [!Note]  
    > **Edição conhecida**<!--486652-->: Não é possível selecionar a partir dos parâmetros disponíveis e, em vez disso, insira-os manualmente. Introduza os valores para O Nome do *Grupo limite* e o Tipo de *Rejeição,* como visto no relatório de rejeição de conteúdo de **origem de cache peer.** Por exemplo, para *o Tipo de Rejeição* pode introduzir *MaxCPULoad* ou *MaxDiskIO*.  

3. Detalhes de **rejeição**de conteúdo de fonte de cache peer : Mostrar o conteúdo que o cliente estava a solicitar quando rejeitado.  

    > [!Note]  
    > **Edição conhecida**<!--486652-->: Não é possível selecionar a partir dos parâmetros disponíveis e, em vez disso, insira-os manualmente. Introduza o valor para o Tipo de *Rejeição,* tal como apresentado no relatório de rejeição do conteúdo da **fonte de cache peer.** Em seguida, introduza o ID de *recurso* para a fonte de conteúdo sobre a qual pretende mais informações. 
    > 
    > Para encontrar o ID de recurso da fonte de conteúdo:  
    > 
    > 1. Encontre o nome do computador que apresenta como fonte de *cache peer* nos resultados da rejeição do conteúdo da fonte de cache peer por relatório de **condição.**  
    > 
    > 2. Vá ao espaço de trabalho **de Ativos e Compliance,** selecione o nó de **Dispositivos** e procure o nome desse computador. Utilize o valor da coluna de ID de recurso.  

