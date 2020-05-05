---
title: Ponto de distribuição de puxar
titleSuffix: Configuration Manager
description: Conheça as configurações e limitações para utilizar um ponto de distribuição de puxar com o Gestor de Configuração."
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c243897a4c52eff04263325b998c4b23d6b3dde4
ms.sourcegitcommit: ad4b3e4874a797b755e774ff84429b5623f17c5c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82166592"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Utilize um ponto de distribuição de puxar com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Quando distribui conteúdo para um ponto de distribuição padrão na consola 'Gestor de Configuração', o servidor do site empurra o conteúdo para o ponto de distribuição. Um ponto de distribuição de puxar obtém conteúdo descarregando-o de um local de origem como um cliente.  

Quando distribui conteúdo para muitos pontos de distribuição, os pontos de distribuição ajudam a reduzir a carga de processamento no servidor do site. Também podem acelerar a transferência de conteúdo para cada servidor. Normalmente, o componente do gestor de distribuição no servidor do site envia conteúdo para cada ponto de distribuição. Em vez disso, o site descarrega o processo de transferência do conteúdo para os pontos de distribuição de puxar.  

Configura pontos de distribuição individuais para ser pontos de distribuição de puxar. Para cada ponto de distribuição de puxar, especifique um ou mais pontos de distribuição de origem a partir dos quais pode obter conteúdo. Um ponto de distribuição de puxar só pode descarregar conteúdo a partir de um ponto de distribuição que especifica como um ponto de distribuição de origem.

Quando distribui conteúdo para um ponto de distribuição na consola, o servidor do site envia-lhe uma notificação. O ponto de distribuição de puxar em seguida descarrega o conteúdo a partir de um ponto de distribuição de origem. Um ponto de distribuição de puxar gere a transferência de conteúdo descarregando de um ponto de distribuição que já tem uma cópia do conteúdo.  

Os pontos de distribuição de puxar suportam as mesmas configurações e funcionalidades que os pontos de distribuição típicos. Por exemplo, um ponto de distribuição de puxar suporta:

- Configurações multicast e PXE
- Validação de conteúdos
- Distribuição de conteúdo a pedido
- Comunicações HTTP ou HTTPS dos clientes
- As mesmas opções de certificado que outros pontos de distribuição
- Gerir individualmente ou como membro de um grupo de pontos de distribuição  

Configure um ponto de distribuição de puxar quando instalar o ponto de distribuição. Depois de criar um ponto de distribuição, configure-o como um ponto de distribuição de puxar, editando as propriedades do papel. Para obter mais informações sobre como ativar um ponto de distribuição como ponto de distribuição de puxar, consulte o [ponto de distribuição de puxar](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Remova a configuração para ser um ponto de distribuição de puxar, editando as propriedades do ponto de distribuição. Quando remove a configuração como ponto de distribuição de puxar, volta ao funcionamento normal. O servidor do site gere futuras transferências de conteúdo para o ponto de distribuição.  

## <a name="distribution-process"></a>Processo de distribuição

Quando distribui conteúdo para um ponto de distribuição de puxar, ocorre a seguinte sequência de eventos:

- Uma vez distribuído conteúdo para um ponto de distribuição na consola, o componente Do Gestor de Transferência de Pacotes no servidor do site verifica a base de dados do site para confirmar se o conteúdo está disponível num ponto de distribuição de origem. Se não puder confirmar que o conteúdo está num ponto de distribuição de origem para o ponto de distribuição de puxar, repete o cheque a cada 20 minutos até que o conteúdo esteja disponível.  

- Quando o Gestor de Transferência de Pacote confirmar que os conteúdos estão disponíveis, notificará o ponto de distribuição de solicitação para que proceda à transferência dos mesmos. Se esta notificação falhar, retenta com base nas definições de **Retry** do componente de distribuição de software para pontos de distribuição de puxar. Quando o ponto de distribuição de puxar recebe esta notificação, tenta descarregar o conteúdo a partir dos seus pontos de distribuição de origem.  

- Enquanto o ponto de distribuição de puxar descarrega o conteúdo, o Gestor de Transferência de Pacotes vota o estado com base nas definições de **sondagens do componente** de distribuição de software Status para pontos de distribuição de puxar.  Quando o ponto de distribuição de puxar completa o download de conteúdo, submete este estatuto a um ponto de gestão.  

## <a name="configure-site-component-settings"></a>Configurar as definições do componente do site

Quando utilizar um ponto de distribuição de puxar, reveja e configure as seguintes definições do componente do site:  

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. Selecione o site. Na fita, **selecione Configure Componentes**do Site , e selecione Distribuição de **Software**.  

3. Mude para o separador **Ponto de Distribuição de Puxar.**  

4. No grupo **de definições de retry,** reveja os seguintes valores:  

    - **Número de repetições**: O número de vezes que o Gestor de Transferência de Pacotes tenta notificar o ponto de distribuição de puxar para descarregar o conteúdo. Depois de tentar este número de vezes, o Gestor de Transferência de Pacotecancela a transferência. Este valor é de 30 por defeito.  

    - Atraso antes de **voltar a tentar (minutos)**: O número de minutos que o Gestor de Transferência de Pacotes aguarda entre tentativas. Este valor é de 20 por defeito.  

5. No grupo de **definições de sondagens status,** reveja os seguintes valores:  

    - **Número de sondagens**: O número de vezes que o Gestor de Transferência de Pacotes contacta o ponto de distribuição de puxar para recuperar o estado de trabalho. Se tentar este número de vezes antes do trabalho estar concluído, o Gestor de Transferência de Pacotes cancela a transferência. Este valor é de 72 por defeito.

    - Atraso antes de **voltar a tentar (minutos)**: O número de minutos que o Gestor de Transferência de Pacotes aguarda entre tentativas. Este valor é de 60 por defeito.

    > [!NOTE]  
    >  Quando o Gestor de Transferência de Pacotes cancela um trabalho porque excede o número de repetições de sondagens, o ponto de distribuição de puxar continua a descarregar o conteúdo. Quando termina, o ponto de distribuição de puxar envia a mensagem de estado apropriada, e a consola reflete o novo estado.  

## <a name="limitations"></a>Limitações

- Não se pode configurar um ponto de distribuição em nuvem como um ponto de distribuição de puxar.  

- Não é possível configurar a função do ponto de distribuição num servidor de site como ponto de distribuição de puxar.  

- A configuração de conteúdo pré-configurado substitui a configuração de ponto de distribuição de extração. Se ligar a opção de ativar este ponto de **distribuição para conteúdo pré-encenado** num ponto de distribuição de puxar, aguarda o conteúdo. Não retira conteúdo do ponto de distribuição de origem. Como um ponto de distribuição padrão ativado para conteúdo pré-encenado, não recebe conteúdo do servidor do site. Para mais informações, consulte [o conteúdo pré-encenado.](manage-network-bandwidth.md#BKMK_PrestagingContent)  

- Um ponto de distribuição de puxar não utiliza configurações de horário ou limite de tarifa. Quando configura um ponto de distribuição previamente instalado para ser um ponto de distribuição de puxar, as configurações para os limites de horário e de tarifação são guardadas, mas não utilizadas. Se remover mais tarde a configuração do ponto de distribuição de puxar, as configurações de limite de horário e de limite de taxa são implementadas como previamente configuradas.  

    > [!NOTE]  
    >  Os separadores **de limites** de horário e **de tarifação** não são visíveis nas propriedades do ponto de distribuição.  

- Os pontos de distribuição de puxar não utilizam as definições no separador **Geral** das Propriedades dos Componentes de Distribuição de **Software** para cada site. Estas definições incluem **distribuição simultânea** e **retentativa multicast.**  

- Para transferir conteúdo de um ponto de distribuição de origem numa floresta remota, instale o cliente do Gestor de Configuração no ponto de distribuição de puxar. Configure também uma conta de acesso à rede que possa aceder ao ponto de distribuição de fonte. Se ativar a opção do site de **utilizar certificados gerados pelo Gestor de Configuração para sistemas de site HTTP,** então não precisa de uma conta de acesso à rede.<!--1358228-->  

- Se o ponto de distribuição de puxar também for um cliente do Gestor de Configuração, a versão do cliente deve ser a mesma que o site do Gestor de Configuração que instala o ponto de distribuição de puxar. O ponto de distribuição de puxar utiliza o CCMFramework que é comum tanto ao ponto de distribuição de puxar como ao cliente do Gestor de Configuração.  

## <a name="about-source-distribution-points"></a>Acerca dos pontos de distribuição de origem  

Quando configurar o ponto de distribuição de puxar, especifique um ou mais pontos de distribuição de origem:  

- O assistente apenas exibe pontos de distribuição que se qualificam para serem pontos de distribuição de origem.  

- Um ponto de distribuição de solicitação pode ser especificado como um ponto de distribuição de origem para outro ponto de distribuição de solicitação.  

- Apenas os pontos de distribuição que suportam HTTP podem ser especificados como pontos de distribuição de origem quando utilizar a consola 'Gestor de Configuração'.  

- Utilize o Gestor de Configuração SDK para especificar um ponto de distribuição de fonte que está configurado para HTTPS. Para utilizar um ponto de distribuição de fonte sintetizado para HTTPS, instale o cliente Do Gestor de Configuração no ponto de distribuição de puxar.  

- Se os seus escritórios remotos tiverem uma melhor ligação à internet ou para reduzir a carga nas suas ligações WAN, utilize um ponto de distribuição em [nuvem](use-a-cloud-based-distribution-point.md) no Microsoft Azure como fonte. O ponto de distribuição de puxar precisa de acesso à Internet para comunicar com o Microsoft Azure. O conteúdo deve ser distribuído para o ponto de distribuição da nuvem de origem.<!--1321554-->  

    > [!Note]  
    > Esta funcionalidade incorre em encargos para a sua subscrição Azure para armazenamento de dados e saída de rede. Para mais informações, consulte o [Custo da utilização de um ponto de distribuição em nuvem](use-a-cloud-based-distribution-point.md#bkmk_cost).  

> [!Tip]  
> Quando um ponto de distribuição de extração transfere conteúdo de um ponto de distribuição de origem, esse ponto de distribuição de extração é contabilizado como um cliente na coluna **Acessos de Clientes (Exclusivos)** do relatório **Resumo de utilização do ponto de distribuição** .  

### <a name="source-priorities"></a>Prioridades de origem

- Atribuir uma prioridade separada a cada ponto de distribuição de fonte, ou atribuir vários pontos de distribuição de origem à mesma prioridade.  

- A prioridade determina a ordem pela qual o ponto de distribuição de puxar solicita conteúdo dos seus pontos de distribuição de origem.  

- Inicialmente, os pontos de distribuição de solicitação contactam um ponto de distribuição de origem com o valor de prioridade mais baixo. Se houver vários pontos de distribuição de fonte com a mesma prioridade, o ponto de distribuição de puxar seleciona aleatoriamente uma das fontes com essa prioridade.  

- Se o conteúdo não estiver disponível numa fonte selecionada, o ponto de distribuição de puxar tenta então descarregar o conteúdo de outro ponto de distribuição com a mesma prioridade.  

- Se nenhum dos pontos de distribuição com uma determinada prioridade tiver o conteúdo, o ponto de distribuição de puxar tenta descarregar o conteúdo a partir de um ponto de distribuição de fonte com o próximo nível prioritário. Continua esta pesquisa até que o conteúdo esteja localizado.

- Se nenhum dos pontos de distribuição de origem atribuídos tiver o conteúdo, o ponto de distribuição de puxar aguarda 30 minutos e, em seguida, reinicia o processo novamente.  

## <a name="inside-the-pull-distribution-point"></a>Dentro do ponto de distribuição de puxar

- Para gerir a transferência de conteúdos, os pontos de distribuição de puxar utilizam o componente **CCMFramework.** O cliente do Gestor de Configuração inclui este componente.  

- Quando ativa o ponto de distribuição de puxar, o site instala **pulldp.msi**. Este instalador também adiciona o componente CCMFramework. A estrutura não requer o cliente do Gestor de Configuração.  

- Após a instalação do ponto de distribuição de puxar, utiliza principalmente o serviço **CCMExec** para funcionar.  

- Quando o ponto de distribuição de puxar transfere o conteúdo, utiliza o Serviço de **Transferência Inteligente de Fundo** (BITS) incorporado no Windows. Um ponto de distribuição de puxar não requer que instale a extensão BITS para o Servidor IIS.<!--sms.503672 -Clarified BITS use-->

- Para obter detalhes operacionais, consulte os seguintes ficheiros de registo no ponto de distribuição de puxar:  

  - **DataTransferService.log**
  - **PullDP.log**

> [!TIP]
> Se vir os erros HTTP 403 nos ficheiros de registo depois de adicionar um ponto de distribuição de puxar, faça a seguinte alteração:
>
> 1. No ponto de distribuição de origem, detete o seguinte valor de registo:`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL, ClientAuthTrustMode = 2 (REG_DWORD)`
> 1. Reiniciar o servidor de ponto de distribuição de origem.
>
> Em seguida, o ponto de distribuição de puxar deve começar a descarregar conteúdo a partir da fonte. Para obter mais informações sobre esta chave de registo, consulte [a visão geral do TLS - SSL (Schannel SSP)](https://docs.microsoft.com/windows-server/security/tls/what-s-new-in-tls-ssl-schannel-ssp-overview).<!-- SCCMDocs#1973 -->

## <a name="see-also"></a>Consulte também  

[Conceitos fundamentais da gestão de conteúdos](fundamental-concepts-for-content-management.md)
