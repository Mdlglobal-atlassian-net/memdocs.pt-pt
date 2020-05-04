---
title: Monitorizar a utilização da aplicação com a medição de software
titleSuffix: Configuration Manager
description: Saiba mais sobre as operações que estão disponíveis na medição de software do Gestor de Configuração.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710084"
---
# <a name="software-metering-in-configuration-manager"></a>Medição de software em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém uma referência para todas as operações que poderá executar ao utilizar a medição de software do Gestor de Configuração.

> [!IMPORTANT]
>  A medição de software é utilizada para monitorizar aplicações de ambiente de trabalho de PCs Windows com um nome de ficheiro que termine em **.exe**. A medição de software não monitoriza aplicações modernas do Windows (por exemplo, as que são utilizadas pelo Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Pré-requisitos de medição de software
A medição de software não tem dependências externas, apenas dependências no produto.

|Dependência|Mais informações|
|----------------|----------------------|
|Definições de cliente para medição de software.|Para utilizar a medição de software, a definição de cliente **Ativar a medição de software nos clientes** tem de estar ativada e implementada nos computadores. Pode implementar as definições de medição de software em todos os computadores na hierarquia ou implementar definições personalizadas em grupos de computadores. Consulte a medição de **software Configure** neste tópico.|
|O ponto do reporting services.|Deve configurar um ponto do reporting services antes de poder visualizar relatórios de medição de software. Para mais informações, consulte [Introdução a relatórios.](../../core/servers/manage/introduction-to-reporting.md)|

##  <a name="configure-software-metering"></a>Configure software metering
 Este procedimento configura as predefinições de cliente para medição de software e aplica-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, crie uma definição personalizada do cliente do dispositivo e implemente-a numa coleção que contenha os computadores que pretende que utilizem medição de software. Para obter mais informações sobre como criar configurações personalizadas do dispositivo, consulte as definições do [cliente Configurar](../../core/clients/deploy/configure-client-settings.md).

1. Na consola 'Gestor de Configuração', clique em**Definições** > padrão do**cliente**da **Administração** > .

2. No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.

3. Na caixa de diálogo **Predefinições** , clique em **Medição de Software**.

4. Na lista **Definições do Dispositivo** , configure as seguintes definições:

   -   **Ativar a medição de software nos clientes**: selecione **Verdadeiro** para ativar a medição de software.

   -   **Agendar a recolha de dados**: configure com que frequência são recolhidos os dados de medição de software a partir dos computadores cliente. Utilize o valor predefinido de a cada **sete dias** ou clique em **Agenda** para especificar uma agenda personalizada.

5. Clique em **OK** para fechar a caixa de diálogo **Predefinições** .

   Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a recuperação de políticas para um único cliente, consulte [Gerir clientes.](../../core/clients/manage/manage-clients.md)

##  <a name="create-software-metering-rules"></a> Criar regras de medição de software
 Utilize o assistente de regra de medição de software Create software para criar uma nova regra de medição de software para o seu site de Configuração Manager.

1.  Na consola de Configuração Manager, clique em **Assets e Compliance** > **Software Metering**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Regra de Medição de Software**.

4.  Na página **geral** do assistente de regra de medição de software, especifique as seguintes informações:

    -   **Nome** - o nome da regra de medição de software. Deve ser único e descritivo.

        > [!NOTE]
        >  As regras de medição de software podem partilhar o mesmo nome se o nome de ficheiro contido nas mesmas for diferente.

    -   **Nome do Ficheiro** - o nome do ficheiro do programa que pretende medir. Pode clicar em **Procurar** para apresentar a caixa de diálogo **Abrir** , na qual pode selecionar o ficheiro do programa a utilizar.

        > [!NOTE]
        >  Se escrever o nome do ficheiro executável na caixa **Nome do Ficheiro** , não são efetuadas verificações para determinar se este ficheiro já existe ou se contém as informações de cabeçalho necessárias. Sempre que possível, clique em **Procurar** e selecione o ficheiro executável a ser medido.
        >
        >  Não são permitidos carateres universais no nome do ficheiro.
        >
        >  Esta caixa é opcional se for especificado um valor para **Nome do ficheiro original** .

    -   **Nome do Ficheiro Original** - O nome do ficheiro executável que pretende medir. Este nome corresponde à informação no cabeçalho do ficheiro, e não ao próprio nome do ficheiro, para que possa ser útil nos casos em que foi mudado o nome do ficheiro executável, mas quer medi-lo com o nome original.

        > [!NOTE]
        >  Não são permitidos carateres universais no nome do ficheiro original.
        >
        >  Esta caixa é opcional, se for especificado um valor para **Nome do Ficheiro** .

    -   **Versão** - a versão do ficheiro executável que pretende medir. Você pode usar o personagem wildcard ( &#42; ) para representar qualquer série de caracteres ou o personagem wildcard ( ? ), para representar qualquer personagem único. Se pretender medir todas as versões de um ficheiro executável, utilize o valor predefinido (&#42; ).

    -   **Idioma** - o idioma do ficheiro executável a medir. O valor predefinido é a região atual do sistema operativo que está a utilizar. Se selecionar um ficheiro executável para ser medido ao clicar no botão **Procurar** , esta caixa é preenchida automaticamente se a informação do idioma estiver presente no cabeçalho do ficheiro. Para medir todas as versões de idiomas de um ficheiro, selecione **Qualquer** na lista pendente.

    -   **Descrição** - uma descrição opcional para a regra de medição de software.

    -   **Aplicar esta regra de medição de software aos seguintes clientes** – selecione se pretende aplicar a regra de medição de software a todos os clientes da hierarquia ou aos clientes que estão atribuídos ao site especificado na lista **Site** .

5.  Para continuar, clique em **Seguinte**.

6.  Reveja e confirme as definições e conclua o assistente para criar a regra de medição de software. A nova regra de medição de software é apresentada no nó **Medição de Software** na área de trabalho **Recursos e Compatibilidade** .

##  <a name="configure-automatic-software-metering-rules"></a> Configurar regras de medição de software automáticas
 Pode configurar a medição de software no Configurmanager para gerar automaticamente regras de medição de software desativadas a partir de dados recentes de inventário de utilização mantidos na base de dados do site. Pode configurar estes dados de inventário para que sejam criadas regras de medição apenas para aplicações que são utilizadas numa percentagem de computadores especificada. Também pode especificar o número máximo de regras de medição de software geradas automaticamente permitidas no site.

> [!NOTE]
>  Por predefinição, as regras de medição de software que são criadas automaticamente estão desativadas. Antes de poder começar a recolher dados de utilização a partir destas regras, deve ativá-las.

1.  Na consola do Gestor de Configuração, clique em **Assets e Compliance** > **Software Metering**, e depois, no separador **Home,** no grupo **Definições,** clique em **Propriedades de Medição**de Software .

3.  Na caixa de diálogo **Propriedades de Medição de Software** , configure as seguintes opções:

    -   **Retenção de dados (em dias)** - especifica o período de tempo durante o qual os dados gerados pelas regras de medição de software são mantidos na base de dados do site. O valor predefinido é **90** dias.

    -   Ative a opção **Criar automaticamente regras de medição desativadas a partir dos dados de inventário de utilização recente**.

    -   **Especificar a percentagem de computadores na hierarquia que têm de utilizar um programa antes de ser criada automaticamente uma regra de medição de software** - o valor predefinido é **10** por cento.

    -   **Especificar o número de regras de medição de software que devem ser excedidas na hierarquia antes de a criação automática de regras ser desativada** - o valor predefinido é **100** regras.

4.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de Medição de Software** .

##  <a name="manage-software-metering-rules"></a> Gerir regras de medição de software
 Na área de trabalho **Ativos e Compatibilidade** , selecione **Medição de Software**, selecione a regra de medição de software que pretende gerir e, em seguida, selecione uma tarefa de gestão.

 Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.

|Tarefa de Gestão|Detalhes|
|---------------------|-------------|
|**Ativar**<br /><br /> **Desativar**|Ativa ou desativa um regra de medição de software. Esta definição é transferida para computadores cliente de acordo com o **Intervalo de consulta da política de cliente** , na secção **Política de Cliente** das definições de cliente (por predefinição, a cada 60 minutos).<br /><br /> Consulte as definições do [cliente configurar](../../core/clients/deploy/configure-client-settings.md) .|

##  <a name="monitor-software-metering"></a> Monitorizar a medição de software
 A medição de software no Gestor de Configuração inclui uma série de relatórios incorporados que lhe permitem monitorizar informações sobre operações de medição de software. Estes relatórios têm a categoria de relatórios de **Medição de Software**.

 Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).

 Além disso, pode criar consultas e coleções com base nos dados armazenados na base de dados do Gestor de Configuração através da medição de software.

 Para obter mais informações sobre coleções em 'Gestor de Configuração', consulte [Introdução às coleções.](../../core/clients/manage/collections/introduction-to-collections.md)

 Para mais informações sobre consultas no Gestor de Configuração, consulte [Introdução a consultas](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Segurança e privacidade para medição de software

### <a name="security-issues-for-software-metering"></a>Problemas de Segurança para Medição de Software
 Um intruso poderia enviar informações de medição de software inválidas para o Gestor de Configuração, que serão aceites pelo ponto de gestão mesmo quando a definição de cliente de medição de software é desativada. Isto pode resultar num grande número de regras de medição que são replicadas ao longo da hierarquia, causando uma negação de serviço na rede e para servidores de site do Gestor de Configuração.

 Uma vez que um atacante pode criar dados de medição de software inválidos, não considere as informações de medição de software como autoritativas.

 A medição de software está ativada por predefinição como uma definição de cliente.

###  <a name="privacy-information-for-software-metering"></a> Informações de Privacidade para Medição de Software
 A medição de software monitoriza a utilização de aplicações em computadores cliente. A medição de software está ativada por predefinição. Tem de configurar as aplicações que vai medir. A informação de medição é armazenada na base de dados do Gestor de Configuração. A informação é encriptada durante a transferência para um ponto de gestão, mas não é armazenada de forma encriptada na base de dados do Gestor de Configuração.

 Estas informações são conservadas na base de dados até serem eliminadas pelas tarefas de manutenção do site **Eliminar Dados de Medição de Software Desatualizados** (a cada cinco dias) e **Eliminar Dados de Resumo de Medição de Software Desatualizados** (a cada 270 dias). Pode configurar o intervalo de eliminação. As informações de medição não são enviadas à Microsoft.

 Antes de configurar as medições de software, considere os requisitos de privacidade.

## <a name="example-scenario-for-using-software-metering"></a>Cenário de exemplo de utilização de medição de software
 Nesta secção, irá criar uma regra de exemplo que o pode ajudar a resolver os seguintes requisitos comerciais de medição de software:

- Determinar o número de cópias de uma aplicação específica da empresa

- Detetar as cópias não utilizadas de uma aplicação

- Determinar os utilizadores que utilizam regularmente uma aplicação específica

  O Banco Woodgrove implementou p Microsoft Office 2010 como o conjunto padrão de aplicações de produtividade no escritório. No entanto, para suportar uma aplicação legada, alguns computadores têm de continuar a executar o Microsoft Office Word 2003. O departamento de TI pretende reduzir os custos de suporte e licenciamento, removendo estas cópias do Word 2003, se a aplicação legada já não estiver em utilização. O suporte técnico também pretende identificar os utilizadores que utilizam a aplicação legada.

  O Gestor de Sistemas de TI do Woodgrove Bank utiliza a medição de software no Gestor de Configuração para atingir estes objetivos de negócio. O Administrador executa as seguintes ações:

- Verifica os pré-requisitos para a medição de software e confirma que o ponto de serviços de reporte está instalado e operacional.
- Configura as definições padrão do cliente para a medição de software:<br>O Administrador permite a medição de software e utiliza o calendário de recolha de dados padrão de uma vez a cada sete dias.<br>O Administrador configura o inventário de software para ficheiros de inventário que têm a extensão .exe configurando o cliente de inventário de software definindo **Inventário estes tipos de ficheiros**.<br>O Administrador adiciona uma nova regra de medição de software, chamada **woodgrove.exe,** para monitorizar a aplicação antiga.
- Espera por sete dias, após o que os computadores do cliente começam a reportar dados de uso para o **woodgrove.exe** executável.
- O Administrador utiliza o relatório 'Gestor de Configuração' Instalar base para todos os programas de **software medidos** para ver quais os computadores que têm a aplicação **woodgrove.exe** carregada.
- Após seis meses, o Administrador executa o relatório **Computadores que têm um programa medido instalado, mas que não executam o programa desde uma data especificada**, especificando a regra de medição de software e uma data de seis meses no passado. Este relatório identifica 120 computadores que não executaram o programa nos últimos seis meses.
- O Administrador faz mais algumas verificações para confirmar que a aplicação do legado não é necessária nos computadores identificados. O Administrador desinstala então a aplicação legacy e a cópia do Word 2003 a partir destes computadores.<br>O Administrador executa o relatório **Utilizadores que executaram um programa de software medido específico** para fornecer ao balcão de ajuda uma lista de utilizadores que continuam a usar a aplicação legacy.
- O Administrador continua a verificar semanalmente os relatórios de medição de software e toma medidas corretivas se necessário.

  Como resultado deste método de ação, os custos do suporte de TI e de licenciamento são reduzidos, através da remoção das aplicações que já não são necessárias. Além disso, o suporte técnico tem agora a lista pretendida dos utilizadores que executam a aplicação legada.
