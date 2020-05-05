---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724112"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a>Aplicar atualizações de software para uma imagem

> [!Note]  
> Esta secção aplica-se tanto às **imagens do OS** como aos pacotes de **atualização do OS.** Utiliza o termo geral "imagem" para se referir ao ficheiro de imagem do Windows (WIM). Ambos os objetos têm uma WIM, que contém ficheiros de instalação do Windows. As atualizações de software aplicam-se a estes ficheiros em ambos os objetos. O comportamento deste processo é o mesmo entre ambos os objetos.  

Todos os meses há novas atualizações de software aplicáveis à imagem. Antes de poder aplicar atualizações de software, precisa dos seguintes pré-requisitos:

- Um software atualiza a infraestrutura  
- Atualizações de software sincronizadas com sucesso  
- Descarreguei as atualizações de software para a biblioteca de conteúdos no servidor do site  

Para mais informações, consulte [a implementação](../../../sum/deploy-use/deploy-software-updates.md)de atualizações de software .  

Aplique atualizações de software aplicáveis a uma imagem num horário especificado. Este processo é por vezes chamado *de manutenção offline*. Neste horário, o Gestor de Configuração aplica as atualizações de software selecionadas à imagem. Pode também redistribuir a imagem atualizada para pontos de distribuição.

> [!Important]  
> Embora possa selecionar qualquer atualização de software aplicável à imagem com base na versão, o DISM só pode aplicar certos tipos de atualizações à imagem. O ficheiro **OfflineServicingMgr.log** mostra `Not applying this update binary, it is not supported`a seguinte entrada: .<!-- SCCMDocs issue 1324 -->

A base de dados do site armazena informações sobre a imagem, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software que aplica à imagem desde que foi inicialmente adicionada também estão armazenadas na base de dados do site. Quando inicia o assistente para aplicar atualizações de software, ele recupera a lista de atualizações de software aplicáveis que o site ainda não se aplica à imagem. O Gestor de Configuração copia as atualizações de software que seleciona a partir da biblioteca de conteúdos no servidor do site. Em seguida, aplica as atualizações de software à imagem.  

### <a name="servicing-process"></a>Processo de manutenção

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos,** e depois selecione imagens **do sistema operativo** ou **pacotes de atualização**do sistema operativo.  

2. Selecione o objeto para aplicar atualizações de software.  

3. Na fita, selecione **'Atualizações de horários'** para iniciar o assistente.  

4. Na página **Choose Updates,** selecione as atualizações de software para aplicar à imagem. Pode levar algum tempo para que a lista de atualizações apareça no assistente. Utilize o **Filtro** para procurar cordas nos metadados. Utilize a lista de abandono da **arquitetura do Sistema** para filtrar em **X86**, **X64**, ou **All**. Pode selecionar uma, muitas ou todas as atualizações da lista. Quando terminar de selecionar atualizações, selecione **Next**.  

5. Na página **Definir Agendamento** , especifique as seguintes definições e clique em **Seguinte**.  

    1. **Horário**: Especifique a programação para quando o site aplicar as atualizações do software à imagem.  

    2. **Continuar a trabalhar**: Selecione esta opção para continuar a aplicar atualizações de software na imagem mesmo quando houver um erro.  

    3. **Atualizar pontos**de distribuição com a imagem : Selecione esta opção para atualizar a imagem nos pontos de distribuição após o site aplicar as atualizações do software.  

6. Complete o Assistente de Atualizações de Horários.  

> [!NOTE]  
> Para minimizar o tamanho da carga útil, a manutenção de pacotes de upgrade de OS e imagens de SO remove a versão mais antiga.  

### <a name="servicing-operations"></a>Operações de manutenção

Na consola do Gestor de Configuração, no nó de Pacotes de **Atualização** **OS** ou oss, adicione as seguintes colunas à vista:

- Data de **Atualizações Agendadas**: Esta propriedade mostra o próximo horário que definiu.  
- Estado das **Atualizações Programadas**: Esta propriedade mostra o estado. Por exemplo, **Bem-sucedido** ou **em processo.**  

Selecione um objeto de imagem específico e, em seguida, mude para o **separador 'Estado da actualização'** no painel de detalhes. Este separador mostra a lista de atualizações na imagem.

Selecione um objeto de imagem específico e selecione **Propriedades** na fita. O separador **Atualizações Instaladas** mostra a lista de atualizações na imagem. O separador **de manutenção** é uma visão apenas para leitura do calendário de manutenção atual e das atualizações que você tem agendado para se candidatar.

Quando o estado estiver **em processo,** pode selecionar **as Atualizações Agendadas** na fita. Esta ação cancela o processo de manutenção ativa.

Para resolver este processo, consulte os ficheiros **OfflineServicingMgr.log** e **dism.log** no servidor do site. Para mais informações, consulte [ficheiros De registo](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a>Especifique a unidade para manutenção de imagem offline do OS

<!--1358924-->

A partir da versão 1810, especifique a unidade que o Gestor de Configuração utiliza durante a manutenção offline das imagens de OS. Este processo pode consumir uma grande quantidade de espaço em disco com ficheiros temporários. Esta opção dá-lhe flexibilidade para selecionar a unidade a utilizar.

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.** Na fita, clique em **Configurar componentes** do site e selecione **Implementação**do sistema operativo .  

2. No separador de **manutenção offline,** especifique a opção para uma unidade local a utilizar através de **uma manutenção offline de imagens**.  

Por predefinição, esta definição é **Automática**. Com este valor, o Gestor de Configuração seleciona a unidade em que está instalada.

Se selecionar uma unidade que não existe no servidor do site, o Gestor de Configuração comporta-se da mesma forma que selecione **Automatic**.

Durante a manutenção offline, o Gestor de `<drive>:\ConfigMgr_OfflineImageServicing`Configuração armazena ficheiros temporários na pasta, . Também monta a imagem de OS nesta pasta.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a>Manutenção de imagem otimizada

<!--3555951-->

A partir da versão 1902, quando aplica atualizações de software a uma imagem de OS, há uma nova opção para otimizar a saída removendo quaisquer atualizações supersed. A otimização da manutenção offline aplica-se apenas a imagens com um único índice.

Ao agendar o site para aplicar atualizações de software a uma imagem de OS, utiliza a ferramenta de linha de comando de implementação de imagem e gestão do Windows (DISM). Durante o processo de manutenção, esta alteração introduz os seguintes dois passos adicionais:  

- Executa dISM contra a imagem offline `/Cleanup-Image /StartComponentCleanup /ResetBase`montada com os parâmetros . Se este comando falhar, o atual processo de manutenção falha. Não comete alterações na imagem.  

- Depois de o Gestor de Configuração comprometer alterações na imagem e desmontá-la do sistema de ficheiros, exporta a imagem para outro ficheiro. Este passo utiliza o parâmetro `/Export-Image`DISM . Remove ficheiros desnecessários da imagem, o que reduz o tamanho.  

A Microsoft recomenda que aplique regularmente atualizações nas suas imagens offline. Não precisa usar esta opção sempre que serve uma imagem. Ao fazer este processo todos os meses, esta nova opção proporciona-lhe a maior vantagem ao usá-lo ao longo do tempo. Para mais informações, consulte [as recomendações para instalar](../../understand/install-software-updates.md#recommendations)o passo de Atualizações de Software .

Embora esta opção ajude a reduzir o tamanho total da imagem servida, demora mais tempo a concluir o processo. Utilize o assistente para agendar a manutenção durante os horários convenientes. Também requer armazenamento adicional no servidor do site. Pode personalizar o site para utilizar uma localização alternativa. Para mais informações, consulte [Especifique a unidade para manutenção de imagem de osso offline](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Processo para otimizar o serviço de imagem

1. Inicie o [processo de manutenção](#servicing-process).  

2. Na página **'Agendar conjunto',** selecione a opção de **remover atualizações supersed após a atualização da imagem**. Esta opção não está ativada automaticamente. Se a imagem tiver mais de um índice, não pode usar esta opção.  

3. Para agendar a manutenção da imagem, complete o assistente.  

Validar e monitorizar o processo utilizando o **offlineServicing.log**.
