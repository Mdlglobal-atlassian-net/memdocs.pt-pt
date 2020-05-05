---
title: Tamanho do site e FAQ de desempenho
titleSuffix: Configuration Manager
description: Respostas a perguntas comuns do Gestor de Configuração sobre o tamanho e desempenho do site.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073267"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Tamanho do site do Gestor de Configuração e FAQ de desempenho

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este documento aborda frequentemente perguntas sobre o site do Gestor de Configuração, orientação de tamanho e problemas de desempenho comuns.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>FaQs e exemplos de configuração de máquinas e discos

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Como vou formatar os discos no meu servidor de site e no Servidor SQL?

Separe as caixas de entrada do Gestor de Configuração e os ficheiros SQL em pelo menos dois volumes diferentes. Esta separação permite otimizar os tamanhos de alocação de cluster para os diferentes tipos de I/O que realizam. 

Para o volume que hospeda as caixas de entrada do servidor dos seus sites, utilize o NTFS com unidades de alocação 4K ou 8K. ReFS escreve 64k mesmo para pequenos ficheiros. O Gestor de Configuração tem muitos ficheiros pequenos, para que o ReFS possa produzir despesas desnecessárias com o disco.

Para discos que contenham ficheiros de base de dados SQL, utilize a formatação NTFS ou ReFS, com unidades de alocação de 64K.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Como e onde devo apresentar os meus ficheiros de base de dados SQL?

As matrizes modernas de unidades de estado sólido (SSD) e armazenamento Premium Azure podem fornecer iOPS elevados num único volume, com poucos discos. Normalmente, adiciona mais unidades a uma matriz para armazenamento adicional, e não uma entrada adicional. Se estiver a usar discos físicos à base de eixos, pode precisar de mais IOPS do que pode gerar num único volume. Deve atribuir 60% do total recomendado de IOPS e espaço em disco para o ficheiro *.mdf,* 20% para o ficheiro *.ldf* e 20% para os ficheiros de registo e data temp. Os ficheiros *.ldf* e temporário podem todos residir num único volume com 40% (20% + 20%) do seu IOPS atribuído.

Servidores SQL mais cedo do que o SQL Server 2016 criado por padrão apenas um ficheiro de dados temporário. Deve criar mais, para evitar fechaduras SQL e esperar pelo acesso a um único ficheiro. As opiniões comunitárias variam no melhor número de ficheiros de dados temporários para criar, de quatro para oito. Os testes revelam pouca diferença entre quatro a oito, para que possa criar quatro ficheiros de dados temporários *de tamanho igual.* Os seus ficheiros de dados tempdb devem ter até 20 a 25% do tamanho da sua base de dados completa.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Há outras recomendações para a configuração do disco?

Quando configurável, detete a memória do controlador RAID para 70% de alocação para operações de escrita e 30% para as operações de leitura. Em geral, utilize uma configuração de matriz RAID 10 para a base de dados do site. Raid 1 também é aceitável para sites de pequena escala com requisitos de I/S baixos, ou se você usar SSDs rápidos. Com matrizes de disco maiores, configure discos sobressalentes para substituir automaticamente os discos em falha.

**Exemplo: Máquina física com discos físicos** 

[Dimensionar as diretrizes](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para um servidor de site colocalizado e servidor SQL com **100.000** clientes são 1200 IOPS para caixas de entrada de servidores de site e 5000 IOPS para ficheiros SQL Server.

A configuração do disco resultante pode parecer:

| Unidades<sup>1</sup> | RAID | Formato | Conteúdo de volume | IOPS mínimos necessários| Aprox. IOPS fornecido<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | Caixas de entrada ConfigMgr    |     1700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | SQL .mdf             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | SQL .ldf, ficheiros temporários | 40%*5000 = 2000     | 2322             |

1. Não inclui discos de reserva recomendados. 
2. Este valor é de configurações de [disco exemplo.](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations) 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Uso Hyper-V no Windows Server. Como posso configurar os discos para os meus VMs de Configurão para melhor desempenho?

O Hyper-V oferece um desempenho semelhante a um servidor físico, se os recursos de hardware (núcleos de CPU e armazenamento de passagem) forem 100% dedicados à máquina virtual (VM). A utilização de ficheiros de disco de tamanho fixo *.vhd* ou *.vhdx* provoca um impacto mínimo de desempenho de 1-5% em I/O. A utilização de ficheiros de disco de expansão dinâmica *.vhd* ou *.vhdx* provoca um impacto de desempenho de até 25% em I/O para a carga de trabalho do Gestor de Configuração. Se precisar de discos de expansão dinâmica, compense adicionando um desempenho adicional de 25% de IOPS à matriz.

Ao executar o servidor do site do Gestor de Configuração ou SQL dentro de um VM, isola as unidades de SISTEMA de hospedeiros hiper-V do VM OS e unidades de dados.

Para obter mais informações sobre a otimização de VMs, consulte [os servidores Hiper-V de afinação](/windows-server/administration/performance-tuning/role/hyper-v-server/)de desempenho.

**Exemplo: Servidor de site baseado em Hyper-V VM** 

[As diretrizes](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) de dimensionamento para um servidor de site colocalizado e servidor SQL com **150.000** clientes são 1800 IOPS para caixas de entrada de servidores de site e 7400 IOPS para ficheiros SQL Server.

A configuração do disco resultante pode parecer:

| Unidades<sup>1</sup> | RAID | Formato<sup>2</sup> | Conteúdo de volume | IOPS mínimos necessários| Aprox. IOPS fornecido<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Os hospedeiros hiper-V           | -                    | -                |
| 2x10k          | 1         | -              | (VM) servidor de site OS       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) Caixas de entrada ConfigMgr    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64k ReFS       | (VM) Host SQL (todos os ficheiros) | 7400                 | 14346            |

1. Não inclui discos de reserva recomendados. 
2. Tamanho fixo, pass-through *.vhdx* para a unidade VM dedicada ao volume subjacente. 
3. Este valor é de configurações de [disco exemplo.](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations) 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Existem algumasugestões para ambientes de Configuração Manager no Microsoft Azure?

Comece por ler o Gestor de [Configuração em Azure frequentemente feito perguntas](configuration-manager-on-azure.md).

A infraestrutura Azure como um serviço (IaaS) VMs que alavancam discos baseados em Armazenamento Premium pode ter IOPS elevados. Nestes VMs, configure discos adicionais para necessidades de espaço de disco antecipadas, em vez de iOPS adicionais.

O armazenamento azure é inerentemente redundante e não requer vários discos para disponibilidade. Pode riscar discos em Disk Manager ou Espaços de Armazenamento para fornecer espaço e desempenho adicionais.

Para mais informações e recomendações sobre como maximizar o desempenho do Armazenamento Premium e executar servidores SQL em VMs Azure IaaS, consulte:

- [Otimizar o desempenho da aplicação](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Orientação de discos](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Exemplo: Servidor de site baseado em Azure** 

[As diretrizes](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) de dimensionamento para um servidor de site colocalizado e servidor SQL com **50.000** clientes são oito núcleos, 32 GB e 1200 IOPS para caixas de entrada do servidor do site e 2800 IOPS para ficheiros SQL Server.

A sua máquina Azure resultante pode ser um DS13v2 (oito núcleos, 56 GB) com a seguinte configuração do disco:

| Unidades | Formato | Contains | IOPS mínimos necessários| Aprox. IOPS fornecido<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Servidor do site OS     | -                    | -                |
| 1xP20 (512 GB)    | NTFS 8k       | Caixas de entrada ConfigMgr  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64k ReFS      | SQL (todos os ficheiros<sup>2)</sup> | 2800                 | 3112             |

1. Este valor é de configurações de [disco exemplo.](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations)
2. A [orientação azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permite colocar o TempDB no D local, baseado em SSD: unidade, dado que não exceda o espaço disponível e permite uma distribuição adicional de I/S do disco. *D:*

**Exemplo: Servidor de site baseado em Azure (para aumento instantâneo de desempenho)** 

A entrada em disco azul é limitada pelo tamanho do VM. A configuração no exemplo anterior do Azure pode limitar a expansão futura ou o desempenho adicional. Se adicionar discos adicionais durante a implementação inicial do seu VM Azure, pode aumentar o seu VM Azure para aumentar a potência de processamento no futuro, com o mínimo de investimento inicial. É muito mais simples planear com antecedência para aumentar o desempenho do site à medida que os requisitos mudam, em vez de mais tarde precisar de fazer uma migração mais complicada.

Mude os discos no exemplo azure anterior para ver como o IOPS muda.

**DS13v2** 

| Unidades<sup>1</sup> | Formato | Contains | IOPS mínimos necessários| Aprox. IOPS fornecido<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Servidor do site OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Caixas de entrada ConfigMgr  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (todos os ficheiros<sup>3)</sup> | 2800                 | 3984             |

1. Os discos são listrados utilizando espaços de armazenamento.
2. Este valor é de configurações de [disco exemplo.](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations) O tamanho da VM limita o desempenho.
3. A [orientação azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permite colocar o TempDB no D local, baseado em SSD: unidade, dado que não exceda o espaço disponível e permite uma distribuição adicional de I/S do disco. *D:*

Se precisar de mais desempenho no futuro, pode aumentar o seu VM para um DS14v2, que duplicará o CPU e a memória. A largura de banda adicional do disco permitida por esse tamanho VM também aumentará instantaneamente o IOPS do disco disponível nos seus discos previamente configurados.

**DS14v2**

| Unidades<sup>1</sup> | RAID | Formato | Contains | IOPS mínimos necessários| Aprox. IOPS fornecido<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;padrão&gt; | -             | Servidor do site OS     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS 8k       | Caixas de entrada ConfigMgr  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64k ReFS      | SQL (todos os ficheiros<sup>3)</sup> | 2800                 | 6182             |

1. Os discos são listrados utilizando espaços de armazenamento.
2. Este valor é de configurações de [disco exemplo.](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations) O tamanho da VM limita o desempenho.
3. A [orientação azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) permite colocar o TempDB no D local, baseado em SSD: unidade, dado que não exceda o espaço disponível e permite uma distribuição adicional de I/S do disco. *D:*

## <a name="other-common-sql-server-related-performance-questions"></a>Outras questões comuns de desempenho relacionadas com o Servidor SQL 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>É melhor correr com o SQL colocalizado com o servidor do site, ou executá-lo num servidor remoto?

Ambos podem executar adequadamente, assumindo que o servidor único é adequadamente dimensionado, ou a conectividade da rede é suficiente entre os dois servidores.

O SQL remoto requer o custo inicial e operacional de um servidor adicional, mas é típico entre a maioria dos clientes em larga escala. Os benefícios desta configuração incluem:

- Opções de disponibilidade de site aumentadas, como SQL Always On
- Capacidade de executar relatórios pesados com menos ouvido sao ouvido sao processado seletiva
- Recuperação de desastres mais simples em algumas situações
- Gestão de segurança mais fácil
- Separação de papéis para a gestão da SQL, como com uma equipa de DBA separada

O SQL colocalizado requer um único servidor, e é típico para a maioria dos clientes de pequena escala. Os benefícios desta configuração incluem:

- Custos mais baixos para máquinas, licenças e manutenção
- Menos pontos de falha no site
- Melhor controlo para planear o tempo de inatividade

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Quanto RAM devo atribuir para a SQL?

Por padrão, a SQL utiliza toda a memória disponível no seu servidor, potencialmente esfomeando o SISTEMA e outros processos na máquina. Para evitar potenciais problemas de desempenho, é importante atribuir explicitamente a memória à SQL. Nos servidores do site colocalizados com servidores SQL, certifique-se de que o OS tem RAM suficiente para o cache de ficheiros e outras operações. Certifique-se de que ainda há RAM suficiente para smsexec e outros processos de Gestor de Configuração. Ao executar o SQL num servidor remoto, pode alocar a *maior parte* da memória ao SQL, mas não a toda a. Reveja as diretrizes de [dimensionamento](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) para orientação inicial. 

A atribuição de memória do Servidor SQL deve ser arredondada para toda a GB. Além disso, à medida que a RAM aumenta para grandes quantidades, pode deixar a SQL ter uma percentagem mais elevada. Por exemplo, quando 256 GB ou mais de RAM estiver disponível, pode configurar o SQL até 95%, uma vez que isso ainda preserva muita memória para o Sistema Operativo. Monitorizar o ficheiro da página é uma boa forma de garantir que há memória suficiente para o SISTEMA e quaisquer processos do Gestor de Configuração.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Os núcleos são baratos hoje em dia. Devo adicionar um monte deles ao meu servidor SQL?

Pode encontrar problemas de contenção de memória se houver mais de 16 núcleos físicos e não houver RAM suficiente no seu servidor SQL. A carga de trabalho do Gestor de Configuração funciona melhor quando pelo menos 3-4 GB de RAM por núcleo está disponível para SQL. Ao adicionar núcleos aos seus servidores SQL, certifique-se de aumentar a RAM em quantidades proporcionais.

### <a name="will-sql-always-on-impact-my-performance"></a>O SQL Sempre No Impacto no meu desempenho?

Em geral, o SQL Always On tem um efeito negligenciável no desempenho do sistema quando existe uma rede suficiente entre os servidores de réplica SQL. Pode ter um rápido registo de base de dados *.ldf* crescimento de ficheiros num ambiente movimentado SQL Always On. No entanto, o espaço de ficheirode registo é automaticamente divulgado após uma cópia de segurança de base de dados bem sucedida. Adicione um trabalho SQL para a base de dados do Gestor de Configuração para efetuar uma cópia de segurança, por exemplo, a cada 24 horas, e uma cópia de segurança *.ldf* a cada seis horas. Para obter mais informações sobre o SQL Always On and Configuration Manager, incluindo mais sobre estratégias de backup SQL, consulte o SQL Server Always On para obter uma base de dados de [site altamente disponível.](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)

### <a name="should-i-enable-sql-compression-on-my-database"></a>Devo ativar a compressão SQL na minha base de dados?

A compressão SQL não é recomendada para a base de dados do Gestor de Configuração. Embora não existam problemas funcionais com a compressão numa base de dados do Gestor de Configuração, os resultados dos testes não mostram muitas economias de tamanho em comparação com o potencial impacto considerável de desempenho no sistema.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Devo ativar a encriptação SQL na minha base de dados?

Quaisquer segredos na base de dados do Gestor de Configuração já estão armazenados de forma segura, mas adicionar encriptação SQL pode adicionar mais uma camada de segurança. Não existem problemas funcionais com a encriptação na sua base de dados, mas pode haver até uma degradação de desempenho de 25%, dependendo das tabelas que escolhe encriptar e da versão do SQL que está a usar. Portanto, criptografe com cuidado, especialmente em ambientes de grande escala. Lembre-se também de atualizar os seus planos de backup e recuperação para garantir que pode recuperar com sucesso os dados encriptados.

### <a name="what-version-of-sql-should-i-run"></a>Que versão do SQL devo executar?

Para versões suportadas do SQL, consulte [o Suporte para versões SQL Server](../plan-design/configs/support-for-sql-server-versions.md). Do ponto de vista do desempenho, todas as versões suportadas do SQL cumprem os critérios de desempenho exigidos. No entanto, o SQL 2012 e o SQL 2016 ou mais recente tendem a superar o SQL 2014 em alguns aspetos da carga de trabalho do Gestor de Configuração. Além disso, correr sQL 2014 no Nível de compatibilidade SQL 2012 (110) melhora o desempenho em geral. No momento da instalação, as bases de dados do Gestor de Configuração em execução no SQL 2012 e No SQL 2014 estão definidas para o nível de compatibilidade 110. O SQL 2016 ou mais recente está definido para o nível de compatibilidade padrão da versão SQL, tal como 130 para o SQL 2016. Atualizar o SQL no lugar não atualiza os níveis de compatibilidade até instalar a próxima versão atual do Gestor de Configuração. 

Se vir tempoinamente inusitado ou lentidão em determinadas consultas SQL no SQL 2016 ou posteriormente, como quando utilizar o RBAC na Consola de Administração, tente alterar o nível de compatibilidade SQL na base de dados do Gestor de Configuração para 110. Correr no Nível de compatibilidade SQL 110 no SQL 2014 e versões mais recentes do SQL são totalmente suportadas. Para mais informações, consulte os [tempos de consulta sQL ou](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d)a consola de forma lenta em determinadas consultas de base de dados do Gestor de Configuração .

A partir de janeiro de 2018, deverá *evitar* as seguintes versões SQL, devido a várias questões potenciais conhecidas relacionadas com o desempenho ou outras questões potenciais:

- SQL 2012 SP3 CU1 a CU5
- SQL 2014 SP1 CU6 para SP2 CU2
- SQL 2016 RTM para CU3, SP1 CU3 a CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Devo implementar alguma tarefa adicional de indexação SQL?

Sim, atualizar índices tantas vezes como uma vez por semana e estatísticas tantas vezes como uma vez por dia para melhorar o desempenho do SQL. Scripts de terceiros e informações adicionais disponíveis do Gestor de Configuração e das comunidades SQL podem ajudar a otimizar estas tarefas.

Em grandes sites, algumas tabelas\_SQL, tais como CI CurrentComplianceStatusDetails, HinvChangeLog, podem ser grandes, dependendo dos seus padrões de utilização. Pode ser necessário reduzir ou alterar a sua abordagem de manutenção, um a um.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Quando devo usar o Servidor SQL completo em vez do SQL Express nos meus sites secundários?

A SQL Express não tem implicações significativas no desempenho em sites secundários, e é adequada para a maioria dos clientes. Também é fácil de implementar e gerir, e é a configuração recomendada para quase todos os clientes em qualquer tamanho.

Há uma situação em que uma instalação completa do SQL Server pode ser necessária. Se tiver um grande número de pontos de distribuição e pacotes ou fontes no seu ambiente, é possível ultrapassar o limite de tamanho de 10 GB da SQL Express. Se o número de pacotes vezes o número de pontos de distribuição for superior a 4.000.000, como 2.000 DPs com 2.000 peças de conteúdo, considere usar o Servidor SQL completo nos seus sites secundários. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Devo alterar as definições do MaxDOP na minha base de dados?

Deixar a sua definição em 0 (utilizar todos os processadores disponíveis) é ideal para o desempenho geral do processamento na maioria das circunstâncias.

Muitos administradores do Gestor de Configuração seguem as orientações em [Recomendações e orientações para a opção de configuração "max degree of parallelism" no Servidor SQL](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Na maioria dos hardware grandes modernos, esta orientação leva a uma configuração máxima sugerida de oito. No entanto, se executar muitas consultas menores em comparação com o seu número de processadores, pode ajudar a defini-lo para um número mais elevado. Limitar-se a oito não é necessariamente o melhor cenário em sites maiores quando há mais núcleos disponíveis. 

Nos servidores SQL com mais de oito núcleos, comece com uma definição de 0, e só faça alterações se tiver problemas de desempenho ou bloqueio excessivo. Se precisar de alterar o MaxDOP porque encontra problemas de desempenho em 0, comece com um novo valor pelo menos maior ou igual ao número mínimo recomendado de núcleos para o tamanho do servidor SQL desse site. Ir mais baixo que este valor quase sempre tem implicações negativas no desempenho. Por exemplo, um servidor SQL remoto para um site de 100.000 clientes precisa de pelo menos 12 núcleos. Se o seu servidor SQL tiver 16 núcleos, comece a testar a sua definição MaxDOP com um valor de 12.

## <a name="other-common-performance-related-questions"></a>Outras questões comuns relacionadas com o desempenho

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Que pastas no servidor do site (ou outras funções) devo excluir para software antivírus?

Tome cuidado ao desativar a proteção antivírus em qualquer sistema. Em ambientes de grande volume e seguros, recomendamos que a *monitorização ativa* desativa seja desativada para um desempenho ótimo.

Para obter mais informações sobre exclusões antivírus recomendadas, consulte [exclusões recomendadas de antivírus para O Gestor de Configuração 2012 e Servidores de Site de Sucursais, Sistemas de Sites e Clientes.](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu)

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>O que posso fazer para que a WSUS tenha um melhor desempenho quando é usada com o Diretor de Configuração?

Alterar algumas definições chave IIS, como o Comprimento da Fila WsusPool e o limite de Memória Privada WsusPool, pode melhorar o desempenho da WSUS, mesmo em instalações mais pequenas. Para mais informações, consulte [o hardware recomendado](../plan-design/configs/recommended-hardware.md).

Certifique-se também de que tem as últimas atualizações instaladas para o sistema operativo que executa o WSUS:

- Windows Server 2012: Qualquer atualização cumulativa não "apenas de segurança" lançada em outubro de 2017 ou posterior. [(KB4041690)](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690)
- Windows Server 2012 R2: Qualquer atualização cumulativa não "apenas de segurança" lançada em agosto de 2017 ou posterior. [(KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016: qualquer atualização cumulativa não "apenas de segurança" lançada em agosto de 2017 ou posterior. [(KB403939)](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396)

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Que tipo de manutenção devo executar nos meus servidores WSUS?

Consulte o guia completo para a manutenção sup do [Microsoft WSUS e do Gestor](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)de Configuração .

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Quero criar uma monitorização básica do desempenho para o meu site. O que devo ver?

A monitorização do desempenho do servidor tradicional funciona eficazmente para o Diretor Geral de Configuração. Também pode aproveitar os vários pacotes de gestão de Gestor de Operações do System Center para O Gestor de Configuração, Servidor SQL e Servidor Windows para monitorizar a saúde básica dos seus servidores. Também pode monitorizar diretamente o Sistema de Configuração de Contadores do Windows Performance Monitor (PerfMon). Monitorize os atrasos nas várias caixas de entrada para obter sinais de alerta precoce de potenciais problemas de desempenho do local ou atrasos.

## <a name="see-also"></a>Consulte também

- [Diretrizes de dimensionamento e desempenho do site](../plan-design/configs/site-size-performance-guidelines.md)
- [Gestor de Configuração em Azure frequentemente fez perguntas](configuration-manager-on-azure.md)
