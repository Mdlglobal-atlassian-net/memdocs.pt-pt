---
title: Criar suportes de dados pré-configurados
titleSuffix: Configuration Manager
description: Utilize meios pré-encenados no Gestor de Configuração para simplificar a implementação do Windows em vários cenários.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d5219b518d46ccca174c7aa3fef62fe3334def35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711113"
---
# <a name="create-prestaged-media"></a>Criar suportes de dados pré-configurados

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os meios de comunicação pré-encenados no 'Gestor de Configuração' são um ficheiro Windows Image (WIM). Pode ser instalado num computador de metal nu pelo fabricante ou no seu centro de paragem que não esteja ligado ao ambiente do Gestor de Configuração de Produção. Os meios de comunicação pré-encenados contêm a imagem de arranque usada para iniciar o computador de destino e a imagem de OS que é aplicada ao computador de destino. Também pode especificar aplicações, pacotes e pacotes de controladores para incluir como parte do suporte de dados pré-configurado. A sequência de tarefas que implanta o Sistema operativo não está incluída nos meios de comunicação. O suporte de dados pré-configurado é aplicado no disco rígido do computador novo antes do seu envio para o utilizador final.

Utilize meios pré-encenados para os seguintes cenários de implantação do SO:  

- [Criar uma imagem de um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Implementar o Windows to Go](deploy-windows-to-go.md)  


## <a name="usage"></a>Utilização

Quando o computador começa pela primeira vez depois de ter aplicado os meios pré-encenados, o computador começa no Windows PE. Liga-se a um ponto de gestão para localizar a sequência de tarefas que completa o processo de implementação do SO. Ao implementar uma sequência de tarefas que utiliza meios pré-encenados, o cliente verifica primeiro a cache da sequência de tarefas local para obter conteúdo válido. Se o conteúdo não puder ser encontrado ou tiver sido revisto, o cliente descarrega o conteúdo a partir de um ponto de distribuição ou de um par.  


## <a name="prerequisites"></a>Pré-requisitos

Antes de criar meios pré-encenados utilizando o Assistente de Mídia de Sequência de Tarefas Create, certifique-se de que todas as condições estão reunidas.

### <a name="boot-image"></a>Imagem de arranque

Considere os seguintes pontos sobre a imagem de arranque que utiliza na sequência de tarefas para implantar o Sistema Operativo:

- A arquitetura da imagem de arranque deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.
- Certifique-se de que a imagem de arranque contém os controladores de rede e armazenamento que são necessários para fornecer o computador de destino.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Criar uma sequência de tarefas para implantar um SO

Como parte dos meios pré-encenados, especifique a sequência de tarefas para implantar o Sistema Operativo. Para mais informações, consulte Criar uma sequência de [tarefas para instalar um OS](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuir todo o conteúdo associado à sequência de tarefas

Distribua todos os conteúdos que a sequência de tarefas requer para pelo menos um ponto de distribuição. Este conteúdo inclui a imagem de arranque, a imagem do OS e outros ficheiros associados. O assistente recolhe o conteúdo a partir do ponto de distribuição quando cria os meios pré-encenados.

A sua conta de utilizador precisa, pelo **menos, de ler** os direitos de acesso à biblioteca de conteúdos nesse ponto de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Disco rígido no computador de destino

O disco rígido do computador de destino deve ser formatado antes de lhe aplicarem os meios de comunicação pré-encenados. Se o disco rígido não for formatado quando os meios de comunicação são aplicados, a sequência de tarefas que implanta o Sistema operativo falha quando tenta ligar o computador de destino.

> [!NOTE]  
> O Assistente de Mídia de sequência de tarefas Create define a seguinte condição variável de sequência de tarefas nos meios de comunicação: **_SMSTSMediaType = OEMMedia**. Pode utilizar esta mesma condição na sua sequência de tarefas.  


## <a name="process"></a>Processo

 > [!NOTE]  
 > Para os ambientes PKI, uma vez que a Root CA é especificada no local primário, certifique-se de que os meios pré-encenados são criados no local primário. O site CAS não dispõe da informação Root CA para criar corretamente os meios pré-encenados.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione Criar Meios de Sequência de **Tarefas**. Esta ação inicia o Assistente de Mídia de Sequência de Tarefas Create Task Sequence.  

3. Na página **Select Media Type,** especifique as seguintes opções:  

    - Selecione **Suporte de dados pré-configurado**.  

    - Opcionalmente, se pretender apenas permitir que o Sistema operativo seja implantado sem necessitar de entrada do utilizador, selecione Permitir a **implementação do sistema operativo sem supervisão**.  

        > [!IMPORTANT]  
        > Ao selecionar esta opção, o utilizador não é solicitado para informações de configuração de rede ou para sequências de tarefas opcionais. Se configurar os meios de proteção de palavras-passe, o utilizador ainda é solicitado para obter uma palavra-passe.  

4. Na página de **Media Management,** especifique uma das seguintes opções:  

    - **Meios dinâmicos**: Permitir que um ponto de gestão redirecione os meios de comunicação para outro ponto de gestão, com base na localização do cliente nos limites do site.  

    - Meios de comunicação **baseados no site**: Os meios de comunicação apenas contactam o ponto de gestão especificado.  

5. Na página **Media Properties,** especifique as seguintes informações:  

    - **Criado por**: especifique quem criou o suporte de dados.  

    - **Versão**: especifique o número de versão do suporte de dados.  

    - **Comentário**: especifique uma descrição exclusiva da finalidade do suporte de dados.  

    - **Ficheiro do suporte de dados**: especifique o nome e o caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo: `\\servername\folder\outputfile.wim`  

    - **Pasta de encenação**<!--1359388-->: O processo de criação de meios de comunicação pode requerer muito espaço de condução temporária. Por defeito, esta localização é `%UserProfile%\AppData\Local\Temp`semelhante ao seguinte caminho: . A partir da versão 1902, para lhe dar maior flexibilidade com onde armazenar estes ficheiros temporários, altere este valor para outra unidade e caminho.  

6. Na página **de Segurança,** especifique as seguintes opções:  

    - **Ativar suporte de computador desconhecido**: Permitir que os meios de comunicação implementem um SISTEMA para um computador que não seja gerido pelo Gestor de Configuração. Não há registo destes computadores na base de dados do Diretor de Configuração. Para mais informações, consulte [Prepare-se para implementações de computadordesconhecidas](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Proteja os meios com uma palavra-passe**: Introduza uma senha forte para ajudar a proteger os meios de acesso não autorizados. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados pré-configurado.  

        > [!IMPORTANT]  
        > Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados pré-configurado.  
 
    - Para comunicações HTTP, selecione **Criar certificado de mídia auto-assinado**. Em seguida, especifique a data de início e expiração do certificado.  
    
        > [!NOTE] 
        > Se selecionar esta opção, os pontos de gestão HTTPS não estarão disponíveis para seleção na página de **imagem Boot** deste assistente.

    - Para comunicações HTTPS, selecione **certificado Import PKI**. Em seguida, especifique o certificado de importação e a sua palavra-passe.  

        Para obter mais informações sobre este certificado de cliente que as imagens de arranque utilizem, consulte [os requisitos do certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Afinidade do dispositivo do utilizador**: Para apoiar a gestão centrada no utilizador no Gestor de Configuração, especifique como pretende que os meios de comunicação associem os utilizadores ao computador de destino. Para obter mais informações sobre como a implementação do OS suporta a afinidade do dispositivo do utilizador, consulte [os utilizadores associados com um computador](../get-started/associate-users-with-a-destination-computer.md)de destino .  

        - **Permitir a finidade**do dispositivo do utilizador com a aprovação automática : Os meios de comunicação associam automaticamente os utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o SISTEMA. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o S para o computador de destino.  

        - **Permitir a afinidade do utilizador pendente da aprovação do administrador**: Os meios de comunicação associam os utilizadores ao computador de destino após a aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o SISTEMA. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do SISTEMA.  

        - **Não permita a finção**do dispositivo do utilizador : Os meios de comunicação não associam os utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa os utilizadores ao computador de destino quando implementa o SISTEMA.  

7. Na página da Sequência de **Tarefas,** selecione a sequência de tarefas que corre no computador de destino. Verifique a lista de conteúdos referenciados pela sequência de tarefas.  

    - **Detete dependências de aplicações associadas e adicione-as a este meio de comunicação**: Adicione também conteúdo aos meios de comunicação para dependências de aplicações.  

        > [!TIP]  
        > Se não vir as dependências esperadas da aplicação, desmarque e, em seguida, reselecione esta opção para atualizar a lista.  

8. Na página de **imagem Boot,** especifique as seguintes opções:  

    > [!IMPORTANT]  
    > A arquitetura da imagem de arranque que distribui deve ser adequada para a arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86.  

    - **Imagem de arranque**: Selecione a imagem de arranque para iniciar o computador de destino.  

    - **Ponto de distribuição**: Selecione o ponto de distribuição que tem a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        > A sua conta de utilizador precisa, pelo menos, **de ler** permissões para a biblioteca de conteúdos no ponto de distribuição.  

    - **Ponto de gestão**: Apenas para *meios baseados no site,* selecione um ponto de gestão de um site primário.  

    - **Pontos de gestão associados**: Apenas para *meios dinâmicos*, selecione os pontos de gestão do site primário a utilizar e uma ordem prioritária para a comunicação inicial.  

        > [!NOTE]  
        > Os pontos de gestão ativados HTTPS só serão apresentados quando um certificado PKI for especificado na página de **Segurança** deste assistente.  

9. Na página **Imagens,** especifique as seguintes opções:  

    - **Pacote de imagem**: Especifique a imagem de OS a utilizar. Para mais informações, consulte [Gerir imagens do OS](../get-started/manage-operating-system-images.md).  

    - **Índice de imagem**: Se o pacote contiver múltiplas imagens de SO, especifique o índice da imagem a ser implantado.  

    - **Ponto de distribuição**: Especifique o ponto de distribuição que tem o pacote de imagem S. O assistente obtém a imagem de Sdo do ponto de distribuição e escreve-a para os meios de comunicação.  

10. Na página **Select Application,** selecione aplicações adicionais para adicionar ao ficheiro de mídia pré-encenado.  

11. Na página **Select Package,** selecione pacotes adicionais para adicionar ao ficheiro de mídia pré-encenado.  

12. Na página **Select Driver Package,** selecione pacotes adicionais de controlador para adicionar ao ficheiro de mídia pré-encenado.  

13. Na página Pontos de **Distribuição,** selecione um ou mais pontos de distribuição a partir dos quais obter conteúdo.  

    O Gestor de Configuração apenas exibe pontos de distribuição que tenham o conteúdo. Distribua todos os conteúdos associados à sequência de tarefas para pelo menos um ponto de distribuição antes de continuar. Depois de distribuir o conteúdo, refresque a lista de pontos de distribuição. Remova quaisquer pontos de distribuição que já tenha selecionado nesta página, vá para a página anterior e, em seguida, volte para a página Pontos de **Distribuição.** Em alternativa, reinicie o assistente. Para mais informações, consulte [Distribuir conteúdo referenciado por uma sequência](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) de tarefas e gerir a [infraestrutura](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)de conteúdo e conteúdo .  

14. Na página de **Personalização,** especifique as seguintes opções:  

    - Adicione quaisquer variáveis que a sequência de tarefas utilize.  

    - **Ativar**o comando prestart : Especifique quaisquer comandos prestart que pretenda executar antes da sequência de tarefas ser executada. Os comandos prestart são um script ou um executável que pode interagir com o utilizador no Windows PE antes da sequência de tarefas ser executada. Para mais informações, consulte os [comandos da Prestat para meios](../understand/prestart-commands-for-task-sequence-media.md)de sequência de tarefas .  

        > [!TIP]  
        > Durante a criação de meios de comunicação, a sequência de tarefas escreve o id do pacote e a linha de comando prestart, incluindo o valor para quaisquer variáveis de sequência de tarefas, para o ficheiro **CreateTSMedia.log** no computador que executa a consola Do Gestor de Configuração. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

        Se o comando prestart necessitar de qualquer conteúdo, selecione a opção **de Incluir ficheiros para o comando prestart**.  

15. Conclua o assistente.  


## <a name="next-steps"></a>Passos seguintes

[Criar uma imagem de um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
