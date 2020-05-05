---
title: Capacidades na Pré-visualização Técnica 1701
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: f100d28b3fd4ce0d310ddb2f0b4e777c72f72881
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076208"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1701 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*



Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1701. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Melhorias dos grupos de fronteira para pontos de atualização de software
A partir desta pré-visualização, utiliza agora grupos de fronteira para associar clientes a pontos de atualização de software. Isto faz parte do trabalho contínuo para expandir as mudanças para os grupos de fronteira saem para gerir funções adicionais do sistema do site.  As alterações para os grupos de fronteira suporam-se pela primeira vez na Pré-Visualização Técnica 1609 e na Atual Sucursal na versão 1610.  

Com esta pré-visualização, você usa o novo comportamento do grupo de limites para gerir quais os pontos de atualização de software que um cliente pode usar, semelhante à forma como gere o ponto de distribuição que um cliente pode usar:  

- Configura grupos de limites para associar um ou mais servidores que acolhem um ponto de atualização de software.
- Os clientes que procuram um novo ponto de atualização de software tentarão usar um que esteja associado ao seu atual grupo de fronteiras.
- Quando o cliente não consegue alcançar o seu atual ponto de atualização de software e não consegue encontrar um do seu atual grupo de limites, o cliente utiliza o comportamento do Fallback para expandir o conjunto disponível de pontos de atualização de software que pode usar.    

Para obter mais informações sobre os grupos de fronteira, consulte [os grupos de fronteira](../servers/deploy/configure/boundary-groups.md) no conteúdo do Ramo Atual.

No entanto, com esta pré-visualização, os grupos de fronteira para pontos de atualização de software são apenas parcialmente implementados. Pode adicionar pontos de atualização de software e configurar grupos de fronteira sinuosos que contêm pontos de atualização de software, mas o tempo de recuo para pontos de atualização de software ainda não é suportado, e os clientes vão esperar duas horas antes de iniciar o recuo.

O seguinte descreve o comportamento dos pontos de atualização de software com esta pré-visualização técnica:  

- **Novos clientes usam grupos de limites para selecionar pontos** de atualização de software, Um cliente que instala depois de instalar a versão 1701 seleciona um ponto de atualização de software daqueles associados ao grupo de fronteira do cliente.

  Isto substitui o comportamento anterior, onde os clientes selecionam um ponto de atualização de software aleatoriamente a partir de uma lista daqueles que partilham a floresta de clientes.   

- **Os clientes anteriormente instalados continuam a utilizar o seu ponto de atualização de software atual até que recuem para encontrar um novo.**
  Os clientes que foram previamente instalados e que já tenham um ponto de atualização de software continuarão a utilizar esse ponto de atualização de software até que caiam. Isto inclui pontos de atualização de software que não estão associados ao atual grupo de fronteiras do cliente. Não tentam imediatamente encontrar e utilizar um ponto de atualização de software do seu atual grupo de fronteiras.

  Um cliente que já tem um ponto de atualização de software começa a usar este novo comportamento de grupo de limites apenas depois de o cliente não conseguir alcançar o seu atual ponto de atualização de software e iniciar o recuo.
  Este atraso na mudança para o novo comportamento é intencional. Isto porque uma mudança no ponto de atualização de software pode resultar num grande uso da largura de banda da rede à medida que o cliente sincroniza os dados com o novo ponto de atualização de software. O atraso na transição pode ajudar a evitar saturar a sua rede caso todos os seus clientes mudem para novos pontos de atualização de software ao mesmo tempo.

- **Configurações para o tempo de recuo:** As configurações para quando os clientes começam a recuar para procurar um novo ponto de atualização de software não são suportadas nesta pré-visualização técnica. Isto inclui configurações para **tempos de recuo (em minutos)** e **Never fallback**, que você pode configurar para diferentes relações de grupo de limites.

  Em vez disso, os clientes mantêm o seu comportamento atual onde um cliente tenta ligar-se ao seu ponto de atualização de software atual durante duas horas antes de iniciar o recuo, para encontrar um novo ponto de atualização de software que possa usar.

  Quando um cliente usa o backback, usará as configurações do grupo de limites para o recuo para criar um conjunto de pontos de atualização de software disponíveis. Este pool inclui todos os pontos de atualização de software do grupo de *fronteira*atual dos clientes, *grupos de fronteira vizinhos,* e o grupo de *fronteira padrão do site*dos clientes.

- **Configure o grupo de fronteira do site predefinido:**  
  Considere adicionar um ponto de atualização de software ao código de site do *Grupo&lt;padrão-site-boundary-group>*. Isto garante que os clientes que não são membros de outro grupo de fronteirapodem recuar para encontrar um ponto de atualização de software.


Para gerir pontos de atualização de software para grupos de fronteira, utilize os [procedimentos a partir da documentação do Ramo Atual](../servers/deploy/configure/boundary-group-procedures.md), mas lembre-se que os tempos de recuo que pode configurar ainda não são utilizados para pontos de atualização de software.


## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações da UEFI
Uma nova classe de inventário de hardware (**SMS_Firmware**) e propriedade **(UEFI**) estão disponíveis para ajudá-lo a determinar se um computador começa no modo UEFI. Quando um computador é iniciado no modo UEFI, a propriedade **UEFI** está definida para **TRUE**. Isto é ativado no inventário de hardware por padrão. Para obter mais informações sobre o inventário de hardware, consulte [Como configurar o inventário](../clients/manage/inventory/configure-hardware-inventory.md)de hardware .

## <a name="improvements-to-operating-system-deployment"></a>Melhorias na implementação do sistema operativo
Fizemos as seguintes melhorias na implementação do sistema operativo, muitas das quais foram o resultado do feedback de voz do utilizador.
- [**Suporte para mais aplicações para a etapa**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t)de sequência de tarefas de instalação de aplicações : Aumentámos o número máximo de aplicações que pode instalar para 99 na etapa de sequência de tarefas de Instalação de **Aplicações.** O número máximo anterior era de 9 candidaturas.
- [**Selecione várias aplicações na etapa**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step)de sequência de tarefas da App de instalação : Quando adicionar aplicações ao passo de sequência de tarefas da Aplicação instalada no editor de sequência de tarefas, pode agora selecionar várias aplicações a partir da **aplicação Select a aplicação para instalar** o painel.
- [**Expire meios autónomos**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): Quando cria meios de comunicação autónomos, existem novas opções para definir datas opcionais de início e expiração nos meios de comunicação. Estas definições são desativadas por defeito. As datas são comparadas com o tempo de sistema no computador antes que os meios de comunicação autónomos sejam executados. Quando o tempo de sistema é mais cedo do que o tempo de início ou mais tarde do que o tempo de validade, os meios de comunicação autónomos não são iniciados. Estas opções também estão disponíveis utilizando o cmdlet New-CMStandaloneMedia PowerShell.
- [**Suporte para conteúdos adicionais em meios autónomos**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): Conteúdo adicional é agora suportado em meios autónomos. Pode selecionar pacotes adicionais, pacotes de controladores e aplicações a serem encenadas nos meios de comunicação, juntamente com os outros conteúdos referenciados na sequência de tarefas. Anteriormente, apenas o conteúdo referenciado na sequência de tarefas era encenado em meios autónomos.
- [**Tempo de tempo configurável para**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout)o passo de sequência de tarefas do condutor de aplicação automática : Novas variáveis de sequência de tarefas estão agora disponíveis para configurar o valor de tempo limite na fase de sequência de tarefas do condutor de aplicação automática ao fazer pedidos de catálogo HTTP. Estão disponíveis as seguintes variáveis e valores predefinidos (em segundos):
   - SMSTSDriverRequestResolveResolveTimeOut Default: 60
   - Padrão de tempo de ligação smstsdriverrequest: 60
   - Padrão de tempo de envio de SMSTSDriverRequest: 60
   - SMSTSDriverRequestReceber Predefinido: 480
- [**O ID do pacote é agora apresentado em passos**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste)de sequência de tarefas : Qualquer passo de sequência de tarefas que refira um pacote, pacote de controlador, imagem do sistema operativo, imagem de arranque ou pacote de atualização do sistema operativo irá agora exibir o ID do pacote do objeto referenciado. Quando uma sequência de tarefas faz referência a uma aplicação, apresentará o ID do objeto.
- **Windows 10 ADK rastreado pela versão build**: O Windows 10 ADK é agora rastreado por versão build para garantir uma experiência mais suportada ao personalizar as imagens de boot do Windows 10. Por exemplo, se o site utilizar o Windows ADK para o Windows 10, versão 1607, apenas as imagens de arranque com a versão 10.0.14393 podem ser personalizadas na consola. Para mais detalhes sobre personalizar as versões WinPE, consulte [Personalizar imagens de boot](../../osd/get-started/customize-boot-images.md).
- O caminho de origem de **imagem de arranque padrão já não pode ser alterado**: As imagens de boot predefinidas são geridas pelo 'Gestor de Configuração' e o caminho de origem de imagem de arranque predefinido já não pode ser alterado na consola do Gestor de Configuração ou utilizando o SDK do Gestor de Configuração. Pode continuar a configurar um caminho de origem personalizado para imagens de boot personalizadas.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Atualizações de software de hospedar em pontos de distribuição baseados na nuvem
A partir desta versão de pré-visualização, pode utilizar um ponto de distribuição baseado na nuvem para hospedar um pacote de atualização de software. No entanto, uma vez que pode configurar os clientes para descarregar atualizações de software diretamente a partir do Microsoft Update, considere os custos adicionais que a implementação de um pacote de atualização de software para um ponto de distribuição baseado na nuvem pode incorrer.

Para obter informações sobre a utilização de pontos de distribuição baseados na nuvem, consulte [Utilize um ponto de distribuição baseado na nuvem](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) no conteúdo para o Atual Ramo de Gestor de Configuração.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Validar dados de atestado de saúde do dispositivo através de pontos de gestão

A partir desta versão de pré-visualização, pode configurar pontos de gestão para validar dados de informação sobre atestados de saúde para serviço de atestado de saúde em nuvem ou no local. Um novo separador **Opções Avançadas** na caixa de diálogo **Management Point Component Properties** **permite-lhe adicionar,** **editar**ou **remover** o URL do serviço de atestado de saúde do dispositivo **no local**. Também pode especificar **Definições de DispositivoS Personalizados** para o agente cliente **utilizar no local o Serviço de Atestado**de Saúde .  Definição **Sim** para esta definição permitirá reportar ao ponto de gestão no local em vez do serviço baseado na nuvem.

### <a name="try-it-out"></a>Experimente

- **Ativar o atestado de saúde do dispositivo no local num ponto de gestão**<br>  Na consola do Gestor de Configuração, navegue até ao ponto de gestão e abra propriedades componentes de **pontode gestão** e, em seguida, clique no separador **Opções Avançadas.** Clique em **Adicionar** e especifique o URL no local (por exemplo, https://10.10.10.10) para **URLs**de atesta de atesta de dispositivos no local .
- **Ativar relatórios de atestado de gestão no local para o agente cliente**<br>Na consola 'Gestor de Configuração', escolha**as Definições** do Cliente **de Administração** > e clique duas vezes ou crie novas **Definições**de Dispositivo Personalizado . Selecione **Computer Agent** e set **Use on-premises Health Attestation Service** to **Yes**. Se a comunicação enable com o Serviço de **Atestados** de Saúde do Dispositivo estiver definida para **Sim** e **use no local A Atestar** a Saúde está definida para **Não,** o ponto de gestão utilizará o serviço de atestado de saúde do dispositivo baseado na nuvem.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Utilize o conector OMS para a nuvem do Governo Microsoft Azure
Com esta pré-visualização técnica, pode agora utilizar o conector Microsoft Operations Management Suite (OMS) para se ligar a um espaço de trabalho OMS que está na nuvem do Governo do Microsoft Azure.  

Para tal, modifica um ficheiro de configuração para apontar para a nuvem do Governo e, em seguida, instala o conector OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Criar um conector OMS para a nuvem do Governo Microsoft Azure
1. Em qualquer computador que tenha a consola Do Gestor de Configuração instalada, edite o seguinte ficheiro de configuração para apontar para a nuvem governamental: *** &lt;CM instale caminho>\AdminConsole\bin\Microsoft.configuramanagmenet.exe.config***

   **Edites:**

   Alterar o valor para o nome de definição *FairFaxArmResourceID* para ser igual a "<https://management.usgovcloudapi.net/">

   - **Original:** &lt;definição de nome="FairFaxArmResourceId" serializeAs="String">   
     &lt;valor &lt;>/> de valor   
     &lt;/definição>

   - **Editado:**     
     &lt;definindo o nome="FairFaxArmResourceId" serializeAs="String"> &lt;valor><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/definição>

   Alterar o valor para o nome de definição<https://login.microsoftonline.com/> *FairFaxAuthorityResource* para ser igual a " "

   - **Original:** &lt;definição de nome="FairFaxAuthorityResource" serializeAs="String">   
     &lt;valor &lt;>/> de valor

   - **Editado:** &lt;definição de nome="FairFaxAuthorityResource" serializeAs="String">   
     &lt;valor><https://login.microsoftonline.com/&lt;/value>>

2. Depois de guardar o ficheiro com as duas alterações, reinicie a consola 'Gestor de Configuração' no mesmo computador e, em seguida, utilize essa consola para instalar o conector OMS. Para instalar o conector, utilize as informações em [Dados Sync do Gestor de Configuração para a Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)de Gestão de Operações da Microsoft e selecione o espaço de trabalho da Suite de Gestão de **Operações** que está na nuvem do Governo do Microsoft Azure.

3. Após a instalação do conector OMS, a ligação à nuvem do Governo está disponível quando utilizar qualquer consola que se conecte ao site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>As versões Android e iOS já não são direcionadas para os assistentes de criação de MDM híbrido

A partir desta pré-visualização técnica para a gestão de dispositivos móveis híbridos (MDM), já não é necessário direcionar versões específicas do Android e iOS ao criar novas políticas e perfis para dispositivos geridos por Intune. Em vez disso, escolhe um dos seguintes tipos de dispositivos:

- Android
- Samsung KNOX Standard 4.0 e superior
- iPhone
- iPad

Esta alteração afeta os assistentes para a criação dos seguintes itens:

- Itens de configuração
- Políticas de conformidade
- Perfis de certificado
- Perfis de e-mail
- Perfis VPN
- Perfis Wi-Fi

Com esta mudança, as implementações híbridas podem fornecer suporte mais rapidamente para novas versões Android e iOS sem precisar de um novo lançamento ou extensão do Gestor de Configuração. Uma vez que uma nova versão é suportada em Intune autónoma, os utilizadores poderão atualizar os seus dispositivos móveis para essa versão.

Para evitar problemas ao atualizar a partir de versões anteriores do 'Gestor de Configuração', as versões do sistema operativo móvel ainda estão disponíveis nas páginas de propriedades para estes itens. Se ainda precisar de direcionar uma versão específica, pode criar o novo item e, em seguida, especificar a versão direcionada na página de propriedades do item recém-criado.
