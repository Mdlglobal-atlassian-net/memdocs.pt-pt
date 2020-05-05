---
title: Capacidades na Pré-visualização Técnica 1702
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 73b8111cbada129997cec965ca685f1ef22b1f3a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721438"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1702 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1702. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar feedback da consola 'Gestor de Configuração'

Esta pré-visualização introduz novas opções de feedback na consola 'Gestor de Configuração'. As opções de Feedback permitem enviar feedback diretamente para a equipa de desenvolvimento, através do site de feedback do Gestor de Configuração UserVoice.  

> Pode encontrar a opção **Feedback:**
> -  Na fita, na esquerda do separador Home de cada nó.  
>    ![Fita](./media/feedback-home.png)

-  Quando clicar em qualquer objeto na consola.   
    ![Opção righ-click](./media/feedback-option.png)   

Escolher **o Feedback** abre o seu navegador para o https://configurationmanager.uservoice.com/forums/300492-ideassite de feedback do Gestor de Configuração UserVoice, em .
##  <a name="changes-for-updates-and-servicing"></a>Alterações para Atualizações e Manutenção
São introduzidos os seguintes com esta pré-visualização.

**Escolhas de atualização mais simples**  
Da próxima vez que a sua infraestrutura se qualificar para duas ou mais atualizações, apenas a última atualização é descarregada. Por exemplo, se a versão atual do site for duas ou mais mais antiga do que a versão mais recente que está disponível, apenas que a versão de atualização mais recente é descarregada automaticamente.  

Tem a opção de descarregar e instalar as outras atualizações disponíveis, mesmo quando não são a versão mais atual. No entanto, receberá um aviso de que a atualização foi substituída por uma mais recente. Para descarregar uma atualização *disponível para descarregar,* selecione a atualização na consola e clique em **Baixar**.

**Melhor limpeza de atualizações mais antigas**   
Adicionámos uma função de limpeza automática que elimina os downloads desnecessários da pasta 'EasySetupPayload' no servidor do seu site.  


## <a name="peer-cache-improvements"></a>Melhorias do Peer Cache
A partir desta versão, um computador de origem de cache peer rejeitará um pedido de conteúdo quando o computador de origem de cache peer satisfaz qualquer uma das seguintes condições:  
-  Está em modo de bateria baixa.
-  A carga de CPU ultrapassa os 80% no momento em que o conteúdo é solicitado.
-  O disco I/O tem um *AvgDiskQueueLength* que ultrapassa 10.
-  Não há mais ligações disponíveis ao computador.   

Pode configurar estas definições utilizando a classe config do agente cliente para a funcionalidade de origem de pares *(SMS_WinPEPeerCacheConfig*) quando utilizar o SDK do Gestor de Configuração.

Quando o computador rejeitar um pedido de conteúdo, o computador solicitado continuará a procurar fontes alternativas de conteúdo no seu conjunto de locais disponíveis de origem de conteúdo.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a>Utilize os Serviços de Domínio de Diretório Ativo Azure para gerir dispositivos, utilizadores e grupos

Com esta versão de pré-visualização técnica pode gerir dispositivos que se juntam a um domínio gerido pelo Azure Ative Directory (AD). Também pode descobrir dispositivos, utilizadores e grupos nesse domínio com vários métodos de Configuração Manager Discovery.

A infraestrutura técnica do site de pré-visualização, os clientes e o domínio dos Serviços de Domínio Azure AD devem ser executados em Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurar o Gestor de Configuração para utilizar o Azure AD
Para utilizar o Azure AD com o Gestor de Configuração, vai precisar do seguinte:
- Subscrição do Azure.
- Azure AD com Serviços de Domínio (DS).
- Um site de Gestor de Configuração que funciona num VM Azure que se junta ao seu Azure AD.
- Clientes do Gestor de Configuração que funcionam no mesmo ambiente da AD Azure.

Para configurar o Serviço de Domínio Azure AD, consulte Iniciar com serviços de [domínio Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Detetar recursos
Depois de configurar o Gestor de Configuração para executar em Azure AD, pode utilizar os seguintes métodos de descoberta de Diretório Ativo para pesquisar a AD Azure por recursos:  
- Deteção de Sistemas do Active Directory
- Deteção de Utilizadores do Active Directory
- Deteção de Grupos do Active Directory  

Para cada método que utilizar, edite a consulta LDAP para pesquisar as estruturas Azure AD OU em vez dos recipientes que são típicos do Diretório Ativo no local. Isto requer que direcione a consulta para pesquisar o seu Diretório Ativo na sua subscrição Azure.  

Os seguintes exemplos utilizam um Anúncio Azure de *contoso.onmicrosoft.com:*
- **Descoberta do Sistema**   
  A Azure AD armazena dispositivos sob o **AADDC Computers** OU.  Configure o seguinte:  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **Descoberta do Utilizador** A AAD armazena utilizadores sob o **AADDC Users** OU.  Configure o seguinte:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Descoberta de Grupo**  
A Azure AD não tem um Ou que armazena grupos. Em vez disso, utilize a mesma estrutura geral que o Sistema ou as consultas do Utilizador e configure a consulta LDAP para apontar para o OU que contém os grupos que pretende descobrir.

Consulte o seguinte para mais informações sobre a AD Azure:  
- Serviços de Domínio de [Diretório Ativo Azure](https://azure.microsoft.com/services/active-directory-ds) na azure.microsoft.com.
- [Documentação](https://docs.microsoft.com/azure/active-directory-domain-services) de Serviços de Domínio de Diretório Ativo sobre docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Melhorias da política de conformidade do dispositivo de acesso condicional

Uma nova regra de política de conformidade de dispositivos está disponível para ajudá-lo a bloquear o acesso a recursos corporativos que suportam o acesso condicional, quando os utilizadores estão a usar apps que fazem parte de uma lista não conforme de aplicações. A lista não conforme de aplicações pode ser definida pelo administrador ao adicionar a nova regra de conformidade **Apps que não podem ser instaladas**. Esta regra requer que o administrador introduza o Nome da **Aplicação,** o ID da **Aplicação**e o Editor de **Aplicações** (opcional) ao adicionar uma aplicação à lista não conforme. Esta definição aplica-se apenas aos dispositivos iOS e Android.

Além disso, isto ajuda as organizações a mitigar a fuga de dados através de aplicações não seguras e a prevenir o consumo excessivo de dados através de certas apps.

### <a name="try-it-out"></a>Experimente

**Cenário:** Identifique aplicações que possam estar a causar fugas de dados através do envio de dados corporativos para fora da sua empresa, ou que estejam a causar consumo excessivo de dados, e depois crie uma política de [conformidade de dispositivos](../../mdm/understand/what-happened-to-hybrid.md) de acesso condicional que adicione estas aplicações na lista de aplicações não conformes. Isto bloqueará o acesso a recursos corporativos que suportam o acesso condicional até que o utilizador possa remover a aplicação bloqueada.

## <a name="antimalware-client-version-alert"></a>Alerta de versão de cliente antimalware
A partir desta versão de pré-visualização, a Configuração Manager Endpoint Protection fornece um alerta se mais de 20% (padrão) de clientes geridos estiverem a utilizar uma versão expirada do cliente antimalware (ou seja, Windows Defender ou cliente endpoint Protection).

### <a name="try-it-out"></a>Experimente
Certifique-se de que a Proteção endpoint está ativada em todos os clientes de desktop e servidor usando a política de definições do cliente. Agora pode ver a **versão antimalware do cliente** e o estado de implementação da proteção do ponto **final,** indo **para ativos e** > **dispositivos** > de**visão geral** > de conformidade**todos os desktops e clientes de serviço.** Para verificar se há um alerta, consulte **alertas** no espaço de trabalho **de Monitorização.** Se mais de 20% dos clientes geridos estiverem a executar uma versão expirada do software antimalware, a versão cliente Antimalware é desatualizada. Este alerta não aparece no separador **'Visão Geral** **de Monitorização'.** >  Para atualizar clientes antimalware expirados, ative atualizações de software para clientes antimalware.

Para configurar a percentagem em que o alerta é gerado, expandir**alertas** > de **monitorização** > **Todos os alertas,** clicar em dois **cliques em clientes Antimalware desatualizados** e modificar o **alerta De aumento se a percentagem de clientes geridos com uma versão desatualizada do cliente antimalware for mais do que** opção.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Avaliação de conformidade para atualização do Windows para atualizações de negócios
Agora pode configurar uma regra de atualização da política de conformidade para incluir um resultado de avaliação do Windows Update for Business como parte da avaliação de acesso condicional.
> [!IMPORTANT]
> Tem de ter o Windows 10 Insider Preview Build 15019 ou mais tarde para utilizar a avaliação de conformidade para a Atualização do Windows para atualizações de Negócios.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir que o Windows Update para o Negócios gere as atualizações do Windows 10
Para recolher informações sobre a avaliação de conformidade para o Windows Update para atualizações de Negócios, utilize o seguinte procedimento para configurar a definição do agente cliente para permitir explicitamente o Windows Update for Business para gerir as atualizações do Windows 10.
1. Na consola de Gestor de Configuração, vá às**Definições**do Cliente **de Administração.** > 
2. Nas propriedades para as definições do cliente, vá a **Atualizações**de Software , e selecione **Sim** para as **atualizações Manage Windows 10 com** a definição de Windows Update para Business.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Criar uma política de conformidade para a atualização do Windows para avaliação de negócios
1. Na consola do Gestor de Configuração, vá às políticas de**Compliance Settings** > **conformidade**de Conformidade de **Ativos e Compliance.** > 
2. Clique em **Criar Política** de Conformidade ou selecione uma política de conformidade existente para modificar.
3. Na página Geral, forneça um nome e descrição, selecione regras de **conformidade para dispositivos geridos com o cliente do Gestor de Configuração,** delineie a gravidade do incumprimento para reportar e clique em **Next**.
4. Na página Plataformas Suportadas, selecione **o Windows 10**e, em seguida, clique em **Seguinte**.
5. Na página Regras, clique em **New....**, e depois para **Condição** escolha **Exigir Atualização do Windows para a conformidade com o Negócio**. A definição **de Valor** é automaticamente definida para **True**.

A nova política é apresentada no nó **Políticas de Conformidade** da área de trabalho **Ativos e Conformidade**.

### <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade
1. Na consola do Gestor de Configuração, vá às**Definições**de Conformidade de **Ativos e Conformidade,** > e clique em Políticas de **Conformidade**.
2. No separador **Home Page**, no grupo **Implementação**, clique em **Implementar**.
3. Na caixa de diálogo **Implementar Política de Conformidade**, clique em **Procurar** para selecionar a coleção de utilizadores na qual a política será implementada.
   Além disso, pode selecionar opções de geração de alertas quando a política não está em conformidade, bem como configurar a agenda com base na qual a política será avaliada em termos de conformidade.
4. Quando tiver terminado, clique em **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade
Depois de criar a política de conformidade, pode monitorizar os resultados de conformidade na consola Do Gestor de Configuração. Para mais detalhes, consulte [Monitorize a política](../../mdm/understand/what-happened-to-hybrid.md)de conformidade .


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Melhorias nas definições do Software Center e mensagens de notificação para sequências de tarefas de alto impacto
Esta versão inclui as seguintes melhorias nas definições do Software Center e mensagens de notificação para sequências de tarefas de implementação de alto impacto:

- Nas propriedades da sequência de tarefas, pode agora configurar qualquer sequência de tarefas, incluindo sequências de tarefas do sistema não operacional, como uma implementação de alto risco. Qualquer sequência de tarefa que satisfaça determinadas condições é automaticamente definida como de alto impacto. Para mais detalhes, consulte [Gerir implementações de alto risco](../servers/manage/settings-to-manage-high-risk-deployments.md).
- Nas propriedades da sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinida ou criar a sua própria mensagem de notificação personalizada para implementações de alto impacto.
- Nas propriedades da sequência de tarefas, pode configurar as propriedades do Software Center, que incluem fazer um reinício necessário, o tamanho de descarregamento da sequência de tarefas e o tempo estimado de execução.
- A mensagem de implementação padrão de alto impacto para atualizações no local indica agora que as suas aplicações, dados e configurações são automaticamente migradas. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicava que todas as aplicações, dados e configurações seriam perdidos, o que não era verdade para uma atualização no local.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefade alto impacto
Utilize o procedimento seguinte para definir uma sequência de tarefas como de alto impacto.
> [!NOTE]
> Qualquer sequência de tarefa que satisfaça determinadas condições é automaticamente definida como de alto impacto. Para mais detalhes, consulte [Gerir implementações de alto risco](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. Na consola do Gestor de Configuração, vá a sequências de tarefas de > **sistemas** > **operativos**da Biblioteca de **Software.**
2. Selecione a sequência de tarefas para editar e clique em **Propriedades**.
3. No separador Notificação do **Utilizador,** selecione **Esta é uma sequência de tarefas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implementações de alto risco
1. Na consola do Gestor de Configuração, vá a sequências de tarefas de > **sistemas** > **operativos**da Biblioteca de **Software.**
2. Selecione a sequência de tarefas para editar e clique em **Propriedades**.
3. No separador Notificação do **Utilizador,** selecione **Use texto personalizado**.
   > [!NOTE]
   >  Só é possível definir texto de notificação do utilizador quando se leciona **uma sequência de tarefas de alto impacto.**

4. Configure as seguintes definições (máx.

   **Texto de manchete**de notificação do utilizador : Especifica o texto azul que apresenta na notificação do utilizador do Centro de Software. Por exemplo, na notificação padrão do utilizador, esta secção contém algo como "Confirme que pretende atualizar o sistema operativo neste computador".

   Texto de mensagem de **notificação**do utilizador : Existem três caixas de texto que fornecem o corpo da notificação personalizada.
   - 1ª caixa de texto: Especifica o corpo principal do texto, que normalmente contém instruções para o utilizador. Por exemplo, na notificação padrão do utilizador, esta secção contém algo como "Atualizar o sistema operativo levará tempo e o seu computador poderá reiniciar várias vezes."
   - 2ª caixa de texto: Especifica o texto arrojado sob o corpo principal do texto. Por exemplo, na notificação padrão do utilizador, esta secção contém algo como "Esta atualização no local instala o novo sistema operativo e migra automaticamente as suas aplicações, dados e configurações."
   - 3ª caixa de texto: Especifica a última linha de texto sob o texto arrojado. Por exemplo, na notificação padrão do utilizador, esta secção contém algo como "Clique em Instalar para começar. Caso contrário, clique em Cancelar."   

   Digamos que configura a seguinte notificação personalizada em propriedades.

   ![Notificação personalizada para uma sequência de tarefas](./media/user-notification.png)

   A seguinte mensagem de notificação será exibida quando o utilizador final abrir a instalação a partir do Software Center.

   ![Notificação personalizada para uma sequência de tarefas](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configure propriedades do Centro de Software
Utilize o seguinte procedimento para configurar os detalhes para a sequência de tarefas apresentada no Centro de Software. Estes detalhes são apenas para informação.  
1. Na consola do Gestor de Configuração, vá a sequências de tarefas de > **sistemas** > **operativos**da Biblioteca de **Software.**
2. Selecione a sequência de tarefas para editar e clique em **Propriedades**.
3. No separador **Geral,** estão disponíveis as seguintes definições para O Centro de Software:
   - **Reinício requerido**: Informe o utilizador se é necessário reiniciar durante a instalação.
   - **Tamanho do download (MB)**: Especifica quantos megabytes são apresentados no Centro de Software para a sequência de tarefas.  
   - **Tempo estimado de execução (minutos)**: Especifica o tempo estimado de execução em minutos que é apresentado no Centro de Software para a sequência de tarefas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique se executa ficheiros executáveis antes de instalar uma aplicação

No * \<nome* do tipo de implementação>caixa de diálogo **Propriedades** de um tipo de implementação, no separador 'Comportamento de Instalação', pode agora especificar um dos ficheiros mais executáveis que, se estiver em execução, bloqueará a instalação do tipo de implementação. O utilizador deve fechar o ficheiro executável em execução (ou pode ser fechado automaticamente para implementações com o objetivo necessário) antes de o tipo de implementação poder ser instalado.

### <a name="try-it-out"></a>Experimente!

1. Nas propriedades de um tipo de implementação do Gestor de Configuração, escolha o separador **'Comportamento de Instalação'.**
2. Escolha **Adicionar** um ou mais nomes de ficheiros executáveis que deseja verificar. Também pode adicionar um nome de exibição para facilitar a identificação de aplicações por parte dos utilizadores na lista.
3. Se a implementação tiver um propósito necessário, no assistente de software de implementação, pode optar opcionalmente por **fechar automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa**de diálogo de propriedades do tipo de implementação .

Se a aplicação foi implementada como **Disponível**, e um utilizador final tentar instalar uma aplicação, serão solicitados a encerrar quaisquer executíveis de execução especificados antes de poderem prosseguir com a instalação.

Se a aplicação foi implementada conforme **necessário,** e a opção **fechar automaticamente quaisquer executáveis de execução especificadas no separador de comportamento de instalação da caixa** de diálogo de propriedades de implementação é selecionada, eles verão uma caixa de diálogo que os informa que executáveis que especificou serão automaticamente fechados quando o prazo de instalação da aplicação for atingido. Pode agendar estes diálogos no**Agente informático** **de Definições** > do Cliente . Se não quiser que o utilizador final veja estas mensagens, selecione **Hide in Software Center e todas as notificações** no separador User **Experience** das propriedades da implementação.

Se a aplicação foi implementada conforme **necessário** e a opção **fechar automaticamente quaisquer executáveis de execução especificadas no separador** de comportamento de instalação da caixa de diálogo de propriedades de implementação não é selecionada, então a instalação da app falhará se uma ou mais das aplicações especificadas estiverem em execução.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Criar certificados PFX com suporte S MIME

Agora pode criar um perfil de certificado PFX que suporta S/MIME e implementá-lo para os utilizadores.  Este certificado pode então ser utilizado para encriptação e desencriptação S/MIME em todos os dispositivos que o utilizador inscreveu.

Além disso, pode agora especificar várias autoridades de certificação (A) sobre várias funções do sistema do site do Ponto de Registo de Certificados e, em seguida, atribuir quais os pedidos de processo dos CAs como parte do perfil do certificado.

Para dispositivos iOS, pode associar um perfil de certificado PFX a um perfil de e-mail e ativar a encriptação S/MIME.  Isto permite então s/MIME no cliente de e-mail nativo no iOS e associa-lhe o certificado de encriptação S/MIME correto.

Para obter mais informações sobre certificados no Gestor de Configuração, consulte Introdução aos perfis de [certificados]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Novas definições de conformidade para dispositivos iOS

Adicionámos novas definições que pode utilizar nos seus itens de configuração para dispositivos iOS. Estas são configurações que existiam anteriormente no Microsoft Intune numa configuração autónoma, e estão agora disponíveis quando utiliza o Intune com o 'Configuração Manager'. Se precisar de ajuda em qualquer destas definições, consulte as definições de [política do iOS no Microsoft Intune](/mem/intune/configuration/device-restrictions-ios).

- **Sincronizar dados de aplicações geridas para iCloud**
- **Entrega para continuar atividades em outros dispositivos**
- **partilha de fotos iCloud**
- **Biblioteca de fotos iCloud**
- **Confie em novos autores de aplicações empresariais**
- **Permitir que o utilizador descarregue conteúdos da loja iBook sinalizada como 'Erotica'** (apenas o modo supervisionado)
- **Forçar os Relógios Apple emparelhados a utilizar deteção no pulso**
- **Palavra-passe para pedidos de saída do AirPlay**
- **Modificar as definições de conta** (apenas o modo supervisionado)
- **Alterações nas definições de utilização de dados celulares** da aplicação (apenas no modo supervisionado)
- **Apagar todos os conteúdos e configurações** (apenas o modo supervisionado)
- **Configurar restrições no dispositivo** (apenas no modo supervisionado)
- **Utilize o emparelhamento do hospedeiro para controlar os dispositivos** com os que um dispositivo iOS pode emparelhar (apenas o modo supervisionado)
- **Instalar perfis e certificados** de configuração (apenas em modo supervisionado)
- **Modificação do nome** do dispositivo (apenas modo supervisionado)
- **Modificação de código** de acesso (apenas modo supervisionado)
- **Emparelhamento Apple Watch** (apenas em modo supervisionado)
- **Modificação das definições de notificação** (apenas no modo supervisionado)
- **Modificação de papel de parede** (apenas modo supervisionado)
- **Modificação das definições de submissão** de diagnóstico (apenas o modo supervisionado)
- **Modificação Bluetooth** (apenas no modo supervisionado)
- **AirDrop** (apenas modo supervisionado)
- **Utilize a Siri para consultar conteúdos gerados** pelo utilizador a partir da Internet (apenas o modo supervisionado)
- **Filtro de profanação Siri** (apenas em modo supervisionado)
- **Resultados de devolução da pesquisa na Internet em Destaque** (apenas no modo supervisionado)
- **Procura de definição** de palavras (apenas modo supervisionado)
- **Teclados preditivos** (apenas em modo supervisionado)
- **Correção automática** (apenas modo supervisionado)
- **Verificação ortográfica do teclado** (apenas modo supervisionado)
- **Atalhos de teclado** (apenas modo supervisionado)
  <!--- - **Enterprise app trust settings modification** --->
- **Instalação de aplicações usando apenas o Configurador Apple e o iTunes** (apenas o modo supervisionado)
- **Downloads automáticos de apps** (apenas em modo supervisionado)
- **Faça alterações nas definições da aplicação Find My Friends** (apenas no modo supervisionado)
- **Acesso à loja iBooks** (apenas em modo supervisionado)
- **Aplicação de mensagens** (apenas em modo supervisionado)
- **Podcasts** (apenas modo supervisionado)
- **Apple Music** (apenas em modo supervisionado)
- **Rádio iTunes** (apenas em modo supervisionado)
- **Apple News** (apenas em modo supervisionado)
- **Game Center** (apenas em modo supervisionado)
- **Trate o AirDrop como um destino não gerido**

## <a name="android-for-work-support"></a>Suporte do Android for Work

A partir da versão 1702 de Pré-visualização Técnica, pode ligar uma conta da Google ao seu inquilino híbrido do MDM. Isto permite-lhe fazer o seguinte:

- Inscreva [dispositivos Android suportados](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android para Trabalho, criando perfis de trabalho nesses dispositivos matriculados
- Aprove aplicações na loja Play for Work, sincronize-as com a consola Do Gestor de Configuração e, em seguida, implemente-as para os perfis de trabalho dos dispositivos
- Criar e implementar itens de configuração para configurar o perfil de trabalho e as definições de palavra-passe para esses dispositivos
- Crie e implemente itens de política de conformidade e perfis de acesso a recursos para dispositivos Android for Work, como já faz para dispositivos Android
- Execute a limpeza seletiva em dispositivos Android for Work

Quando se matricula um dispositivo como Android for Work cria um perfil de trabalho no dispositivo que intune pode gerir. Este perfil de trabalho existe lado a lado com o perfil pessoal no dispositivo Android. Os utilizadores podem facilmente alternar entre aplicações de perfil de trabalho e aplicações de perfil pessoal. Não é possível gerir itens no perfil pessoal. As aplicações pessoais e os dados permanecem por gerir. O Gestor de Configuração tem controlo total sobre o perfil de trabalho e o seu conteúdo e pode removê-lo do dispositivo.

O Android for Work é uma plataforma separada do Android, e terá de decidir qual a forma de gestão a utilizar para dispositivos Android que suportem perfis de trabalho.

### <a name="try-it-out"></a>Experimente!
As seguintes secções descrevem o Android para a gestão do trabalho.

#### <a name="enable-android-for-work-management"></a>Ativar o Android para gestão de trabalho
1. Crie uma https://accounts.google.com/SignUp conta Google para usar como sua conta de administrador Android for Work que estará associada a todas as tarefas de gestão do Android para o Trabalho para este inquilino Intune. Esta pode ser uma conta da Google partilhada entre os administradores que gerem dispositivos Android. Esta é a conta Google que a sua organização utiliza para gerir e publicar aplicações na consola Play for Work. Utilizará esta conta para aprovar aplicações na loja Play for Work, por isso, mantenha o registo do nome da conta e da palavra-passe.
2. Ativar a inscrição do Android ligando a conta da Google ao inquilino Intune gerido no Gestor de Configuração:
   1. Vá ao **Administration** > **Overview** > **Cloud Services** > **Microsoft Intune Subscriptions** e selecione a sua subscrição Intune.
   2. Na fita, clique em **Configure Platforms** > **Android** e **certifique-se** de que a inscrição do Android é verificada.
   3. Na fita, clique em **Configure Platforms** > **Android for Work**.
   4. Na caixa de diálogo, clique em **Configurar Android para Trabalhar na consola Intune**. A consola Intune abre no seu navegador web.
   5. Utilize as suas credenciais de administrador Intune para iniciar sessão no portal Intune.
   6. Clique em **Configure** para abrir o site Android for Work do Google Play.
   7. Na página de entrada do Google, introduza as credenciais da conta do Google a partir do passo 1 e, em seguida, forneça informações à sua empresa.
3. Quando regressar ao portal Intune, o Android for Work está ativado e tem três opções de inscrição para dispositivos Android for Work:
   - **Gerir todos os dispositivos como Android** - (Desativação) Todos os dispositivos Android, incluindo dispositivos que suportam o Android para o Trabalho, serão matriculados como dispositivos Android convencionais
   - **Gerir dispositivos suportados como Android for Work** – (ativado) todos os dispositivos que suportam o Android for Work são inscritos como dispositivos Android for Work. Qualquer dispositivo Android que não suporte o Android for Work é inscrito como um dispositivo Android convencional.
   - **Gerir dispositivos suportados para utilizadores apenas nestes grupos como Android for Work** - (Testing) Permite-lhe direcionar o Android para a gestão do Trabalho para um conjunto limitado de utilizadores. Apenas os membros destes grupos selecionados que inscrevam um dispositivo que suporte o Android for Work são inscritos como dispositivos Android for Work. Todos os outros dispositivos são inscritos como dispositivos Android.
  
> [!NOTE]
> Um problema conhecido impede que os **dispositivos suportados manage para utilizadores apenas nestes grupos, uma** vez que a opção Android for Work funcione como esperado. Os dispositivos dos utilizadores nos referidos grupos De AD Azure vão inscrever-se como Android em vez do Android para o Trabalho. Para testar o Android para o Trabalho, tem de utilizar todos **os dispositivos suportados como Android for Work**.


  Para permitir a inscrição do Android para o Trabalho, tem de escolher uma das duas opções inferiores. Os **dispositivos suportados pela Manage para utilizadores apenas nestes grupos, uma** vez que a opção Android for Work requer que tenha os grupos de segurança Do Diretório Ativo Azure criados primeiro.

Você verá o nome da conta e nome da organização no portal Intune quando a ligação estiver completa; nessa altura, pode fechar ambos os navegadores.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar aplicativos Android para trabalho
Siga estes passos para aprovar aplicações na play for Work store, sincronizá-las na consola Do Gestor de Configuração e implementá-las para dispositivos Android for Work geridos. Para implementar aplicações para os perfis de trabalho dos utilizadores, terá de aprovar as aplicações em Play for Work e, em seguida, sincronizar as aplicações com a consola 'Gestor de Configuração'.

1. Abra um navegador e https://play.google.com/workvá para: .
2. Inscreva-se na conta de administração do Google que vincula ao seu inquilino Intune.
3. Procure por apps que gostaria de implementar no seu ambiente e clique em **Aprovar** cada uma delas.
4. Na consola de Configuração Manager, vá ao **Administrator** > **Overview** > **Cloud Services** > **Android for Work** e clique em **Sync**.
5. Aguarde até 10 minutos para que as aplicações sincroniem e, em seguida, vá para a Aplicação de Gestão de Aplicações de**Aplicações** > de Aplicações**Overview** > de**Aplicações**de Visão geral da **Biblioteca** > de Software .
6. Clique numa aplicação sincronizada a partir de Play for Work e, em seguida, clique em **Criar Aplicação**.
7. Complete o assistente e clique **em Fechar**.
8. Vá a**Aplicações**de**Gestão** > de Aplicações de Visão**Geral** > da Biblioteca > de **Software,** selecione um Android para aplicações de trabalho e implemente como de costume.

Para sincronizar aplicações Play for Work com O Gestor de Configuração, tem de aprovar pelo menos uma aplicação no site play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Inscreva um dispositivo Android para Trabalho
A forma como se matricula dispositivos Android for Work é semelhante à inscrição para Android. Descarregue e execute o aplicativo Portal da Empresa para Android no seu dispositivo móvel. Será solicitado a criar um perfil de trabalho como parte do processo de inscrição.  Uma vez criado o perfil de trabalho, tem de mudar para a versão gerida do Portal da Empresa. O Portal da Empresa gerido é marcado com uma pequena pasta laranja no canto inferior direito.

#### <a name="create-and-deploy-a-configuration-item"></a>Criar e implementar um item de configuração
Android for Work tem dois grupos de definição para itens de configuração:
- Palavra-passe
- Perfil de trabalho

Pode configurar a partilha de conteúdos entre perfis de trabalho, bem como os seguintes itens de configuração em dispositivos com android 6 ou superior:
- O comportamento das aplicações que pedem permissões específicas
- Se as notificações para aplicações dentro do perfil de trabalho são visíveis no ecrã de bloqueio

Para experimentar isto, crie um item de configuração através do fluxo de trabalho padrão, escolha **Android para Trabalhar** na página **Geral** e configure as definições para cada um dos grupos de definição, adicionando o item de configuração a uma linha de base e implementando como de costume. Estas definições aplicar-se-ão apenas a dispositivos matriculados como Android for Work, e não aos matriculados como Android.

#### <a name="perform-selective-wipe"></a>Realizar limpeza seletiva
Os dispositivos matriculados como Android for Work só podem ser limpos seletivamente porque você só gere o perfil de trabalho. Isto protege o perfil pessoal de ser limpo. A realização de uma limpeza seletiva num dispositivo Android for Work remove o perfil de trabalho, incluindo todas as aplicações e dados, e desinscriço o dispositivo.

Para limpar seletivamente um dispositivo Android for Work, utilize o processo normal de [limpeza seletiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) na consola Do Gestor de Configuração.

#### <a name="known-issues-for-android-for-work"></a>Questões conhecidas para Android para Trabalho
**Configurar a programação** de sincronização nos perfis de email do Android para o Trabalho faz com que não se implementem Uma das opções no UI ConfigMgr para perfis de email Android for Work é "Schedule". Noutras plataformas, isto permite ao administrador configurar um calendário para sincronizar e-mails e outros dados de conta de e-mail até aos dispositivos móveis para os seus dispositivos móveis para os dispositivos móveis a que está implantado. No entanto, não funciona para perfis de email Android for Work, e escolher qualquer outra opção que não seja "Não Configurado" fará com que o perfil não seja implementado para nenhum dispositivo.
