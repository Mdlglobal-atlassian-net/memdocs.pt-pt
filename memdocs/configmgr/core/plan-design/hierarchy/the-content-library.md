---
title: A biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Conheça a biblioteca de conteúdos que o Gestor de Configuração utiliza para reduzir o tamanho global dos conteúdos distribuídos.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 253de522937e48fa1f3939c7303faf7e43e4e047
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720899"
---
# <a name="the-content-library-in-configuration-manager"></a>A biblioteca de conteúdos em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A biblioteca de conteúdos é uma loja de conteúdo de uma instância única no Gestor de Configuração. O site usa-o para reduzir o tamanho total do corpo combinado de conteúdo que distribui. A biblioteca de conteúdos armazena todos os ficheiros de conteúdo para implementações de software, por exemplo: atualizações de software, aplicações e implementações de OS.  

- O site cria e mantém automaticamente uma cópia da biblioteca de conteúdos em cada servidor do site e em cada ponto de distribuição.  

- Antes de o Gestor de Configuração adicionar ficheiros de conteúdo ao servidor do site ou cópias dos ficheiros para pontos de distribuição, verifica se cada ficheiro de conteúdo já se encontra na biblioteca de conteúdos.  

- Se o ficheiro de conteúdo estiver disponível, o Gestor de Configuração não copia o ficheiro. Em vez disso, associa o ficheiro de conteúdo existente à aplicação ou embalagem.  

Nos servidores de pontos de distribuição, configure as seguintes opções:

- Uma ou mais unidades de disco em que pretende criar a biblioteca de conteúdos.  

- Uma prioridade para cada unidade que usa.  

O Gestor de Configuração copia ficheiros de conteúdo para a unidade com a maior prioridade até que essa unidade contenha menos de uma quantidade mínima de espaço livre que especifica.  

- Configura as definições de unidade durante a instalação do ponto de distribuição.  

- Não é possível configurar as definições de unidade nas propriedades do ponto de distribuição após a instalação ter terminado.  

Para obter mais informações sobre como configurar as definições de unidade para o ponto de distribuição, consulte Gerir a infraestrutura de [conteúdo e conteúdo](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Para mover a biblioteca de conteúdos para um local diferente num ponto de distribuição após a instalação, utilize a ferramenta de transferência da Biblioteca de **Conteúdos** nas ferramentas do Gestor de Configuração. Para mais informações, consulte a ferramenta de transferência da Biblioteca de [Conteúdos](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Sobre a biblioteca de conteúdos no site da administração central

Por padrão, o Gestor de Configuração cria uma biblioteca de conteúdos no site da administração central quando o site é instalado. A biblioteca de conteúdos é colocada na unidade do servidor do site que tem o espaço de disco mais livre. Como não se pode instalar um ponto de distribuição no site da administração central, não se pode dar prioridade às unidades de utilização pela biblioteca de conteúdos. Semelhante à biblioteca de conteúdos em outros servidores do site e em pontos de distribuição, quando a unidade que contém a biblioteca de conteúdos fica sem espaço de disco disponível, a biblioteca de conteúdos estende-se automaticamente à próxima unidade disponível.  

O Gestor de Configuração utiliza a biblioteca de conteúdos no site da administração central nos seguintes cenários:  

- Cria conteúdo no site da administração central  

- Migra conteúdo de outro site do Gestor de Configuração e atribui o site da administração central como o site que gere esse conteúdo  

> [!NOTE]  
> Quando cria conteúdo num site primário e depois distribui-o para um site primário diferente ou para um site secundário abaixo de um site primário diferente, o site da administração central armazena temporariamente esse conteúdo na caixa de entrada do programador no site da administração central, mas não adiciona esse conteúdo à sua biblioteca de conteúdos.  

Utilize as seguintes opções para gerir a biblioteca de conteúdos no site da administração central:  

- Para evitar que a biblioteca de conteúdos seja instalada numa unidade específica, crie um ficheiro vazio chamado **no_sms_on_drive.sms**. Copie-o para a raiz da unidade antes da criação da biblioteca de conteúdos.  

- Depois da criação da biblioteca de conteúdos, utilize a ferramenta de transferência da Biblioteca de **Conteúdos** a partir das ferramentas do Gestor de Configuração para gerir a localização da biblioteca de conteúdos. Para mais informações, consulte a ferramenta de transferência da Biblioteca de [Conteúdos](../../support/content-library-transfer.md).  

> [!Note]  
> Os pontos de distribuição em nuvem não usam armazenamento de uma instância única. O site encripta pacotes antes de enviar para o Azure, e cada pacote tem uma chave encriptada única. Mesmo que dois ficheiros fossem idênticos, as versões encriptadas não seriam as mesmas.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a>Configure uma biblioteca de conteúdos remotos para o servidor do site

<!--1357525-->
Começando na versão 1806, para configurar a [alta disponibilidade](../../servers/deploy/configure/site-server-high-availability.md) do servidor do site ou para libertar o espaço de disco rígido na sua administração central ou servidores de sites primários, realocar a biblioteca de conteúdos para outro local de armazenamento. Mova a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerantes a falhas numa rede de área de armazenamento (SAN). Um SAN é recomendado, porque é altamente disponível, e fornece armazenamento elástico que cresce ou encolhe ao longo do tempo para satisfazer os seus requisitos de conteúdo em mudança. Para mais informações, consulte [Opções de Alta Disponibilidade](../../servers/deploy/configure/site-server-high-availability.md).

Uma biblioteca de conteúdos remotos é um pré-requisito para a elevada disponibilidade do servidor do [site.](../../servers/deploy/configure/site-server-high-availability.md)

> [!Note]  
> Esta ação apenas move a biblioteca de conteúdos no servidor do site. Não afeta a localização da biblioteca de conteúdos nos pontos de distribuição. 

> [!Tip]  
> Também planeia gerir o conteúdo de origem de pacotes, que é externo à biblioteca de conteúdos. Todos os objetos de software no Gestor de Configuração têm uma fonte de pacote numa partilha de rede. Considere centralizar todas as fontes para uma única parte, mas certifique-se de que este local é redundante e altamente disponível.
>
> Se mover a biblioteca de conteúdos para o mesmo volume de armazenamento que as fontes do seu pacote, não pode marcar este volume para a duplicação de dados. Embora a biblioteca de conteúdos suporte a duplicação de dados, o volume de fontes de pacote não o suporta. Para mais informações, consulte [a desduplicação de Dados](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Pré-requisitos  

- A conta do computador do servidor do site precisa de permissões de **controlo completos** para o caminho da rede para o qual está a mover a biblioteca de conteúdos. Esta permissão aplica-se tanto à parte como ao sistema de ficheiros. Não são instalados componentes no sistema remoto.

- O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também usa a biblioteca de conteúdos, e esta função não suporta uma biblioteca de conteúdos remotos. Depois de mover a biblioteca de conteúdos, não pode adicionar a função de ponto de distribuição ao servidor do site.  

> [!Important]  
> Não reutilize uma localização partilhada da rede entre vários sites. Por exemplo, não use o mesmo caminho tanto para um site de administração central como para um local primário para crianças. Esta configuração tem o potencial de corromper a biblioteca de conteúdos, e exigir que a reconstrua.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Processo de gestão da biblioteca de conteúdos

1. Crie uma pasta numa partilha de rede como alvo para a biblioteca de conteúdos. Por exemplo, `\\server\share\folder`.  

    > [!Warning]  
    > Não reutilize uma pasta existente com conteúdo. Por exemplo, não utilize a mesma pasta que as fontes do seu pacote. Antes de copiar a biblioteca de conteúdos, o Gestor de Configuração remove qualquer conteúdo existente da localização que especifica.  

2. Na consola 'Gestor de Configuração', mude para o espaço de trabalho da **Administração.** Expandir a Configuração do **Site,** selecionar o nó **dos Sites** e selecionar o site. No separador **Resumo** na parte inferior do painel de detalhes, note uma nova coluna para a **Biblioteca de Conteúdos**.  

3. Selecione Gerir a **Biblioteca de Conteúdos** na fita.  

4. Na janela Manage Content Library, o campo **Current Location** mostra a unidade e o caminho locais. Introduza um caminho de rede válido para a **Nova Localização**. Este caminho é o local para onde o site move a biblioteca de conteúdos. Deve incluir um nome de pasta que já `\\server\share\folder`existe na parte, por exemplo, . Selecione **OK**.  

5. Note o valor **de Estado** na coluna da Biblioteca de Conteúdos no separador Resumo do painel de detalhes. Atualiza para mostrar o progresso do site na mudança da biblioteca de conteúdos.  

   - Enquanto **em curso,** o valor **Move Progress (%)** mostra a percentagem completa.  

        > [!Note]  
        > Se tiver uma grande biblioteca de `0%` conteúdos, poderá ver progressos na consola por um tempo. Por exemplo, com uma biblioteca de 1 TB, tem `1%`de copiar 10 GB antes de aparecer . Reveja **distmgr.log**, que mostra o número de ficheiros e bytes copiados. A partir da versão 1810, o ficheiro de registo também mostra um tempo estimado restante.

   - Se houver um estado de erro, o estado mostra o erro. Erros comuns incluem **acesso negado** ou **disco completo**.  

   - Quando estiver concluído, mostra **Completo**.  

     Consulte o **distmgr.log** para obter mais detalhes. Para mais informações, consulte os [registos](log-files.md#BKMK_SiteSiteServerLog)do servidor do servidor do Site e do servidor do site .  

Para obter mais informações sobre este processo, consulte [Flowchart - Gerir](manage-content-library-flowchart.md)a biblioteca de conteúdos .

O site *realmente copia* os ficheiros da biblioteca de conteúdos para o local remoto. Este processo não elimina os ficheiros da biblioteca de conteúdos na localização original do servidor do site. Para libertar espaço, um administrador deve eliminar manualmente estes ficheiros originais.

Se a biblioteca de conteúdos original abranger duas unidades, é fundida numa única pasta no novo destino.

A partir da versão 1810, durante o processo de cópia, os componentes do Gestor **de Despooler** e **Distribuição** não processam novos pacotes. Esta ação garante que o conteúdo não é adicionado à biblioteca enquanto se move. Independentemente disso, agende esta mudança durante a manutenção do sistema.

Se precisar de mover a biblioteca de conteúdos de volta para o servidor do site, repita este processo, mas introduza uma unidade local e caminho para a **Nova Localização**. Deve incluir um nome de pasta que já `D:\SCCMContentLib`existe na unidade, por exemplo, . Quando o conteúdo original ainda existe, o processo move rapidamente a configuração para o local local para o servidor do site.

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, utilize a ferramenta de transferência da **Biblioteca de Conteúdos.** Para mais informações, consulte a ferramenta de transferência da Biblioteca de [Conteúdos](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>Dentro da biblioteca de conteúdos

> [!Warning]  
> A secção seguinte é fornecida apenas para fins informantes. Não altere, adicione ou remova quaisquer ficheiros ou pastas na biblioteca de conteúdos. Fazê-lo poderia corromper pacotes, conteúdos ou a biblioteca de conteúdos como um todo. Se suspeitar de dados em falta, corruptos ou inválidos, utilize a funcionalidade de validação na consola Do Gestor de Configuração para detetar tais problemas. Em seguida, redistribua o conteúdo afetado para corrigir os problemas.

Por predefinição, a biblioteca de conteúdos é armazenada na raiz de uma unidade numa pasta chamada **SCCMContentLib**. Esta pasta é partilhada por padrão como **SCCMContentLib$**. A pasta e a partilha têm permissões restritas para evitar danos acidentais. Todas as alterações devem ser feitas a partir da consola 'Gestor de Configuração'. Dentro desta pasta estão os seguintes objetos:  

- A biblioteca de pacotes (pasta**PkgLib):** Informação sobre quais os pacotes presentes no ponto de distribuição.  

- A biblioteca de dados (pasta**DataLib):** Informação sobre a estrutura original dos pacotes.  

- A biblioteca de ficheiros (pasta**FileLib):** Os ficheiros originais da embalagem. Esta pasta é tipicamente o que utiliza a maior parte do armazenamento.  

![Visão geral do diagrama da biblioteca de conteúdos do Gestor de Configuração](media/content-library-overview.png)

> [!Tip]  
> Utilize a ferramenta **Do Explorador** da Biblioteca de Conteúdos a partir das ferramentas do Gestor de Configuração para navegar nos conteúdos da biblioteca de conteúdos. Não é possível utilizar esta ferramenta para modificar o conteúdo. Fornece uma visão do que está presente, bem como permite a validação e redistribuição. Para mais informações, consulte o Explorador da Biblioteca de [Conteúdos.](../../support/content-library-explorer.md)  

### <a name="package-library"></a>Biblioteca de pacotes

A pasta da biblioteca de pacotes, **PkgLib,** inclui um ficheiro para cada pacote distribuído ao ponto de distribuição. O nome do ficheiro é o `ABC00001.INI`ID do pacote, por exemplo, . Neste ficheiro da `[Packages]` secção encontra-se uma lista de IDs de conteúdo que fazem parte do pacote, bem como outras informações, como a versão. Por exemplo, **o ABC00001** é um pacote legado na versão **1**. O ID de conteúdo `ABC00001.1`neste ficheiro é .

### <a name="data-library"></a>Biblioteca de dados

A pasta da biblioteca de dados, **DataLib,** inclui um ficheiro e uma pasta para cada um dos conteúdos em cada pacote. Por exemplo, este ficheiro `ABC00001.1.INI` e `ABC00001.1`pasta são nomeados e, respectivamente. O ficheiro inclui informações para validação. A pasta recria a estrutura da pasta a partir do pacote original.

Os ficheiros na biblioteca de dados são substituídos por ficheiros INI com o nome do ficheiro original na embalagem. Por exemplo, `MyFile.exe.INI`. Estes ficheiros incluem informações sobre o ficheiro original, tais como o tamanho, tempo modificado e o haxixe. Use os primeiros quatro caracteres do haxixe para localizar o ficheiro original na biblioteca de ficheiros. Por exemplo, o haxixe em MyFile.exe.INI é **DEF98765**, e os primeiros quatro caracteres são **DEF9**.

### <a name="file-library"></a>Biblioteca de arquivos

Se a biblioteca de conteúdos se estender por várias unidades, os ficheiros do pacote podem estar na pasta da biblioteca de ficheiros, **FileLib,** em qualquer uma destas unidades.

Localize um ficheiro específico utilizando os primeiros quatro caracteres do haxixe encontrado na biblioteca de dados. Dentro da pasta da biblioteca de ficheiros estão muitas pastas, cada uma com um nome de quatro caracteres. Encontre a pasta que corresponde aos quatro primeiros caracteres do hash. Uma vez encontrado esta pasta, inclui um ou mais conjuntos de três ficheiros. Estes ficheiros partilham o mesmo nome, mas um tem a extensão INI, um tem a extensão SIG, e um não tem extensão de ficheiro. O ficheiro original é aquele sem extensão cujo nome é igual ao haxixe da biblioteca de dados.

Por exemplo, a pasta `DEF98765.INI` `DEF98765.SIG` **DEF9** inclui , e `DEF98765`. `DEF98765`é o `MyFile.exe`original. O ficheiro INI inclui uma lista de "utilizadores" ou iDs de conteúdo que partilham o mesmo ficheiro. O site não remove um ficheiro a menos que todos estes conteúdos também sejam removidos.

### <a name="drive-spanning"></a>Extensão de unidade

A biblioteca de conteúdos pode ser atravessada por várias unidades. Escolhe estas unidades ao criar o ponto de distribuição. Por predefinição, o Gestor de Configuração escolhe automaticamente as unidades ao abranger a biblioteca de conteúdos.

Quando escolher as unidades, selecione uma unidade primária e secundária. O site armazena todos os metadados na unidade principal. Só atravessa a biblioteca de ficheiros até à unidade secundária. O nome de partilha da pasta para unidades secundárias inclui a letra de unidade. Por exemplo, se D: e E: forem unidades secundárias para a biblioteca de conteúdos, os nomes das ações são **SCCMContentLibD$** e **SCCMContentLibE$**.

Se escolheu a opção **Automática,** o Gestor de Configuração seleciona a unidade com o espaço gratuito mais disponível como unidade principal. Armazena todos os metadados desta unidade. O site só abrange a biblioteca de ficheiros até unidades secundárias.

Especifica um valor de espaço de reserva durante a configuração. O Gestor de Configuração tenta utilizar um disco secundário uma vez que o melhor disco disponível tenha apenas este valor de espaço de reserva deixado livre. Cada vez que uma nova unidade é selecionada para utilização, a unidade com o espaço livre mais disponível é selecionada.

Não é possível especificar que um ponto de distribuição deve usar todas as unidades, exceto um conjunto específico. Evite este comportamento criando um ficheiro vazio na `NO_SMS_ON_DRIVE.SMS`raiz da unidade, chamada . Coloque este ficheiro antes de o Select Manager selecionar a unidade para utilização. Se o Gestor de Configuração detetar este ficheiro na raiz da unidade, não utiliza a unidade para a biblioteca de conteúdos.


## <a name="troubleshooting"></a>Resolução de problemas

As seguintes dicas podem ajudá-lo a resolver problemas com a biblioteca de conteúdos:  

- Reveja os registos no servidor do site **(distmgr.log** e **PkgXferMgr.log**) e o ponto de distribuição **(smsdpprov.log**) para obter quaisquer indicações para as falhas.  

- Utilize a ferramenta Do Explorador da Biblioteca de [Conteúdos.](../../support/content-library-explorer.md)  

- Verifique se existem bloqueios de ficheiros por outros processos, como software antivírus. Exclua a biblioteca de conteúdos em todas as unidades de antivírus automáticos, bem como o diretório de encenação temporária, **SMS_DP$,** em cada unidade.  

- Para ver se existem desajustes de hash, valide o pacote a partir da consola 'Gestor de Configuração'.  

- Como última opção, redistribua o conteúdo. Esta ação deve resolver a maioria das questões.  
