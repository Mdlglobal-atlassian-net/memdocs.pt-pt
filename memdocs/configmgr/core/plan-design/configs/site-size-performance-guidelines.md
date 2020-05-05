---
title: Diretrizes de tamanho e desempenho do site
titleSuffix: Configuration Manager
description: Resultados dos testes de desempenho relacionados com o tamanho do site, metodologia e orientação.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073505"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Configuração Manager tamanho do site e diretrizes de desempenho

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração lidera a indústria em escalabilidade e desempenho. Outradocumentação abrange [limites máximos de escalabilidade suportados](size-and-scale-numbers.md) e diretrizes de [hardware](recommended-hardware.md) para sites de execução nos maiores tamanhos ambientais. Este artigo dá orientação suplementar de desempenho para ambientes de todos os tamanhos. Esta orientação pode ajudá-lo a estimar com maior precisão o hardware de que necessita para implementar o 'Gestor de Configuração'.

Este artigo centra-se no maior contribuinte para os estrangulamentos de desempenho do Gestor de Configuração: o subsistema de entrada/saída do disco ou iOPS. O artigo:

- Apresenta detalhes e resultados de testes focados no IOPS
- Documenta como reproduzir os testes com os seus próprios ambientes e hardware
- Sugere requisitos de IOPS de disco para ambientes de vários tamanhos 

## <a name="performance-test-methodology"></a>Metodologia de teste de desempenho

Você pode implementar O Gestor de Configuração de muitas maneiras únicas, mas é importante entender algumas variáveis em quaisquer discussões de tamanho. Uma variável é o intervalo de *características,* como um ciclo de inventário. Outra variável é o número de utilizadores, implementações de software ou outros *objetos* que o sistema referencia ou implementa. Os testes de desempenho aplicam estas variáveis como parte de uma *carga*. A carga gera objetos a uma taxa típica para os clientes empresariais que usam implementações de produção em ambientes de diferentes tamanhos.

> [!NOTE] 
> Os dados de telemetria do cliente permitem testar as construções atuais da sucursal com os cenários, configurações e configurações mais comuns para a maioria dos clientes. As recomendações deste artigo baseiam-se nestas médias. As suas experiências podem variar em função do tamanho e configuração do ambiente. Em geral, o Gestor de Configuração requer bom senso quando se trata de objetos e intervalos. Só porque pode recolher todos os ficheiros de um sistema, ou definir o intervalo para um ciclo para um minuto, não significa que deva.

As seguintes secções destacam algumas definições e configurações chave a utilizar ao testar e modelar necessidades de processamento para grandes empresas. Estas diretrizes ajudam a definir as expectativas básicas de desempenho do sistema para os tamanhos de hardware sugeridos.

### <a name="feature-intervals-settings"></a>Definições de intervalos de funcionalidades 
A maioria dos testes deve utilizar intervalos predefinidos para os ciclos-chave do sistema. Por exemplo, os testes de inventário de hardware ocorrem uma vez por semana com um ficheiro *.mof* maior do que o padrão. Alguns intervalos de funcionalidades recorrentes, especialmente ciclos de inventário de hardware e software, podem ter efeitos significativos nas características de desempenho de um ambiente. Ambientes que permitem intervalos de padrão agressivos para recolha de dados precisam de hardware de grandes dimensões em proporção direta ao aumento da atividade. Por exemplo, diga que tem 25.000 clientes de desktop e quer recolher o inventário de hardware duas vezes mais rápido do que o intervalo padrão. Devia começar por dimensionar o hardware do seu site como se tivesse 50.000 clientes.

### <a name="objects"></a>Objetos 
Os testes devem utilizar a *média superior* dos objetos que as grandes empresas tendem a usar com o sistema. Valores típicos são milhares de coleções e aplicações, que são implantadas para centenas de milhares de utilizadores ou sistemas. Os testes devem ser executados simultaneamente em *todos os* objetos do sistema nestes limites. Muitos clientes aproveitam várias funcionalidades, mas geralmente não usam todas as características do produto nestes limites superiores. Testar com todas as funcionalidades do produto ajuda a garantir o melhor desempenho possível em todo o sistema, e permite um tampão para funcionalidades que alguns clientes podem usar acima da média. 

### <a name="loads"></a>Cargas 
Os testes também devem ser executados em cargas diárias superiores às *médias* padrão, através da realização de simulações que geram exigências de utilização máximano sistema. Um exemplo é simular os lançamentos do Patch Tuesday, para garantir que o sistema pode devolver os dados de conformidade da atualização prontamente durante estes dias de atividade máxima. Outro exemplo é simular a atividade do site durante um surto de malware generalizado, para garantir que a notificação e resposta oportunas são possíveis. Embora as máquinas implantadas do tamanho recomendado possam ser subutilizadas num determinado dia, situações mais extremas requerem algum tampão de processamento.

### <a name="configurations"></a>Configurações
Executar testes numa gama de hardware físico, Hyper-V e Azure, com uma mistura de sistemas operativos suportados e versões SQL Server. Valide sempre os piores casos para a configuração suportada. Em geral, a Hyper-V e a Azure devolvem resultados de desempenho comparáveis a hardware físico equivalente quando configurados da mesma forma. Os sistemas operativos de servidores mais recentes tendem a executar igualmente ou melhor do que os sistemas operativos suportados mais antigos do servidor. Apesar de todas as plataformas suportadas cumprirem os requisitos mínimos, normalmente as versões mais recentes de produtos de suporte como windows e SQL produzem um desempenho ainda melhor. 

A maior variação provém das versões SQL Server em uso. Para obter mais informações sobre as versões Do SQL Server, veja qual a [versão do SQL que devo executar?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run) 

## <a name="key-performance-determinants"></a>Principais determinantes de desempenho

Pode testar e medir o desempenho do Gestor de Configuração com uma variedade de configurações, de diferentes formas e em diferentes tamanhos do site. As seguintes definições e objetos podem afetar dramaticamente o desempenho. Não se esqueça de os considerar ao testar e modelar o desempenho no seu ambiente.

> [!CAUTION]
> Embora poucos aspetos do Gestor de Configuração tenham máximos oficiais ou limites de interface do utilizador que impeçam o uso excessivo, ir além das diretrizes pode ter efeitos adversos significativos no desempenho de um site. Exceder os níveis recomendados ou ignorar a orientação de dimensionamento normalmente requer hardware maior, e pode tornar o seu ambiente insustentável até reduzir a frequência ou contagem de vários objetos.

### <a name="hardware-inventory"></a>Inventário de Hardware
Para testar o desempenho da linha de base, detete a recolha de inventário de hardware para uma vez por semana, com o tamanho padrão de ficheiro *.mof* mais aproximadamente 20% de propriedades adicionais. Não ative todas as propriedades e colete apenas propriedades que realmente precisa. Preste especial atenção ao recolher propriedades, como a memória virtual disponível, que mudará *sempre* a *cada* ciclo de inventário. A recolha destas propriedades pode causar excesso de agitação em todos os ciclos de inventário de todos os clientes.

### <a name="software-inventory"></a>Inventário de software
Para testar o desempenho da linha de base, detete a recolha de inventário de software para uma vez por semana, com apenas detalhes do *produto.* A recolha de muitos ficheiros pode colocar uma pressão significativa no subsistema de inventário. Evite especificar filtros que possam acabar por recolher milhares de ficheiros em muitos clientes, tais como * \*.exe* ou * \*.dll*.

### <a name="collections"></a>Coleções
Os testes de desempenho de base podem incluir vários milhares de coleções com uma variedade de definições de âmbito, tamanho, complexidade e atualização. O desempenho do site não é uma função direta do número absoluto de coleções num site. O desempenho é também um produto transversal da complexidade da consulta das coleções, atualizações completas e incrementais e mudança de frequência, dependências entre coleções e número de clientes nas coleções.

Sempre que possível, minimize as coleções que tenham consultas dinâmicas caras ou complicadas. Para coleções que exijam este tipo de regras, detete os intervalos de atualização adequados e os tempos de atualização adequados para minimizar o impacto da reavaliação da recolha no sistema. Por exemplo, atualização à meia-noite em vez das 8:00 da manhã.

Permitir atualizações incrementais nas coleções garante atualizações rápidas e atempadas à adesão à recolha. Mas mesmo que as atualizações incrementais sejam eficientes, ainda colocam carga no sistema. Equilibre a frequência de mudança que antecipa com a necessidade de atualizações quase em tempo real sobre a adesão. Por exemplo, diga que espera uma forte agitação nos membros da coleção, mas não precisa de atualizações de membros em tempo real. É mais eficiente e produz menos carga no sistema para atualizar a coleção com uma atualização completa agendada em algum intervalo, do que para permitir atualizações incrementais. 

Quando ativa atualizações incrementais, reduza quaisquer atualizações completas programadas nas mesmas coleções. São apenas um método de avaliação de backup, uma vez que as atualizações incrementais devem manter a sua coleção atualizada em tempo real. [As melhores práticas para coleções](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) recomendam um número máximo de coleções totais para atualizações incrementais, mas, como o artigo salienta, a sua experiência pode variar em função de muitos fatores.

Coleções com apenas regras de adesão diretas e com uma coleção limitativa que não está a realizar atualizações incrementais não precisam de atualizações completas agendadas. Desative os horários de atualização deste tipo de coleções para evitar cargas desnecessárias no sistema. Se a recolha limitada utilizar atualizações incrementais, as coleções com apenas regras de adesão diretas podem não refletir atualizações de adesão até 24 horas, ou até que ocorra uma atualização programada.

Embora não seja uma boa prática, algumas organizações criam centenas ou mesmo milhares de coleções como parte de vários processos de negócio. Se utilizar a automatização para criar coleções, é importante permitir as atualizações incrementais necessárias corretamente. Minimize e espalhe todos os horários de atualização completos para evitar pontos quentes de avaliação de recolha durante um único período de tempo. Estabeleça um processo regular de preparação para eliminar coleções não utilizadas, especialmente se criar automaticamente coleções de que já não precisa após algum tempo.

Lembre-se que o Gestor de Configuração cria políticas para todos os objetos nas suas coleções quando direciona tarefas como implementações para eles. As mudanças de adesão, seja através de atualizações programadas ou incrementais, podem criar muito trabalho para todo o sistema. As mais recentes construções de ramo têm otimizações políticas especiais para as coleções De Todos os Sistemas e Todos os Utilizadores. Ao direcionar toda a sua empresa, use as coleções incorporadas em vez de um clone destas coleções incorporadas.

Para investigar o desempenho da coleção ainda mais fundo, pode utilizar o Visualizador de Avaliação de Recolha (CEViewer) no Kit de [Ferramentas do Gestor](https://www.microsoft.com/download/details.aspx?id=50012)de Configuração .

### <a name="discovery-methods"></a>Métodos de descoberta
Para testes de desempenho de base, executar métodos de descoberta baseados em servidores uma vez por semana, permitindo a descoberta delta conforme apropriado para manter os dados frescos durante a semana. Os testes devem descobrir uma quantidade de objeto proporcional ao tamanho da empresa simulada. O teste de base de desempenho para a descoberta do batimento cardíaco também deve ser executado uma vez por semana.

Os dados da descoberta são dados globais. Um problema comum relacionado com o desempenho é configurar mal os métodos de descoberta baseados em servidores numa hierarquia, causando a descoberta duplicada dos mesmos recursos de vários locais primários. Configure cuidadosamente os métodos de descoberta para otimizar a comunicação com o serviço alvo, como controladores de domínio ative diretório, evitando a duplicação do mesmo âmbito de descoberta em vários locais primários.

## <a name="general-sizing-guidelines"></a>Diretrizes gerais de dimensionamento 

Com base na [metodologia](#performance-test-methodology)de teste de desempenho anterior, o quadro seguinte apresenta orientações *gerais* de requisitos mínimos de hardware para números específicos de clientes geridos. Estes valores devem permitir à maioria dos clientes com o número especificado de clientes processar objetos suficientemente rápido para administrar o site especificado. A potência de computação continua a diminuir no preço todos os anos, e alguns dos requisitos abaixo são pequenos em termos de configurações modernas de hardware do servidor. Hardware que excede as seguintes diretrizes aumenta proporcionalmente o desempenho de sites que requerem poder de processamento adicional, ou têm padrões especiais de utilização do produto. 

| Clientes de desktop  | Tipo/função do site  | Núcleos<sup>1</sup>   | Memória (GB)   | Atribuição de memória SQL  | IOPS: Caixas de entrada<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Espaço de armazenamento necessário (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Primário ou CAS com função de site de base de dados no mesmo servidor   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | Primário ou CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | SQL remoto                                                  | 4   | 16  | 70% |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50k  | Primário ou CAS com função de site de base de dados no mesmo servidor   | 8   | 32  | 70% | 1200 | 2800 | 600  |
| 50k  | Primário ou CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | SQL remoto                                                  | 8   | 24  | 70% |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100k | Primário ou CAS com função de site de base de dados no mesmo servidor   | 12  | 64  | 70% | 1200 | 5000 | 1100 |
| 100k | Primário ou CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | SQL remoto                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Primário ou CAS com função de site de base de dados no mesmo servidor   | 16  | 96  | 70% | 1800 | 7400 | 1600 |
| 150k | Primário ou CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | SQL remoto                                       | 16  | 72   | 90% |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | CAS com função de site de base de dados no mesmo servidor   | Mais de 20 | 128+ | 80% | 1800+ | 9000+   | 5000+ |
| 700k | CAS                                              | 8+  | 16+  |     | 1800+ |         | 500+  |
|      | SQL remoto                                       | 16+ | 96+  | 90% |       | 9000+   | 4500+ |
|      |                                                             |     |     |     |      |      |      |
| 5k   | Local Secundário                                   | 4   | 8    |     | 500   | -       | 200   |
| 15k  | Local Secundário                                   | 8   | 16   |     | 500   | -       | 300   |

**Notas**

1. **Cores**: O Gestor de Configuração realiza muitos processos simultâneos, pelo que necessita de um certo número mínimo de núcleos de CPU para vários tamanhos do site. Enquanto os núcleos são mais rápidos a cada ano, é importante garantir que um certo número mínimo de núcleos funcione em paralelo. Em geral, qualquer CPU de nível de servidor produzido após 2015 satisfaz as necessidades básicas de desempenho para os núcleos especificados na tabela. O Gestor de Configuração aproveita os núcleos adicionais para além das recomendações, mas geralmente, uma vez que você tem os núcleos mínimos sugeridos, você deve priorizar o investimento de recursos CPU para aumentar a velocidade dos núcleos existentes, não adicionar mais, núcleos mais lentos. Por exemplo, o Gestor de Configuração terá um melhor desempenho em tarefas de processamento chave com 16 núcleos rápidos do que com 24 núcleos mais lentos, assumindo que existem recursos suficientes do sistema, como o IOPS do disco.
   
   A relação entre os núcleos e a memória também é importante. Em geral, ter menos de 3-4 GB de RAM por núcleo reduz a capacidade total de processamento nos seus servidores SQL. Precisa de mais RAM por núcleo quando o SQL é colocalizado com os componentes do servidor do site.
   
   > [!NOTE]
   > Todos os conjuntos de teste planeiam a energia da máquina para permitir o máximo de consumo e desempenho de energia cpu.
   
2. **IOPS: Caixas de entrada e IOPS: SQL** refere-se às necessidades do IOPS para o Gestor de Configuração e unidades lógicas SQL. A coluna **IOPS: Inboxes** mostra os requisitos do IOPS para a unidade lógica onde residem os diretórios de caixa de caixa do Gestor de Configuração. O **IOPS: Coluna SQL** mostra as necessidades totais do IOPS para a(s) unidade lógica que vários ficheiros SQL usam. Estas colunas são diferentes porque as duas unidades devem ter formatação diferente. Para mais informações e exemplos sobre configurações de discos SQL sugeridas e melhores práticas de arquivo, incluindo detalhes sobre a divisão de ficheiros em vários volumes, consulte o tamanho do [Site e desempenho faQ](../../understand/site-size-performance-faq.md).
   
   Ambas as colunas IOPS utilizam dados da ferramenta padrão da indústria, *Diskspd*. Consulte [como medir o desempenho do disco](#how-to-measure-disk-performance) para obter instruções sobre a duplicação destas medições. Em geral, uma vez que satisfaça os requisitos básicos de CPU e memória, o subsistema de armazenamento tem o maior impacto no desempenho do site, e as melhorias aqui darão o maior retorno ao investimento.
   
3.  **Espaço de armazenamento necessário:** Estes valores do mundo real podem diferir de outras recomendações documentadas. Fornecemos estes números apenas como uma orientação geral; requisitos individuais podem variar muito. Planeie cuidadosamente as necessidades de espaço do disco antes da instalação do local. Assuma que alguma quantidade deste armazenamento permanece como espaço de disco livre a maior parte do tempo. Você pode usar este espaço tampão em um cenário de recuperação, ou para atualizar cenários que precisam de espaço de disco gratuito para a expansão do pacote de configuração. O seu site pode necessitar de armazenamento adicional para grandes quantidades de recolha de dados, períodos mais longos de retenção de dados e grandes quantidades de conteúdo de distribuição de software. Também pode armazenar estes itens em volumes separados e de menor produção.

## <a name="how-to-measure-disk-performance"></a>Como medir o desempenho do disco 

Pode utilizar a ferramenta padrão da indústria *Diskspd* para fornecer sugestões padronizadas para o IOPS que os ambientes de Configuração de várias dimensões exigem. Embora não exaustivas, os seguintes passos de teste e linhas de comando fornecem uma forma simples e reprodutível de estimar a entrada do subsistema do disco dos seus servidores. Pode comparar os seus resultados com o IOPS mínimo recomendado na tabela de diretrizes de [dimensionamento geral.](#general-sizing-guidelines) 

Ver Configurações de discos exemplo para [resultados](#example-disk-configurations) de testes de uma variedade de configurações de hardware em ambientes de laboratório. Pode utilizar os dados para um ponto de partida difícil ao conceber o subsistema de armazenamento para um novo ambiente a partir do zero.

### <a name="to-test-disk-iops"></a>Para testar o IOPS do disco  
1. Baixe o utilitário *Diskspd* aqui: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Certifique-se de que tem pelo menos 100 GB de espaço em disco livre. Desative quaisquer aplicações que possam interferir ou causar carga extra no disco, como a digitalização ativa antivírus do diretório, SQL ou SMSExec.
   
1. Executar *Diskspd* de um pedido de comando elevado. 
   
   Execute duas tiras da ferramenta em sequência para o volume que pretende testar. O primeiro teste realiza operações de escrita aleatórias de 64k por um minuto. Este teste garante a colocação de cache do controlador e a atribuição de espaço em disco, caso o volume esteja a expandir-se dinamicamente. Elimine os resultados do primeiro teste. O segundo teste deve seguir *imediatamente* o primeiro teste e efetuar a mesma carga durante cinco minutos.
   
   Por exemplo, utilize as seguintes linhas\\ de comando específicas para testar o volume G: volume.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Reveja a saída do segundo teste para encontrar o total de IOPS na coluna **De/O por s.** No exemplo seguinte, o total de IOPS é **de 3929.18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Configurações de discos de exemplo

As tabelas seguintes mostram resultados de executar os passos de teste em [Como medir o desempenho](#how-to-measure-disk-performance) do disco com várias configurações do laboratório de teste. Utilize estes dados para um ponto de partida *difícil* ao conceber o subsistema de armazenamento para um novo ambiente de raiz. 

### <a name="physical-machines-and-hyper-v"></a>Máquinas físicas e Hiper-V 
O hardware está sempre a melhorar. Espera-se que as novas gerações de hardware e diferentes combinações de hardware, como SSDs e SANs, excedam o desempenho indicado abaixo. Estes resultados são um ponto de partida básico a ter em conta ao conceber um servidor ou discutir com o seu fornecedor de hardware.

A tabela seguinte mostra os resultados dos testes em vários subsistemas de disco, incluindo eixos e discos rígidos baseados em SSD, em várias configurações de laboratório de teste. Todas as configurações formam os discos com clusters de 64k e fixam-nos a um controlador de disco de classe empresarial. Além da contagem de discos raid array, cada um deles tem pelo menos um disco sobressalente.

| Tipo de disco   | Contagem de discos, sem incluir +1 disco sobressalente | RAID     | IOPS medido  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15k SAS          | 2                                                  |           1   | 620           |
| 15k SAS          | 4                                                  |           10  | 1206          |
| 15k SAS          | 6                                                  |           10  | 1751          |
| 15k SAS          | 8                                                  |           10  | 2322          |
| 15k SAS          | 10                                                 |           10  | 2882          |
| 15k SAS          | 12                                                 |           10  | 3476          |
| 15k SAS          | 16                                                 |           10  | 4236          |
| 15k SAS          | 20                                                 |           10  | 5148          |
| 15k SAS          | 30                                                 |           10  | 7398          |
| 15k SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

Estes são os dispositivos que o exemplo utilizado. Esta informação não é uma recomendação para qualquer modelo ou fabricante de hardware específico. 

| Tipo de disco    | Modelo      | Controlador RAID | Memória e configuração de cache |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15k RPM SAS HD    | HP EH0300JDYTH  | Matriz Inteligente P822     | 2GB, 20% Ler / 80% Escrever           |
| SSD SATA          | ATA MK0200GCTYV | Array Inteligente P420i    | 1GB, 20% Ler / 80% Escrever           |
| SSD SAS           | HP MO0800 JEFPB | Array Inteligente P420i    | 1GB, 20% Ler / 80% Escrever           |

### <a name="azure-machine-and-disk-performance"></a>Desempenho da máquina azure e do disco 
O desempenho do disco Azure depende de vários fatores, como o tamanho do VM Azure, e o número e tipo de discos que utiliza. O Azure também está constantemente a adicionar novos tipos de máquinas e velocidades de disco que são diferentes da tabela a seguir. Para obter mais informações sobre o Gestor de Configuração em execução no Azure, e informações adicionais sobre a compreensão do disco I/O no Azure, consulte o Gestor de [Configuração no Azure frequentemente questionado](../../understand/configuration-manager-on-azure.md).

Todos os discos são formados do tamanho do cluster NTFS 64k, e as linhas com mais de um disco são configuradas como volumes listrados através do utilitário de Gestão de Discos Windows.

| VM do Azure| Disco azure| Contagem de discos | Espaço disponível | IOPS medido   | Fator limitativo   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Tamanho da VM do Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Tamanho da VM do Azure   |
| **DS3/DS12/F4s**                          | P20                     | 1                   | 512 MB                    | 1994  | Tamanho da VM do Azure   |
| **DS3/DS12/F4s**                          | P20                     | 2                   | 1024 MB                   | 1992  | Tamanho da VM do Azure   |
| **DS3/DS12/F4s**                          | P30                     | 1                   | 1024 MB                   | 1993  | Tamanho da VM do Azure   |
| **DS3/DS12/F4s**                          | P30                     | 2                   | 2048 MB                   | 1992  | Tamanho da VM do Azure   |
| **DS4/DS13/F8s**                          | P20                     | 1                   | 512 MB                    | 2334  | Disco P20        |
| **DS4/DS13/F8s**                          | P20                     | 2                   | 1024 MB                   | 3984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8s**                          | P20                     | 3                   | 1536 MB                   | 3984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8s**                          | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS4/DS13/F8s**                          | P30                     | 2                   | 2048 MB                   | 3984  | Tamanho da VM do Azure   |
| **DS4/DS13/F8s**                          | P30                     | 3                   | 3072 MB                   | 3996  | Tamanho da VM do Azure   |
| **DS5/DS14/F16s**                         | P20                     | 1                   | 512 MB                    | 2335  | Disco P20        |
| **DS5/DS14/F16s**                         | P20                     | 2                   | 1024 MB                   | 4639  | Disco P20        |
| **DS5/DS14/F16s**                         | P20                     | 3                   | 1536 MB                   | 6913  | Disco P20        |
| **DS5/DS14/F16s**                         | P20                     | 4                   | 2048 MB                   | 7966  | Tamanho da VM do Azure   |
| **DS5/DS14/F16s**                         | P30                     | 1                   | 1024 MB                   | 3112  | Disco P30        |
| **DS5/DS14/F16s**                         | P30                     | 2                   | 2048 MB                   | 6182  | Disco P30        |
| **DS5/DS14/F16s**                         | P30                     | 3                   | 3072 MB                   | 7963  | Tamanho da VM do Azure   |
| **DS5/DS14/F16s**                         | P30                     | 4                   | 4096 MB                   | 7968  | Tamanho da VM do Azure   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | Disco P30        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | Disco P30        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | Disco P30        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Tamanho da VM do Azure   |

## <a name="see-also"></a>Consulte também

- [FaQ de tamanho e desempenho do site](../../understand/site-size-performance-faq.md)
- [Gestor de Configuração em Azure frequentemente fez perguntas](../../understand/configuration-manager-on-azure.md)
- [Dimensionamento e números da escala](size-and-scale-numbers.md)
- [Hardware recomendado](recommended-hardware.md)

