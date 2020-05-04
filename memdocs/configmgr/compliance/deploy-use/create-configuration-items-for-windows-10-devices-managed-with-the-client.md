---
title: Criar itens de configuração para o Windows 10
titleSuffix: Configuration Manager
description: Utilize o item de configuração do Windows 10 para gerir as definições para computadores Windows 10 que são geridos pelo cliente do Gestor de Configuração.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712401"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Criar itens de configuração para dispositivos Windows 10

Utilize o item de configuração do Gestor de Configuração **do Windows 10** para gerir as definições para computadores Windows 10 que são geridos pelo cliente do Gestor de Configuração.  
  
> [!IMPORTANT]  
>  Nesta versão, se tiver criado uma definição de **Palavra-passe** como parte de um item de configuração do tipo **Windows 10** (para um dispositivo gerido com o cliente Do Gestor de Configuração), esteja ciente do seguinte problema. Se a definição ainda não existir, ou não tiver sido configurada no dispositivo Windows 10, irá avaliar incorretamente como conforme.  
>   
>  Como solução, quando cria uma definição para estes dispositivos, certifique-se de que a opção **Remediar definições incompatíveis** está selecionada nas páginas de definições do assistente estiver selecionada nas páginas de definições do Assistente de Criação de Item de Configuração. Além disso, quando implementar uma linha de base de configuração contendo um item de configuração do Windows 10 contendo definições de palavra-passe, **selecione Remediar regras não conformes quando for suportado**. Faça esta seleção na caixa de diálogo de configuração de configuração de configuração. Ao utilizar esta suposição, a definição é monitorizada e remediada se se constatar que não é compatível. Após a reparação, a definição é corretamente comunicada como **Conforme** (a menos que se encontre um problema, caso em que irá reportar **erro**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Para criar um item de configuração do Windows 10  
  
1. Na consola 'Gestor de Configuração', selecione **Ativos e Conformidade.**  
  
2. No espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e, em seguida, selecione Itens de **Configuração**.  
  
3. No separador **Home,** no grupo **Criar,** selecione **Create Configuration Item**.  
  
4. Na página **geral** do assistente de **configuração criar,** especifique um nome e descrição opcional para o item de configuração.  
  
5. Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Windows 10**.  
  
6. Se criar e atribuir categorias para ajudá-lo a pesquisar e filtrar itens de configuração na consola do Gestor de Configuração, selecione **Categorias**.  
  
7. Na página **Plataformas Suportadas** do assistente, selecione as plataformas específicas do Windows 10 que irão avaliar o item de configuração.  
  
8. Na página **Definições do Dispositivo** do assistente, selecione o grupo de definições que pretende configurar. (Para mais detalhes, consulte a referência de definições de [configuração do Windows 10](#BKMK_Ref) neste artigo.) Em seguida, selecione **Seguinte**.  
  
   > [!TIP]  
   >  Se a definição que deseja não estiver listada, selecione as **definições adicionais do Configure que não estão na caixa de verificação de grupos predefinidos**.  
  
9. Em cada página de definições, configure as definições necessárias e se pretende remediar quando não estão em conformidade com os dispositivos (quando esta for suportada).  
  
10. Para cada grupo de definições, também pode configurar a gravidade relatada quando um item de configuração é considerado incompatível:  
  
    -   **Nenhum**: Os dispositivos que insebem esta regra de conformidade não reportam uma falha nos relatórios do Gestor de Configuração.  
  
    -   **Informações**: Os dispositivos que falham nesta regra de conformidade reportam uma falha de **informação** para relatórios do Gestor de Configuração.  
  
    -   **Aviso**: Os dispositivos que insebem esta regra de conformidade reportam uma falha de **aviso** para relatórios do Gestor de Configuração.  
  
    -   **Crítico**: Os dispositivos que falham nesta regra de conformidade reportam uma falha dos relatórios **críticos** para o Gestor de Configuração.  
  
    -   **Crítico com evento**: Os dispositivos que falham nesta regra de conformidade reportam uma falha dos relatórios **críticos** para o Gestor de Configuração. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  
  
11. Na página de **Aplicabilidade** da Plataforma do assistente, reveja quaisquer definições que não sejam compatíveis com as plataformas suportadas que selecionou anteriormente. Pode voltar atrás e remover estas definições ou pode continuar.  
  
    > [!TIP]  
    >  As definições não suportadas não são avaliadas em termos de compatibilidade.  
  
12. Conclua o assistente.  
  
    Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Palavra-passe  
  
|Definição|Detalhes|  
|-------------|-------------|  
|**Exigir definições de palavra-passe em dispositivos**|Requer uma palavra-passe em dispositivos suportados.|  
|**Comprimento mínimo de palavra-passe (carateres)**|O comprimento mínimo, em carateres, da palavra-passe.|  
|**Expiração da palavra-passe em dias**|O número de dias antes de a palavra-passe ter de ser alterada.|  
|**Número de palavras-passe memorizadas**|Impede a reutilização de senhas anteriores.|  
|**Número de tentativas de início de sessão falhadas antes de um dispositivo ser apagado**|Limpa o dispositivo se o início de sessão falhar este número de vezes.|  
|**Tempo de inatividade antes de o dispositivo móvel ser bloqueado**|Especifica quantos minutos o dispositivo deve estar inativo antes de ser bloqueado automaticamente.|  
|**Complexidade da palavra-passe**|Escolha se pode especificar um PIN como '1234', ou se deve fornecer uma senha forte.|
|**Número de conjuntos de caracteres complexos necessários na palavra-passe**|Se selecionou uma palavra-passe **Forte,** utilize esta definição para configurar o número de conjuntos de caracteres complexos necessários. Para uma senha forte, esta definição deve ser definida para pelo menos **3**, o que significa que ambas as letras e números são necessários. Selecione **4** se quiser impor uma palavra-passe que exija adicionalmente caracteres especiais, tais como **(%$**.<br>(Apenas no Windows 10)  |
  
###  <a name="device"></a>Dispositivo  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Bluetooth**|Permite a utilização da funcionalidade Bluetooth no dispositivo.|  
  
### <a name="cloud"></a>Nuvem  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Sincronização de definições**|Permite a sincronização de definições entre dispositivos.|  
|**Sincronização de credenciais**|Permite a sincronização de credenciais entre dispositivos.|  
|**Sincronização de definições através de ligações com tráfego limitado**|Permite que as definições sejam sincronizadas quando a ligação à internet é medição.|  
  
### <a name="roaming"></a>Roaming  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Roaming de dados**|Permite o roaming entre redes ao aceder a dados.|  
  
### <a name="encryption"></a>Encriptação  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Encriptação de ficheiros no dispositivo**|Requer que os ficheiros no dispositivo estejam encriptados.|  
  
### <a name="system-security"></a>Segurança do sistema  
  
|Nome da definição|Detalhes|  
|------------------|-------------|  
|**Controlo de Conta de Utilizador**|Configura o modo de funcionamento do Controlo de Conta de Utilizador do Windows no dispositivo.<br />Por exemplo, pode desativá-lo ou definir o nível no qual o notifica.|  
|**Firewall da rede**|Ativa ou desativa a Firewall do Windows.|  
|**SmartScreen**|Ativa ou desativa o Windows SmartScreen.|  
|**Proteção contra vírus**|Requer que o software antivírus esteja instalado e configurado.|  
|**As assinaturas da proteção contra vírus estão atualizadas**|Requer que os ficheiros de assinatura do software antivírus no dispositivo devem estar atualizados.|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Com o aumento de dispositivos pertencentes aos colaboradores na empresa, há também um risco crescente de fugas de dados acidentais através de apps e serviços, como e-mail, redes sociais e nuvem pública. Estes estão fora do controlo da organização. Exemplos incluem quando um empregado:

- Envia as últimas imagens de engenharia da sua conta de e-mail pessoal.
- Cópias e colares informações do produto num tweet.
- Guarda um relatório de vendas em andamento para o seu armazenamento em nuvem pública.

A Proteção de Informação do Windows (WIP, anteriormente proteção de dados da empresa) ajuda a proteger contra esta potencial fuga de dados, sem interferir de outra forma com a experiência do colaborador. O WIP também ajuda a proteger aplicações e dados da empresa contra fugas de dados acidentais em dispositivos e dispositivos pessoais que os colaboradores trazem para o trabalho. O WIP não requer alterações no seu ambiente ou outras aplicações.

Configuração Manager Windows Information Protection itens gerem o seguinte:

- A lista de aplicações protegidas pela WIP
- Localizações da rede empresarial
- Nível de proteção
- Definições de encriptação
  
Para obter informações sobre como configurar wip com Gestor de Configuração, consulte:

- [Proteja os seus dados empresariais utilizando a Proteção de Informação do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Criar e implementar uma política de Proteção de Informação do Windows (WIP) utilizando o Gestor de Configuração](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Limitações ao utilizar a Proteção de Informação do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Consulte também  
[Itens de configuração para dispositivos geridos com o cliente do Gestor de Configuração](../../compliance/deploy-use/create-configuration-items.md)
