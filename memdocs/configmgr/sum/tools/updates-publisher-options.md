---
title: Configurar opções
titleSuffix: Configuration Manager
description: Configure opções para utilizar o System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717728"
---
# <a name="configure-options-for-updates-publisher"></a>Configure opções para Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Reveja e configure as opções e configurações relacionadas que afetam o funcionamento do Editor de Atualizações.

Para aceder às opções da Editora de Atualizações, no canto superior esquerdo da consola, clique no separador **Atualizações Publisher** **Properties** e, em seguida, escolha **Opções**.

![Opções](media/properties1.png)   


As opções dividem-se no seguinte:

-   Update Server
-   Servidor ConfigMgr
-   Definições de procuração
-   Publicadores Fidedignos
-   Avançado
-   Atualizações
-   Registo

## <a name="update-server"></a>Update Server
Tem de configurar atualizações do Publisher para trabalhar com o servidor de atualizações como o Windows Server Update Services (WSUS) antes de [poder publicar atualizações](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace). Isto inclui especificar o servidor, métodos para ligar a esse servidor quando este está remoto da consola, e um certificado para usar para assinar atualizações digitalmente que publica.

- **Configure um servidor**de atualização . Quando configurar um servidor de atualização, selecione o servidor WSUS de nível superior (servidor de atualização) na hierarquia do Gestor de Configuração para que todos os sites infantis tenham acesso às atualizações que publica.

  Se o servidor de atualização estiver afastado do servidor 'Actualizações', especifique o nome de domínio totalmente qualificado (FQDN) do servidor e se se ligar por SSL. Quando se liga por SSL, a porta predefinida muda de 8530 para 8531. Certifique-se de que a porta que define corresponde ao que está a ser utilizado pelo seu servidor de atualização.

  > [!TIP]  
  > Se não configurar um servidor de atualização, ainda pode utilizar o Updates Publisher para autorizar atualizações de software.

- **Configure o certificado**de assinatura . Tem de configurar e ligar-se com sucesso a um servidor de atualização antes de configurar o certificado de assinatura.

  Atualiza o Editor utiliza o certificado de assinatura para assinar as atualizações de software que são publicadas no servidor de atualização. A publicação falha se o certificado digital não estiver disponível na loja de certificados do servidor de atualizações ou no computador que executa atualizações da Editora.

  Para obter mais informações sobre a adição do certificado à loja de certificados, consulte [Certificados e segurança para Editor](updates-publisher-security.md)de Atualizações .

  Se um certificado digital não for automaticamente detetado para o servidor de atualização, escolha um dos seguintes:

  -   **Navegar**: O BrowsE só está disponível quando o servidor de atualização estiver instalado no servidor onde executa a consola. Depois de selecionar um certificado, tem de escolher **criar** para adicionar esse certificado à loja de certificados WSUS no servidor de atualização. Tem de introduzir a palavra-passe do ficheiro **.pfx** para os certificados que selecionar por este método.

  -   **Criar:** Utilize esta opção para criar um novo certificado. Isto também adiciona o certificado à loja de certificados WSUS no servidor de atualização.

  **Se criar o seu próprio certificado**de assinatura, configure o seguinte:

  -   Permitir que a **chave privada Permitir seja exportada.**

  -   Dete tese **de utilização da chave** para a assinatura digital.

  -   Deteto o **tamanho mínimo** da chave para um valor igual ou superior a 2048 bit.

  Utilize a opção Remover a opção **Remover** um certificado do certificado WSUS. Esta opção está disponível quando o servidor de atualização é local para a consola da Atualização que utiliza, ou quando utilizou **o SSL** para se ligar a um servidor de atualização remoto.

## <a name="configmgr-server"></a>Servidor ConfigMgr
Utilize estas opções quando utilizar o Gestor de Configuração com o Editor de Atualizações.

-   **Especifique o servidor do Gestor de Configuração:** Depois de ativar o suporte para o Gestor de Configuração, especifique a localização do servidor de topo do site a partir da hierarquia do Gestor de Configuração. Se esse servidor estiver à distância da instalação do Editor de Atualizações, especifique o FQDN do servidor do site. Escolha a **Ligação de Teste** para garantir que pode ligar-se ao servidor do site.

-   **Configure limiares:** Os limiares são usados quando publica atualizações com um tipo de publicação de Automatic. Os valores-limiar ajudam a determinar quando é publicado o conteúdo completo para uma atualização em vez de apenas os metadados. Para saber mais tipos de publicação, consulte [as atualizações do Atribuir para uma publicação](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication)

    Pode um ou ambos os seguintes limiares:

    -   **Limiar de contagem de clientes solicitado:** Isto define quantos clientes devem solicitar uma atualização antes que a Editora de Atualizações possa publicar automaticamente o conjunto completo de conteúdos para essa atualização. Até que o número especificado de clientes solicite a atualização, apenas os metadados de atualizações são publicados.

    -   **Limiar de tamanho da fonte de embalagem (MB):** Isto impede a publicação automática de atualizações que excedam o tamanho que especifica. Se o tamanho das atualizações exceder este valor, apenas os metadados são publicados. As atualizações que são menores do que o tamanho especificado podem ter o seu conteúdo completo publicado.

## <a name="proxy-settings"></a>Definições de procuração
Atualizações A Publisher utiliza as definições de procuração quando importa catálogos de software a partir da Internet ou publica atualizações para a Internet.

-   Especifique o endereço FQDN ou IP de um servidor proxy. São suportados IPv4 e IPv6.

-   Se o servidor proxy autenticar os utilizadores para acesso à Internet, deve especificar o nome Windows. Não é apoiado um nome de princípio universal (UPN).

## <a name="trusted-publishers"></a>Publicadores Fidedignos
Quando importa um catálogo de atualizações, a fonte desse catálogo (com base no seu certificado), é adicionada como uma editora de confiança. Da mesma forma, quando publica uma atualização, a fonte do certificado de atualização é adicionada como um editor de confiança.

Pode ver os dados do certificado para cada editor e remover um editor da lista de editores de confiança.

O conteúdo de editores que não são confiáveis pode potencialmente prejudicar os computadores dos clientes quando o cliente procura atualizações. Só deve aceitar conteúdo de editores em quem confia.

## <a name="advanced"></a>Avançado
As opções avançadas incluem:

-   **Localização do repositório:** Ver e modificar a localização do ficheiro Base de Dados, **scupdb.sdf**. Este ficheiro é o repositório da Editora de Atualizações.

-   **Carimbo de tempo:** Quando ativado, é adicionado um carimbo de tempo às atualizações que assina que se identifica quando foi assinado. Uma atualização que foi assinada enquanto um certificado era válido pode ser usada após o termo do certificado de assinatura. Por predefinição, as atualizações de software não podem ser implementadas após o seu certificado de assinatura expirar.

-   **Consulte as atualizações dos catálogos subscritos:** Cada vez que a Atualização o Editor começa, pode verificar automaticamente as atualizações para catálogos que subscreveu. Quando uma atualização do catálogo é encontrada, os detalhes são fornecidos como **Alertas Recentes** na janela **de visão geral** do espaço de trabalho de **atualizações**.

-   **Revogação do certificado:** Escolha esta opção para permitir verificações de revogação de certificados.

-   **Publicação de fonte local:** Updates O Publisher pode utilizar uma cópia local de uma atualização que está a publicar antes de descarregar essa atualização a partir da Internet. A localização deve ser uma pasta no computador que executa atualizações do Editor. Por padrão, esta localização é **My Documents\LocalSourcePublishing.** Use isto quando já descarregou uma ou mais atualizações, ou fez alterações numa atualização que pretende implementar.

-   **Assistente de limpeza** de atualizações de software: Inicie o assistente de limpeza de atualizações. O assistente expira as atualizações que estão no servidor de atualização, mas não no repositório da Editora de Atualizações. Consulte [as atualizações não referenciadas](#expire-unreferenced-software-updates) do Expire para obter mais detalhes.

## <a name="updates"></a>Atualizações
 Atualizações A Editora pode verificar automaticamente novas atualizações sempre que abrir. Também pode optar por receber as construções de pré-visualização da Editora updates.

Para verificar manualmente se há atualizações, na ![consola Updates Publisher clique em Propriedades](media/properties2.png)  
para abrir as Propriedades da **Editora atualizações,** e depois escolher **Verificar a atualização**.

Depois de atualizações, a Editora encontra uma nova atualização, apresenta a janela **'Atualização Disponível'** e pode optar por instalá-la. Se optar por não instalar a atualização, é oferecida a próxima vez que abrir a consola.

## <a name="logging"></a>Registo
Atualizações A Editora regista informações básicas sobre updates Publisher para **%WINDIR%\Temp\UpdatesPublisher.log**.

Utilize o bloco de notas ou **cmTrace** para visualizar o registo. CMTrace é a ferramenta de ficheiro de registo do Gestor de Configuração e pode ser encontrada na pasta **\SMSSetup\Tools** do suporte de origem do Gestor de Configuração.

Pode alterar o tamanho do tronco e o seu nível de detalhe.

Quando ativa o registo de bases de dados, estão incluídas informações sobre as consultas que são feitas contra a base de dados Updates Publisher. A utilização do registo de bases de dados pode levar a um desempenho reduzido do computador Updates Publisher.

Para ver o ficheiro de registo, na consola clique ![em](media/properties2.png) Propriedades para abrir as Propriedades da Editora de **Atualizações**e, em seguida, escolha ver ficheiro de **registo**.

## <a name="expire-unreferenced-software-updates"></a>Expire atualizações de software não referenciadas
Pode executar o Assistente de Limpeza de **Atualizações** de Software para expirar atualizações que estão no seu servidor de atualização, mas não no repositório da Editora de Atualizações. Isto notifica o Gestor de Configuração que, em seguida, remove essas atualizações de quaisquer futuras implementações.

O ato de caducidade de uma atualização não pode ser invertido. Só execute esta tarefa quando tiver a certeza de que as atualizações de software selecionadas já não são necessárias pela sua organização.

### <a name="to-remove-expired-software-updates"></a>Para remover as atualizações de software expiradas
1.  Na consola Updates Publisher, ![](media/properties2.png) clique em Propriedades para abrir as Propriedades da **Editora de Atualizações**, e depois escolha **Opções**.

2.  Escolha **Avançado**, e, em seguida, em software **Update Clean Wizard,** escolha **Iniciar**.

3.  Selecione as atualizações de software que pretende expirar e, em seguida, escolha **A Seguinte**.

4.  Depois de rever as suas seleções, optou por **Next** para aceitar as seleções e expirar essas atualizações.

5.  Depois de terminar o assistente, escolha **Perto** para completar o assistente.
