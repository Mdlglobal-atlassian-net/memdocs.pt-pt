---
title: Capacidades na Pré-visualização Técnica 1612
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721508"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1612 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*



Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1612. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="the-data-warehouse-service-point"></a>O ponto de serviço do armazém de dados
Começando com a versão de Pré-visualização Técnica 1612, o ponto de serviço de armazém de dados permite-lhe armazenar e reportar dados históricos a longo prazo para a implementação do seu Gestor de Configuração. Isto é realizado por sincronizações automatizadas da base de dados do Site do Gestor de Configuração para uma base de dados de armazém de dados de dados. Esta informação é então acessível a partir do seu ponto de serviços de Report.

Por predefinição, quando instala a nova função do sistema de site, o Gestor de Configuração cria a base de dados de depósito de dados para si numa instância do Servidor SQL que especifica. O armazém de dados suporta até 2 TB de dados, com carimbos temporais para rastreio de alterações.  Por padrão, os dados sincronizados a partir da base de dados do site incluem os grupos de dados para Dados Globais, Dados do Site, Global_Proxy, Dados de Nuvem e Pontos de Vista de Base de Dados. Também pode modificar o que é sincronizado para incluir tabelas adicionais, ou excluir tabelas específicas dos conjuntos de replicação predefinidos.
Os dados predefinidos que são sincronizados incluem informações sobre:
- Saúde das infraestruturas
- Segurança
- Conformidade
- Software maligno   
- Implementações de software
- Detalhes do inventário (no entanto, o histórico de inventário não é sincronizado)

Além de instalar e configurar a base de dados do armazém de dados, vários novos relatórios são instalados para que possa facilmente pesquisar e reportar sobre estes dados.

### <a name="data-warehouse-dataflow"></a>Fluxo de dados do Armazém de Dados   
![Datawarehouse_flow](./media/datawarehouse.png)

| Passo         | Detalhes  |
|:------:|-----------|  
| **1** | O servidor do site transfere e armazena dados na base de dados do site.  |  
| **2** | Com base na sua programação e configuração, o ponto de Serviço de Armazém de Dados obtém dados da base de dados do site.  |  
| **3** | O ponto de serviço de armazém de dados transfere e armazena uma cópia dos dados sincronizados na base de dados do Data Warehouse. |  
| **A** | Utilizando relatórios incorporados, é feito um pedido de dados que é passado para o ponto de Serviços de Reporte utilizando os Serviços de Relato do Servidor SQL. |  
| **B** | A maioria dos relatórios são para informações atuais, e estes pedidos são executados contra a base de dados do site. |  
| **C** | Quando um relatório solicita dados históricos, utilizando um dos relatórios com *categoria* de **Data Warehouse,** o pedido é executado contra a base de dados do Data Warehouse.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Pré-requisitos para o ponto de serviço de armazém de dados e base de dados
- A sua hierarquia deve ter uma função de sistema de ponto de ponto de ponto de serviços de Reporte instalada.
- O computador onde instala a função do sistema do site requer .NET Framework 4.5.2 ou posterior.
- A conta de computador do computador onde instala a função do sistema do site deve ter permissões de administração locais para o computador que acolherá a base de dados do armazém de dados.
- A conta administrativa que utiliza para instalar a função do sistema do site deve ser um DBO na instância do SQL Server que irá alojar a base de dados do armazém de dados de dados.  
- A base de dados é suportada:
  - Com o SQL Server 2012 ou mais tarde, edição enterprise ou Datacenter.
  - Em uma instância padrão ou nomeada
  - Num cluster de *servidor SQL*. Embora esta configuração deva funcionar, não foi testada e o suporte é o melhor esforço.
  - Quando co-localizado com a base de dados do site ou com a base de dados de pontos de ponto de ponto de reporte. No entanto, recomendamos que seja instalado num servidor separado.  
- A conta que é utilizada como Conta Ponto de Serviços de *Informação* deve ter a **db_datareader** permissão para a base de dados do armazém de dados.  
- A base de dados não é suportada num grupo de *disponibilidade sQL Server AlwaysOn*.

### <a name="install-the-data-warehouse"></a>Instalar o Armazém de Dados
Instala a função do sistema do site do Data Warehouse num site de administração central ou no local primário utilizando o Assistente de **Funções** do Sistema do Site add ou o Assistente do Servidor do **Sistema de Criação**do Site . Consulte [as funções](../servers/deploy/configure/install-site-system-roles.md) do sistema do site para obter mais informações. Uma hierarquia apoia vários casos deste papel, mas apenas uma instância é apoiada em cada site.  

Quando instala a função, o Gestor de Configuração cria a base de dados do armazém de dados para si na instância do Servidor SQL que especifica. Se especificar o nome de uma base de dados existente (como faria se mover a base de dados do armazém de [dados para um novo Servidor SQL),](#move-the-data-warehouse-database)o Gestor de Configuração não cria uma nova base de dados, mas utiliza a que especifica.

#### <a name="configurations-used-during-installation"></a>Configurações utilizadas durante a instalação
Utilize as seguintes informações para concluir a instalação da função do sistema do site:

Página de **seleção de funções** do sistema:  
Antes de o Assistente apresentar uma opção para selecionar e instalar o ponto de serviço do Armazém de Dados, deve ter instalado um ponto de serviço suportável.

Página **geral:** São necessárias as seguintes informações gerais:
- **Configurações da base de dados do Gestor de Configuração:**   
  - **Nome** do servidor - Especifique o FQDN do servidor que acolhe a base de dados do site. Se não utilizar uma instância predefinida do Servidor SQL, deve especificar a instância após o FQDN no seguinte formato: *** &lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Nome** da base de dados - Especifique o nome da base de dados do site.
  - **Verifique** - Clique **em Verificar** se a ligação à base de dados do site é bem sucedida.
</br></br>
- **Definições da base de dados do Data Warehouse:**
  - **Nome** do servidor - Especifique o FQDN do servidor que acolhe o ponto de serviço de armazém de dados e a base de dados. Se não utilizar uma instância predefinida do Servidor SQL, deve especificar a instância após o FQDN no seguinte formato: *** &lt;Sqlserver_FQDN>\&lt;Instance_name>***
  - **Nome** da base de dados - Especifique o FQDN para a base de dados do armazém de dados.  O Gestor de Configuração criará a base de dados com este nome. Se especificar um nome de base de dados que já existe na instância do servidor SQL, o Gestor de Configuração utilizará essa base de dados.
  - **Verifique** - Clique **em Verificar** se a ligação à base de dados do site é bem sucedida.

Página de definições de **sincronização:**   
- **Definições de dados:**
  - **Grupos de replicação para sincronizar** – Selecione os grupos de dados que pretende sincronizar. Para obter informações sobre os diferentes tipos de grupos de dados, consulte a [replicação da Base](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) de Dados e **as vistas distribuídas** nas [transferências](../plan-design/hierarchy/data-transfers-between-sites.md)de Dados entre sites .
  - **Tabelas incluídas para sincronizar** – Especifique o nome de cada tabela adicional que pretende sincronizar. Separe várias mesas usando uma vírem. Estas tabelas serão sincronizadas a partir da base de dados do site, para além dos grupos de replicação que selecionar.
  - **Tabelas excluídas para sincronizar** - Especifique o nome das tabelas individuais dos grupos de replicação que sincroniza. As tabelas que especificar serão excluídas. Separe várias mesas usando uma vírem.
- **Definições de sincronização:**
  - Intervalo de **sincronização (minutos)** - Especifique um valor em minutos. Após o intervalo ser alcançado, começa uma nova sincronização. Isto suporta uma autonomia de 60 a 1440 minutos (24 horas).
  - **Horário** - Especifique os dias que pretende que a sincronização seja executada.

**Acesso ao ponto de reporte:**   
Após a instalação da função de armazém de dados, certifique-se de que a conta que é utilizada como *Conta Ponto* de Relato tem a **db_datareader** permissão para a base de dados do armazém de dados.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Instalação de resolução de problemas e sincronização de dados
Utilize os seguintes registos para investigar problemas com a instalação do ponto de serviço do Armazém de Dados ou sincronização de dados:
- **DWSSMSI.log** e **DWSSSetup.log** - Utilize estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
- **Microsoft.ConfigMgrDataWarehouse.log** – Utilize este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.

### <a name="reporting"></a>Relatórios
Depois de instalar uma função do sistema de site data Warehouse, os seguintes relatórios estão disponíveis no seu ponto de serviços de Reporte com uma *categoria* de **Data Warehouse:**

|Relatório                   | Detalhes                                  |
|-------------------------|------------------------------------------|
| **Relatório de Implementação de Aplicações** | Consulte os detalhes para a implementação da aplicação para uma aplicação e máquina específicas.|
| **Relatório de Conformidade de Proteção de Pontofinal e Atualização de Software**   | Ver computadores que faltam atualizações de software.|
| **Relatório Geral de Inventário de Hardware**  | Veja todo o inventário de hardware para uma máquina específica.|
| **Relatório Geral de Inventário de Software**  | Veja todo o inventário de software para uma máquina específica.|
| **Visão geral da saúde das infraestruturas**  |Apresenta uma visão geral da saúde da sua infraestrutura de Gestor de Configuração.|
| **Lista de Malware Detetado**  |Veja o malware que foi detetado na organização.|
| **Relatório de Resumo da Distribuição de Software** | Um resumo da distribuição de software para um anúncio e máquina específicos.|

### <a name="move-the-data-warehouse-database"></a>Mova a base de dados do Data Warehouse
Utilize os seguintes passos para mover a base de dados do armazém de dados para um novo Servidor SQL:

1. Reveja a configuração da base de dados atual e grave os detalhes da configuração, incluindo:  
   - Os grupos de dados que sincroniza
   - Tabelas que inclui ou exclui da sincronização       

   Irá reconfigurar estes grupos e tabelas de dados depois de restaurar a base de dados num novo servidor e reinstalar a função do sistema do site.  

2. Utilize o SQL Server Management Studio para fazer backup na base de dados do armazém de dados e, em seguida, novamente para restaurar essa base de dados para um servidor SQL no novo computador que irá alojar o armazém de dados.

   Depois de restaurar a base de dados no novo servidor, certifique-se de que as permissões de acesso à base de dados são as mesmas na nova base de dados de depósitos de dados como estavam na base de dados original do armazém de dados.

3. Utilize a consola 'Gestor de Configuração' para remover a função do sistema de ponto de ponto do Serviço de Depósito de Dados do servidor atual.

4. Instale um novo ponto de serviço de armazém de dados e especifique o nome do novo Servidor SQL e instância que acolhe a base de dados do Data Warehouse que restaurou.

5. Após a instalação da função do sistema do local, o movimento está completo.

Pode rever os seguintes registos do Gestor de Configuração para confirmar que a função do sistema do site foi reinstalada com sucesso:  
- **DWSSMSI.log** e **DWSSSetup.log** - Utilize estes registos para investigar erros ao instalar o ponto de serviço do armazém de dados.
- **Microsoft.ConfigMgrDataWarehouse.log** – Utilize este registo para investigar a sincronização de dados entre a base de dados do site para a base de dados do armazém de dados.


## <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos
Começando com a versão de pré-visualização técnica 1612, pode utilizar uma nova ferramenta de linha de comando **(ContentLibraryCleanup.exe**) para remover conteúdos que já não estão associados a qualquer pacote ou aplicação a partir de um ponto de distribuição (conteúdo órfão). Esta ferramenta é chamada de ferramenta de limpeza da biblioteca de conteúdos.

Esta ferramenta apenas afeta o conteúdo no ponto de distribuição que especifica quando executa a ferramenta e não consegue remover o conteúdo da biblioteca de conteúdos no servidor do site.

Depois de instalar a Pré-visualização Técnica 1612, pode encontrar **contentLibraryCleanup.exe** no *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* no servidor do site de pré-visualização técnica.

A ferramenta lançada com esta Pré-Visualização Técnica destina-se a substituir versões mais antigas de ferramentas semelhantes lançadas para produtos anteriores do Gestor de Configuração. Embora esta versão da ferramenta deixe de funcionar após o dia 1 de março de 2017, novas versões serão lançadas com futuras Pré-visualizações técnicas até que esta ferramenta seja lançada como parte da Current Branch, ou uma produção pronta fora da banda.

### <a name="requirements"></a>Requisitos  
- A ferramenta pode ser executada diretamente no computador que acolhe o ponto de distribuição, ou remotamente a partir de outro servidor. A ferramenta só pode ser executada contra um único ponto de distribuição de cada vez.
- A conta de utilizador que executa a ferramenta deve ter diretamente permissões de administração baseadas em funções que sejam iguais a um Administrador Completo na hierarquia do Gestor de Configuração.  A ferramenta não funciona quando a conta de utilizador é concedida permissões como membro de um grupo de segurança windows que tem as permissões do Administrador Completo.

### <a name="modes-of-operation"></a>Modos de funcionamento
A ferramenta pode ser executada em dois modos:
1. **Modo E se:**   
   Quando não especifica o interruptor **/apagar,** a ferramenta funciona no modo What-If e identifica o conteúdo que seria eliminado do ponto de distribuição, mas não apaga quaisquer dados.

   - Quando a ferramenta funciona neste modo, as informações sobre o conteúdo que seriam eliminadas são automaticamente escritas no ficheiro de registo das ferramentas. O utilizador não é solicitado a confirmar cada possível eliminação.
   - Por predefinição, o ficheiro de registo é escrito na pasta temporária dos utilizadores no computador onde executa a ferramenta, no entanto pode utilizar o interruptor /log para redirecionar o ficheiro de registo para outro local.  
   </br>

   Recomendamos que execute a ferramenta neste modo e reveja o ficheiro de registo resultante antes de executar a ferramenta com o interruptor /apagar.  

2. **Eliminar**o modo : Quando executar a ferramenta com o interruptor **/apagar,** a ferramenta funciona no modo de apagar.

   - Quando a ferramenta funciona neste modo, o conteúdo órfão que é encontrado no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.
   -  Antes de apagar cada ficheiro, o utilizador é solicitado a confirmar que o ficheiro deve ser eliminado.  Você pode selecionar, **Y** para sim, **N** para não, ou **Sim para todos** para saltar mais solicitações e apagar todos os conteúdos órfãos.  
   </br>

   Recomendamos que execute a ferramenta no modo "E Se" e reveja o ficheiro de registo resultante antes de executar a ferramenta com o interruptor /apagar.  

Quando a ferramenta de limpeza da biblioteca de conteúdos funciona em ambos os modos, cria automaticamente um registo com um nome que inclui o modo em que a ferramenta funciona, nome de ponto de distribuição, data e hora de funcionamento. O ficheiro de registo abre-se automaticamente quando a ferramenta termina. Por predefinição, este registo é escrito para a pasta **temporária** dos utilizadores no computador onde executa a ferramenta.No entanto, pode utilizar um interruptor de linha de comando para redirecionar o ficheiro de registo para outro local, incluindo uma partilha de rede.   


### <a name="run-the-tool"></a>Executar a ferramenta
Para executar a ferramenta:
1. Abra um pedido de comando administrativo para uma pasta que contenha **ContentLibraryCleanup.exe**.  
2. Em seguida, introduza uma linha de comando que inclua os interruptores de linha de comando necessários e os interruptores opcionais que pretende utilizar.

**Edição conhecida** Quando a ferramenta é executada, um erro como o seguinte pode ser devolvido quando qualquer pacote ou implementação falhou, ou está em curso:
-  *Sistema.InvalidOperationException: Esta biblioteca de conteúdos não pode \<ser limpa neste momento porque o pacote de pacotes ID> não está totalmente instalado.*

**Solução:** Nenhuma. A ferramenta não pode identificar ficheiros órfãos quando o conteúdo está em andamento ou não foi implementado. Por isso, a ferramenta não lhe permitirá limpar o conteúdo até que esse problema seja resolvido.



### <a name="command-line-switches"></a>Interruptores de linha de comando  
Os seguintes interruptores de linha de comando podem ser utilizados em qualquer ordem.   

|Comutador|Detalhes|
|---------|-------|
|**/excluir**  |**Opcional** </br> Utilize este interruptor quando pretender eliminar o conteúdo do ponto de distribuição. É solicitado antes de o conteúdo ser apagado. </br></br> Quando este interruptor não é utilizado, os registos da ferramenta resultam em que conteúdo seria eliminado, mas não apaga qualquer conteúdo do ponto de distribuição. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Executar a ferramenta em modo silencioso que suprime todas as solicitações (como as solicitações quando está a eliminar o conteúdo), e não abra automaticamente o ficheiro de registo. </br></br> Exemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;ponto de distribuição FQDN>**  | **Necessário** </br> Especifique o nome de domínio totalmente qualificado (FQDN) do ponto de distribuição que pretende limpar. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;site primário FQDN>**       | **Opcional** na limpeza de conteúdos de um ponto de distribuição num local primário.</br>**Necessário** para a limpeza do conteúdo de um ponto de distribuição num local secundário. </br></br> Especifique o FQDN do local primário a que o ponto de distribuição pertence, ou do progenitor principal quando o ponto de distribuição estiver num local secundário. </br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **código do &lt;site primário /sc>**  | **Opcional** na limpeza de conteúdos de um ponto de distribuição num local primário.</br>**Necessário** para a limpeza do conteúdo de um ponto de distribuição num local secundário. </br></br> Especifique o código do site do local primário a que o ponto de distribuição pertence, ou do local primário dos pais quando o ponto de distribuição estiver num local secundário.</br></br> Exemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log \<log registrlog diretório de registo>**       |**Opcional** </br> Especifique um diretório para colocar ficheiros de registo. Isto pode ser uma unidade local, ou numa partilha de rede.</br></br> Quando este interruptor não é utilizado, os ficheiros de registo são automaticamente colocados na pasta temporária dos utilizadores.</br></br> Exemplo de unidade local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemplo de partilha de rede: ***ContentLibraryCleanup.exe \\ &lt;/dp server1.contoso.com /log share>\&lt;folder>***|


## <a name="improvements-for-in-console-search"></a>Melhorias para pesquisa na consola
Com base no feedback do User Voice, adicionámos as seguintes melhorias à pesquisa na consola:
- **Caminho do objeto:**  
  Muitos objetos suportam agora uma nova coluna chamada **Caminho do Objeto.**  Quando pesquisar e incluir esta coluna nos resultados do seu visor, pode ver o caminho para cada objeto. Por exemplo, se executar uma pesquisa de apps no nó de Aplicações e também estiver procurando sub-nós, a coluna *Object Path* no painel de resultados mostrar-lhe-á o caminho para cada objeto devolvido.   

- **Preservação do texto de pesquisa:**  
  Quando introduzir texto na caixa de texto de pesquisa e, em seguida, alternar entre procurar um sub-nó e o nó atual, o texto que digitou irá agora persistir e permanecer disponível para uma nova pesquisa sem ter que reescrever.

- **Preservação da sua decisão de pesquisar sub-nódosos:**  
  A opção que seleciona para pesquisar o *nó atual* ou *todos os sub-nós* agora persiste quando muda o nó em que está a trabalhar.   Este novo comportamento significa que não precisa de redefinir constantemente a decisão à medida que se move em torno da consola.  Por predefinição, quando abre a consola, a opção é apenas pesquisar o nó atual.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Impedir a instalação de uma aplicação se estiver em execução um programa especificado.
Pode agora configurar uma lista de ficheiros executáveis (com a extensão .exe) em propriedades do tipo de implementação que, se estiver em execução, bloquearão a instalação de uma aplicação. Após a instalação ser tentada, os utilizadores verão uma caixa de diálogo pedindo-lhes que fechem os processos que estão bloqueando a instalação.

### <a name="try-it-out"></a>Experimente
Para configurar uma lista de ficheiros executáveis
1. Na página de propriedades de qualquer tipo de implementação, escolha o separador de manuseamento do **instalador.**
2. Clique em **Adicionar,** para adicionar um dos ficheiros mais executáveis à lista (por **exemplo, Edge.exe**)
3. Clique **em OK** para fechar a caixa de diálogo de propriedades do tipo de implementação.

Agora, quando implementar esta aplicação para um utilizador ou dispositivo, e um dos executáveis que adicionou está em execução, o utilizador final verá uma caixa de diálogo do Software Center a dizer-lhes que a instalação falhou porque uma aplicação está em execução.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nova notificação do Windows Hello para negócios para utilizadores finais

Uma nova notificação do Windows 10 informa os utilizadores finais de que devem tomar medidas adicionais para completar a configuração do Windows Hello for Business (por exemplo, configurar um PIN).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Windows Store para suporte a negócios em Gestor de Configuração

Agora pode implementar aplicações licenciadas online com um propósito de implementação de **Disponível** a partir da Windows Store para Empresas para Computadores que executam o cliente do Gestor de Configuração.
Para mais detalhes, consulte [Gerir aplicações da Windows Store para Negócios com Gestor de Configuração](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

O suporte para esta funcionalidade encontra-se atualmente apenas disponível para PCs que executam a pré-visualização do Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Volte à página anterior quando uma sequência de tarefas falhar
Agora pode voltar a uma página anterior quando executar uma sequência de tarefas e houver uma falha. Antes desta libertação, teve de reiniciar a sequência de tarefas quando houve uma falha. Por exemplo, pode utilizar o botão **Anterior** nos seguintes cenários:

- Quando um computador começa no Windows PE, o diálogo de armadilha de sequência de tarefas pode ser exibido antes da sequência de tarefas estar disponível. Quando clicar em Next neste cenário, a página final da sequência de tarefas mostra com uma mensagem que não existem sequências de tarefas disponíveis. Agora, pode clicar em **Anteriorpara** procurar novamente as sequências de tarefas disponíveis. Pode repetir este processo até que a sequência de tarefas esteja disponível.
- Quando executa uma sequência de tarefas, mas os pacotes de conteúdo dependente ainda não estão disponíveis nos pontos de distribuição, a sequência de tarefas falha. Agora pode distribuir o conteúdo em falta (se ainda não foi distribuído) ou esperar que o conteúdo esteja disponível nos pontos de distribuição e, em seguida, clique **em Anterior** para ter a sequência de tarefas novamente pesquisado para o conteúdo.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Suporte de ficheiros de instalação express para atualizações do Windows 10
Adicionámos suporte a ficheiros de instalação expresso no 'Gestor de Configuração' para atualizações do Windows 10. Quando utilizar uma versão suportada do Windows 10, pode agora utilizar as definições do 'Gestor de Configuração' para descarregar apenas o delta entre a Atualização Cumulativa do Windows 10 do mês em curso e a atualização do mês anterior. Atualmente no 'Configuração Manager Current Branch', a atualização cumulativa completa do Windows 10 (incluindo todas as atualizações dos meses anteriores) é descarregada todos os meses. A utilização de ficheiros de instalação expresso fornece transferências menores e tempos de instalação mais rápidos nos clientes.

> [!IMPORTANT]
> Embora as definições para suportar a utilização de ficheiros de instalação expresso estão disponíveis no 'Gestor de Configuração', esta funcionalidade só é suportada na versão 1607 do Windows 1607 com uma atualização do Windows Update Agent incluída nas atualizações lançadas a 10 de janeiro de 2017 (Patch Tuesday). Para mais informações sobre estas atualizações, consulte o [artigo de suporte 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Pode usufruir de ficheiros de instalação expresso quando o próximo conjunto de atualizações for lançado a 14 de fevereiro de 2017. A versão 1607 do Windows 10 sem a atualização e as versões anteriores não suportam ficheiros de instalação expresso.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Para permitir o download de ficheiros de instalação expresso para atualizações do Windows 10 no servidor
Para começar a sincronizar os metadados dos ficheiros de instalação expresso do Windows 10, deve ative-os nas Propriedades do Ponto de Atualização de Software.
1. Na consola de Gestor de Configuração, navegue para**sites**de**configuração** > do site **da administração.** > 
2. Selecione o site da administração central ou o local primário autónomo.
3. No separador **Home Page** , no grupo **Definições** , clique em **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**. No separador **'Ficheiros' de atualização,** selecione **Descarregue ficheiros completos para todas as atualizações aprovadas e expresse ficheiros de instalação para o Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para permitir o suporte aos clientes para descarregar e instalar ficheiros de instalação expressa
Para permitir o suporte de ficheiros de instalação expresso nos clientes, deve ativar ficheiros de instalação expresso nos clientes na secção de Atualizações de Software das definições do cliente. Isto cria um novo ouvinte HTTP que ouve pedidos para descarregar ficheiros de instalação expresso na porta que especifica. Uma vez implementada as definições do cliente para ativar esta funcionalidade no cliente, tentará descarregar o delta entre a Atualização Cumulativa do Windows 10 do mês em curso e a atualização do mês anterior (os clientes devem executar uma versão do Windows 10 que suporta ficheiros de instalação expresso).
1. Ativar o suporte para ficheiros de instalação expresso nas propriedades do Componente de Ponto de Atualização de Software (procedimento anterior).
2. Na consola De Configuração Manager, navegue para**As Definições**de Cliente **de Administração.** > 
3. Selecione as definições apropriadas do cliente, em seguida, no separador **Casa,** clique em **Propriedades**.
4. Selecione a página de Atualizações de **Software,** configure **Sim** para a **instalação ativa de Atualizações Expressas na** definição de clientes e configure a porta utilizada pelo ouvinte HTTP no cliente para a Porta utilizada para descarregar conteúdo para a definição de **Express Updates.**


## <a name="odata-endpoint-data-access"></a>Acesso de dados de ponto final oData

 O Gestor de Configuração fornece agora um ponto final restful OData para aceder aos dados do Gestor de Configuração. O ponto final é compatível com a versão 4 do Odata, que permite a ferramentas como o Excel e o Power BI acederem facilmente aos dados do Gestor de Configuração através de um único ponto final. Pré-visualização técnica 1612 apenas suporta ler acesso a objetos no Gestor de Configuração.  

Os dados que estão atualmente disponíveis no [Fornecedor De Configuração WMI](../../develop/reference/configuration-manager-reference.md) também estão agora acessíveis com o novo ponto final OData RESTful. Os conjuntos de entidades expostos pelo ponto final do OData permitem-lhe enumerar os mesmos dados que pode consultar com o fornecedor wMI.

### <a name="try-it-out"></a>Experimente

Antes de poder utilizar o ponto final do OData, tem de o ativar para o site.

1.  Vá a**Sites**de**Configuração** > do Site **da Administração** > .
2.  Selecione o site principal e clique em **Propriedades**.
3.  No separador Geral da folha de propriedades do site primário, clique em **Enable REST endpoint para todos os fornecedores deste site**, e, em seguida, clique EM **OK**.

No seu espectador favorito da consulta OData, experimente consultas semelhantes aos seguintes exemplos para devolver vários objetos no Gestor de Configuração:

| Objetivo | Consulta OData |
|---|---|
| Obtenha todas as coleções | `http://localhost/CMRestProvider/Collection` |
| Obter uma coleção | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obtenha os 100 melhores dispositivos da coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obtenha um dispositivo com uma identificação de recursos na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obtenha o sistema operativo do dispositivo na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obter utilizadores na coleção | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> As consultas de exemplo mostradas na tabela utilizam o *hospedeiro local* como nome de anfitrião no URL e podem ser utilizadas no computador que executa o Provedor sms. Se estiver a executar as suas consultas a partir de um computador diferente, substitua o anfitrião local pelo FQDN do servidor pelo Fornecedor SMS instalado.

## <a name="azure-active-directory-onboarding"></a>Onboarding Azure Ative Directory

O onboarding Azure Ative Directory (AD) cria uma ligação entre o Diretor de Configuração e o Diretório Ativo Azure a ser utilizado por outros serviços na nuvem. Isto pode atualmente ser usado para criar a ligação necessária para o Gateway de Gestão de Nuvem.

Execute esta tarefa com um administrador Azure, pois necessitará de credenciais de administrador Azure.

#### <a name="to-create-the-connection"></a>Para criar a ligação:

2. No espaço de trabalho **da Administração,** escolha **Cloud Services** > **Azure Ative Directory** > **Add Azure Ative Directory**.
2. Escolha **iniciar sessão** para criar a ligação com o Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Requisitos do cliente do Gestor de Configuração

Existem vários requisitos para permitir a criação da política de utilizadores no Gateway de Gestão de Nuvem.

- O processo de embarque da AD Azure tem de estar concluído e o cliente tem de estar inicialmente ligado à rede corporativa para obter a informação de ligação.
- Os clientes devem ser ambos unidos por domínio (registados em Diretório Ativo) e unidos em nuvem (registados em Azure AD).
- Tem de executar a [Ative Directory User Discovery](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Deve modificar o cliente do Gestor de Configuração para permitir pedidos de política de utilizador através da Internet e implementar a alteração para o cliente. Uma vez que esta alteração ao cliente ocorre *no dispositivo cliente,* pode ser implementada através do Gateway de Gestão de Nuvem, embora não tenha concluído as alterações de configuração necessárias para a política do utilizador.
- O seu ponto de gestão deve ser configurado para utilizar HTTPS para fixar o token na rede e deve ter .Net 4.5 instalada.

Depois de efazer estas alterações de configuração, pode criar uma política de utilizador e mover os clientes para a Internet para testar a política. Os pedidos de política de utilizador através do Gateway de Gestão de Cloud serão autenticados com autenticação baseada em token Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Alterar para configurar a autenticação de vários fatores para a inscrição do dispositivo

Agora que pode configurar a autenticação de vários fatores (MFA) para a inscrição do dispositivo no portal Azure, a opção MFA foi removida na consola 'Gestor de Configuração'. Pode encontrar mais informações sobre a criação de MFA para inscrição [neste tópico Microsoft Intune](/mem/intune/enrollment/multi-factor-authentication).
