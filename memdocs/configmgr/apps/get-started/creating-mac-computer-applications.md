---
title: Criar aplicações para computadores Mac
titleSuffix: Configuration Manager
description: Veja quais as considerações que deve ter em conta quando cria e implementa aplicações para computadores Mac.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075793"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Criar aplicações de computador Mac com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Tenha em mente as seguintes considerações quando criar e implementar aplicações para computadores Mac.  

> [!IMPORTANT]  
>  Os procedimentos neste tópico cobrem informações sobre a implementação de aplicações para computadores Mac nos quais instalou o cliente do Gestor de Configuração. Os computadores Mac que inscreveu no Microsoft Intune não suportam a implementação de aplicação.  

## <a name="general-considerations"></a>Considerações gerais  
 Pode utilizar o Gestor de Configuração para implementar aplicações em computadores Mac que executam o cliente Do Gestor de Configuração Mac. As etapas para implementar software para computadores Mac são semelhantes às etapas para implementar software para computadores Windows. No entanto, antes de criar e implementar aplicações para computadores Mac que são geridos pelo Gestor de Configuração, considere o seguinte:  

-   Antes de poder implementar pacotes de aplicações Mac para computadores Mac, tem de utilizar a ferramenta **CMAppUtil** num computador Mac para converter estas aplicações num formato que possa ser lido pelo Gestor de Configuração.  

-   O Gestor de Configuração não suporta a implementação de aplicações Mac para os utilizadores. Em vez disso, estas implementações devem ser efetuadas num dispositivo. Da mesma forma, para as implementações de aplicações Mac, o Gestor de Configuração não suporta o **software de pré-implementação para a** opção principal do dispositivo do utilizador na página de Definições de **Implementação** do **Assistente de Software de Implementação**.  

-   As aplicações MAC suportam implementações simuladas.  

-   Não é possível implementar aplicações em computadores Mac que tenham um objetivo de **Disponível**.  

-   A opção de enviar pacotes de reativação ao implementar software não é suportada para computadores Mac.  

-   Os computadores Mac não suportam o Background Intelligent Transfer Service (BITS) para descarregar conteúdo de aplicação. Se uma transferência de aplicação falhar, é reiniciada desde o início.  

-   O Gestor de Configuração não suporta condições globais quando cria tipos de implementação para computadores Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Passos para criar e implementar uma aplicação  
 A tabela seguinte fornece os passos, detalhes e informações para a criação e implementação de aplicações para computadores Mac.  


|                                         Passo                                          |                                                                                                             Detalhes                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Passo 1**: Preparar aplicações Mac para Gestor de Configuração             | Antes de poder criar aplicações do Gestor de Configuração a partir de pacotes de software Mac, tem de utilizar a ferramenta **CMAppUtil** num computador Mac para converter o software Mac num ficheiro 'Gestor de Configuração<strong>.cmmac'.</strong> |
| **Passo 2**: Criar uma aplicação de Gestor de Configuração que contenha o software Mac |                                                                       Utilize o **Assistente de Aplicação Criar** para criar uma aplicação para o software Mac.                                                                       |
|             **Passo 3**: Criar um tipo de implementação para a aplicação Mac              |                                                              Este passo só será necessário se não tiver importado automaticamente estas informações a partir da aplicação.                                                               |
|                        **Passo 4**: Implementar a aplicação Mac                         |                                                                          Utilize o **Assistente de Software de implementação** para implementar a aplicação para computadores Mac.                                                                          |
|               **Passo 5**: Monitorizar a implementação da aplicação Mac               |                                                                                 Monitorize o êxito das implementações de aplicações para computadores Mac.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedimentos suplementares para criar e implementar aplicações para computadores Mac  
 Utilize os seguintes procedimentos para criar e implementar aplicações para computadores Mac que são geridos pelo Gestor de Configuração.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Passo 1: preparar aplicações Mac para o Configuration Manager  
 O processo de criação e implementação de aplicações do Gestor de Configuração para computadores Mac é semelhante ao processo de implementação dos computadores Windows. No entanto, antes de criar aplicações do Gestor de Configuração que contenham tipos de implementação Mac, deve preparar as aplicações utilizando a ferramenta **CMAppUtil.** Esta ferramenta é transferida com os ficheiros de instalação do cliente Mac. A ferramenta **CMAppUtil** reúne informações sobre a aplicação, incluindo os dados de deteção dos seguintes pacotes Mac:  

-   Imagem de Disco Apple (.dmg)  

-   Ficheiro de Pacote Meta (.mpkg)  

-   Pacote Instalador do Mac OS X (.pkg)  

-   Aplicação do Mac OS X (.app)  

Após recolher as informações, a ferramenta **CMAppUtil** cria um ficheiro com a extensão **.cmmac**. Este ficheiro contém os ficheiros de instalação do software Mac e informações sobre métodos de deteção que podem ser utilizados para avaliar se a aplicação já está instalada. A ferramenta**CMAppUtil** também pode processar ficheiros **.dmg** que contenham várias aplicações Mac e criar tipos de implementação diferentes para cada aplicação.  

1.  Copie o pacote de instalação do software Mac para a pasta do computador Mac onde extraiu os conteúdos do ficheiro **macclient.dmg** que transferiu a partir do Centro de Transferências da Microsoft.  

2.  No mesmo computador Mac, abra uma janela de terminal e navegue para a pasta onde extraiu os conteúdos do ficheiro **macclient.dmg** .  

3.  Navegue na pasta **Ferramentas** e escreva o seguinte comando de linha de comando:  

     **./CMAppUtil** *<properties\>*  

     Por exemplo, diga que pretende converter o conteúdo de um ficheiro de imagem de disco Apple chamado **MySoftware.dmg** que está armazenado na pasta de ambiente de trabalho do utilizador num ficheiro **cmmac** na mesma pasta. Também pretende criar ficheiros **cmmac** para todas as aplicações que se encontram no ficheiro de imagem do disco. Para tal, utilize a seguinte linha de comandos:  

     **./CMApputil –c /Users/** *<User Name\>* **/Desktop/MySoftware.dmg -o /Users/** *<User Name\>* **/Desktop -a**  

    > [!NOTE]  
    >  O nome da aplicação não pode ser mais de 128 caracteres.  

     Para configurar as opções da ferramenta **CMAppUtil**, utilize as propriedades da linha de comandos da seguinte tabela:  

  	|Propriedade|Mais informações|  
  	|--------------|----------------------|  
  	|**-h**|Apresenta as propriedades da linha de comandos disponíveis.|  
  	|**-r**|Produz o **detection.xml** do ficheiro **.cmmac** fornecido para **stdout**. A saída contém os parâmetros de deteção e a versão da ferramenta **CMAppUtil** que foi utilizada para criar o ficheiro **.cmmac** .|  
  	|**-c**|Especifica o ficheiro fonte a converter.|  
  	|**-o**|Especifica o caminho de saída em conjunto com a propriedade -c.|  
  	|**- a**|Cria automaticamente ficheiros .cmmac em conjunto com a propriedade –c para todas as aplicações e pacotes no ficheiro de imagem do disco.|  
  	|**-s**|Ignora a geração de **detection.xml** se não forem encontrados parâmetros de deteção e força a criação do ficheiro **.cmmac** sem o ficheiro **detection.xml** .|  
  	|**-v**|Apresenta uma saída mais detalhada da ferramenta **CMAppUtil** , juntamente com informações de diagnóstico.|  

4.  Certifique-se de que o ficheiro **.cmmac** foi criado na pasta de saída que especificou.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Criar uma aplicação De Configuração Manager que contenha o software Mac  

Utilize o seguinte procedimento para o ajudar a criar uma aplicação para computadores Mac que são geridas pelo Gestor de Configuração.  

1.  Na consola de Configuração Manager, escolha aplicações de**gestão** > de**aplicações**da Biblioteca > de **Software.**  

3.  No separador **Casa,** no grupo **Criar,** escolha **Criar Aplicação**.  

4.  Na página **geral** do Assistente de **Aplicação Criar,** selecione **detete automaticamente informações sobre esta aplicação a partir de ficheiros de instalação**.  

    > [!NOTE]  
    >  Se quiser especificar informações sobre a aplicação, **selecione manualmente especificar as informações da aplicação**. Para obter mais informações sobre como especificar manualmente as informações, consulte [como criar aplicações com o Gestor de Configuração](../../apps/deploy-use/create-applications.md).  

5.  Na lista pendente **Tipo** , selecione **Mac OS X**.  

6.  No campo **Localização,** especifique o caminho unC no formulário * \\ \\<servidor\> \\<partilhar\> \\<nome\> * de ficheiro para o ficheiro de instalação de aplicação Mac (ficheiro **.cmmac)** que irá detetar informações de aplicação. Em alternativa, escolha **navegar** para navegar e especificar a localização do ficheiro de instalação.  

    > [!NOTE]  
    >  Terá de ter acesso ao caminho UNC que contém a aplicação.  

7.  Escolha **Seguinte**.  

8.  Na página de **Informações** sobre Importação do Assistente de **Aplicação Criar,** reveja as informações importadas. Se necessário, pode escolher **O Anterior** para voltar atrás e corrigir quaisquer erros. Escolha **o próximo** para prosseguir.  

9. Na página **informação geral** do Assistente de **Aplicação Criar,** especifique informações sobre a aplicação, como o nome da aplicação, comentários, versão e uma referência opcional para ajudá-lo a referenciar a aplicação na consola Do Gestor de Configuração.  

    > [!NOTE]  
    >  Algumas das informações da aplicação podem já estar nesta página se forpreviamente obtida a partir dos ficheiros de instalação da aplicação.  

10. Escolha **a seguir,** reveja as informações da aplicação na página **Resumo** e, em seguida, complete o Assistente de **Aplicação Criar**.  

11. A nova aplicação é apresentada no nó de **Aplicações** da consola 'Gestor de Configuração'.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Passo 3: criar um tipo de implementação para a aplicação Mac  
 Utilize o seguinte procedimento para o ajudar a criar um tipo de implementação para computadores Mac que são geridos pelo Gestor de Configuração.  

> [!NOTE]  
>  Se importou automaticamente informações sobre a aplicação no **Assistente de Aplicação Criar,** um tipo de implementação para a aplicação pode já ter sido criado.  

1.  Na consola de Configuração Manager, escolha aplicações de**gestão** > de**aplicações**da Biblioteca > de **Software.**  

3.  Selecione uma aplicação. Em seguida, no separador **Home,** no grupo **Aplicação,** escolha Criar tipo de **implementação** para criar um novo tipo de implementação para esta aplicação.  

    > [!NOTE]  
    >  Também pode iniciar o Assistente do **Tipo de Implementação Criar** a partir do Assistente de **Aplicação Criar** e a partir do separador Tipos de **Implementação** do *\> nome de<caixa* de diálogo **Propriedades.**  

4.  Na página **geral** do Assistente do **Tipo de Implantação Create**, na lista de drop-down do **Tipo,** selecione **Mac OS X**.  

5.  No campo **Localização,** especifique o \\ \\ caminho\> \\ UNC no formulário<servidor<partilhar\> \\<nome\> de ficheiro no ficheiro de instalação da aplicação (ficheiro **.cmmac).** Em alternativa, escolha **navegar** para navegar e especificar a localização do ficheiro de instalação.  

    > [!NOTE]  
    >  Terá de ter acesso ao caminho UNC que contém a aplicação.  

6.  Escolha **Seguinte**.  

7.  Na página **Importar Informação** do **Assistente para Criar Tipo de Implementação**, reveja as informações que foram importadas. Se necessário, escolha **Anterior** para voltar atrás e corrigir quaisquer erros. Selecione **Seguinte** para continuar.  

8.  Na página **Informações Gerais** do **Assistente para Criar Tipo de Implementação**, especifique informações sobre a aplicação, tais como o respetivo nome, comentários e os idiomas em que o tipo de implementação está disponível.  

    > [!NOTE]  
    >  Algumas das informações do tipo de implementação podem já estar nesta página se forpreviamente obtida a partir dos ficheiros de instalação da aplicação.  

9. Escolha **Seguinte**.  

10. Na página **Requisitos** do Assistente do **Tipo de Implementação Create,** pode especificar as condições que devem ser satisfeitas antes de o tipo de implementação poder ser instalado nos computadores Mac.  

11. Escolha **Adicionar** para abrir a caixa de diálogo **Criar Requisitos** e adicionar um novo requisito.  

    > [!NOTE]  
    >  Também pode adicionar novos requisitos no separador **Requisitos** do nome de<*\> tipo* de implementação **Properties.**  

12. Na lista pendente **Categoria** , selecione que este requisito se aplica a um dispositivo.  

13. A partir da lista de desistência da **Condição,** selecione a condição que pretende utilizar para avaliar se o computador Mac cumpre os requisitos de instalação. O conteúdo desta lista varia consoante a categoria que selecionar.  

14. A partir da lista de abandono do **Operador,** escolha o operador para utilizar para comparar a condição selecionada com o valor especificado para avaliar se o utilizador ou dispositivo cumpre os requisitos de instalação. Os operadores disponíveis variam consoante a condição selecionada.  

15. No campo **Valor,** especifique os valores a utilizar com a condição selecionada e o operador para avaliar se o utilizador ou dispositivo cumpre o requisito de instalação. Os valores disponíveis variam consoante a condição e o operador que seleciona.

16. Escolha **OK** para salvar a regra de exigência e saia da caixa de diálogo **Create Requirement.**  

17. Na página **Requisitos** do Assistente do **Tipo de Implementação Create,** escolha **Seguinte**.  

18. Na página **Resumo** do **Assistente para Criar Tipo de Implementação**, reveja as ações que o assistente deverá executar.  Se necessário, escolha **Anterior** para voltar atrás e alterar as definições do tipo de implementação. Escolha **o próximo** para criar o tipo de implementação.  

19. Depois de terminar a página **Progress,** reveja as ações que foram tomadas e, em seguida, escolha **Perto** para completar o Assistente do **Tipo de Implementação Create**.  

20. Se tiver iniciado este assistente a partir do Assistente de **Aplicação Criar,** regressará à página De tipos de **implementação.**  

###  <a name="deploy-the-mac-application"></a>Implementar a aplicação Mac  
 As etapas para implementar uma aplicação para computadores Mac são as mesmas que as etapas para implementar uma aplicação para computadores Windows, exceto para as seguintes diferenças:  

-   A implementação de aplicações para utilizadores não é suportada.  

-   Não são suportadas implementações que tenham um objetivo de **Disponível** .  

-   O **software de pré-implementação para a** opção principal do dispositivo do utilizador na página de Definições de **Implementação** do **Assistente de Software de Implementação** não é suportado.  

-   Uma vez que os computadores Mac não suportam o Software Center, a definição de **notificações** do utilizador na página **da Experiência** do Utilizador do **Assistente de Software de Implementação** é ignorada.  

-   A opção de enviar pacotes de reativação ao implementar software não é suportada para computadores Mac.  

> [!NOTE]  
>  Pode construir uma coleção que contenha apenas computadores Mac. Para tal, crie uma coleção que use uma regra de consulta e use o exemplo de consulta WQL no [tópico como criar consultas.](../../core/servers/manage/create-queries.md)  

 Para mais informações, consulte [aplicações de implementação](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Passo 5: Monitorizar a implementação da aplicação Mac  
 Pode utilizar o mesmo processo para monitorizar as implementações de aplicações em computadores Mac, tal como poderia monitorizar as implementações de aplicações para computadores Windows.  

 Para mais informações, consulte [as aplicações do Monitor](../deploy-use/monitor-applications-from-the-console.md).  
