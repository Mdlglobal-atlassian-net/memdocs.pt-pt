---
title: Preparar a instalação de sites
titleSuffix: Configuration Manager
description: Se estiver a planear instalar vários sites do Gestor de Configuração, leia esta informação para o ajudar a economizar tempo e para evitar erros.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718183"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Prepare-se para instalar sites do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para se preparar para uma implementação bem-sucedida de um ou mais sites de Configuração Manager, familiarize-se com os detalhes deste artigo. Estes passos podem poupar-lhe tempo durante a instalação de vários locais e ajudar a prevenir erros que possam resultar na necessidade de reinstalar um ou mais locais.

> [!TIP]
> Ao gerir o site do Gestor de Configuração e a infraestrutura da hierarquia, os termos *de atualização,* *atualização*e *instalação* são usados para descrever três conceitos distintos. Para saber como cada termo é usado, consulte [sobre atualização, atualização e instalação.](../../../understand/upgrade-update-install.md)

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>Opções para instalar diferentes tipos de sites
Quando instala um novo site do Gestor de Configuração, a versão dos ficheiros de origem que pode utilizar depende da versão dos sites que já se encontram na hierarquia (se houver). Os métodos de instalação que pode utilizar dependem do tipo de local que pretende instalar.  

Antes de instalar um site, certifique-se de ter planeado a sua hierarquia e que compreende o tipo de site que pretende instalar. Para mais informações, consulte [Design uma hierarquia de sites.](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)


### <a name="first-site"></a>Primeiro site
O primeiro site que instalar numa hierarquia será um local primário autónomo ou um site de administração central.

Meios de **instalação**: Para instalar um site de administração central ou um local primário autónomo como o primeiro site de uma nova hierarquia, deve [utilizar uma versão de base](../../../../core/servers/manage/updates.md#bkmk_Baselines) do Gestor de Configuração. Não instale o primeiro local de uma nova hierarquia utilizando ficheiros de origem atualizados a partir do [CD. Última pasta](../../../../core/servers/manage/the-cd.latest-folder.md) de qualquer site.

**Método de instalação**: Pode instalar qualquer tipo de local utilizando o Assistente de Configuração do Gestor de [Configuração,](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)ou pode configurar um script para utilizar com uma [instalação de linha de comando escrita](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites adicionais
Depois de instalado o site inicial, pode adicionar mais sites a qualquer momento. Tem as seguintes opções para adicionar sites (até [limites suportados):](../../../../core/plan-design/configs/size-and-scale-numbers.md)

|Site que você tem|Tipo de site adicional que pode instalar|
|---|---|
|Site de administração central|Site principal subordinado|
|Site principal subordinado|Site Secundário|
|Site primário autónomo|Local secundário (pode expandir o local primário, que converte o local primário autónomo para um local primário infantil)|

Meios de **instalação**: Quando instalar um site de administração central para expandir um local primário autónomo, ou se instalar um novo local primário para crianças numa hierarquia existente, deve utilizar meios de instalação (que contenham ficheiros de origem) que correspondam à versão do site ou sites existentes.

> [!IMPORTANT]
> Se tiver instalado atualizações na consola que alteraram a versão dos sites previamente instalados, não utilize os meios de instalação originais. Em vez disso, neste cenário, utilize ficheiros de origem do [CD. Última pasta](../../../../core/servers/manage/the-cd.latest-folder.md) de um site atualizado. O Gestor de Configuração requer que utilize ficheiros de origem que correspondam à versão do site existente a que o seu novo site se irá ligar.

Um site secundário deve ser instalado a partir da consola 'Gestor de Configuração'. Desta forma, os sites secundários são sempre instalados utilizando ficheiros de origem do local primário dos pais.

Método de **instalação**: O método utilizado para instalar locais adicionais depende do tipo de local que pretende instalar.
- Adicione um site de **administração central:** Pode utilizar o Assistente de Configuração do Gestor de Configuração ou uma linha de comando scriptd para instalar o novo site da administração central como um site de pais para o seu site primário autónomo existente. Para mais informações, consulte [Expandir um site primário autónomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Adicione um site primário para crianças:** Pode utilizar o Assistente de Configuração do Gestor de Configuração ou uma instalação de linha de comando para adicionar um local primário para crianças abaixo de um site de administração central.
- **Adicione um site secundário:** Utilize a consola do Gestor de Configuração para instalar um local secundário como um local infantil abaixo de um local primário. Outros métodos não são suportados para a adição de sites secundários.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a>Tarefas comuns para completar antes de iniciar uma instalação
- **Compreenda a topologia da hierarquia que utilizará para a sua implantação**    
Para mais informações, consulte [Design uma hierarquia de sites para Gestor de Configuração](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Prepare e configure servidores individuais para atender pré-requisitos e configurações suportadas para utilização com O Gestor de Configuração**         
Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Instale e configure o Servidor SQL para alojar a base de dados do site**     
Para mais informações, consulte as [versões De Suporte para Servidor SQL para O Gestor de Configuração](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Prepare o ambiente da sua rede para apoiar o Gestor de Configuração**      
Para mais informações, consulte [configurar firewalls, portas e domínios para se preparar para o Gestor de Configuração](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Se utilizar uma infraestrutura de chaves públicas (PKI), prepare a sua infraestrutura e certificados**      
Para mais informações, consulte [os requisitos de certificado PKI para O Gestor de Configuração](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Instale as mais recentes atualizações de segurança em computadores que utilizará como servidores de servidores de sites ou servidores do sistema do site e, quando necessário, reinicie-as**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>Sobre os nomes do site e os códigos do site
Os códigos do site e os nomes do site são usados para identificar e gerir os sites numa hierarquia do Gestor de Configuração. Na consola 'Gestor de Configuração', o código &lt;do site e o nome do site são apresentados no formato de*nome* \> do *site do site.*\> - &lt; Todos os códigos de site que usas na tua hierarquia devem ser únicos. Se o esquema de Diretório Ativo for estendido para O Gestor de Configuração e os seus sites estiverem a publicar dados, os códigos de site utilizados dentro de uma floresta de Diretório Ativo devem ser únicos mesmo que sejam utilizados numa hierarquia de Gestor de Configuração diferente ou se tenham sido utilizados em instalações anteriores do Gestor de Configuração. Certifique-se de planear cuidadosamente os códigos do seu site e os nomes do site antes de implementar a sua hierarquia.

### <a name="specify-a-site-code-and-site-name"></a>Especificar um código do site e o nome do site
Ao executar configuração do Gestor de Configuração, é solicitado um código de site e nome do site para o site da administração central, e para cada local primário e instalação do site secundário. Um código de site deve identificar exclusivamente cada site na hierarquia. Como o código do site é utilizado em nomes de pastas, nunca utilize os seguintes nomes para o código do site, que incluem nomes reservados para 'Gestor de Configuração' e Windows:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Configuração Do Gestor de Configuração Não verifica se um código de site ainda não está a ser utilizado.

Para introduzir o código do site para um site quando estiver a executar a Configuração do Gestor de Configuração, tem de introduzir três caracteres alfanuméricos. Apenas as letras *A* a *Z* e os números *0* a *9,* em qualquer combinação, são permitidas nos códigos do site. A sequência de letras ou números não tem qualquer efeito na comunicação entre os locais. Por exemplo, não é necessário nomear um site primário *ABC* e um site secundário *DEF*.

O nome do site é um identificador de nome amigável para o site. Você só pode usar os caracteres *A* a *Z*, *a* através*-* *z*, *0* a *9*, e o hífen ( ) em nomes do site.

> [!IMPORTANT]
> Uma alteração do código do site ou do nome do site depois de instalar o site não é suportada.

### <a name="reuse-a-site-code"></a>Reutilizar um código de site
Os códigos do site não podem ser usados mais de uma vez numa hierarquia do Gestor de Configuração para um site de administração central ou para um site primário, mesmo que o código original do site e do site tenha sido desinstalado. Se reutilizar um código de site, arrisca-se a ter conflitos de identificação de objetos na sua hierarquia. Pode reutilizar o código do site para um site secundário se esse site secundário e o código do site já não estiverem em uso na hierarquia do Gestor de Configuração ou na floresta de Diretório Ativo.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limites e restrições para sites instalados
Antes de instalar um site, é importante compreender as seguintes limitações que se aplicam aos sites e hierarquias do site:
- Depois de executar a Configuração, não é possível alterar as seguintes propriedades do site sem desinstalar o site e, em seguida, reinstalá-lo utilizando os novos valores:  
  - Diretório de instalação de Ficheiros de Programa  
  - Código do site  
  - Descrição do site  
- Quando a sua hierarquia inclui um site de administração central:  
  - O Gestor de Configuração não suporta a deslocação de um local primário infantil para fora de uma hierarquia para criar um local primário autónomo ou para anexá-lo a uma hierarquia diferente. Em vez disso, desinstale o local primário da criança e, em seguida, reinstale-o como um novo local primário autónomo ou como um local infantil do local da administração central de uma hierarquia diferente.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a>Passos opcionais antes de executar a configuração
**Executar manualmente [o downloader de configuração](../../../../core/servers/deploy/install/setup-downloader.md)**

Para descarregar os ficheiros de Configuração atualizados para O Gestor de Configuração, pode executar o Downloader de Configuração. Se o computador onde irá executar a Configuração não estiver ligado à Internet, ou se espera instalar vários servidores de sites, considere utilizar o Downloader de Configuração para descarregar as atualizações necessárias para configurar. Aqui está uma informação adicional:
- Por padrão, a Configuração liga-se à Internet para descarregar ficheiros de configuração atualizados.
- Por predefinição, os ficheiros são armazenados na pasta Redist.
- Pode direcionar a Configuração para um local na sua rede onde já guardou uma cópia destes ficheiros.

**Executar manualmente [o verificador pré-requisito](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Para identificar e corrigir problemas antes de executar a Configuração para instalar um site e antes de instalar uma função do sistema de site num servidor, pode executar o Verificador Pré-Requisito. O Verificador pré-requisito ajuda a garantir que o computador cumpre os requisitos para acolher a função do site ou do sistema do site. Aqui está uma informação adicional:
- Por predefinição, a configuração executa o Verificador Pré-Requisito.
- Se houver erros, a configuração para até que o problema seja corrigido.

**Identificar portas opcionais**

Pode identificar portas opcionais para sistemas de sites e clientes a utilizar. Aqui está uma informação adicional:
- Por padrão, os sistemas de site e os clientes utilizam portas pré-definidas para comunicar.
- Durante a configuração, pode configurar portas alternativas.

Para mais informações, consulte [portos utilizados](../../../../core/plan-design/hierarchy/ports.md).
