---
title: Criar atualizações
titleSuffix: Configuration Manager
description: Criar e agregar atualizações de software com o System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723986"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar atualizações de software e atualizar pacotes com updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com atualizações, pode utilizar o assistente **Create Update** para criar as suas próprias atualizações e o assistente **Create Bundle** para criar pacotes de atualizações.

Como estes dois assistentes têm um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se ao procedimento para a criação de atualizações, com apenas as diferenças relevantes detalhadas.

## <a name="use-the-create-update-wizard"></a>Utilize o assistente de atualização criar
1. Na consola vai para **atualizações workspace**, e depois no painel **Getting Started,** escolha **Update** a partir do separador **Home** da fita. Isto abre o assistente **Create Update.**

2. Na página **Pacote,** utilize as seguintes informações para o ajudar a configurar a atualização:

   -   Escolha **o Browse** para localizar o pacote de atualização de software que utilizará como fonte de pacote. Fontes válidas incluem . MSI, . MSP, ou . Ficheiros EXE. Atualizações O Publisher requer acesso ao ficheiro para criar um hash de ficheiro. O hash e o nome do ficheiro são então utilizados nos metadados da atualização para a atualização que está a criar.

   -   Especifique a localização de origem do conteúdo para esta atualização. Normalmente, este é o local onde o binário da atualização será descarregado durante a publicação para um servidor WSUS.  Se for selecionada uma fonte local para publicar a opção de atualização de **software,** o caminho não é necessário.

       Mais tarde, quando a atualização é publicada num servidor WSUS, a Atualização editora descarrega os binários para a atualização a partir da localização de origem indicada.  Se não for fornecido nenhum caminho, a Update Publisher procurará a rota de publicação de [fonte local](updates-publisher-options.md#advanced) para o binário de atualização.

   -   Especifique o **idioma binário** da atualização do software.

   -   Especifique códigos de **devolução de sucesso**e **Códigos de reinício pendentes para** a atualização. Separe vários códigos de devolução utilizando uma vírem. Pode utilizar códigos de devolução para determinar quando a instalação da atualização foi bem sucedida e quando foram necessárias reinicializações.

       -   Ficheiros e patches do instalador do Windows (. MSI e. Ficheiros MSP) configuram automaticamente estes valores e não podem ser modificados.

       -   Pois. Atualizações EXE, os códigos predefinidos definidos pelo . O ficheiro EXE é utilizado se não forem especificados códigos de devolução.

   -   Especifique quaisquer argumentos de linha de comando que sejam necessários para instalar a atualização do software.

       -   Ficheiros e patches do instalador do Windows (. MSI e. Ficheiros MSP) configuram automaticamente estes valores. Para estes tipos de ficheiros, os argumentos devem ser especificados como ** \[valor\]=\[\]** de nome . Além disso, todas as **/** opções que começam com um (como **/qn)** não são suportadas para . MSI ou. Atualizações de software MSP.

       -   Pois. Atualizações EXE, todos os argumentos são válidos.

3. Na página **informação,** especifique detalhes sobre a atualização que estão incluídas quando a atualização for publicada ou exportada. Os detalhes incluem propriedades localizadas como o nome das atualizações (título) e descrição. Em seguida, especifica detalhes mais gerais, como a classificação, fornecedor, produto e onde saber mais sobre a atualização.

    __Propriedades localizadas:__

   - **Idioma**: Selecione um idioma e, em seguida, especifique um título e descrição. Em seguida, pode selecionar idiomas adicionais, um de cada vez, com cada idioma suportando o seu próprio título e descrição.

   - **Título**: Introduza o nome da atualização. Este nome apresenta-se no Espaço de Trabalho das Atualizações da consola Updates Publisher.

   - **Descrição**: Uma descrição amigável da atualização. Pode incluir o que a atualização instala e porquê ou quando deve ser utilizada.

   **Classificação:** Seguem-se descrições comuns para as diferentes classificações.

   - **Atualização**: Uma atualização de uma aplicação ou ficheiro que está atualmente instalado.

   - **Critical**: Uma atualização amplamente lançada para um problema específico que aborda um bug crítico que não está relacionado com a segurança.

   - **Pack de funcionalidades**: Novas funcionalidades que são distribuídas fora de um lançamento do produto e que são normalmente incluídas na próxima versão completa do produto.

   - **Segurança**: Uma atualização amplamente divulgada para uma questão específica do produto que está relacionada com a segurança.

   - **Atualização Rollup**: Um conjunto cumulativo de hotfixes que são embalados em conjunto para uma fácil implantação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualização geralmente aborda uma área específica, como segurança ou uma funcionalidade de produto.

   - **Pacote de serviços**: Um conjunto cumulativo de hotfixos que são aplicados a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.

   - **Ferramenta**: Especifica uma ferramenta ou funcionalidade que ajuda a completar uma ou mais tarefas.

   - **Condutor**: Uma atualização para o software do condutor.

   **Vendedor:** Especifique um fornecedor para a atualização. Pode utilizar a lista de abandono para utilizar valores a partir de atualizações que se encontram no repositório. Quando especifica um fornecedor, o assistente cria uma pasta com esse nome de fornecedor em **Todas as Atualizações** de Software no Espaço de Trabalho de **Atualizações** se essa pasta ainda não existir. Seguem-se os Serviços de Atualização do Servidor do Windows (WSUS) que não podem ser introduzidos para atualizações que cria:
   - Microsoft Corporation
   - Microsoft
   - Atualizar
   - Atualização de Software
   - Ferramentas
   - Ferramenta
   - Crítica
   - Atualizações Críticas
   - Segurança
   - Atualizações de Segurança
   - Pacote de recursos
   - Atualizar Rollup
   - Service Pack
   - Controlador
   - Atualização do condutor
   - Pacote
   - Atualização do pacote

   **Produto**: Especifique o tipo de produto para o qual a atualização se destina. Pode utilizar a lista de abandono para utilizar valores a partir de atualizações que se encontram no repositório. A mesma lista de nomes reservados da WSUS que não podem ser utilizados para **o Fornecedor,** não pode ser utilizada para **o Produto**.

   **Mais informações URL**: Especifique o URL onde pode encontrar mais informações sobre esta atualização. Deve utilizar letras minúsculas para **https** ou **http** quando introduzir este URL.

4. Na página **Informação Opcional,** pode configurar detalhes que forneçam informações adicionais sobre a atualização.

   -   **ID do boletim**: Os IDs do boletim são geralmente, mas nem sempre, fornecidos pelos fornecedores de atualização.

   -   **ID do artigo**: Se um artigo de atualização de software estiver disponível, o ID do artigo pode ser útil para os indivíduos que procuram informações adicionais sobre a atualização.

   -   **IDs CVE:** Enumerar um ou mais identificadores comuns de vulnerabilidades e exposições (CVE) que fornecem informações de segurança sobre o pacote de atualização ou atualização. Ao enumerar mais de um, utilize um ponto evívio para separar os CVEs como neste exemplo: *CVE1; CVE2.*

   -   **URL de suporte:** Enumera o URL que contém informações de suporte para esta atualização, se disponível. Deve utilizar letras minúsculas para **https** ou **http** quando introduzir este URL.

   -   **Gravidade:** Detete o nível de gravidade para esta atualização.

   -   **Impacto:** As seguintes opções podem ser utilizadas para especificar o impacto:
       -   **Normal –** Utilize isto para indicar que a atualização requer procedimentos típicos de instalação.
       -   **Menor –** Utilize isto para indicar que a atualização requer procedimentos mínimos de instalação.
       -   **Requer manuseamento exclusivo –** Utilize isto para indicar que a atualização deve ser instalada por si só, exclusiva de quaisquer outras atualizações.   <br /><br />

   -   **Reiniciar Comportamento:** Use isto para fornecer informações sobre as atualizações reiniciar o comportamento. Esta definição não afeta o comportamento real da instalação da atualização.

       -   **Nunca reinicia**: O computador nunca executa um reinício do sistema após a instalação da atualização do software.
       -   **Requer sempre o reboot**: O computador executa sempre um reinício do sistema após a instalação da atualização do software.
       -   **Pode solicitar o reboot**: Depois de instalar a atualização do software, o computador solicita um reinício do sistema apenas se for necessário um reinício. O utilizador tem a opção de adiar o reinício. Este é o valor predefinido. <br /><br />

5. Na página **Pré-Requisito,** especifique os pré-requisitos que devem ser instalados num computador antes de esta atualização poder instalar. Os pré-requisitos podem ser **detectóides** ou outras atualizações. Detectóides são regras de alto nível como uma que exige que o CPU dos computadores seja um processador de 64 bits. Os detectóides também podem especificar atualizações específicas que devem ser instaladas antes de esta atualização poder instalar.

   -   Para um melhor desempenho, utilize detectóides em vez de criar regras *instaladas* e *instaladas* que realizem a mesma verificação ou ação.

   Utilize a opção de pesquisa para **atualizações de software disponíveis e detectóides** para ajudá-lo a encontrar atualizações ou detectóides específicos. Por exemplo, procure no **CPU** para encontrar os detectóides que lhe permitem limitar a instalação com base em arquitetura cpu específica.

   Pode selecionar um ou mais itens de cada vez para adicionar como pré-requisito. Ao adicionar pré-requisitos, os detectóides selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador deve satisfazer a exigência de pelo menos um membro de cada grupo que configura:

   -   Quando clicar em **Adicionar Pré-requisito,** todos os itens selecionados são adicionados a grupos separados, individuais. Para se qualificar para esta atualização, um computador deve cumprir o pré-requisito neste grupo e passar requisitos para quaisquer grupos adicionais que estejam configurados.

   -   Quando clica em **Adicionar Grupo,** todos os itens selecionados são adicionados a um único grupo. Para se qualificar para esta atualização, um computador deve cumprir pelo menos um dos requisitos pré-requisitos deste grupo e passar requisitos para quaisquer grupos adicionais que estejam configurados.

6. Na página **de Supersedence,** especifique as atualizações que são substituídas (substituídas) por esta atualização. Quando esta atualização for publicada, o Gestor de Configuração marcará cada atualização que é substituído como **Expirado**. Os clientes irão então instalar esta atualização em vez das atualizações supersed.

7. Na página **de Aplicabilidade** utilize o Editor de **Regras** para definir um conjunto de regras que determinam se um dispositivo precisa desta atualização. (Esta página é semelhante à página **instalada,** que a segue.)

   Para adicionar uma nova regra, clique em ![Nova Regra](media/newrule.png). Isto abre a página da Regra da Aplicabilidade onde pode configurar regras.

   Os tipos de regras que pode criar incluem:

   -   **Arquivo** – Utilize esta regra para exigir que um dispositivo tenha um ficheiro com propriedades que satisfaçam um ou mais critérios que especifique antes de esta atualização poder ser aplicada.

   -   **Registo –** Utilize este tipo para especificar os detalhes do registo que devem estar presentes antes de um dispositivo se qualificar para instalar esta atualização.

   -   **Sistema –** Esta regra utiliza detalhes do sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão Windows, um idioma Windows, arquitetura de processador, ou especificar uma consulta wmi para identificar o sistema operativo dos dispositivos.

   -   **Instalador de Janelas –** Utilize este tipo de regra para determinar a aplicabilidade com base num instalado . Patch de MSI ou Instalador de Janelas (. MSP). Também pode determinar se componentes ou funcionalidades específicas são instalados como parte da exigência.

       > [!IMPORTANT]  
       > Em dispositivos geridos, o Windows Update Agent não consegue detetar pacotes de instalação do Windows que são instalados por utilizador. Quando utilizar este tipo de regra, configure regras adicionais de aplicabilidade, como versões de ficheiros ou valores-chave de registo, para que o pacote do Instalador do Windows possa ser devidamente detetado independentemente de uma base por utilizador ou por sistema.

   -   **Regra guardada –** Esta opção permite encontrar e utilizar as regras criadas *no Espaço de Trabalho das Regras.*

       Depois de criar uma regra, pode usar os outros ícones para modificar a regra, e se houver várias regras, para definir relações entre essas regras.

   Quando terminar de criar e adicionar regras, clique em **OK** na caixa de diálogo **Create Rule set** para guardar esse conjunto. Em seguida, pode criar uma **nova** regra e adicioná-lo ao conjunto também.

   Quando tiver várias regras ou conjuntos de regras para adicionar a uma atualização, pode utilizar os operadores lógicos do Editor de **Regras** para determinar as condições entre as regras e em que ordem processam.

8. Na página **Instalada** utilize o 'Editor de **Regras' para** definir um conjunto de regras que determinam se um dispositivo já instalou a atualização que está a configurar. (Esta página é semelhante à página de **Aplicabilidade,** que procede a esta página.)

   Esta página do assistente suporta a configuração de regras com as mesmas opções e critérios que a página **de Aplicabilidade.**

   Quando o assistente estiver concluído, a nova atualização é adicionada a um nó no Espaço de Trabalho de **Atualizações** que é identificado pelo **nome do Fornecedor** e **produto** que utilizou para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Use o assistente Create Bundle
Como este assistente utiliza o mesmo fluxo de trabalho que o [assistente Create Update,](#use-the-create-update-wizard)utilize esse fluxo de trabalho, mas note a seguinte diferença para os pacotes:

1.  Para iniciar o assistente, na consola vá ao **Workspace updates**, e, em seguida, selecione **Bundle** a partir do separador **Home** da fita.

2.  Ao contrário do assistente create update, não existe página de Pacote ao criar um pacote.

3.  Na página **informação,** especifique detalhes sobre o pacote de atualização que estão incluídos quando a atualização for publicada ou exportada.

4.  Na página **Informação Opcional,** pode configurar detalhes que forneçam informações adicionais sobre o pacote de atualização. As opções disponíveis são as mesmas que para criar uma atualização. No entanto, as opções para Impact e Restart Behavior não estão disponíveis, uma vez que não se aplicam a pacotes.

5.  Na página **Pré-Requisito,** especifique os pré-requisitos que devem ser instalados num computador antes de este pacote poder instalar. Estas regras são as mesmas que se vê nas atualizações individuais.

6.  Na página **de Supersedence,** especifique as atualizações que são substituídas (substituídas) por este pacote de atualização. Estas regras são as mesmas que se vê nas atualizações individuais.

7.  Na página **dos Membros,** selecione atualizações para adicionar ao pacote de atualizações. Apenas estão disponíveis atualizações que criou ou importou para updates Publisher.

Quando o assistente estiver concluído, o novo pacote de atualizações é adicionado a um nó no Espaço de Trabalho de **Atualizações** que é identificado pelo nome do **Fornecedor** que utilizou para o pacote de atualização.
