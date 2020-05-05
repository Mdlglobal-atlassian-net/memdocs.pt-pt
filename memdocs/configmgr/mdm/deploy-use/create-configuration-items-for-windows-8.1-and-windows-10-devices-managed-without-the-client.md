---
title: Criar itens de configuração para Windows
titleSuffix: Configuration Manager
description: Crie itens de configuração para gerir as definições para computadores Windows 10 com gestão de dispositivos móveis no local (MDM) no Gestor de Configuração.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8186b45a0b0c74840582052f9c585c0557180493
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721949"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Criar itens de configuração para dispositivos Windows com MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize o dispositivo de configuração do Gestor de Configuração **Windows 8.1 e Windows 10** para gerir as definições para dispositivos Windows que gere com a gestão de dispositivos móveis no local (MDM).

Para obter informações mais gerais sobre as definições de conformidade no Gestor de Configuração, consulte os seguintes artigos:

- [Introdução às definições de compatibilidade](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Planear e configurar as definições de conformidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Criar um item de configuração

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e compliance,** expanda **as Definições**de Conformidade e, em seguida, selecione o nó de Itens de **Configuração.**

1. No separador **Casa** da fita, no grupo **Criar,** selecione **Create Configuration Item**.

1. Na página **geral** do Assistente de **Configuração Criar,** especifique as seguintes informações:

    - **Nome**: Um nome único para identificar este item de configuração.

    - **Descrição**: Uma descrição opcional para fornecer mais informações sobre a sua utilização.

    - Em **Definições para dispositivos geridos *sem* o cliente Do Gestor de Configuração,** selecione O Windows **8.1 e o Windows 10**.

    - **Categorias:** Pode criar e atribuir categorias para ajudá-lo a pesquisar e filtrar itens de configuração na consola 'Gestor de Configuração'.

1. Na página plataformas **suportadas** do assistente, selecione as plataformas específicas do Windows para avaliar este item de configuração.

1. Na página Definições do **Dispositivo,** selecione os grupos de definições que pretende configurar. Para obter mais informações sobre as definições disponíveis, consulte a [referência Definições](#bkmk_setref).

    > [!TIP]
    > Se a definição que deseja não estiver listada, selecione a opção de **configurar configurações adicionais que não estejam nos grupos de definição predefinidos**. Esta opção adiciona a página **Definições Adicionais** ao assistente.

1. Em cada página de definições, configure as definições necessárias. Quando as definições o suportam, também pode **remediar as definições não conformes**. Se um dispositivo avaliar a definição como não conforme com este item de configuração, irá remediar a definição para ser conforme.

    Para cada grupo de definições, também pode configurar a gravidade que reporta quando a definição não é conforme. Escolha um dos seguintes valores para a **severidade** do incumprimento para a opção de relatórios:

    - **Nenhum**: Os dispositivos que insebem esta regra de conformidade não reportam uma falha nos relatórios do Gestor de Configuração.

    - **Informações**

    - **Aviso**

    - **Crítica**

    - **Crítico com evento**: Os dispositivos que falham nesta regra de conformidade reportam uma falha dos relatórios **críticos** para o Gestor de Configuração. Também regista o estado não conforme como um evento Windows no registo de eventos da aplicação.

1. Na página de **Aplicabilidade** da Plataforma do assistente, reveja quaisquer definições que não sejam compatíveis com as plataformas suportadas selecionadas. Volte e remova estas definições, altere as plataformas de suporte ou continue.

    > [!IMPORTANT]
    > Os dispositivos não avaliam o cumprimento de configurações não suportadas.

1. Conclua o assistente.

Pode ver o novo item de configuração no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a>Referência de definições  

As seguintes secções detalham as definições específicas disponíveis em cada grupo. Configure estas definições na página de **Definições** do Dispositivo do Assistente de **Configuração criar** para dispositivos **Windows 8.1 e Windows 10** geridos *sem* o cliente do Gestor de Configuração.

### <a name="password"></a>Palavra-passe

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.

- **Requerer definições de palavra-passe nos dispositivos**: Exija uma palavra-passe nos dispositivos suportados.
- **Comprimento mínimo da palavra-passe (caracteres)**: O comprimento mínimo para a palavra-passe.
- **Expiração da palavra-passe em dias**: O número de dias antes de o utilizador alterar a sua palavra-passe.
- **Número de palavras-passe lembradas**: Impede a reutilização de senhas usadas anteriormente.
- **Número de tentativas de logon falhadas antes**de o dispositivo ser limpo : Se este número de tentativas de login falharem, o MDM limpa o dispositivo
- **Tempo de inatividade antes**de o dispositivo estar bloqueado : Especifique a quantidade de tempo que um dispositivo pode ficar inativo antes de estar bloqueado. O dispositivo está inativo quando não há entrada do utilizador.
- **Complexidade da palavra-passe**: Escolha se pode `1234`especificar um PIN numérico como , ou se deve fornecer uma senha forte.
  - **Número de conjuntos de caracteres complexos exigidos na palavra-passe**: Se a complexidade da palavra-passe for **forte,** selecione quantos tipos de caracteres a palavra-passe requer: letras maiúsculas, letras minúsculas, números ou símbolos. Por defeito, `2`este valor é .
- **Enviar PIN de recuperação da palavra-passe para o Exchange Server**

### <a name="device"></a>Dispositivo

- **Captura do ecrã**: Ativar esta definição para permitir ao utilizador tirar uma imagem do ecrã do dispositivo. (Apenas no Windows 10)
- **Submissão de dados de diagnóstico**: Ative esta definição para permitir dados de diagnóstico do Windows para análise. (Apenas no Windows 8.1)
- Permitir a submissão de dados de **diagnóstico (Windows 10)**: Detete o nível de dados de diagnóstico do Windows para análise: Desativar, Básico, Melhorado ou Completo. (Apenas no Windows 10)
- **Geolocalização**: Ative esta definição para permitir que o dispositivo utilize informações sobre os serviços de localização. (Apenas no Windows 10)
- **Cópia e Pasta**: Ative esta definição para utilizar cópia e pasta para transferir dados entre aplicações. (Apenas no Windows 10)
- **Reposição de fábrica**: Ativar esta definição para permitir ao utilizador redefinir o dispositivo nas suas definições iniciais. (Apenas no Windows 10)
- **Bluetooth**: Permitir ou proibir a utilização da capacidade Bluetooth do dispositivo.
- **Modo de descoberta Bluetooth**: Permita ou proíba que o dispositivo seja descoberto por outros dispositivos Bluetooth. (Apenas no Windows 10)
- **Publicidade Bluetooth**: Permitir ou proibir a utilização de publicidade Bluetooth. (Apenas no Windows 10)
- **Gravação de voz**: Permitir ou proibir a utilização das características de gravação de voz do dispositivo. (Apenas no Windows 10)
- **Cortana**: Permitir ou proibir a utilização do assistente de voz Cortana. (Apenas no Windows 10)
- **Notificações**do Action Center : Ativar ou desativar o painel de notificação no Windows 10. (Apenas no Windows 10)
- **Modificação das definições da região (apenas no ambiente**de trabalho) : Permitir ou proibir o utilizador de alterar as definições regionais do dispositivo.
- **Modificação das definições de alimentação e sono (apenas no ambiente**de trabalho) : Permita ou proíba que o utilizador mude as definições de energia e de sono no dispositivo.
- **Modificação das definições de idiomas (apenas no ambiente**de trabalho) : Permitir ou proibir o utilizador de alterar as definições de idioma no dispositivo.
- **Modificação do tempo**do sistema : Permita ou proíba que o utilizador mude a data e a hora do dispositivo.
- **Modificação do nome**do dispositivo : Permita ou proíba que o utilizador mude o nome do dispositivo.

### <a name="email-management"></a>Gestão de e-mail

Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.  

- **E-mail POP e IMAP**: Permitir ou proibir ligações a contas de e-mail que utilizem os padrões POP e IMAP.
- **Tempo máximo para manter o e-mail**: Quanto tempo para manter o e-mail antes de o servidor o apagar.
- **Formatos de mensagem permitidos**: Especifique se os e-mails são **Texto Simples** ou HTML e **Texto Simples**.
- **Tamanho máximo para e-mail de texto simples (descarregado automaticamente)**: Desbloqueie o tamanho máximo dos e-mails de texto simples quando forem automaticamente descarregados.
- **Tamanho máximo para e-mail HTML (descarregado automaticamente)**: Desbloqueie o tamanho máximo dos e-mails HTML quando forem automaticamente descarregados.
- **Tamanho máximo de um anexo (descarregado automaticamente)**: Desbloqueie o tamanho máximo dos anexos de e-mail que são automaticamente descarregados.
- **Sincronização do calendário**: Permitir ou proibir a sincronização dos calendários no dispositivo.
- **Conta de e-mail personalizada**: Permitir ou proibir a utilização de uma conta de e-mail não organizacional no dispositivo.
- **Tornar a Conta Microsoft opcional na aplicação Windows Mail**: Ativar esta opção para não necessitar de uma conta Microsoft no Windows Mail.

### <a name="store"></a>Arquivo

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.

- **Loja de aplicações**: Permitir ou proibir o acesso à Microsoft Store no dispositivo.
- **Introduza uma palavra-passe para aceder à loja de aplicações**: Ative esta opção para exigir que os utilizadores introduzam uma palavra-passe para aceder à aplicação da Microsoft Store.
- **Compras in-app**: Permitir ou proibir os utilizadores de fazer compras in-app.
- **Lançamento da aplicação com origem**na loja : Desative todas as aplicações que foram pré-instaladas no dispositivo ou instaladas a partir da Microsoft Store.
- **Aplicações de atualização automática a partir da loja**: Permitir ou proibir aplicações instaladas a partir da Microsoft Store para atualizar automaticamente.
- **Instale aplicações na unidade do sistema**: Permitir ou proibir o `C:` dispositivo de instalar aplicações na unidade do sistema, que normalmente é a unidade.
- **Instale dados de aplicações no volume do sistema**: Ative esta opção para permitir que as aplicações armazenem dados na unidade do sistema.
- **Utilize apenas uma loja privada**: Exija que os utilizadores descarreguem aplicações da sua loja privada.
- **DVR do jogo**: Desativar a gravação e a transmissão do Windows Game

### <a name="browser"></a>Browser

Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.

- **Permitir**o navegador web : Permitir ou proibir a utilização do navegador web no dispositivo.
- **Preenchimento automático**: Permitir ou proibir a alteração das definições automáticas no navegador.
- **Scripting ativo**: Permitir ou proibir se o navegador pode executar scripts, como scripts ActiveX.
- **Plug-ins**: Permitir ou proibir a adição de plug-ins ao Internet Explorer.
- **Bloqueador pop-up**: Permitir ou proibir o bloqueador pop-up do navegador.
- **Cookies**: Permitir ou proibir que os cookies sejam guardados no dispositivo.
- **Aviso de fraude**: Permitir ou proibir avisos de potenciais sites fraudulentos.

### <a name="internet-explorer"></a>Internet Explorer

Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.

- **Envie sempre Não rastreie o cabeçalho**: Permita ou proíba enviar informações de navegação para sites de terceiros.
- Zona de **segurança intranet**: Permitir ou proibir a atribuição de um nível de segurança à zona de segurança intranet.
- **Nível de segurança para a zona**de Internet : Desdefinido o nível de segurança para a zona da Internet: Alto, Médio-Alto ou Médio.
- **Nível de segurança para a zona intranet**: Desdefinido o nível de segurança para a zona intranet: Alto, Médio-Alto, Médio, Médio-Baixo ou Baixo.
- **Nível de segurança para a zona**de sites fidedignos : Delineie o nível de segurança para a zona de sites fidedignos: Alto, Médio-Alto, Médio, Médio-Baixo ou Baixo.
- **Nível de segurança para a zona de sites restritos**: Delineie o nível de segurança para a zona de locais restritos: Alto.
- **Espaços de nome para zona intranet**: Configure websites para adicionar ou remover da zona intranet.
- **Vá ao site intranet para uma única palavra :** Permita ou proíba que o Internet Explorer vá automaticamente a `https://`um site intranet se o utilizador introduzir um nome de site válido sem um protocolo anterior, por exemplo.
- **Opção de menu modo empresarial**: Ativar os utilizadores para ativar e desativar o modo enterprise a partir do menu **Ferramentas** do Internet Explorer.
  - **Localização do relatório de registo (URL)**: Quando o Modo Enterprise estiver ativo, especifique um URL para registar websites visitados.
- **Localização da lista de sites do Modo Empresarial (URL)**: Quando o Modo Enterprise estiver ativo, especifique a lista de websites que a utilizam.

### <a name="cloud"></a>Nuvem

Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.

- **Definições sincronização**: Permitir ou proibir configurações para sincronizar entre dispositivos.
- **Sincronização de credenciais**: Permitir ou proibir credenciais para sincronizar entre dispositivos.
- **Conta Microsoft**: Ative esta definição para permitir a utilização de uma conta Microsoft no dispositivo.
- **Definições sincronização sobre ligações medimétricas**: Permitir ou proibir configurações para sincronizar quando a ligação à rede é medido.

### <a name="security"></a>Segurança

- **Instalação de ficheiros não assinados**: Permite quem pode instalar um ficheiro não assinado. (Apenas no Windows 10)
- **Aplicações não assinadas**: Permitir ou proibir a instalação de aplicações não assinadas. (Apenas no Windows 10)
- **SMS e mensagens MMS**: Permitir ou proibir protocolos de mensagens de texto no dispositivo. (Apenas no Windows 10)
- **Armazenamento amovível**: Permitir ou proibir a utilização de armazenamento amovível, como um cartão SD. (Apenas no Windows 10)
- **Câmara**: Permitir ou proibir a utilização da câmara do dispositivo. (Apenas no Windows 10)
- **Comunicação de campo próximo (NFC)**: Permitir ou proibir a comunicação utilizando o NFC. (Apenas no Windows 10)
- **Modo AntiTheft**: Permitir ou proibir a utilização do modo AntiTheft do Windows 10. (Apenas no Windows 10)
- **Permitir a ligação USB**: Permitir ou proibir outros dispositivos de ligação a este dispositivo utilizando uma ligação USB. (Apenas no Windows 10)
- **Perfil VPN do Windows RT**: Disponibiliza um perfil VPN para dispositivos Windows RT (apenas Windows 8.1)

### <a name="peak-synchronization"></a>Sincronização de pico

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.

- **Especificar**o tempo de pico : Desconte o tempo de pico e os dias da semana para a sincronização do dispositivo móvel.
- Frequência de **sincronização do pico:** Configure a frequência com que a sincronização ocorre durante as horas de ponta.
- **Frequência de sincronização fora do pico:** Configure a frequência com que a sincronização ocorre fora das horas de pico.

### <a name="roaming"></a>Roaming

- **Gestão do dispositivo durante o roaming**: Permita ou proíba o Gestor de Configuração de gerir o dispositivo quando estiver em roaming. (Apenas no Windows 10)
- **Descarregue o software durante o roaming**: Permitir ou proibir o descarregamento de apps e software durante o roaming. (Apenas no Windows 10)
- **E-mail descarregue durante o roaming**: Permitir ou proibir transferências de e-mail durante o roaming. (Apenas no Windows 10)
- **Roaming de dados**: Permitir ou proibir o roaming entre redes ao aceder a dados.
- **VPN através do telemóvel**: Permita ou proíba que o dispositivo utilize uma ligação VPN enquanto está ligado a uma rede celular. (Apenas no Windows 10)
- **VPN roaming over cellular**: Allow or proibi do dispositivo de utilizar uma ligação VPN durante o roaming numa rede celular. (Apenas no Windows 10)

### <a name="encryption"></a>Encriptação

- **Encriptação do cartão**de armazenamento : Despem-se para exigir ao utilizador que encripte quaisquer cartões de armazenamento utilizados no dispositivo. (Apenas no Windows 10)
- **Encriptação de ficheiros no dispositivo**: Configurar para encriptar ficheiros armazenados no dispositivo.
- **Requerer a assinatura de e-mail**: O utilizador tem de assinar e-mails digitalmente antes de serem enviados.
  - **Algoritmo de assinatura**: Selecione o algoritmo para a assinatura de e-mails: Padrão, SHA ou MD5
- **Requerer encriptação de e-mail**: O utilizador tem de encriptar e-mails antes de serem enviados.
  - Algoritmo de **encriptação**: Selecione o algoritmo para encriptar e-mails: Padrão, Triple DES, DES, RC2 128-bit, RC2 64-bit, RC2 40-bit

### <a name="wireless-communications"></a>Comunicações sem fios

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.

- **Ligação de rede sem fios**: Permitir ou proibir a capacidade Wi-Fi do dispositivo.
- **Wi-Fi tethering**: Ative o utilizador a utilizar o dispositivo como um hotspot móvel.
- **Descarregar dados para Wi-Fi sempre que possível:** Ativar o dispositivo para utilizar a ligação Wi-Fi o máximo possível.
- **Relatório de hotspot wi-fi**: Ative o dispositivo para enviar informações sobre ligações Wi-Fi para ajudar o utilizador a descobrir ligações próximas.
- **Configuração Wi-Fi manual**: Ative o utilizador a configurar manualmente as ligações sem fios.

#### <a name="configured-wireless-network-connections"></a>Ligações de rede sem fios configuradas

1. Na página de definições de **comunicação sem fios do dispositivo móvel Configure,** selecione **Adicionar**.

1. Na janela de ligação à **rede sem fios,** especifique as seguintes informações sobre a ligação sem fios à oferta em dispositivos móveis:

    - **Nome da rede (SSID)**: Introduza o nome da rede Wi-Fi.
    - **Ligação de rede**: Escolha **internet** ou **trabalho**.
    - **Autenticação**: Escolha o método de autenticação para a ligação sem fios:
        - **Abrir**
        - **Partilhado**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Encriptação de dados**: Escolha o método de encriptação utilizado por esta ligação. Os valores disponíveis mudam com base no método de **Autenticação** que selecionar:
        - **Desativado**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Índice chave**: Quando definir **a encriptação de dados** para O **WEP,** selecione um índice chave de **1** a **4**.
    - **Esta rede liga-se à Internet**: Fornecer configurações de procuração para permitir que dispositivos móveis numa rede sem fios se conectem à internet.
        - **Definições do servidor proxy**: Configure as definições do **servidor** e **da porta** para os proxies **HTTP,** **WAP**e **Sockets.**
    - **802.1X definições:**
        - **Ativar o acesso à rede 802.1X**: Proteja a ligação especificando um tipo EAP.
        - **Tipo EAP**: Escolha um dos seguintes protocolos de autenticação:
            - **PEAP**
            - **Smart card ou certificado**

### <a name="certificates"></a>Certificados

Importar certificados para instalar em dispositivos móveis.

Selecione **Import**e, em seguida, especifique os seguintes valores:

- Arquivo de **certificado:** Navegue e selecione um ficheiro de certificado **(.cer)** para importar.
- **Loja**de destino : Escolha uma ou mais das seguintes lojas de certificados:
  - **Raiz**
  - **CA**
  - **Normal**
  - **Com privilégios**
  - **SPC**
  - **Elemento da rede**
- **Função**: Se escolher a loja de **certificados SPC** (Certificado editor de software), escolha a função a associar ao certificado:
  - **Operador de Rede Móvel**
  - **Gestor**
  - **Utilizador Autenticado**
  - **Administrador de TI**
  - **Utilizador Não Autenticado**
  - **Servidor de Aprovisionamento Fidedigno**

### <a name="system-security"></a>Segurança do sistema

- **Controlo da conta**do utilizador : Configure o comportamento do Controlo de Conta do Utilizador do Windows no dispositivo.
- **Firewall da rede**: Exija que o Windows ative a firewall incorporada. (Windows 8.1)
- **Atualizações**: Configure o comportamento das atualizações de software do Windows. (Windows 8.1)
  - **Classificação mínima das atualizações**: Escolha a classificação mínima das atualizações para descarregar e instalar: **Nenhuma,** **importante**ou **recomendada**.
- **Atualizações (Windows 10)**: Configure o comportamento das atualizações do software windows. (Apenas no Windows 10)
  - **Dia de instalação**: Escolha o dia programado quando o dispositivo instalar automaticamente atualizações e reiniciar. (Apenas no Windows 10)
  - Tempo de **instalação**: Escolha o horário programado quando o dispositivo instalar automaticamente atualizações e reiniciar. (Apenas no Windows 10)
- **SmartScreen**: Ativar ou desativar o Ecrã Inteligente do Windows.
- **Proteção contra o vírus**: Exija que o Windows tenha software antivírus.
- **As assinaturas de proteção contra vírus estão atualizadas**: Exija que os ficheiros de assinatura antivírus estejam atualizados.
- **Visualização**de notificação do ecrã de bloqueio : Ativar ou desativar notificações para visualizar no ecrã de bloqueio.
- **Funcionalidades de pré-lançamento**: Configure se o dispositivo aceita definições e funcionalidades de pré-desbloqueio. (Apenas no Windows 10)
- **Instalação manual**do certificado de raiz : Ative ou desative o utilizador para instalar manualmente um certificado de raiz, que permite confiar em qualquer certificado emitido por essa raiz. (Apenas no Windows 10)
- Permitir a **não inscrição manual**: Permitir ou proibir o utilizador de desinscrever o dispositivo a partir da gestão de dispositivos móveis no local com o Diretor de Configuração.

### <a name="windows-server-work-folders"></a>Pastas de Trabalho do Windows Server

Estas definições destinam-se apenas a dispositivos com o Windows 8.1 e o Windows 10.

- URL de **pastas de trabalho**: Especifique a localização de uma pasta de trabalho do Windows Server a que os utilizadores podem ligar a partir do seu dispositivo.

### <a name="allowed-and-blocked-apps-list"></a>Lista de aplicativos permitidos e bloqueados

Estas definições destinam-se apenas a dispositivos que executam o Windows Phone, que o Gestor de Configuração no local o MDM não suporta. Para mais informações, veja [o que aconteceu ao híbrido?](../understand/what-happened-to-hybrid.md)

### <a name="windows-10-team"></a>Windows 10 Team

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 Team.

- **Deixe o ecrã acordar automaticamente quando os sensores detetarem alguém na sala**: Permita ou proíba que o dispositivo acorde automaticamente quando o sensor detetar alguém na sala.
- **Exija PIN para projeção sem fios**: Ative ou desative se tem de introduzir um PIN antes que outro dispositivo possa ligar-se sem fios para a projeção.
- **Janela de manutenção**: Ative esta definição para configurar a janela quando as atualizações puderem instalar e reiniciar o dispositivo.
  - **Início**: Desmarcar a hora de início da janela de manutenção.
  - **Duração (Horas)**: Desloque o comprimento em horas da janela de manutenção.
- **Azure Operational Insights**: Permitir que os [Insights Operacionais do Azure](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) recolham, armazenem e analisem os dados de ficheiros de registo dos dispositivos da Equipa Windows 10.
  - **ID do espaço de trabalho**: Introduza um ID de espaço de trabalho válido
  - **Chave do espaço de trabalho**: Introduza a chave para o espaço de trabalho associado
- **Projeção sem fios Miracast**: Permitir que dispositivos com miracast se desloque para este dispositivo Windows 10 Team.
  - **Canal Miracast**: Selecione um canal Miracast para projetar conteúdos.
- **Informações de reunião exibidas no ecrã de boas-vindas**: Escolha o tipo de informação que o dispositivo exibe no azulejo do **ecrã** **de boas-vindas:**
  - **Mostrar apenas organizador e hora**
  - **Mostrar organizador, tempo e assunto (assunto escondido para reuniões privadas)**
- **URL de imagem**de fundo do ecrã de bloqueio : Especifique um URL para exibir um fundo personalizado no ecrã de **boas-vindas** de um dispositivo da Equipa Windows 10. Inicie o `https://` URL e utilize o formato PNG.

### <a name="windows-information-protection"></a>Windows Information Protection  

Para obter mais informações sobre como configurar a proteção de dados da empresa com o Gestor de Configuração, consulte [Proteger os seus dados empresariais utilizando a Proteção de Informação do Windows (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge"></a>Microsoft Edge

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.  

- **Permitir sugestões de pesquisa na barra**de endereços : Deixe o motor de busca sugerir sites à medida que escreve frases de pesquisa.
- **Não permita rastrear**: Informe os websites de que não quer que rastreiem a sua visita.
- **Ativar o SmartScreen**: Verifique se os ficheiros descarregados não contêm código malicioso.
- **Permitir pop-ups**: Configure pop-ups de navegador.
- **Permitir cookies**: Configure a utilização de cookies.
- **Permitir o auto-enchimento**: Deixe o navegador preencher automaticamente formulários com informações armazenadas como nome, endereço e telefone.
- **Permitir o Gestor de Passwords**: Deixe o navegador armazenar e gerir senhas para sites.
- **Ferramentas**de desenvolvimento : Permitir ou proibir a função de ferramentas de desenvolvimento do Edge.
- **Extensões**: Permitir ou proibir extensões de borda.
- **Navegação inprivada**: Permitir ou proibir a navegação inprivada, que não armazena histórico ou cookies.
- Endereço IP do **local webRTC**: Permita ou proíba o endereço IP local do dispositivo para exibir quando o utilizador efefeha chamadas telefónicas utilizando o protocolo RTC web.
- **Bloqueie o acesso a cerca de:bandeiras** `about:flags` : Permitir ou proibir o utilizador de aceder à página, que contém definições de programador e experimentais.
- **Substituição de aviso do SmartScreen para ficheiros**: Permita ou proíba que o utilizador ignore os avisos de filtro do SmartScreen sobre o descarregamento de ficheiros potencialmente maliciosos.
- **Substituição de aviso do SmartScreen**: Permita ou proíba que o utilizador ignore os avisos de filtro smartScreen sobre websites potencialmente maliciosos.
- **URL de primeira execução**: Especifique um website para exibir quando um utilizador abre o Edge pela primeira vez.

### <a name="windows-defender-antivirus"></a>Antivírus do Windows Defender

Estas definições destinam-se apenas a dispositivos que executam o Windows 10 e posteriormente.

- **Permitir a monitorização em tempo real**: Ative a pesquisa em tempo real de malware, spyware e outros softwares indesejados.
- **Permitir a monitorização do comportamento**: O Defender verifica certos padrões conhecidos de atividade suspeita em dispositivos.
- **Ativar o Sistema**de Inspeção de Rede : O Sistema de Inspeção da Rede (NIS) ajuda a proteger os dispositivos contra explorações baseadas em rede. Utiliza as assinaturas de vulnerabilidades conhecidas do Microsoft Endpoint Protection Center para ajudar a detetar e bloquear tráfego malicioso.
- **Scaneie todos os downloads:** O Defender digitaliza todos os ficheiros que descarrega a partir da internet.
- **Permitir a digitalização do script**: O Defender digitaliza scripts que são usados no Internet Explorer.
- Monitorizar a atividade de **ficheiros e programas**: O Defender monitoriza a atividade de ficheiros e programas nos dispositivos.
  - **Ficheiros monitorizados:** Escolha o tipo de ficheiros para monitorizar: todos, entrada ou saída.
- **Dias para rastrear malware resolvido**: O Defender continua a rastrear malware resolvido durante o número de dias que especifica. Em seguida, pode verificar manualmente os dispositivos anteriormente afetados. Se definir o número de dias para 0, o malware permanece na pasta quarentena e não é removido automaticamente. O valor máximo é de 90.
- **Permitir o acesso ui do cliente**: Controla se esconde a interface de utilizador do Defender dos utilizadores. Quando muda esta definição, entra em vigor da próxima vez que o dispositivo recomeçar.
- **Agende uma varredura**do sistema: Escolha uma varredura completa ou rápida que ocorra regularmente no dia e hora que selecionar:
  - **Dia agendado**: Escolha o dia programado quando o Defender eexecuta a varredura.
  - **Horário agendado**: Escolha a hora programada quando o Defender executa a varredura.
- **Agende uma sondagem rápida diária**: Escolha a hora programada quando o Defender fazer uma sondagem rápida todos os dias.
- Limite a utilização do **CPU durante uma varredura:** Delineie a percentagem do processador que o Defender pode utilizar quando executa uma varredura. Introduza um valor de 1 a 100.
- **Arquivo de digitalização:** Os ficheiros comprimidos do Defender, como ficheiros .zip ou .cab.
- **Scan e-mail mensagens**: O Defender digitaliza mensagens de correio eletrónico à medida que chegam ao dispositivo.
- **Scan e unidades amovíveis:** O defensor digitaliza unidades amovíveis, como os bastões USB.
- **Scan mapeado drives**: Os scans do Defender são mapeados para partilhas de rede. Por exemplo, `H:` está mapeado para o impulso pessoal de um utilizador. Se os ficheiros na unidade forem apenas de leitura, o Defender não pode remover qualquer malware que encontre lá.
- **Scaneie ficheiros abertos a partir de pastas partilhadas pela rede**: O Defender digitaliza ficheiros quando um utilizador os abre a partir de uma rede partilhada. Por exemplo, `\\server\share\file.doc`. Se o ficheiro da parte for apenas para leitura, o Defender não pode remover qualquer malware que encontre.
- Intervalo de **atualização de assinaturas:** Escolha o intervalo de tempo quando o Defender verificar se há novos ficheiros de assinatura.
- **Permitir a proteção na nuvem**: O Defender utiliza a nuvem da Microsoft para receber informações sobre a atividade de malware e ativar funcionalidades como bloquear à primeira vista.
- **Solicitação aos utilizadores para submissão de amostras**: Escolha o comportamento do Defender quando os ficheiros podem necessitar de uma análise mais aprofundada. Por exemplo, o Defender pode enviar automaticamente ficheiros para a Microsoft para determinar se são mal-intencionados.
- **Deteção de Aplicações potencialmente indesejadas**: Protege o dispositivo contra software de funcionamento classificado pela Defender como potencialmente indesejado. Pode proteger-se contra estas aplicações em execução ou utilizar o modo de auditoria para reportar quando um utilizador instala uma aplicação potencialmente indesejada.
- **Exclusões de ficheiros e pastas**: Adicione um ou mais ficheiros e pastas à lista de exclusões. Por exemplo, `C:\Path` ou `%ProgramFiles%\Path\filename.exe`. O Defender não inclui estes ficheiros e pastas em quaisquer exames em tempo real ou programados.
- **Exclusões**de extensão de ficheiros : Adicione uma ou mais extensões de ficheiros à lista de exclusões. Por exemplo, `java` ou `exe`. O Defender não inclui ficheiros com estas extensões em nenhum scans em tempo real ou programado.
- **Exclusões de processos**: Adicione processos específicos à lista de exclusões. Por exemplo, `C:\path\myproc.exe`. Este tipo de exclusão apenas `exe` `com`suporta `scr`as seguintes extensões: , ou . O Defender não inclui estes processos em nenhum scans em tempo real ou programado.

### <a name="additional-settings"></a>Configurações adicionais

Na página **definições** do dispositivo do assistente, se selecionar a opção de **configurar configurações adicionais que não se encontram nos grupos de definição predefinidos,** utilize esta página de **Definições Adicionais** para configurar essas definições. Selecione **Adicionar** e, em seguida, escolher entre a lista de definições móveis disponíveis. Escolha **Selecione** para modificar a definição incorporada ou **criar definição** para criar um valor de registo personalizado ou tipo de definição OMA URI.

## <a name="next-steps"></a>Passos seguintes

[Monitorizar as definições de compatibilidade](../../compliance/deploy-use/monitor-compliance-settings.md)
