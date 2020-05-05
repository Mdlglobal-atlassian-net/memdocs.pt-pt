---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Crie e execute scripts PowerShell em dispositivos de cliente.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2113baf43c377379a2a996c59fd13e55072cf898
ms.sourcegitcommit: d05b1472385c775ebc0b226e8b465dbeb5bf1f40
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605189"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts PowerShell a partir da consola De Configuração Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1236459-->
O Gestor de Configuração tem uma capacidade integrada de executar scripts PowerShell. A PowerShell tem o benefício de criar scripts sofisticados e automatizados que sejam compreendidos e partilhados com uma comunidade maior. Os scripts simplificam a construção de ferramentas personalizadas para administrar software e permitem-lhe realizar tarefas mundanas rapidamente, permitindo-lhe obter grandes trabalhos feitos de forma mais fácil e consistente.  

> [!Note]  
> O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Com esta integração no Gestor de Configuração, pode utilizar a funcionalidade *Executar Scripts* para fazer as seguintes coisas:

- Crie e edite scripts para uso com O Gestor de Configuração.
- Gerencie o uso do script através de funções e âmbitos de segurança. 
- Executar scripts em coleções ou computadores individuais no local geridos pelo Windows.
- Obtenha resultados rápidos de script agregados a partir de dispositivos clientes.
- Monitorize a execução do script e veja os resultados dos relatórios a partir da saída do script.

> [!WARNING]
> - Dado o poder dos guiões, lembramo-lo de ser intencional e cuidadoso com o seu uso. Construímos salvaguardas adicionais para o ajudar; papéis e âmbitos segregados. Certifique-se de validar a precisão dos scripts antes de executá-los e confirmar que são de uma fonte fidedigna, para evitar a execução não intencional do script. Esteja atento a personagens estendidos ou outras obfuscções e educe-se sobre a obtenção de scripts. [Saiba mais sobre a segurança do script PowerShell](learn-script-security.md)
> - Certos softwares anti-malware podem inadvertidamente desencadear eventos contra as funcionalidades de execução do Gestor de Configuração ou CMPivot. Recomenda-se excluir %windir%\CCM\ScriptStore para que o software anti-malware permita que essas funcionalidades executem sem interferências.

## <a name="prerequisites"></a>Pré-requisitos

- Para executar scripts PowerShell, o cliente deve estar executando a versão 3.0 da PowerShell ou mais tarde. No entanto, se um script que executa contém funcionalidades a partir de uma versão posterior do PowerShell, o cliente no qual executa o script deve estar executando essa versão do PowerShell.
- Os clientes do Gestor de Configuração devem estar a executar o cliente a partir do lançamento de 1706, ou mais tarde para executar scripts.
- Para utilizar scripts, deve ser membro da função de segurança do Gestor de Configuração apropriado.
- Para importar e escrever scripts de autor - A sua conta deve ter permissões **para criar** permissões para **scripts SMS**.
- Para aprovar ou negar scripts - A sua conta deve ter permissões **de aprovação** para **scripts SMS**.
- Para executar scripts - A sua conta deve ter permissões **de Script executar** para **Coleções**.

Para mais informações sobre as funções de segurança do Gestor de Configuração:</br>
[Âmbitos de segurança para scripts de execução](#security-scopes)</br>
[Funções de segurança para executar scripts](#bkmk_ScriptRoles)</br>
[Fundamentos da administração baseada em papéis.](../../core/understand/fundamentals-of-role-based-administration.md)

## <a name="limitations"></a>Limitações

Executar Scripts atualmente suporta:

- Scripting idiomas: PowerShell
- Tipos de parâmetros: inteiro, corda e lista.


>[!WARNING]
>Esteja ciente de que ao utilizar parâmetros, abre uma área de superfície para um potencial risco de ataque de injeção PowerShell. Existem várias formas de mitigar e trabalhar ao redor, tais como usar expressões regulares para validar a entrada do parâmetro ou usar parâmetros pré-definidos. A melhor prática comum não é incluir segredos nos seus scripts PowerShell (sem palavras-passe, etc.). [Saiba mais sobre a segurança do script PowerShell](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Executar autores e aprovadores do Script

Executar Scripts usa o conceito de autores de *scripts* e *aprovadores* de scripts como papéis separados para implementação e execução de um script. Ter as funções de autor e aprovador separadas permite uma verificação de processo importante para a ferramenta poderosa que executa scripts é. Há um papel adicional de *script runners* que permite a execução de scripts, mas não a criação ou aprovação de scripts. Ver [Criar funções de segurança para scripts](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Controlo de papéis scripts

Por padrão, os utilizadores não podem aprovar um guião que tenham sido autores. Como os scripts são poderosos, versáteis e potencialmente implantados em muitos dispositivos, pode separar os papéis entre a pessoa que autora o script e a pessoa que aprova o script. Estas funções dão um nível adicional de segurança contra a execução de um guião sem supervisão. Podedesligar a aprovação secundária, para facilitar os testes.

### <a name="approve-or-deny-a-script"></a>Aprovar ou Negar um guião

Os scripts devem ser aprovados, pelo papel de aprovador do *script,* antes de poderem ser executados. Para aprovar um guião:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho da Biblioteca de **Software,** clique em **Scripts**.
3. Na lista **script,** escolha o script que pretende aprovar ou negar e, em seguida, no separador **Home,** no grupo **Script,** clique **em Aprovar/Negar**.
4. Na caixa de diálogo **De aprovação ou negar,** selecione **'Aprovar'** ou **Negar** o script. Opcionalmente, insira um comentário sobre a sua decisão.  Se negar um guião, não pode ser executado em dispositivos de cliente. <br>
![Script - Aprovação](./media/run-scripts/RS-approval.png)
1. Conclua o assistente. Na lista de **Scripts,** vê-se a alteração da coluna do Estado de **Aprovação** dependendo da ação que tomou.

### <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os utilizadores aprovem os seus próprios scripts

Esta aprovação é usada principalmente para a fase de teste do desenvolvimento do script.

1. Na consola do Configuration Manager, clique em **Administração**.
2. No espaço de trabalho da **Administração,** expanda a Configuração do **Site,** e depois clique em **Sites**.
3. Na lista de sites, escolha o seu site e, em seguida, no separador **Home,** no grupo **Sites,** clique em **Definições de Hierarquia**.
4. No separador **Geral** da caixa de diálogo de **definições** de hierarquia, limpe a caixa de diálogo do Script da caixa de verificação que requer um **aprovador de script adicional**.

>[!IMPORTANT]
>Como uma boa prática, não deve permitir que um autor de guião aprove os seus próprios scripts. Só deve ser permitido num laboratório. Considere cuidadosamente o impacto potencial de mudar este cenário num ambiente de produção.

## <a name="security-scopes"></a>Âmbitos de segurança
  
Os Scripts de Execução utilizam âmbitos de segurança, uma funcionalidade existente do Gestor de Configuração, para controlar scripts de autoria e execução através de etiquetas de atribuição que representam grupos de utilizadores. Para obter mais informações sobre a utilização de âmbitos de segurança, consulte a [configuração da administração baseada em funções para o Gestor de Configuração](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a>Criar papéis de segurança para scripts
As três funções de segurança utilizadas para executar scripts não são criadas por padrão no 'Gestor de Configuração'. Para criar os script runners, autores de scripts e papéis de aprovadores de scripts, siga os passos delineados.

1. Na consola de Gestor de Configuração, vá a**Funções** de**Segurança** >da **Administração** >
2. Clique à direita numa função e clique em **Copiar**. O papel que copia tem permissões já atribuídas. Certifique-se de que só aceita as permissões que quiser. 
3. Dê ao papel personalizado um **nome** e uma **descrição.** 
4. Atribuir a função de segurança as permissões descritas abaixo.  

### <a name="security-role-permissions"></a>Permissões de papel de segurança  

**Nome do papel**: Script Runners  
- **Descrição**: Estas permissões permitem que este papel apenas execute scripts que foram previamente criados e aprovados por outras funções.  
- **Permissões:** Certifique-se de que os seguintes estão definidos para **Sim**.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar script|Sim|
|Site|Leitura|Sim|
|SMS Scripts|Leitura|Sim|


**Nome do papel**: Autores do guião  
- **Descrição**: Estas permissões permitem este papel aos scripts de autor, mas não podem aprová-los ou executá-los.  
- **Permissões**: Certifique-se de que estão definidas as seguintes permissões.
 
|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar script|Não|
|Site|Leitura|Sim|
|SMS Scripts|Criar|Sim|
|SMS Scripts|Leitura|Sim|
|SMS Scripts|Eliminar|Sim|
|SMS Scripts|Modificar|Sim|


**Nome de função**: Aprovadores de Script  
- **Descrição**: Estas permissões permitem que esta função aprove scripts, mas não podem criá-los ou executá-los.  
- **Permissões:** Certifique-se de que estão definidas as seguintes permissões.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar script|Não|
|Site|Leitura|Sim|
|SMS Scripts|Leitura|Sim|
|SMS Scripts|Aprovar|Sim|
|SMS Scripts|Modificar|Sim|

     
**Exemplo de permissões de scripts SMS para o papel de autores do script**  

 ![Exemplo de permissões de scripts SMS para o papel de autores do script](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Criar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No espaço de trabalho da Biblioteca de **Software,** clique em **Scripts**.
3. No separador **Home,** no grupo **Criar,** clique em **Criar Script**.
4. Na página **script** do assistente de **script** criar, configure as seguintes definições:
    - **Nome script** - Introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, usar nomes duplicados dificulta-lhe a descoberta do script de que necessita na consola 'Gestor de Configuração'.
    - **Linguagem script** - Atualmente, apenas os scripts PowerShell são suportados.
    - **Import** - Importar um script PowerShell para a consola. O script é exibido no campo **Script.**
    - **Clear** - Remove o script atual do campo Script.
    - **Script** - Exibe o script atualmente importado. Pode editar o guião neste campo conforme necessário.
5. Conclua o assistente. O novo script é apresentado na lista de **Script** com um estatuto de **Espera para aprovação**. Antes de poder executar este guião em dispositivos de cliente, tem de aprová-lo. 

> [!IMPORTANT]
> Evite escrever um reboot de dispositivo ou reiniciar o agente 'Gestor de Configuração' quando utilizar a função 'Executar Scripts'. Fazê-lo pode levar a um estado de reinicialização contínua. Se necessário, existem melhorias na funcionalidade de notificação do cliente que permitem reiniciar os dispositivos. A [coluna de reinício pendente](../../core/clients/manage/manage-clients.md#restart-clients) pode ajudar a identificar dispositivos que precisam de ser reiniciados. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parâmetros do script

A adição de parâmetros a um script proporciona uma maior flexibilidade para o seu trabalho. Pode incluir até 10 parâmetros. O seguinte descreve a capacidade atual da funcionalidade Executar Scripts com parâmetros de script para; *String,* tipos de dados *inteiros.* Estão também disponíveis listas de valores predefinidos. Se o seu script tiver tipos de dados não suportados, recebe um aviso.

No diálogo **Criar script,** clique em **Parâmetros de Script** sob **script**.

Cada um dos parâmetros do seu script tem o seu próprio diálogo para adicionar mais detalhes e validação. Se houver um parâmetro padrão no script, será enumerado no IDe parâmetro e poderá defini-lo. O Gestor de Configuração não sobreporá o valor predefinido, uma vez que nunca modificará o script diretamente. Pode pensar nisto como "valores sugeridos pré-povoados" são fornecidos na UI, mas o Gestor de Configuração não fornece acesso a valores "padrão" no tempo de funcionação. Isto pode ser trabalhado editando o script para ter os predefinidos corretos. <!--17694323-->

>[!IMPORTANT]
> Os valores dos parâmetros não contêm uma única citação. </br></br>
> Há uma questão conhecida em que os valores dos parâmetros que incluem ou são incluídos em citações individuais não são transmitidos corretamente para o script. Ao especificar os valores de parâmetros predefinidos que contêm um espaço dentro de um script, utilize aspas duplas. Ao especificar os valores de parâmetro padrão durante a criação ou execução de um **Script,** em torno do valor predefinido em orçamentos duplos ou únicos não é necessário independentemente de o valor conter ou não um espaço.

### <a name="parameter-validation"></a>Validação de parâmetros

Cada parâmetro no seu script tem um diálogo **script parametria Properties** para que adicione validação para esse parâmetro. Depois de adicionar validação, deve obter erros se estiver a introduzir um valor para um parâmetro que não cumpra a sua validação.

#### <a name="example-firstname"></a>Exemplo: *Primeiro Nome*

Neste exemplo, é possível definir as propriedades do parâmetro de corda, *FirstName*.

![Parâmetros do script - corda](./media/run-scripts/RS-parameters-string.png)


A secção de validação do diálogo **Script Parameter Properties** contém os seguintes campos para a sua utilização:

- **Comprimento mínimo** - número mínimo de caracteres do campo *FirstName.*
- **Comprimento máximo**- número máximo de caracteres do campo *FirstName*
- **RegEx** - abreviatura de *Expressão Regular*. Para obter mais informações sobre a utilização da Expressão Regular, consulte a secção seguinte, *utilizando validação*de expressão regular .
- **Erro personalizado** - útil para adicionar a sua própria mensagem de erro personalizada que substitui quaisquer mensagens de erro de validação do sistema.

#### <a name="using-regular-expression-validation"></a>Utilização da validação de expressão regular

Uma expressão regular é uma forma compacta de programação para verificar uma série de caracteres contra uma validação codificada. Por exemplo, pode verificar a ausência de um personagem alfabético maiúsculo no campo *FirstName* colocando-o `[^A-Z]` no campo *RegEx.*

O processamento regular de expressão para este diálogo é suportado pelo .NET Framework. Para obter orientações sobre a utilização de expressões regulares, consulte [.NET Expressão Regular](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions) e [Linguagem de Expressão Regular](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Exemplos de script

Aqui estão alguns exemplos que ilustram scripts que você pode querer usar com esta capacidade.

### <a name="create-a-new-folder-and-file"></a>Criar uma nova pasta e arquivar

Este script cria uma nova pasta e um ficheiro dentro da pasta, dada a sua entrada de nomeação.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obter versão OS

Este script utiliza o WMI para consultar a máquina para a sua versão OS.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a>Editar ou copiar scripts PowerShell
<!--3705507-->
*(Introduzido com a versão 1902)*  
Pode **editar** ou **copiar** um script PowerShell existente utilizado com a funcionalidade **Executar Scripts.** Em vez de recriar um guião que precisa de mudar, agora edite-o diretamente. Ambas as ações usam a mesma experiência de feiticeiro que quando crias um novo script. Quando edita ou copia um script, o Gestor de Configuração não persiste no estado de aprovação.

> [!Tip]  
> Não edite um guião que esteja ativamente a funcionar com clientes. Eles não vão terminar de executar o script original, e você pode não obter os resultados pretendidos destes clientes.  

### <a name="edit-a-script"></a>Editar um script

1. Vá ao nó **scripts** sob o espaço de trabalho da Biblioteca de **Software.**
1. Selecione o script para editar e, em seguida, clique em **Editar** na fita. 
1. Altere ou reimporte o seu script na página detalhes do **script.**
1. Clique em **Seguir** para ver o **Resumo** e **depois Feche** quando terminar de editar.

### <a name="copy-a-script"></a>Copiar um guião

1. Vá ao nó **scripts** sob o espaço de trabalho da Biblioteca de **Software.**
1. Selecione o script para copiar e, em seguida, clique em **Copiar** na fita.
1. Mude o nome do script no campo de **nome** script e efaça quaisquer edites adicionais que possa precisar.
1. Clique em **Seguir** para ver o **Resumo** e **depois Feche** quando terminar de editar.


## <a name="run-a-script"></a>Executar um roteiro

Depois de um script ser aprovado, pode ser executado contra um único dispositivo ou uma coleção. Assim que a execução do teu guião começa, é lançado rapidamente através de um sistema de alta prioridade que se passa em uma hora. Os resultados do script são então devolvidos usando um sistema de mensagens estatais.

Para selecionar uma coleção de alvos para o seu script:

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Na área de trabalho Ativos e Compatibilidade , clique em **Coleções de Dispositivos**.
3. Na lista de Coleções de **Dispositivos,** clique na recolha de dispositivos em que pretende executar o script.
4. Selecione uma coleção à sua escolha, clique em **Executar Script**.
5. Na página **script** do assistente do **Script Executar,** escolha um script da lista. Apenas são mostrados guiões aprovados.
6. Clique em **Seguinte**e, em seguida, complete o assistente.

> [!IMPORTANT]
> Se um script não funcionar, por exemplo, porque um dispositivo-alvo é desligado durante o período de hora, deve executá-lo novamente.

### <a name="target-machine-execution"></a>Execução de máquina-alvo

O script é executado como *o sistema* ou conta *de computador* no ou cliente visado. Esta conta tem acesso limitado à rede. Qualquer acesso a sistemas e locais remotos pelo script deve ser aprovisionado em conformidade.

## <a name="script-monitoring"></a>Monitorização do script

Depois de ter iniciado a execução de um script numa coleção de dispositivos, utilize o seguinte procedimento para monitorizar a operação. Você é capaz de monitorizar um script em tempo real à medida que executa, e mais tarde voltar ao estado e resultados para uma determinada execução do Script Run. Os dados do estado do script são limpos como parte da tarefa de manutenção de Operações de [Cliente Envelhecido sieliminada](../../core/servers/manage/reference-for-maintenance-tasks.md) ou eliminação do script.<br>

![Script monitor - Script Executar Status](./media/run-scripts/RS-monitoring-three-bar.png)

1. Na consola 'Gestor de Configuração', clique em **Monitorização**.
2. No espaço de trabalho **de monitorização,** clique no **Estado do Script**.
3. Na lista de Estado do **Script,** vê os resultados de cada script que executou nos dispositivos do cliente. Um código de saída de script de **0** geralmente indica que o script correu com sucesso.

 
   ![Script monitor - Truncated Script](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Saída do script

Saída de script de retorno do cliente utilizando a formatação JSON, canalizando os resultados do script para o cmdlet [ConvertTo-Json.](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertto-json) O formato JSON devolve consistentemente a saída de scriptlegível. Para scripts que não devolvem objetos como saída, o cmdlet ConvertTo-Json converte a saída numa simples corda que o cliente devolve em vez de JSON.  

- Scripts que obtêm um resultado desconhecido, ou onde o cliente estava offline, não vão aparecer nas tabelas ou conjunto de dados. <!--507179-->
- Evite devolver a saída de guião grande, uma vez que é truncada a 4 KB. <!--508488-->
- Converta um objeto enum para um valor de cadeia em scripts para que sejam corretamente exibidos na formatação JSON. <!--508377-->

   ![Converter objeto enum para um valor de picada](./media/run-scripts/enum-tostring-JSON.png)

Pode visualizar a saída detalhada do script em formato JSON cru ou estruturado. Esta formatação facilita a leitura e análise da saída. Se o script devolver texto formado por JSON válido ou a saída puder ser convertida para JSON utilizando o cmdlet [ConvertTo-Json](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/convertto-json) PowerShell, então veja a saída detalhada como **JSON Output** ou **Raw Output**. Caso contrário, a única opção é a **Saída do Script.**

### <a name="example-script-output-is-convertible-to-valid-json"></a>Exemplo: A saída do script é convertível para JSON válido

Comando:`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Exemplo: A saída de script não é válida JSON

Comando:`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Ficheiros de registo

- No cliente, por predefinição nos registos C:\Windows\CCM\:  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- No MP, por defeito em C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- No servidor do site, por padrão em C:\Program Files\Configuração Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>Veja também

- [Configure a administração baseada em funções para o Gestor de Configuração](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Noções básicas sobre a administração baseada em funções](../../core/understand/fundamentals-of-role-based-administration.md)
