---
title: Manual do utilizador do Centro de Software
titleSuffix: Configuration Manager
description: Conheça as funcionalidades e funcionalidades do Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722663"
---
# <a name="software-center-user-guide"></a>Manual do utilizador do Centro de Software

*Aplica-se a: Gestor de Configuração (ramo atual)*

O administrador de TI da sua organização utiliza o Software Center para instalar aplicações, atualizações de software e atualizar o Windows. Este manual de utilizadores explica a funcionalidade do Software Center para os utilizadores do computador.

Notas gerais sobre a funcionalidade do Software Center:

- Este artigo descreve as mais recentes funcionalidades do Software Center. Se a sua organização estiver a usar uma versão mais antiga mas ainda suportada do Software Center, nem todas as funcionalidades estão disponíveis. Para mais informações, contacte o seu administrador de TI.

- A sua administração de TI pode desativar alguns aspetos do Software Center. A sua experiência específica pode variar.

- Se vários utilizadores estiverem a utilizar um dispositivo ao mesmo tempo, digamos, através de várias sessões remotas de desktop, o utilizador com o ID de sessão mais baixo será o único a ver todas as implementações disponíveis no Software Center. Os utilizadores com IDs de sessão mais alta podem não ver algumas das implementações no Software Center. Por exemplo, os utilizadores com IDs de sessão mais elevadapodem ver aplicações implementadas, mas não implementados Pacotes ou Sequências de Tarefas. Entretanto, o utilizador com o ID de sessão mais baixo verá todas as aplicações, pacotes e sequências de tarefas implementadas.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Como abrir o Centro de Software

Para que o método mais simples inicie o Software **Start** Center `Software Center`num computador Windows 10, prima Start e type . Pode não precisar de escrever toda a corda para o Windows encontrar a melhor correspondência.

Se navegar no menu Iniciar, procure no grupo **Microsoft Endpoint Manager** o ícone do **Software Center.**

![Ícones de menu inicial do Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> O caminho do menu Iniciar mudou na versão 1910. Na versão 1906 e anterior, o nome da pasta é **Microsoft System Center**. Quando atualizar o Gestor de Configuração para a versão 1910 ou mais tarde, certifique-se de atualizar qualquer documentação interna que mantenha para incluir esta nova localização.

## <a name="applications"></a>Aplicações

Selecione o separador **Aplicações** para encontrar e instalar aplicações que o seu administrador de TI implementa para si ou para este computador.

- **Tudo**: Mostra todas as aplicações que pode instalar
- **Obrigatório**: O seu administrador de TI aplica estas aplicações. Se desinstalar uma destas aplicações, o Software Center reinstala-o.
- **Filtros**: A sua administração de TI pode criar categorias de aplicações. Se disponível, selecione a lista de drop-down para filtrar a vista apenas para essas aplicações numa categoria específica. Selecione **Todos** para mostrar todas as aplicações.
- **Ordenar por**: Reorganizar a lista de aplicações. Por defeito, esta lista classifica-se pelo **mais recente.** As aplicações recentemente disponíveis estão listadas com uma **nova** etiqueta que é visível por 7 dias.
- **Pesquisa:** Ainda não consegue encontrar o que procura? Introduza palavras-chave na caixa de pesquisa para encontrá-la!
- **Alternar a vista**: Selecione os ícones para alternar a vista entre a vista da lista e a vista de azulejos. Por padrão, a lista de aplicações mostra como azulejos gráficos.
    - Vista para azulejos: A sua administração de TI pode personalizar os ícones. Abaixo, cada azulejo apresenta o nome da aplicação, editora e versão.
    - Vista da lista: Esta vista exibe o ícone da aplicação, nome, editor, versão e estado.

### <a name="install-multiple-applications"></a>Instalar várias aplicações

<!-- 1357126 -->
Instale mais de uma aplicação de cada vez em vez de esperar que uma termine antes de começar a seguinte. Nem todas as candidaturas se qualificam:

- A aplicação é visível para si
- A aplicação ainda não está a descarregar ou a instalar
- O seu administrador de TI não requer aprovação para instalar a app

Para instalar mais de uma aplicação de cada vez:

1. Para introduzir o modo multi-select na vista da lista, selecione o ícone multi-select ![Ícone multi-selecionado do Software Center](media/software-center-multi-select-apps.png) no canto superior direito.
2. Selecione duas ou mais aplicações para instalar selecionando a caixa de verificação à esquerda das aplicações na lista.
3. Selecione o botão **Instalar Selecionado.**

As aplicações instalam-se normalmente, só agora sucessivamente.


## <a name="updates"></a>Atualizações

Selecione o separador **Atualizações** para visualizar e instalar atualizações de software que o seu administrador de TI implementa para este computador.  

- **Tudo**: Mostra todas as atualizações que pode instalar
- **Requerido**: O seu administrador de TI aplica estas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por defeito, esta lista classifica pelo **nome da aplicação: A a Z**.

Para instalar atualizações, selecione **Instalar Tudo**.

Para instalar apenas atualizações específicas, selecione o ícone para introduzir o modo multi-select. Verifique as atualizações para instalar e, em seguida, **selecione Instalar Selecionado**.


## <a name="operating-systems"></a>Sistemas Operativos

Selecione o separador **Sistemas Operativos** para visualizar e instalar versões do Windows que o seu administrador de TI implementa para este computador.  

- **Tudo**: Mostra todas as versões do Windows que pode instalar
- **Requerido**: O seu administrador de TI aplica estas atualizações.
- **Ordenar por**: Reorganizar a lista de atualizações. Por defeito, esta lista classifica pelo **nome da aplicação: A a Z**.


## <a name="installation-status"></a>Estado de instalação

Selecione o separador de estado de **instalação** para ver o estado das aplicações. Pode ver os seguintes estados:

- **Instalado**: O Centro de Software já instalou esta aplicação neste computador.
- **Download**: O Software Center está a descarregar o software para instalar neste computador.
- **Failed**: O Centro de Software encontrou um erro ao tentar instalar o software.
- **Programado para instalar depois**: Mostra a data e a hora da próxima janela de manutenção do dispositivo para instalar o próximo software. As janelas de manutenção são definidas pelo seu administrador de TI.<!--1358131-->
    - O estado pode ser visto no separador **All** and the **Upcoming.**
    - Pode instalar antes da janela de manutenção selecionando o botão **Instalar agora.**


## <a name="device-compliance"></a>Conformidade do dispositivo

Selecione o separador de conformidade do **Dispositivo** para ver o estado de conformidade deste computador.

Selecione Verificar a **conformidade** para avaliar as definições deste dispositivo com as políticas de segurança definidas pelo seu administrador de TI.


## <a name="options"></a>Opções

Selecione o separador **Opções** para visualizar definições adicionais para este computador.

### <a name="work-information"></a>Informação de trabalho

Indique as horas que normalmente trabalha. A sua administração de TI pode agendar instalações de software fora do seu horário comercial. Deixe pelo menos quatro horas por dia para tarefas de manutenção do sistema. A sua administração de TI ainda pode instalar aplicações críticas e atualizações de software durante o horário comercial.

- Selecione as listas de drop-down para selecionar as primeiras e últimas horas que utiliza este computador. Por defeito estes valores são das **5:00** às **22:00**

- Selecione a caixa de verificação junto aos dias da semana em que normalmente utiliza este computador. O Software Center só seleciona os dias úteis por padrão.  

Especifique se utiliza regularmente este computador para fazer o seu trabalho. O seu administrador pode instalar automaticamente aplicações ou disponibilizar aplicações adicionais aos computadores primários. <!--3485366-->

- Selecione **que uso regularmente este computador para fazer** o meu trabalho se o computador que está a usar for um computador primário.

### <a name="power-management"></a>Gestão de energia

A sua administração de TI pode definir políticas de gestão de energia. Estas políticas ajudam a sua organização a conservar a eletricidade quando este computador não está a ser utilizado.

Para que este computador seja isento destas políticas, selecione a caixa de verificação **Não aplique as definições de energia do meu departamento de TI para este computador**. Esta definição é desativada por defeito; o computador aplica definições de potência.

### <a name="computer-maintenance"></a>Manutenção de computadores

Especifique como o Software Center aplica alterações ao software antes do prazo

- **Instale ou desinstale automaticamente o software necessário e reinicie o computador apenas fora do horário**de trabalho especificado : Esta definição é desativada por defeito.
- **Suspenda as atividades**do Software Center quando o meu computador estiver no modo de apresentação : Esta definição é ativada por padrão.
- **Política de Sincronização**: Selecione este botão quando instruído pelo seu administrador de TI. Este computador verifica com os servidores qualquer coisa nova, como aplicações, atualizações de software ou sistemas operativos.

### <a name="remote-control"></a>Controlo Remoto

Especifique as definições de acesso remoto e controlo remoto para o seu computador

- **Utilize as definições de acesso remoto do seu Departamento de TI**: Esta caixa de verificação é selecionada por defeito.
- **Nível de acesso remoto permitido**: Selecione entre as seguintes 3 opções
    - **Não permita acesso remoto**
    - **Visualizar apenas**
    - **Completo**: Este nível é ativado por defeito.
- **Permita o controlo remoto deste computador por administradores quando eu estiver fora**. Esta definição está definida para **Sim** por padrão.
- **Quando um administrador tenta controlar este computador remotamente:** Esta definição tem duas opções
    - **Peça permissão cada vez**: Esta opção é selecionada por defeito.
    - **Não peça permissão**
- **Mostre o seguinte durante o telecomando**: Ambas as opções são selecionadas por padrão
    - **Ícone de estado na área de notificação**
    - **Uma barra de conexão de sessão no ambiente de trabalho**
- **Reproduzir som**: Esta definição tem três opções
    - **Quando a sessão começa e termina**: Esta definição é selecionada por defeito.
    - **Repetidamente durante a sessão**
    - **Nunca**

    Para mais informações, consulte [Introdução ao Controlo Remoto](../clients/manage/remote-control/introduction-to-remote-control.md)
    

## <a name="custom-tab-in-software-center"></a>Separador personalizado no Centro de Software

A sua administração de TI pode ter adicionado um separador adicional ao Centro de Software. Este separador é nomeado pela sua administração e leva a um site que especificam. Por exemplo, você pode ter um separador chamado "Help Desk" que leva ao site de help desk da sua organização. <!--1358132-->
