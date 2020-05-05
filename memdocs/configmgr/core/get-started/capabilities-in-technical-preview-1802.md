---
title: Antevisão Técnica 1802 / Microsoft Docs
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na versão de pré-visualização técnica 1802 para O Gestor de Configuração.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 50e05d07ec3e2612c170157c45f5e64abe3766de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718610"
---
# <a name="capabilities-in-technical-preview-1802-for-configuration-manager"></a>Capacidades em Pré-visualização Técnica 1802 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*

Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1802. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração. 

Reveja a [pré-visualização técnica para o Gestor](technical-preview.md) de Configuração antes de instalar esta versão da pré-visualização técnica. Este artigo familiariza-o com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Questões Conhecidas nesta Pré-Visualização Técnica
- **A atualização para uma nova versão de pré-visualização falha quando tiver um servidor de site em modo passivo**. Se tiver um [servidor de site primário em modo passivo,](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)então tem de desinstalar o servidor do site do modo passivo antes de atualizar para esta nova versão de pré-visualização. Pode reinstalar o servidor do site do modo passivo depois de o site completar a atualização.

  Para desinstalar o servidor do site do modo passivo:
  1. Na consola do Gestor de Configuração, vá a Servidores de**Configuração** > de Site de Visão**Geral** > da **Administração** > **e às Funções**do Sistema do Site, e, em seguida, selecione o servidor do site de modo passivo.
  2. No painel de **funções** do Sistema do Site, clique à direita na função do **servidor do Site** e, em seguida, escolha remover a **função**.
  3. Clique à direita no servidor do site do modo passivo e, em seguida, escolha **Eliminar**.
  4. Depois de o servidor do site desinstalar, no servidor do site primário ativo reiniciar o serviço **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de pontofinal de transição para Intune usando cogestão    
<!-- 1357365 -->
Nesta versão, pode agora transitar a carga de trabalho de Proteção de Ponto final do Gestor de Configuração para Intune depois de permitir a cogestão. Para fazer a transição da carga de trabalho de proteção de pontofinal, vá para a página de propriedades de cogestão e mova a barra de slider de Configuração Manager para **Pilot** ou **All**. Para mais detalhes, consulte [a Co-management para dispositivos Windows 10](../../comanage/overview.md).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configure a otimização da entrega do Windows para utilizar grupos de limites do Gestor de Configuração
<!-- 1324696 -->
Utiliza grupos de limites do Gestor de Configuração para definir e regular a distribuição de conteúdos através da sua rede corporativa e para escritórios remotos. A [Otimização](/windows/deployment/update/waas-delivery-optimization) de Entrega do Windows é uma tecnologia baseada em nuvem, peer-to-peer para partilhar conteúdos entre dispositivos Windows 10. A partir desta versão, configure a Otimização da Entrega para utilizar os seus grupos de fronteira ao partilhar conteúdo entre os pares. Uma nova definição de cliente aplica o identificador de grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os pares com o conteúdo pretendido. 

### <a name="prerequisites"></a>Pré-requisitos
- Otimização de Entregas só está disponível nos clientes do Windows 10

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Na consola de Configuração Manager, espaço de trabalho **de Administração,** nó de Definições de **Cliente,** crie uma política personalizada de definições de dispositivos de cliente.
2. Selecione o novo grupo de **Otimização de Entrega.**
3. Ativar a definição de grupos de limitedo do Gestor de **Configuração de Utilização para o ID do Grupo**de Otimização de Entrega .

Para mais informações, consulte a opção modo de entrega **do Grupo** nas opções de [Otimização de Entrega](/windows/deployment/update/waas-delivery-optimization#how-microsoft-uses-delivery-optimization).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de upgrade do Windows 10 no local através do gateway de gestão de nuvem
<!-- 1357149 -->

A sequência [de tarefas de upgrade do](../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 no local suporta agora a implementação de clientes baseados na Internet geridos através do portal de [gestão](../clients/manage/cmg/plan-cloud-management-gateway.md)de nuvem . Esta capacidade permite que os utilizadores remotos atualizem mais facilmente para o Windows 10 sem precisarem de se conectar à rede corporativa. 

Certifique-se de que todo o conteúdo referenciado pela sequência de tarefas de atualização no local é distribuído para um ponto de distribuição em [nuvem](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Caso contrário, os dispositivos não podem executar a sequência de tarefas.

Quando implementar uma sequência de tarefas de atualização, utilize as seguintes definições:
- Permitir que a sequência de **tarefas se decorra para o cliente na Internet,** no separador User Experience da implementação.
- **Descarregue todos os conteúdos localmente antes**de iniciar a sequência de tarefas, no separador Pontos de Distribuição da implementação. Outras opções, como **o descarregamento de conteúdos localmente quando necessário sem a sequência** de tarefas de execução, não funcionam neste cenário. O motor de sequência de tarefas é atualmente incapaz de obter conteúdo a partir de um ponto de distribuição em nuvem. O cliente do Gestor de Configuração deve descarregar o conteúdo a partir do ponto de distribuição da nuvem antes de iniciar a sequência de tarefas.
- *(Opcional)* **Pré-descarregue o conteúdo para esta sequência de tarefas,** no separador Geral da implementação. Para mais informações, consulte o [conteúdo pré-cache da Configure](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhorias na sequência de tarefas de upgrade do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas padrão para a atualização do Windows 10 inclui agora grupos adicionais com ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão a atualizar com sucesso dispositivos para o Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Novos grupos sob **preparação para upgrade**
- **Verificação da bateria**: Adicione passos neste grupo para verificar se o computador está a usar bateria ou energia com fios. Esta ação requer um script ou utilidade personalizado para realizar este cheque.
- **Verificações de ligação rede/com fios**: Adicione passos neste grupo para verificar se o computador está ligado a uma rede e não está a utilizar uma ligação sem fios. Esta ação requer um script ou utilidade personalizado para realizar este cheque.
- **Remova aplicações incompatíveis**: Adicione passos neste grupo para remover quaisquer aplicações incompatíveis com esta versão do Windows 10. O método para desinstalar uma aplicação varia. Se a aplicação utilizar o Instalador do Windows, copie a linha de comando do **programa Desinstalar** a partir do separador **De si** no separador de implementação do Instalador do Windows. Em seguida, adicione um passo de Linha de **Comando executar** neste grupo com a linha de comando do programa desinstalação. Por exemplo: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remova controladores incompatíveis**: Adicione passos neste grupo para remover quaisquer controladores incompatíveis com esta versão do Windows 10.
- **Remova/suspenda a segurança de terceiros**: Adicione passos neste grupo para remover ou suspender programas de segurança de terceiros, como antivírus.
   - Se estiver a utilizar um programa de encriptação de discos de terceiros, forneça o seu controlador de encriptação ao Windows Configuração com a [opção](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)de linha de comando **/ReflectDrivers** . Adicione um passo variável de sequência de [tarefas definido](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) na sequência de tarefas deste grupo. Detete a variável de sequência de tarefas para **OSDSetupAdicionalUpgradeOptions**. Desloque o valor para **/ReflectDriver** com o caminho para o condutor. Esta variável de ação de [sequência de tarefas](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS) apendia a linha de comando de configuração do Windows utilizada pela sequência de tarefas. Contacte o seu fornecedor de software para obter qualquer orientação adicional sobre este processo.

### <a name="new-groups-under-post-processing"></a>Novos grupos em **pós-processamento**
- **Aplique controladores baseados em configuração**: Adicione passos neste grupo para instalar controladores baseados em configuração (.exe) a partir de pacotes.
- **Instalar/ativar a segurança de terceiros**: Adicione passos neste grupo para instalar ou ativar programas de segurança de terceiros, como antivírus. 
- **Definir aplicações e associações padrão do Windows**: Adicione passos neste grupo para definir aplicações padrão do Windows e associações de ficheiros. Primeiro prepare um computador de referência com as associações de aplicações desejadas. Em seguida, executar a seguinte linha de comando para exportar: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Adicione o ficheiro XML a uma embalagem. Em seguida, adicione um passo de Linha de [Comando de Execução](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) neste grupo. Especifique a embalagem que contém o ficheiro XML e, em seguida, especifique a seguinte linha de comando: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Para mais informações, consulte as associações de pedidos por [defeito de exportação ou importação.](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)
- **Aplicar personalizações e personalização**: Adicione passos neste grupo para aplicar personalizações de menu Iniciar, tais como organizar grupos de programas. Para mais informações, consulte [Personalizar o ecrã Iniciar](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Recomendações adicionais
- Reveja a documentação do Windows para resolver erros de [atualização do Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Este artigo também inclui informações detalhadas sobre o processo de upgrade.
- No degrau de **predefinição Verificar Prontidão,** **certifique-se de espaço mínimo de disco livre (MB)**. Detete o valor para pelo menos **16384** (16 GB) para um pacote de upgrade de 32 bits, ou **20480** (20 GB) por 64 bits. 
- Utilize a variável de [sequência de tarefas incorporada](../../osd/understand/task-sequence-variables.md) **SMSTSDownloadRetryCount** para voltar a tentar a política de descarregamento. Atualmente por padrão, o cliente retenta duas vezes; esta variável é definida para dois (2). Se os seus clientes não estiverem numa ligação de rede corporativa com fios, tentativas adicionais ajudam o cliente a obter a política. A utilização desta variável não causa nenhum efeito colateral negativo, para além de uma falha retardada se não conseguir descarregar a política.<!-- 501016 --> Aumente também a variável **SMSTSDownloadRetryDelay** a partir do padrão de 15 segundos.
- Faça uma avaliação de compatibilidade inline. 
   - Adicione um segundo passo do **Sistema Operativo de Upgrade** no início do grupo **Prepare-se para atualizar.** Nomeie-o *Avaliação de Atualização*. Especifique o mesmo pacote de atualização e, em seguida, ative a opção de realizar a compatibilidade do **Windows Configuração sem iniciar a atualização**. Ativar **Continue a erro** no separador Opções. 
   - Imediatamente após este passo de *avaliação* de upgrade, adicione um passo de Linha de **Comando executar.** Especifique a seguinte linha de comando:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>No separador **Opções,** adicione a seguinte condição: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Este código de devolução é o equivalente decimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), que é uma varredura de compatibilidade bem sucedida sem problemas. Se o passo de Avaliação de *Atualização* for bem sucedido e devolver este código, este passo é ignorado. Caso contrário, se o passo de avaliação devolver qualquer outro código de devolução, este passo falha a sequência de tarefas com o código de retorno da compatibilidade do Windows Setup.
   - Para mais informações, consulte o [sistema operativo Upgrade](../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).
- Se pretender alterar o dispositivo de BIOS para UEFI durante esta sequência de tarefas, consulte [Converter de BIOS para UEFI durante uma atualização no local](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Envie **feedback** do separador **Home** da fita se tiver mais recomendações ou sugestões.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Melhorias nos pontos de distribuição ativados pelo PXE
<!-- 1357580 -->
Para clarificar o comportamento da [nova funcionalidade PXE](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6) introduzida pela primeira vez na versão 1706 de Pré-visualização Técnica, rebatizamos a opção **Suporte IPv6.** No separador **PXE** das propriedades do ponto de distribuição, verifique **Ativar um serviço de resposta PXE sem o Serviço**de Implementação do Windows . 

Esta opção permite um resposta PXE no ponto de distribuição, que não requer Serviços de Implementação do Windows (WDS). Se ativar esta nova opção num ponto de distribuição já ativado por PXE, o Gestor de Configuração suspende o serviço WDS. Se desativar esta nova opção, mas ainda assim ativar o **suporte PXE para clientes,** então o ponto de distribuição volta a ativar o WDS.

Como o WDS não é necessário, o ponto de distribuição ativado pelo PXE pode ser um sistema operativo de cliente ou servidor, incluindo o Windows Server Core. Este novo serviço de resposta PXE continua a apoiar o IPv6, e também aumenta a flexibilidade dos pontos de distribuição ativados pelo PXE em escritórios remotos.

> [!NOTE]
> Este serviço utiliza a mesma tecnologia fundamental que o [serviço de resposta PXE baseado no cliente](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) na versão 1712 de Pré-visualização Técnica. Esta funcionalidade não requer a sobrecarga da função do ponto de distribuição.

### <a name="multicast"></a>Multicast
Para ativar e configurar o multicast no separador **Multicast** das propriedades do ponto de distribuição, o ponto de distribuição deve utilizar o WDS. 
- Se **ativar o suporte PXE para clientes** e ativar o **multicast para enviar simultaneamente dados a vários clientes,** então não pode **ativar um respondente PXE sem o Serviço**de Implementação do Windows .
- Se **ativar o suporte PXE para clientes** e **ativar um serviço de resposta PXE sem o Serviço de Implementação do Windows,** então não pode permitir que o **multicast envie simultaneamente enviar dados a vários clientes**



## <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 -->
O assistente de implementação para sequências de tarefas pode agora criar um modelo de implementação. O modelo de implementação pode ser guardado e aplicado a uma sequência de tarefas existente ou nova para criar uma implementação. 

### <a name="try-it-out"></a>Experimente!  
Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava. 

 **Criar um modelo de implementação para uma nova implementação de sequência de tarefas** <br/> 
1. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**
2. Clique à direita numa sequência de tarefas e selecione **Implementar**. 
3. No separador **Geral,** note que existe agora uma opção para selecionar o modelo de **implementação**. 
4. Continue através do **Assistente de Software de Implementação** selecionando as definições de implementação para a sequência de tarefas. 
5. Quando chegar ao separador **Resumo** do Assistente de **Software de Implementação,** clique em Guardar Como **Modelo**.
6. Dê ao modelo um nome e selecione as definições para guardar no modelo. 
7. Clique em **Guardar**. O modelo está agora disponível para utilização a partir da opção **Select Deployment Template.**



## <a name="product-lifecycle-dashboard"></a>Painel de instrumentos de ciclo de vida do produto
<!--1319632-->
O novo [dashboard Product Lifecycle](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md) mostra o estado da política de lifecycle do produto microsoft para os produtos da Microsoft instalados em dispositivos geridos com o Gestor de Configuração. O dashboard fornece-lhe informações sobre produtos da Microsoft no seu ambiente, estado de suporte e datas finais de suporte. Pode utilizar o painel de instrumentos para compreender a disponibilidade de suporte para cada produto. 

Para aceder ao Painel de Instrumentos de Ciclo de Vida, na consola do Gestor de Configuração, vá ao Ciclo de Vida do**Produto lifecycle** **de Ativos e Compliance** >**Asset Intelligence** >



## <a name="improvements-to-reporting"></a>Melhorias na comunicação
<!--1357653-->
Como resultado do [seu feedback,](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) adicionámos um novo relatório, o **Windows 10 A servicing detalhes para uma coleção específica.** Este relatório mostra o Id de Recursos, o nome NetBIOS, o nome OS, o nome de lançamento do OS, a construção, a sucursal de OS e o estado de manutenção dos dispositivos Windows 10. Para aceder ao relatório, aceda a **relatórios de monitorização** >**Reporting** >de**relatórios** >**operativos** >**Windows 10 Detalhes**de manutenção para uma recolha específica .



## <a name="improvements-to-software-center"></a>Melhorias no Centro de Software
<!--1357592-->
Como resultado do [seu feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) as aplicações instaladas podem agora ser ocultadas no Software Center. As aplicações que já estão instaladas deixarão de aparecer no separador Aplicações quando esta opção estiver ativada. 

### <a name="try-it-out"></a>Experimente!
Ative as **aplicações instaladas em ocultar na** definição do Centro de Software nas definições do cliente do Centro de Software. Observe o comportamento no Software Center quando o utilizador final instalar uma aplicação.



## <a name="improvements-to-run-scripts"></a>Melhorias para executar scripts
<!--1236459-->
A função [Executar Scripts](../../apps/deploy-use/create-deploy-scripts.md) agora retorna a saída do script usando a formatação JSON. Este formato devolve consistentemente uma saída de script legível. Os scripts que não executam podem não ser devolvidos à saída. 



## <a name="boundary-group-fallback-for-management-points"></a>Recuo do grupo de fronteirapara pontos de gestão
<!-- 1324594 -->
A partir desta versão, pode configurar relações de recuo para pontos de gestão entre [grupos de fronteira](../servers/deploy/configure/boundary-groups.md). Este comportamento proporciona um maior controlo para os pontos de gestão que os clientes usam. No separador **Relationships** das propriedades do grupo de fronteira, há uma nova coluna para o ponto de gestão. Quando se adiciona um novo grupo de limites de recuo, o tempo de recuo para o ponto de gestão é atualmente sempre zero (0). Este comportamento é o mesmo para o **Comportamento Padrão** no grupo de limite padrão do site.

Anteriormente, um problema comum ocorre quando se tem um ponto de gestão protegido numa rede segura. Os clientes da rede corporativa principal recebem uma política que inclui este ponto de gestão protegido, mesmo que não possam comunicar com ele através de uma firewall. Para resolver este problema, utilize a opção **Nunca recuo** para garantir que os clientes apenas recuem para pontos de gestão com os quais podem comunicar.

Ao atualizar o site para esta versão, o Gestor de Configuração adiciona todos os pontos de gestão não virados para a Internet no grupo de limites padrão do site. Este comportamento de upgrade garante que as versões de clientes mais antigas continuem a comunicar com pontos de gestão. Para tirar o máximo partido desta funcionalidade, mova os seus pontos de gestão para os grupos de fronteira pretendidos.

O recuo do grupo de limites de pontode gestão não altera o comportamento durante a instalação do cliente (ccmsetup). Se a linha de comando não especificar o ponto de gestão inicial utilizando o parâmetro/MP, o novo cliente recebe a lista completa dos pontos de gestão disponíveis. Para o seu processo inicial de bootstrap, o cliente usa o primeiro ponto de gestão a que pode aceder. Assim que o cliente se regista no site, recebe a lista de pontos de gestão devidamente classificada com este novo comportamento. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar [pontos de gestão preferenciais.](../servers/deploy/configure/boundary-groups.md#bkmk_preferred) Na consola De Configuração Manager, vá ao espaço de trabalho da **Administração.** Expandir a **configuração do site** e selecionar **sites**. Clique em **Definições de Hierarquia** na fita. No separador **Geral,** ative **os Clientes que preferem utilizar pontos de gestão especificados em grupos de fronteira**. 

### <a name="known-issues"></a>Problemas conhecidos
- Os processos de implantação do sistema operativo não estão cientes dos grupos de fronteira.

### <a name="troubleshooting"></a>Resolução de problemas
Novas entradas aparecem no **LocationServices.log**. O atributo **da Localidade** identifica um dos seguintes estados:
- 0: Desconhecido
- 1: O ponto de gestão especificado está apenas no grupo de limite sinuoso do site para recuo
- 2: O ponto de gestão especificado encontra-se num grupo de fronteira remoto ou vizinho. Quando o ponto de gestão está em ambos os grupos de fronteira padrão do vizinho e do site, a localidade é 2.
- 3: O ponto de gestão especificado encontra-se no grupo de fronteira local ou atual. Quando o ponto de gestão está no atual grupo de fronteira, bem como um vizinho ou o grupo de fronteira padrão do site, a localidade é 3. Se não permitir a definição de pontos de gestão preferenciais em Definições de Hierarquia, a localidade é sempre 3 independentemente do grupo de fronteira em que o ponto de gestão se encontra.

Os clientes usam os pontos de gestão local primeiro (localidade 3), segundo remoto (localidade 2), depois recuo (localidade 1). 

Quando um cliente recebe cinco erros em dez minutos e não consegue comunicar com um ponto de gestão no seu atual grupo de fronteira, tenta contactar um ponto de gestão num vizinho ou no grupo de fronteira padrão do site. Se o ponto de gestão do atual grupo de fronteiras voltar a funcionar mais tarde, o cliente voltará ao ponto de gestão local no próximo ciclo de atualização. O ciclo de atualização é de 24 horas, ou quando o serviço de agente de configuração reinicia.



## <a name="improved-support-for-cng-certificates"></a>Melhor apoio aos certificados de GNC
<!-- 1357314 -->
Configuração Manager (ramo atual) versão 1710 suporta [Cryptografia: Certificados de Próxima Geração (CNG).](../plan-design/network/cng-certificates-overview.md) A versão 1710 limita o suporte aos certificados de cliente em vários cenários. 

A partir desta versão técnica de pré-visualização, utilize certificados CNG para as seguintes funções de servidor ativadas por HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software

A lista de [cenários não apoiados](../plan-design/network/cng-certificates-overview.md#unsupported-scenarios) continua a mesma.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte de gateway de gestão de nuvem para Gestor de Recursos Azure
<!-- 1324735 -->
Ao criar uma instância do gateway de [gestão](../clients/manage/cmg/plan-cloud-management-gateway.md) da nuvem (CMG), o assistente oferece agora a opção de criar uma implementação do Gestor de **Recursos Azure**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma entidade única, chamada grupo de [recursos.](/azure/azure-resource-manager/resource-group-overview#resource-groups) Ao implantar a CMG com o Azure Resource Manager, o site utiliza o Azure Ative Directory (Azure AD) para autenticar e criar os recursos em nuvem necessários. Esta implantação modernizada não requer o clássico certificado de gestão Azure.  

O assistente CMG ainda fornece a opção para uma **implantação de serviço clássico** usando um certificado de gestão Azure. Para simplificar a implantação e gestão de recursos, recomendamos a utilização do modelo de implantação do Gestor de Recursos Azure para todas as novas instâncias cmg. Se possível, reimplante as instâncias CMG existentes através do Gestor de Recursos.

O Gestor de Configuração não migra as instâncias clássicas de CMG existentes para o modelo de implementação do Gestor de Recursos Azure. Crie novas instâncias CMG utilizando implementações do Gestor de Recursos Azure e, em seguida, remova as instâncias clássicas de CMG. 

> [!IMPORTANT]
> Esta capacidade não permite suporte para fornecedores de serviços de nuvem Azure (CSP). A implantação da CMG com o Azure Resource Manager continua a utilizar o clássico serviço de cloud, que o CSP não suporta. Para mais informações, consulte [os serviços azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Pré-requisitos
- Integração com [a Azure AD.](../clients/deploy/deploy-clients-cmg-azure.md) Não é necessária a descoberta do utilizador da AD Azure.
- Os [mesmos requisitos para](../clients/manage/cmg/plan-cloud-management-gateway.md#requirements)o gateway de gestão de nuvem, com exceção do certificado de gestão Azure.

### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Na consola de Gestor de Configuração, espaço de trabalho **da Administração,** expandir **os Serviços cloud,** e selecionar Gateway de **Gestão**de Cloud . Clique em Criar Gateway de **Gestão** de Nuvem na fita. 
2. Na página **Geral,** selecione implementação do **Gestor de Recursos Azure**. Clique **em Iniciar sessão** para autenticar com uma conta de administrador de subscrição Azure. O assistente povoa automaticamente os restantes campos da informação de subscrição da AD Azure armazenada durante o pré-requisito de integração. Se possuir várias subscrições, selecione a subscrição desejada para utilizar. Clique em **Seguinte**.  
3. Na página **Definições,** forneça o ficheiro de certificado PKI do servidor, como de costume. Este certificado define o nome de serviço CMG em Azure. Selecione a **Região**e, em seguida, selecione uma opção de grupo de recursos para **criar novas** ou **utilizar existentes**. Introduza o novo nome do grupo de recursos ou selecione um grupo de recursos existente na lista de drop-down. 
4. Conclua o assistente.

> [!NOTE] 
> Para a aplicação de servidor AD Azure selecionada, o Azure atribui a permissão do **colaborador** de subscrição. 

Monitorize o progresso da implementação do serviço com **cloudmgr.log** no ponto de ligação de serviço.



## <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de pedido para utilizadores por dispositivo
<!-- 1357015 -->
A partir desta versão, quando um utilizador solicita uma aplicação que requer aprovação, o nome do dispositivo específico é agora uma parte do pedido. Se o administrador aprovar o pedido, o utilizador só poderá instalar a aplicação nesse dispositivo. O utilizador deve submeter outro pedido para instalar a aplicação noutro dispositivo. 

> [!NOTE]
> Esta funcionalidade é opcional. Ao atualizar para esta versão, ative esta funcionalidade no assistente de atualização. Em alternativa, ative a funcionalidade na consola mais tarde. Para mais informações, consulte [Enable optional features from updates](../servers/manage/install-in-console-updates.md#bkmk_options).

### <a name="prerequisites"></a>Pré-requisitos
- Atualize o cliente do Gestor de Configuração para a versão mais recente
- Ativar a definição do cliente **Utilize o novo Centro** de Software no grupo de agentes [informáticos](../clients/deploy/about-client-settings.md#computer-agent)

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Implemente uma aplicação disponível para uma recolha de utilizadores.
2. Na página Definições de **Implementação,** ative a opção: **Um administrador deve aprovar um pedido para esta aplicação no dispositivo**.
3. Como utilizador direcionado, utilize o Software Center para submeter um pedido para a aplicação. 
4. Ver **Pedidos de Aprovação** no âmbito da Gestão de **Aplicações** no espaço de trabalho da Biblioteca de **Software** da consola Do Gestor de Configuração. Existe agora uma coluna **de dispositivo** na lista para cada pedido. Quando toma medidas sobre o pedido, o diálogo do Pedido de Pedido de Pedido também inclui o nome do dispositivo a partir do qual o utilizador submeteu o pedido.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilize o Centro de Software para navegar e instalar aplicações disponíveis pelo utilizador em dispositivos ligados ao Azure AD
<!-- 1322613 -->
Se implementar aplicações como disponível para os utilizadores, elas podem agora navegar e instalá-las através do Software Center nos dispositivos Azure Ative Directory (Azure AD).  

### <a name="prerequisites"></a>Pré-requisitos
- Ativar HTTPS no ponto de gestão
- Integrar o site com [a Azure AD](../clients/deploy/deploy-clients-cmg-azure.md)
- Implementar uma aplicação disponível para uma recolha de utilizadores
- Distribua qualquer conteúdo de aplicação para um ponto de [distribuição na nuvem](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- Ativar a definição do cliente **Utilize o novo Centro** de Software no grupo de agentes [informáticos](../clients/deploy/about-client-settings.md#computer-agent)
- O cliente deve ser: 
   - Windows 10
   - Azure AD-joined, também conhecido como cloud domínio-joined
- Para apoiar clientes baseados na Internet:
    - [Gateway de gestão da cloud](../clients/manage/cmg/plan-cloud-management-gateway.md) 
    - Ativar a definição do cliente: **Ativar pedidos de política de utilizador de clientes da Internet** no grupo Política de [Clientes](../clients/deploy/about-client-settings.md#client-policy)
- Para apoiar os clientes na rede corporativa:
    - Adicione o ponto de distribuição da nuvem a um grupo de fronteira saturado utilizado pelos clientes
    - Os clientes devem ser capazes de resolver o nome de domínio totalmente qualificado (FQDN) do ponto de gestão ativado pelo HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre informações do dispositivo Windows AutoPilot
<!-- 1351442 -->
O Windows AutoPilot é uma solução para o embarque e configuração de novos dispositivos Windows 10 de forma moderna. Para mais informações, consulte uma [visão geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Um dos métodos de registo de dispositivos existentes com o Windows AutoPilot é fazer o upload de informações do dispositivo para a Microsoft Store para negócios e educação. Estas informações incluem o número de série do dispositivo, identificador de produto Windows e um identificador de hardware. Utilize o Gestor de Configuração para recolher e reportar as informações deste dispositivo. 

### <a name="prerequisites"></a>Pré-requisitos
- Esta informação do dispositivo aplica-se apenas aos clientes no Windows 10, versão 1703 e posteriormente

### <a name="try-it-out"></a>Experimente!
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

1. Na consola do Gestor de Configuração, **monitorizar** o espaço de trabalho, expandir o nó **reporte,** expandir **Relatórios**e selecionar o **Hardware -** Nó Geral.
2. Executar o novo relatório, **Windows AutoPilot Device Information** e ver os resultados. 
3. No visualizador do relatório clique no ícone **Export** e selecione a opção **CSV (víruma delimitada).**
4. Depois de guardar o ficheiro, faça o upload dos dados para a Microsoft Store para negócios e educação. Para mais informações, consulte [adicionar dispositivos na Microsoft Store para negócios e educação.](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias nas políticas do Gestor de Configuração para o Windows Defender Exploit Guard
<!-- 1356220 -->
Foram adicionadas definições de política adicionais para os componentes de acesso à pasta Attack Surface Reduction e Controlled foram adicionadas no Gestor de Configuração para [o Windows Defender Exploit Guard](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).

**Novas definições para acesso a pasta controlada**<br/>
Existem duas opções adicionais quando configurao o acesso à pasta Controlada: **bloquear apenas sectores** de disco e **auditar sectores**de discos apenas . Estas duas definições permitem que o acesso à pasta controlada seja ativado apenas para os sectores de arranque e não permite a proteção de pastas específicas ou as pastas protegidas por defeito. 

**Novas definições para a redução da superfície de ataque**
- Utilize proteção avançada contra ransomware.
- Bloqueie o roubo de credenciais do subsistema da autoridade de segurança local do Windows. 
- Impeça ficheiros executáveis de serem executados a menos que cumpram uma lista de critérios de prevalência, idade ou fidedignidade. 
- Bloqueie processos não fidedignos e não assinados executados a partir de USB.



## <a name="microsoft-edge-browser-policies"></a>Políticas de navegador Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o navegador Web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nos clientes do Windows 10, pode agora criar uma política de definições de conformidade do Gestor de Configuração para configurar várias definições do Microsoft Edge. Esta política inclui atualmente as seguintes definições:
- **Definir o navegador Microsoft Edge como padrão**: configura a definição de aplicação padrão do Windows 10 para o navegador web para o Microsoft Edge
- **Permitir a queda da barra**de endereços : Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política de [navegador AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Permitir sincronizar os favoritos entre os navegadores**da Microsoft : Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política do [navegador SyncFavoritesBetweenIEEMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Permitir dados de navegação claros na saída**: Requer o Windows 10, versão 1703 ou mais tarde. Para mais informações, consulte a política de [navegador ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Não permita rastrear os cabeçalhos**: Para mais informações, consulte a política do [navegador AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Permitir a preenchimento automática**: Para mais informações, consulte a política do [navegador AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Permitir cookies**: Para mais informações, consulte a política do [navegador AllowCookies.](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)
- Permita um **bloqueador pop-up**: Para mais informações, consulte a política do [navegador AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Permitir sugestões de pesquisa na barra**de endereços : Para mais informações, consulte a política do navegador [AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Permitir enviar tráfego intranet para o Internet Explorer**: Para mais informações, consulte a política do navegador [SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Permitir o gestor de passwords**: Para mais informações, consulte a política de [navegador AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Permitir ferramentas de desenvolvimento**: Para mais informações, consulte a política do [navegador AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Permitir extensões**: Para mais informações, consulte a política do [navegador AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Pré-requisitos
- Cliente do Windows 10 que é azure Ative Diretório. 

### <a name="known-issues"></a>Problemas conhecidos
- Os dispositivos ligados ao domínio no local não podem aplicar esta política nesta versão. Esta questão também diz respeito a dispositivos híbridos de domínio.

### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.

**Criar a política**
1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance.** Expandir **as Definições** de Conformidade e selecionar o novo nó de perfis de **navegador microsoft Edge.** Clique na opção da fita para criar a política do **navegador Microsoft Edge**.
2. Especifique um **Nome** para a apólice, introduza opcionalmente uma **Descrição,** e clique **em Seguinte**.
3. Na página **Definições,** altere o valor para **Configurado** para as definições a incluir nesta política e clique em **Next**.
4. Na página **Plataformas Suportadas,** selecione as versões e arquiteturas do sistema operativo a que esta política se aplica, e clique em **Next**. 
5. Conclua o assistente.

**Implementar a política**
1. Selecione a sua política e clique na opção de fita para **implementar**.
2. Clique em **Navegar** para selecionar a recolha do utilizador ou do dispositivo para implementar a política. 
3. Selecione opções adicionais se necessário. Gere alertas quando a política não está em conformidade. Detete o horário pelo qual o cliente avalia o cumprimento do dispositivo com esta política.
4. Clique em **OK** para criar a implementação.

Como qualquer política de definições de conformidade, o cliente remedia as definições na programação que especifica. [Monitore e informe sobre](../../compliance/deploy-use/monitor-compliance-settings.md) a conformidade do dispositivo na consola Do Gestor de Configuração.



## <a name="report-for-default-browser-counts"></a>Relatório para contagem de navegador padrão
<!-- 1357830 -->
Agora há um novo relatório para mostrar a contagem de clientes com um navegador web específico como o padrão do Windows. 

### <a name="known-issues"></a>Problemas conhecidos
- Quando abre o relatório pela primeira vez, só mostra a contagem e não o BrowserProgID. Para contornar esta questão, edite a consulta do relatório para a seguinte sintaxe:  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Experimente!  
 Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.
1. Na consola do Gestor de **Configuração,** **monitorizando** o espaço de trabalho, expandir **relatórios,** expandir **Relatórios,** selecionar **Software - Empresas e Produtos.**
2. Executar o relatório de contagem de **navegador padrão.**

Utilize a seguinte referência para browserProgIDs comuns:
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v**: Microsoft Edge
- **Ou não, não é? HTTP**: Microsoft Internet Explorer
- **ChromeHTML**: Google Chrome
- **OperaStable**: Software de Ópera
- **FirefoxURL-308046B0AF4A39CB**: Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos ARM64 do Windows 10
<!-- 1353704 -->
A partir desta versão, o cliente do Gestor de Configuração é suportado nos dispositivos ARM64 do Windows 10. As funcionalidades de gestão de clientes existentes devem funcionar com estes novos dispositivos. Por exemplo, inventário de hardware e software, atualizações de software e gestão de aplicações. Atualmente, a implantação do sistema operativo não é suportada. 

## <a name="changes-to-phased-deployments"></a>Alterações às Implementações Faseadas
<!-- 1357405 -->
As implementações faseadas automatizam um lançamento coordenado e sequenciado de software em várias coleções. Nesta versão De pré-visualização técnica, o assistente de implementação faseado pode ser concluído para sequências de tarefas na consola de administração e as implementações são criadas. No entanto, a segunda fase não começa automaticamente após a satisfação dos critérios de sucesso da primeira fase. A segunda fase pode ser iniciada manualmente com uma declaração SQL.   

### <a name="try-it-out"></a>Experimente!  
  Tente completar as tarefas. Em seguida, envie **feedback** do separador **home** da fita informando-nos como funcionava.
 
**Criar uma implementação faseada para uma sequência de tarefas** </br>
1. No espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione sequências de **tarefas.**
2. Clique à direita numa sequência de tarefas existente e selecione **Criar implantação faseada**. 
3. No separador **Geral,** dê à implementação faseada um nome, descrição (opcional) e selecione Criar automaticamente uma implementação de **duas fases por defeito**. 
4. Povoe os campos **de Primeira Coleção** e Segunda **Coleção.** Selecione **Seguinte**.
5. No separador **Definições,** escolha uma opção para cada uma das definições de agendamento e selecione **Seguinte** quando estiver completo. 
6. No separador **Fases,** edite qualquer uma das fases, se necessário, clique em **Seguinte**.
7. Confirme as suas seleções no separador **Resumo** e clique em **Next** para proceder.
8. Quando os critérios de sucesso para a primeira fase forem atingidos, siga as instruções para iniciar a segunda fase com uma declaração SQL.
 
**Iniciar segunda fase com uma declaração SQL**
1. Identifique o ID de Implantação Faseado para a implementação que criou com a seguinte consulta SQL:<br/> `Select * from PhasedDeployment`
2. Executar a seguinte declaração para iniciar a fase de produção:<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou atualização do ramo de pré-visualização técnica, consulte [a Pré-visualização técnica para o Gestor de Configuração](technical-preview.md).    
