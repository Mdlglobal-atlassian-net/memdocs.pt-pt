---
title: Ver relatórios do BitLocker
titleSuffix: Configuration Manager
description: Conheça os relatórios de gestão bitLocker no Gestor de Configuração
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717357"
---
# <a name="view-bitlocker-reports"></a>Ver relatórios do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Depois de [instalar os relatórios](setup-websites.md) no ponto de serviços de reporte, pode ver os relatórios. Os relatórios mostram a conformidade do BitLocker para a empresa e para dispositivos individuais. Eles fornecem informações e gráficos tabular, e têm filtros que permitem ver dados de diferentes perspetivas.

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização,** expanda **o Reporting**e selecione o nó **de Relatórios.** Os seguintes relatórios estão na categoria **BitLocker Management:**

- [Conformidade com o computador BitLocker](#bkmk-compliancereport)

- [Painel de Conformidade Da Empresa BitLocker](#bkmk-dashboard)

- [Detalhes de conformidade da empresa BitLocker](#bkmk-compliancedetails)

- [Resumo do cumprimento da empresa BitLocker](#bkmk-compliancesummary)

- [Relatório de Auditoria de Recuperação](#bkmk-audit)

Pode aceder a todos estes relatórios diretamente do site de pontos de ponto de reporte.

> [!NOTE]
> Para que estes relatórios apresentem dados completos:
>
> - Criar e implementar uma política de gestão BitLocker para uma coleção de dispositivos
> - Os clientes na coleção de alvos precisam de enviar o inventário de hardware

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>Conformidade do computador BitLocker

Use este relatório para recolher informações específicas para um computador. Fornece informações detalhadas de encriptação sobre a unidade de SE e quaisquer unidades de dados fixas. Para ver os detalhes de cada unidade, expanda a entrada de Nome do Computador. Também indica a política aplicada a cada tipo de unidade no computador.

[![Screenshot de exemplo do relatório de conformidade do computador BitLocker](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

Também pode utilizar este relatório para determinar o último estado de encriptação bitLocker conhecido de computadores perdidos ou roubados. O Gestor de Configuração determina a conformidade do dispositivo com base nas políticas bitLocker que implementa. Antes de tentar determinar o estado de encriptação BitLocker de um dispositivo, verifique as políticas que implementou para o mesmo.

> [!NOTE]
> Este relatório não mostra o estado de encriptação do Volume de Dados Amovíveis.

### <a name="computer-details"></a>Detalhes do computador

|Nome&nbsp;da coluna|Descrição|
|----------------|----|
|Nome do computador|Nome de computador DNS especificado pelo utilizador.|
|Nome de domínio|Nome de domínio totalmente qualificado para o computador.|
|Tipo de computador|Tipo de computador, tipos válidos são **não portáteis** e **portáteis.**|
|Sistema operativo|Tipo de sistema operativo do computador.|
|Conformidade geral|Estado geral de conformidade bitLocker do computador. Os estados válidos são **conformes** e **não conformes.** O [estado de conformidade por unidade](#bkmk_volume) pode indicar diferentes estados de conformidade. No entanto, este campo representa esse estado de conformidade a partir da política especificada.|
|Conformidade do sistema operativo|Estado de conformidade do Sistema operativo no computador. Os estados válidos são **conformes** e **não conformes.**|
|Conformidade de unidade de dados fixos|Estado de conformidade de uma unidade de dados fixa no computador. Os estados válidos são **conformes** e **não conformes.**|
|Última data de atualização|Data e hora que o computador contactou pela última vez o servidor para reportar o estado de conformidade.|
|Isenção|Indica se o utilizador está isento ou não isento da política BitLocker.|
|Utilizador isento|O utilizador que está isento da política bitLocker.|
|Data de isenção|Data em que foi concedida a isenção.|
|Detalhes do estado de conformidade|Error and status messages about the compliance state of the computer from the specificd policy.|
|Força de cifra política|Força de cifra que selecionou na política de gestão bitLocker.|
|Política: Unidade do sistema operativo|Indica se a encriptação é necessária para a unidade de SO e o tipo de protetor apropriado.|
|Política: Unidade de dados fixos|Indica se a encriptação é necessária para a unidade de dados fixa.|
|Fabricante|Nome do fabricante do computador tal como aparece no BIOS do computador.|
|Modelo|Nome do modelo do fabricante de computadores tal como aparece no BIOS do computador.|
|Utilizadores de dispositivos|Utilizadores conhecidos no computador.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a>Volume de computador

|Nome&nbsp;da coluna|Descrição|
|----------------|----|
|Letra da unidade|A carta de condução no computador.|
|Tipo de unidade|Tipo de unidade. Os valores válidos são **a Unidade do Sistema Operativo** e a Unidade de Dados **Fixos.** Estas entradas são unidades físicas em vez de volumes lógicos.|
|Força de cifra|Força de cifra que selecionou durante a política de gestão bitLocker.|
|Tipos protetores|Tipo de protetor que selecionou na política para encriptar a unidade. Os tipos de proteção válidos para uma unidade DE So são **TPM** ou **TPM+PIN**. O tipo de protetor válido para uma unidade de dados fixo é **Password**.|
|Estado protetor|Indica que o computador ativou o tipo protetor especificado na política. Os estados válidos estão **LIGADOs** ou **DESLIGADOs**.|
|Estado de encriptação|Estado de encriptação da unidade. Os estados válidos são **encriptados,** **não encriptados**ou **encriptados.**|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>Painel de conformidade com a empresa BitLocker

Este relatório fornece os seguintes gráficos, que mostram o estado de conformidade do BitLocker em toda a sua organização:

- Distribuição do estado de conformidade

- Não conforme - Distribuição de erros

- Distribuição do estado de conformidade por tipo de unidade

[![Screenshot de exemplo do painel de conformidade da empresa BitLocker](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Distribuição do estado de conformidade

Este gráfico de tartes mostra o estado de conformidade dos computadores da organização. Mostra também a percentagem de computadores com esse estado de conformidade, em comparação com o número total de computadores na coleção selecionada. O número real de computadores com cada estado também é mostrado.

O gráfico da tarte mostra os seguintes estados de conformidade:

- Compatível

- Incompatível

- Isento de utilizador

- Isento de utente temporário

- Política não aplicada

- Desconhecido. Estes computadores relataram um erro de estado, ou fazem parte da recolha, mas nunca reportaram o seu estado de conformidade. A falta de um estado de conformidade pode ocorrer se o computador estiver desligado da organização.

### <a name="non-compliant---errors-distribution"></a>Não conforme - Distribuição de erros

Este gráfico de tartes mostra as categorias de computadores na sua organização que não estão em conformidade com a política de encriptação BitLocker Drive. Mostra também o número de computadores em cada categoria. O relatório calcula cada percentagem do número total de computadores não conformes na recolha.

- Encriptação adiada do utilizador

- Incapaz de encontrar TPM compatível

- Partição do sistema não disponível ou grande o suficiente

- TPM visível, mas não inicializado

- Conflito político

- Esperando o fornecimento automático de TPM

- Ocorreu um erro desconhecido.

- Sem informação. Estes computadores não têm o agente de gestão BitLocker instalado, ou está instalado, mas não está ativado. Por exemplo, o serviço não está a funcionar.

### <a name="compliance-status-distribution-by-drive-type"></a>Distribuição do estado de conformidade por tipo de unidade

Este gráfico de barras mostra o estado de conformidade bitLocker atual por tipo de unidade. Os estatutos são **conformes** e **não conformes**. As barras são mostradas para unidades de dados fixas e unidades de S. O relatório inclui computadores sem uma unidade de dados fixa, e apenas mostra um valor na barra de acionamento do **sistema operativo.** O gráfico não inclui utilizadores a quem foi concedida uma isenção da política de encriptação BitLocker Drive ou da categoria No Policy.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>Detalhes de conformidade da empresa BitLocker

Este relatório mostra informações sobre a conformidade geral do BitLocker em toda a sua organização para a recolha de computadores para os quais implementou a política de gestão bitLocker.

[![Screenshot de exemplo dos detalhes de conformidade da empresa BitLocker](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Nome da coluna|Descrição|
|--- |--- |
|Computadores geridos|Número de computadores para os quais implementou uma política de gestão BitLocker.|
|% conforme|Percentagem de computadores compatíveis na organização.|
|% Incompatível|Percentagem de computadores não conformes na organização.|
|% Conformidade desconhecida|Percentagem de computadores com um estado de conformidade que não é conhecido.|
|% Isento|Percentagem de computadores isentos do requisito de encriptação BitLocker.|
|% Não isento|Percentagem de computadores não isentos do requisito de encriptação BitLocker.|
|Compatível|Contagem de computadores compatíveis na organização.|
|Em Não Conformidade|Contagem de computadores não conformes na organização.|
|Conformidade Desconhecida|Conde de computadores com um estado de conformidade que não é conhecido.|
|Isento|Contagem de computadores isentos do requisito de encriptação BitLocker.|
|Não isento|Contagem de computadores que não estão isentos do requisito de encriptação BitLocker.|

### <a name="computer-details"></a>Detalhes do computador

|Nome da coluna|Descrição|
|--- |--- |
|Nome do computador|Nome do computador DNS do dispositivo gerido.|
|Nome de domínio|Nome de domínio totalmente qualificado para o computador.|
|Estado de conformidade|Estado geral de conformidade do computador. Os estados válidos são **conformes** e **não conformes.**|
|Isenção|Indica se o utilizador está isento ou não isento da política BitLocker.|
|Utilizadores de dispositivos|Utilizadores do dispositivo.|
|Detalhes do estado de conformidade|Error and status messages about the compliance state of the computer from the specificd policy.|
|Último contacto|Data e hora que o computador contactou pela última vez o servidor para reportar o estado de conformidade.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>Resumo do cumprimento da empresa BitLocker

Use este relatório para mostrar a conformidade geral do BitLocker em toda a sua organização. Também mostra a conformidade com os computadores individuais aos quais implementou a política de gestão bitLocker.

[![Screenshot de exemplo do resumo de conformidade da empresa BitLocker](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Nome da coluna|Descrição|
|--- |--- |
|Computadores geridos|Número de computadores que gere com a política bitLocker.|
|% conforme|Percentagem de computadores compatíveis na sua organização.|
|% Incompatível|Percentagem de computadores não conformes na sua organização.|
|% Conformidade desconhecida|Percentagem de computadores com um estado de conformidade que não é conhecido.|
|% Isento|Percentagem de computadores isentos do requisito de encriptação BitLocker.|
|% Não isento|Percentagem de computadores não isentos do requisito de encriptação BitLocker.|
|Compatível|Contagem de computadores compatíveis na sua organização.|
|Incompatível|Contagem de computadores não conformes na sua organização.|
|Conformidade desconhecida|Conde de computadores com um estado de conformidade que não é conhecido.|
|Isento|Contagem de computadores isentos do requisito de encriptação BitLocker.|
|Não isento|Contagem de computadores que não estão isentos do requisito de encriptação BitLocker.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>Relatório de auditoria de recuperação

> [!NOTE]
> Este relatório também está disponível no site de [administração e monitorização bitLocker.](helpdesk-portal.md#reports)
>
> Para ver este relatório na consola Do Gestor de Configuração, vá ao espaço de trabalho **de Monitorização.** No painel de navegação, expanda o nó **reporte,** expanda **os Relatórios**e expanda a pasta **BitLocker Management.** Selecione a subpasta para a versão localizada do relatório, por exemplo, **en-us**.

Utilize este relatório para auditar os utilizadores que solicitaram o acesso às chaves de recuperação do BitLocker. Pode filtrar os seguintes critérios:

- Um tipo específico de utilizador, por exemplo, um utilizador de secretária de ajuda ou um utilizador final
- Se o pedido falhou ou foi bem sucedido
- O tipo específico de chave solicitado: Palavra-passe de chave de recuperação, ID da chave de recuperação ou Hash de senha de tpm
- Um intervalo de data durante o qual ocorreu a recuperação

[![Screenshot exemplo do relatório de auditoria bitLocker Recovery](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Nome&nbsp;da coluna|Descrição|
|----------------|----|
|Data e hora do pedido|Data e hora que um utilizador final ou utilizador de mesa de ajuda solicitou uma chave.|
|Fonte de pedido de auditoria|O local de onde veio o pedido. Os valores válidos são **o Portal de Self-Service** ou **o Helpdesk.**|
|Resultado do pedido|Estado do pedido. Os valores válidos são **bem sucedidos** ou **falhados.**|
|Utilizador de helpdesk|O utilizador administrativo que solicitou a chave. Se um administrador de helpdesk recuperar a chave sem especificar o nome do utilizador, o campo **Utilizador Final** fica em branco. Um utilizador de serviço de assistência padrão deve especificar o nome do utilizador, que aparece neste campo. Para recuperação através do portal de autosserviço, este campo e o campo **Utilizador Final** exibem o nome do utilizador que faz o pedido.|
|Utilizador final|Nome do utilizador que solicitou a recuperação da chave.|
|Computador|Nome do computador que foi recuperado.|
|Tipo de chave|Tipo de chave que o utilizador solicitou. Os três tipos de chaves são:<br/><br/>- **Palavra-passe chave de recuperação**: usado para recuperar um computador em modo de recuperação<br/>- **ID chave de recuperação**: usado para recuperar um computador em modo de recuperação para outro utilizador<br/>- **TPM password hash**: usado para recuperar um computador com um TPM bloqueado|
|Descrição da razão|Por que razão o utilizador solicitou o tipo de chave especificado, com base na opção que selecionou no formulário.|
