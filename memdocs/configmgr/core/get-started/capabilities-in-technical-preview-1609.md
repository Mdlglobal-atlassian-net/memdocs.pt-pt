---
title: Capacidades na Pré-visualização Técnica 1609
titleSuffix: Configuration Manager
description: Conheça as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: e7e803dd1cbacbbd65a5f2968e217656b088d281
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721536"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Capacidades na Pré-visualização Técnica 1609 para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo de pré-visualização técnica)*



Este artigo introduz as funcionalidades disponíveis na Pré-visualização Técnica para O Gestor de Configuração, versão 1609. Pode instalar esta versão para atualizar e adicionar novas capacidades ao site de pré-visualização técnica do Gestor de Configuração.      Antes de instalar esta versão da pré-visualização técnica, reveja o tópico introdutório, [A Pré-Visualização Técnica para O Gestor de Configuração,](../../core/get-started/technical-preview.md)para se familiarizar com os requisitos e limitações gerais para utilizar uma pré-visualização técnica, como atualizar entre versões e como fornecer feedback sobre as funcionalidades numa pré-visualização técnica.    

**Questões Conhecidas nesta Pré-Visualização Técnica:**  
*  Quando atualizar para o Diretor de Configuração 1609 A Pré-visualização Técnica, quaisquer políticas de atualização de edição que tenha implementado serão eliminadas. Para continuar a usar estas políticas, é preciso recriá-las e implantá-las.


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

## <a name="improvements-to-endpoint-protection"></a>Melhorias na Proteção do Ponto Final
Melhoria das definições de política antimalware de proteção de ponto final - Pode agora especificar o nível em que o Serviço de Proteção à Nuvem de Proteção de Pontos Finais bloqueará ficheiros suspeitos. Uma nova definição permite que os administradores especifiquem computadores "arriscados" com base nas elevadas quantidades de malware que encontram.

## <a name="increased-number-of-enrolled-devices"></a>Aumento do número de dispositivos matriculados
Os administradores podem agora permitir que os utilizadores matriculem até 15 dispositivos na gestão de dispositivos móveis híbridos com a Intune. O limite era de 5 dispositivos por utilizador anteriormente.

## <a name="additional-apple-dep-settings"></a>Definições adicionais do Apple DEP

Os administradores podem agora configurar as seguintes definições do Programa de Inscrição de Dispositivos da Apple (DEP) no perfil DEP para dispositivos iOS e Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Se ativado, o Assistente de Configuração da Apple solicita este serviço durante a ativação do dispositivo.

## <a name="integration-with-upgrade-analytics"></a>Integração com Upgrade Analytics

A análise de upgrade permite avaliar e analisar a prontidão e compatibilidade do dispositivo com o Windows 10, para permitir atualizações mais fáceis e suaves. Com a integração do Upgrade Analytics com O Gestor de Configuração, pode aceder aos dados de compatibilidade de upgrade na consola de administração do Gestor de Configuração e, em seguida, a partir da lista de dispositivos, dispositivos-alvo para atualização ou reparação.

Pode ler mais sobre upgrade Analytics em [Get started com Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Tipos de ligação nativa para perfis híbridos VPN do Windows 10

Ao utilizar o Gestor de Configuração com o Intune, pode agora criar perfis VPN do Windows 10 com tipos de ligação Microsoft Automatic, IKEv2, PPTP e L2TP na consola 'Gestor de Configuração' sem utilizar o OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Melhorias na Windows Store para integração de negócios com Gestor de Configuração

Neste lançamento, atualizámos o [Windows Store para integração de negócios](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) com estas novas funcionalidades:

**Atualização:** No atual lançamento técnico de pré-visualização, a função de sincronização imediata não está funcional.

- Anteriormente, só podia implementar aplicações gratuitas a partir da Windows Store for Business. O Gestor de Configuração suporta agora ainda a implementação de aplicações licenciadas online pagas (apenas para dispositivos matriculados no Intune).
- Pode agora iniciar uma sincronização imediata entre a Windows Store para Business e Configuration Manager.
- Agora pode modificar a chave secreta do cliente que obteve do Azure Ative Directory

### <a name="try-it-out"></a>Experimente!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Comprar e sincronizar uma aplicação licenciada online paga

1. Compre uma aplicação licenciada online paga na Windows Store for Business.
2. No espaço de trabalho da **Administração** da consola De Configuração Manager, clique em**Atualizações** > de **Serviços** > cloud e na manutenção**da Windows Store para negócios**.
3. No separador **Home,** no grupo **Sync,** clique em **Sync Now**.
4. Pouco depois, a aplicação que adquiriu aparecerá no nó de Informações de **Licença para Aplicações** de Loja do espaço de trabalho de Gestão de **Aplicações.**

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Criar e implementar uma aplicação de Gestor de Configuração a partir dos dados da aplicação sincronizada

O procedimento para criar e implementar uma aplicação De Configuração Manager a partir de uma aplicação de loja paga é o mesmo que para criar uma aplicação a partir de uma aplicação gratuita. Consulte a secção **Criar e implementar uma aplicação de Gestor de Configuração a partir de uma aplicação Windows Store for Business** na Manage apps da Windows Store for Business com O Gestor de [Configuração](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modificar a chave secreta do cliente do Diretório Ativo Azure

1. No espaço de trabalho da **Administração** da consola De Configuração Manager, clique em**Atualizações** > de **Serviços** > cloud e na manutenção**da Windows Store para negócios**.
2. Selecione a sua conta Windows Store para negócios e, em seguida, clique em **Propriedades**.
3. Na caixa de diálogo **Windows Store for Business Account Properties,** introduza uma nova tecla no campo de chaves secreto do **Cliente** e, em seguida, clique em **Verificar**. Uma vez verificado, clique em **Aplicar**e, em seguida, feche a caixa de diálogo.


## <a name="new-compliance-settings-for-configuration-items"></a>Novas definições de conformidade para itens de configuração

Adicionámos muitas novas definições que pode utilizar nos seus itens de configuração para várias plataformas de dispositivos.
Estas são configurações que existiam anteriormente no Microsoft Intune numa configuração autónoma, e estão agora disponíveis quando utiliza o Intune com o 'Configuração Manager'.
Se precisar de ajuda com qualquer uma destas definições, abra [as definições de Manage e funcionalidades nos seus dispositivos com as políticas Microsoft Intune](/mem/intune/configuration/device-profiles) e, em seguida, selecione as definições subtópicos para a plataforma que deseja.


### <a name="new-settings-for-android-devices"></a>Novas definições para dispositivos Android

#### <a name="password-settings"></a>Definições de palavra-passe

- **Memorizar histórico de palavras-passe**
- **Permitir desbloqueio por impressão digital**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória nos cartões de armazenamento**
- **Permitir captura de ecrã**
- **Permitir submissão de dados de diagnóstico**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir browser**
- **Permitir preenchimento automático**
- **Permitir bloqueador de janelas de pop-up**
- **Permitir cookies**
- **Permitir scripting ativo**

#### <a name="app-settings"></a>Definições da aplicação

- **Permitir loja do Google Play**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo

- **Permitir armazenamento amovível**
- **Permitir partilha de Wi-Fi**
- **Permitir geolocalização**
- **Permitir NFC**
- **Permitir Bluetooth**
- **Permitir chamadas em roaming**
- **Permitir roaming de dados**
- **Permitir mensagens SMS/MMS**
- **Permitir assistente de voz**
- **Permitir marcação por voz**
- **Permitir copiar e colar**


### <a name="new-settings-for-ios-devices"></a>Novas definições para dispositivos iOS

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Minutos de inatividade antes da palavra-passe ser exigida**
- **Memorizar histórico de palavras-passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Novas definições para dispositivos Mac OS X

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número de carateres complexos necessários na palavra-passe**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**
- **Minutos de inatividade antes de a proteção de ecrã ser ativada**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Novas definições para dispositivos desktop e mobile do Windows 10

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Memorizar histórico de palavras-passe**
- **Exija uma senha quando o dispositivo regressar de um estado ocioso**

#### <a name="security-settings"></a>Definições de segurança

- **Encriptação obrigatória no dispositivo móvel**
- **Permitir anular inscrições manualmente**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo

- **Permitir VPN sobre redes móveis**
- **Permitir roaming do VPN sobre redes móveis**
- **Permitir reposição do telefone**
- **Permitir ligação USB**
- **Permitir Cortana**
- **Permitir notificações de centro de ação**

### <a name="new-settings-for-windows-10-team-devices"></a>Novas definições para dispositivos da Equipa Windows 10

#### <a name="device-settings"></a>Definições do dispositivo

- **Ativar as Informações Operacionais do Azure**
- **Ativar projeção sem fios Miracast**
- **Escolher as informações de reunião apresentadas no ecrã de boas-vindas**
- **URL da imagem de fundo do ecrã de bloqueio**


### <a name="new-settings-for-windows-81-devices"></a>Novas definições para dispositivos Windows 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Tipo obrigatório de palavra-passe**
- **Número mínimo de conjuntos de carateres**
- **Comprimento mínimo da palavra-passe**
- **Número de falhas de início de sessão consecutivas permitidas antes de o dispositivo ser apagado**
- **Minutos de inatividade antes de o ecrã se desligar**
- **Expiração da Palavra-passe (dias)**
- **Memorizar histórico de palavras-passe**
- **Impedir a reutilização de palavras-passe anteriores**
- **Permitir palavra-passe por imagem e PIN**

#### <a name="browser-settings"></a>Definições do browser

- **Permitir deteção automática de rede intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Novas definições para dispositivos Windows Phone 8.1

#### <a name="applicability-settings"></a>Definições de aplicabilidade

- **Aplicar todas as configurações ao Windows 10**

#### <a name="password-settings"></a>Definições de palavra-passe

- **Número mínimo de conjuntos de carateres**
- **Permitir palavras-passe simples**
- **Memorizar histórico de palavras-passe**

#### <a name="device-capability-settings"></a>Definições da capacidade do dispositivo

- **Permitir ligação automática a hotspots Wi-Fi**


## <a name="improvements-for-boundary-groups"></a>Melhorias para os grupos de fronteira
Esta pré-visualização introduz mudanças importantes nos grupos de fronteira e como funcionam com pontos de distribuição. Estas alterações ajudarão a simplificar o design da sua infraestrutura de conteúdo, ao mesmo tempo que lhe dará mais controlo sobre como e quando os clientes recuam para pesquisar pontos de distribuição adicionais como localizações de fonte de conteúdo. Isto inclui tanto no local como nos pontos de distribuição baseados na nuvem.

Estas melhorias substituem conceitos e comportamentos que pode conhecer hoje (como configurar pontos de distribuição para serem rápidos ou lentos) e substitui-os por um novo modelo que deve ser mais fácil de configurar e manter. Estas alterações são também bases para futuras alterações que melhorarão outras funções do sistema de sites que associa a grupos de fronteira.  

Durante a atualização para 1609, a atualização converte as configurações atuais do grupo de limites para se adaptar ao novo modelo para que estas alterações não perturbem as configurações de distribuição de conteúdos (ver [Atualizar os grupos de fronteira existentes para o novo modelo).](capabilities-in-technical-preview-1609.md#bkmk_update)

As seguintes secções detalham as alterações introduzidas com esta pré-visualização, como funciona o novo modelo e o que se pode esperar na atualização de um site que já tem grupos de fronteira configurados.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Alterações na UI e comportamento para grupos de fronteiras e localizações de conteúdos
Seguem-se as principais alterações aos grupos de fronteira e à forma como os clientes encontram conteúdo. Muitas destas mudanças e conceitos trabalham em conjunto.
- **As configurações para fast ou slow são removidas:** Já não configura pontos de distribuição individuais para ser rápido ou lento.  Em vez disso, cada sistema de site associado a um grupo de fronteiras é tratado da mesma forma. Devido a esta alteração, o separador **Referências** das propriedades do grupo de fronteira já não suporta a configuração de Fast ou Slow.
- **Novo grupo de limites padrão em cada site:**  Cada site primário tem um novo grupo de limites padrão chamado ***\<Padrão-Site-Boundary-Group sitecode>***.  Quando um cliente não está numa localização de rede que é atribuída a um grupo de limites, esse cliente utilizará os sistemas de site associados ao grupo padrão a partir do seu site designado. Planeie usar este grupo de fronteiras como substituto do conceito de localização de conteúdo de recuo.    
  -  **'Permitir localizações de origem de recaídas para conteúdo'** é removido: Já não configura explicitamente um ponto de distribuição a utilizar para o recuo e as opções para o definir são removidas da UI.

  Além disso, o resultado da definição Permitir que os **clientes utilizem uma localização de origem de recuo para conteúdo** num tipo de implementação para aplicações mudou. Esta definição num tipo de implementação permite agora que um cliente utilize o grupo de limites do site padrão como uma localização de fonte de conteúdo.

  -  **Relações de grupos de fronteira:** Cada grupo de fronteiras pode ser ligado a um ou mais grupos de fronteira adicionais. Estes links formam relações que são configuradas no novo separador de propriedades do grupo de fronteira chamado **Relacionamentos:**
  -   Cada grupo de fronteira saciado diretamente é chamado de grupo de fronteira **atual.**  
  -   Qualquer grupo de fronteira que um cliente possa usar devido a uma associação entre o atual grupo de *fronteiras* desse cliente e outro grupo é chamado de grupo de fronteira sinuoso. **neighbor**
  -  É no separador **Relationships** que se adicionam grupos de fronteira que podem ser usados como um grupo de fronteira *sinuoso.* Também pode configurar um tempo em minutos que determina quando um cliente que não encontra conteúdo a partir de um ponto de distribuição no grupo *atual* começará a pesquisar localizações de conteúdo a partir desses grupos de fronteira *sinuosos.*

      Quando adicionar ou alterar uma configuração de grupo de limites, terá a opção de bloquear o recuo para esse grupo de fronteira específico do grupo atual que está a configurar.

  Para utilizar a nova configuração, define associações explícitas (links) de um grupo de fronteira para outro, e configura todos os pontos de distribuição desse grupo associado com o mesmo tempo em minutos. O tempo que configura determina quando um cliente que não encontra uma fonte de conteúdo do seu grupo de limites *atual* pode começar a procurar fontes de conteúdo desse grupo de fronteira sinuoso.

  Além dos grupos de fronteira que configura explicitamente, cada grupo de fronteira tem uma ligação implícita ao grupo de fronteira do site predefinido. Este link torna-se ativo após 120 minutos em que o grupo de fronteira do site padrão se torna um grupo de fronteira sinuoso que permite que os clientes utilizem os pontos de distribuição associados a esse grupo de fronteira como localizações de fonte de conteúdo.

  Este comportamento substitui o que anteriormente era referido como recuo para o conteúdo.  Pode anular este comportamento padrão de 120 minutos associando explicitamente o grupo de fronteira do site padrão a um grupo *atual,* e definindo um tempo específico em minutos, ou bloqueando totalmente o recuo para impedir a sua utilização.


- **Os clientes tentam obter conteúdo de cada ponto de distribuição por até 2 minutos:** Quando um cliente procura uma localização de fonte de conteúdo, tenta aceder a cada ponto de distribuição durante 2 minutos antes de tentar outro ponto de distribuição. Esta é uma mudança em versões anteriores em que os clientes tentaram ligar-se a um ponto de distribuição por até 2 horas.

  - O primeiro ponto de distribuição que um cliente tenta utilizar é selecionado aleatoriamente a partir do conjunto de pontos de distribuição disponíveis no *atual* grupo de fronteiras do cliente (ou grupos).

  - Após dois minutos, se o cliente não tiver encontrado o conteúdo, muda para um novo ponto de distribuição e tenta obter conteúdo desse servidor. Este processo repete-se de dois em dois minutos até que o cliente encontre o conteúdo ou chegue ao último servidor na sua piscina.

  - Se um cliente não conseguir encontrar uma localização de origem de conteúdo válida a partir do seu pool *atual* antes do período de recuo para um grupo de fronteira *sinuoso,* o cliente adiciona então os pontos de distribuição desse grupo *vizinho* ao final da sua lista atual, e depois procurará o grupo expandido de locais de origem que inclui os pontos de distribuição de ambos os grupos de fronteira.

      > [!TIP]  
      > Quando cria uma ligação explícita do grupo de fronteira atual para o grupo de fronteira do site padrão e define um tempo de recuo inferior ao tempo de recuo para uma ligação a um grupo de fronteiras vizinho, os clientes começarão a procurar localizações de origem do grupo de fronteira do site padrão antes de incluir o grupo vizinho.

  - Quando o cliente não obtém conteúdo do último servidor da piscina, inicia novamente o processo.


### <a name="how-the-new-model-works"></a>Como funciona o novo modelo
Ao configurar grupos de fronteiras, associa limites (localizações de rede) e funções do sistema de site, como pontos de distribuição, ao grupo de fronteiras. Isto ajuda a ligar clientes a servidores do sistema de sites, como pontos de distribuição que estão localizados perto dos clientes da rede.   
- Pode atribuir o mesmo limite a vários grupos de fronteira
- Servidores do sistema do site, como pontos de distribuição, podem ser associados a vários grupos de fronteira, disponibilizando-os a uma ampla gama de localizações de rede
- Se um ponto de distribuição não estiver associado a um grupo de limites, os clientes não poderão utilizar esse ponto de distribuição como uma localização de fonte de conteúdo.

Começando com esta pré-visualização técnica, define as relações de grupo de limites para configurar o comportamento de recuo para localizações de fonte de conteúdo. Este novo comportamento está configurado no novo separador **Relationships** das propriedades do grupo de fronteira e substitui a configuração dos sistemas do site para ser lento ou rápido, e configurar um grupo de limites para permitir a localização da fonte de recuo para o conteúdo.

No separador Relationships adiciona-se outros grupos de fronteira para configurar uma relação com esses grupos. Cada relação é uma ligação de sentido único **do** atual grupo de fronteiras ao grupo de fronteira que você adiciona, que é chamado de **vizinho**. Para cada link que cria, pode configurar pontos de distribuição com um tempo de recuo em minutos. Este tempo é usado para determinar após quanto tempo os clientes *do* atual grupo de fronteira podem começar a usar pontos de distribuição no grupo de fronteira *do vizinho* se não forem capazes de encontrar uma localização de fonte de conteúdo válida do seu grupo de fronteira atual.

Quando um cliente não consegue encontrar conteúdo e começa a pesquisar locais de grupos de fronteira vizinhos, aumenta o conjunto de pontos de distribuição disponíveis para esse cliente de forma controlada.  

- Um grupo de fronteiras pode ter mais do que uma relação. Isto permite configurar o recuo a diferentes vizinhos para ocorrer após diferentes períodos de tempo.
- Os clientes só vão recuar para um grupo de fronteiras que é um vizinho direto do seu atual grupo de fronteiras.
- Quando um cliente é membro de vários grupos de fronteira, o atual grupo de fronteiras é definido como uma união de todos os grupos de fronteira do cliente.  Esse cliente pode então recorrer a um vizinho de qualquer um desses grupos de fronteira originais.

Além dos links que define, existe uma ligação implícita que é criada automaticamente entre os grupos de fronteira que cria e o grupo de limites padrão que é automaticamente criado para cada site. Esta ligação automática:
- É utilizado por clientes que não estejam num limite associado a qualquer grupo de limites na sua hierarquia, utilize automaticamente o grupo de limites padrão do seu site designado para identificar localizações de fonte de conteúdo válidas.   
-  É uma opção de recuo padrão do grupo de fronteira atual para o grupo de limite padrão dos sites que é usado após 120 minutos.

**Exemplo de utilização do novo modelo:** Cria três grupos de fronteira que não partilham limites ou servidores do sistema de site:
- Grupo BG_A com pontos de distribuição DP_A1 e DP_A2 associados ao grupo
- Grupo BG_B com pontos de distribuição DP_B1 e DP_B2 associados ao grupo
- Grupo BG_C com pontos de distribuição DP_C1 e DP_C2 associados ao grupo

Adiciona as localizações de rede dos seus clientes como limites apenas ao grupo de fronteiras BG_A, e depois configura relações desse grupo de fronteira para os outros dois grupos de fronteira:
- Configura pontos de distribuição para o primeiro grupo *vizinho* (BG_B) a ser usado após 10 minutos. Este grupo contém pontos de distribuição DP_B1 e DP_B2. Ambos estão bem ligados aos locais de fronteira dos primeiros grupos.
- Configura o segundo grupo *vizinho* (BG_C) a ser utilizado após 20 minutos. Este grupo contém pontos de distribuição DP_C1 e DP_C2. Ambos estão do outro lado de um WAN dos outros dois grupos de fronteira.
- Também adiciona um ponto de distribuição adicional que está localizado no servidor do site para o grupo de limite sinuoso do site. Esta é a sua localização de origem de conteúdo menos preferencial, mas está centralmente localizada em todos os seus grupos de fronteira.

  Exemplo de grupos de fronteiras e tempos de recuo:

  ![BG_Fallack](media/BG_Fallback.png)


Com esta configuração:
- O cliente começa a procurar conteúdo a partir de pontos de distribuição no *seu* atual grupo de fronteira (BG_A), pesquisando cada ponto de distribuição por dois minutos antes de mudar para o próximo ponto de distribuição no grupo de fronteira. O conjunto de clientes de locais de origem de conteúdo válidoinclui DP_A1 e DP_A2.
- Se o cliente não encontrar conteúdo do *seu* atual grupo de fronteira seleções após 10 minutos de pesquisa, adiciona os pontos de distribuição do grupo de fronteira BG_B à sua pesquisa. Em seguida, continua a procurar conteúdo a partir de um ponto de distribuição no seu conjunto combinado de pontos de distribuição que agora inclui os dos grupos de fronteira BG_A e BG_B. O cliente continua a contactar cada ponto de distribuição durante dois minutos antes de mudar para o próximo ponto de distribuição a partir da sua piscina. O conjunto de clientes de locais de origem de conteúdo válidoinclui DP_A1, DP_A2, DP_B1 e DP_B2.
- Após mais 10 minutos (20 minutos no total) se o cliente ainda não tiver encontrado um ponto de distribuição com conteúdo, expande o seu conjunto de pontos de distribuição disponíveis para incluir os do segundo grupo *vizinho,* grupo de fronteiraBG_C. O cliente tem agora 6 pontos de distribuição para pesquisa (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua a mudar para um novo ponto de distribuição a cada dois minutos até que o conteúdo seja encontrado.
- Se o cliente não tiver encontrado conteúdo após um total de 120 minutos, recua para incluir o grupo de fronteira do *site padrão* como parte da sua pesquisa contínua. Agora, o conjunto de pontos de distribuição inclui todos os pontos de distribuição dos três grupos de fronteira configurados e o ponto de distribuição final localizado no computador do servidor do site.  O cliente continua então a sua pesquisa de conteúdo, alterando pontos de distribuição de dois em dois minutos até que o conteúdo seja encontrado.

Ao configurar os diferentes grupos vizinhos para estarem disponíveis em diferentes momentos, controla quando os pontos de distribuição específicos são adicionados como uma localização de fonte de conteúdo, e quando, ou se, o cliente usa o recuo para o grupo de fronteira do site padrão como uma rede de segurança para conteúdos que não estão disponíveis em qualquer outro local.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Atualizar os grupos de fronteira existentes para o novo modelo
Quando instala a versão 1609 e atualiza o seu site, as seguintes configurações são automaticamente feitas. Estes destinam-se a garantir que o seu comportamento atual de recuo permanece disponível, até configurar novos grupos de fronteira e relacionamentos.  
- Os pontos de distribuição desprotegidos de um site são adicionados ao código de site do grupo de limites do *Site-Boundary-Group\<>* grupo de fronteira seletiva.
- Uma cópia é feita de cada grupo de fronteira existente que inclui um servidor de site configurado com uma ligação lenta. O nome do novo grupo é *** \<o nome original do grupo de fronteira>-Slow-Tmp:***  
  -   Os sistemas do site que têm uma ligação rápida são deixados no grupo de fronteira original.
  -   Uma cópia dos sistemas do site que têm uma ligação lenta são adicionadas à cópia do grupo de fronteira. Os sistemas originais do site configurados como lentopermanecem no grupo de fronteira original para a compatibilidade retrógrada, mas não são usados a partir desse grupo de fronteira.
  -   Esta cópia de grupo de fronteiras não tem limites associados a ela. No entanto, é criada uma ligação de recuo entre o grupo original e a nova cópia do grupo de fronteira que tem o tempo de recuo definido para zero.

  A tabela que se segue identifica o novo comportamento de recuo que pode esperar da combinação das configurações originais de implementação e ponto de distribuição:

Configuração de implementação original para "Não executar programa" em rede lenta  |Configuração original do ponto de distribuição para "Permitir que o cliente utilize uma localização de origem de recuo para conteúdo"  |Novo comportamento de recuo  
---------|---------|---------
Selecionado     |  Selecionado    |  **Sem recuo** - Utilize apenas os pontos de distribuição no atual grupo de fronteiras       
Selecionado     |  Não selecionado|  **Sem recuo** - Utilize apenas os pontos de distribuição no atual grupo de fronteiras       
Não selecionado |  Não selecionado|  **Fallback to neighbor** - Use os pontos de distribuição no grupo de fronteira atual, e, em seguida, adicione os pontos de distribuição do grupo de fronteira vizinho. A menos que seja configurado um link explícito para o grupo de limites do site predefinido, os clientes não recaíram para esse grupo.    
Não selecionado | Selecionado |   **Recuo normal** - Use pontos de distribuição no atual grupo de fronteira, em seguida, os dos grupos de fronteira padrão vizinho e local

 Todas as outras configurações de implementação resultam em **recuo normal**.  



## <a name="office-365-client-management-dashboard"></a>Painel de gestão de clientes do Office 365  
A Pré-visualização Técnica 1609 do Gestor de Configuração introduz um novo painel de instrumentos. Para ver o dashboard, na consola do Gestor de Configuração vá ao Gabinete de**Visão Geral** > da **Biblioteca** > de Software**365 Gestão**de Clientes .
>[!NOTE]
>No **What's New** space na consola 'Configuração Manager', o novo painel de instrumentos é incorretamente nomeado Painel de **Assistência do Office 365**.

O painel de instrumentos exibe gráficos para o seguinte:

- Número de clientes do Office 365
- Versões de clientes do Office 365
- Escritório 365 línguas de cliente
- Escritório 365 canais de clientes     
Para obter mais informações, veja [Overview of update channels for Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx) (Descrição geral dos canais de atualização do Office 365 ProPlus).
- Regras de implantação automática que têm o Office 365 Client selecionado no conjunto de produtos disponíveis.

Pode tomar as seguintes ações no painel de instrumentos:
- Na parte superior do painel de instrumentos, utilize a definição de drop-down **da Recolha** para filtrar os dados do painel de instrumentos pelos membros de uma recolha específica.
- No lado superior direito do painel de instrumentos, clique no **Office 365 Installer** para iniciar o Assistente de Instalação de Clientes do Office 365 para implementar as aplicações do Office 365 para os clientes. Para mais detalhes, consulte [o Deploy Office 365 apps para clientes.](#deploy-office-365-apps-to-clients)
- No lado médio-direito do painel de instrumentos, clique em **Criar um ADR** para abrir o Assistente de Regra de Implementação Automática para criar uma nova regra de implementação automática (ADR). Para criar um ADR para aplicações do Office 365, selecione **Office 365 Client** quando escolher o produto. Para mais informações, consulte [a implementação automática](../../sum/deploy-use/automatically-deploy-software-updates.md)de atualizações de software .
- No lado inferior direito do painel de instrumentos, clique em **Criar Definições** de Agente cliente para abrir as definições do Agente cliente. Para mais informações, consulte [as definições do cliente](../clients/deploy/about-client-settings.md).



Para mais informações sobre as atualizações do Office 365 ProPlus, consulte [as atualizações do Manage Office 365 ProPlus com o Gestor](../../sum/deploy-use/manage-office-365-proplus-updates.md)de Configuração .

## <a name="deploy-office-365-apps-to-clients"></a>Implementar aplicações do Office 365 para clientes
Neste comunicado, a partir do painel de gestão de clientes do Office 365, pode iniciar o Instalador office 365 que lhe permite configurar as definições de instalação do Office 365, transferir ficheiros das Redes de Entrega de Conteúdos do Office (CDNs) e implementar os ficheiros como uma aplicação no Gestor de Configuração.

### <a name="limitations-of-office-365-deployment"></a>Limitações da implantação do Office 365
- Pode ter problemas quando tenta importar as definições de clientes existentes (XML) no assistente de instalação de aplicações do Office 365. Pode configurar manualmente as definições do cliente sem problemas.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Para implementar as aplicações do Office 365 para clientes
1. Na consola de Gestor de Configuração, navegue para o Gabinete de**Visão Geral** > da **Biblioteca** > de Software**365 Gestão**de Clientes.
2. Clique no **Instalador do Office 365** no painel superior direito. Abre o Assistente de Instalação de Clientes do Office 365.
3. Na página Definições de **Aplicação,** forneça um nome e descrição para a aplicação, introduza o local de descarregamento dos ficheiros e, em seguida, clique em **Next**. Note que a localização deve ser especificada no formulário &#92;&#92;*servidor*&#92;*partilhar*.
4. Na página definições do **Cliente importado,** escolha se importa as definições do cliente do Office 365 a partir de um ficheiro de configuração XML existente ou para especificar manualmente as definições e, em seguida, clique em **Next**.
Quando tiver um ficheiro de configuração existente, introduza a localização do ficheiro e salte para o passo 7. Note que a localização deve ser especificada no formulário &#92;&#92;*servidor*&#92;*partilhar*&#92;nome *de ficheiro*. XML.

    > [!IMPORTANT]
    >Pode ter problemas quando tenta importar as definições de clientes existentes (XML) nesta pré-visualização técnica.

5. Na página de **Produtos do Cliente,** selecione a suite Office 365 que utiliza, selecione as aplicações que pretende incluir, selecione quaisquer produtos adicionais do Office que devam ser incluídos e, em seguida, clique em **Next**.
6. Na página Definições do **Cliente,** escolha as definições para incluir e, em seguida, clique em **Seguinte**.
7. Na página **de Implementação,** escolha se implementa a aplicação e, em seguida, clique em **Seguinte**.
Se optar por não colocar a embalagem no assistente, salte para o passo 9.
8. Configure o restante das páginas do assistente como faria para uma implementação típica da aplicação. Para mais informações, consulte [Criar e implementar uma aplicação](../../apps/get-started/create-and-deploy-an-application.md).
9. Conclua o assistente.
10. Pode implementar ou editar a aplicação tal como faria com qualquer outra aplicação no Diretor de Configuração a partir de**Aplicações**de**Gestão** > de Aplicações de**Visão Geral** > da Biblioteca > de **Software.**

>[!NOTE]
>Depois de implementar aplicações do Office 365, pode criar regras de implementação automáticas para manter as aplicações. Para criar um ADR para aplicações do Office 365, clique em **Criar um ADR,** e selecione **Office 365 Client** quando escolher o produto. Para mais informações, consulte [a implementação automática](../../sum/deploy-use/automatically-deploy-software-updates.md)de atualizações de software .

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Melhorias do BIOS à conversão UEFI
Agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o passo do Restart Computer prepare uma partição FAT32 no disco rígido para a transição para o UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para a conversão BIOS para A UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Numa sequência de tarefas existente para instalar um sistema operativo, irá adicionar um novo grupo com passos para fazer o BIOS à conversão UEFI.

1. Crie um novo grupo de sequência de tarefas após os passos para capturar ficheiros e configurações, e antes dos passos para instalar o sistema operativo. Por exemplo, crie um grupo após o grupo **De captura de Ficheiros e Definições** denominado **BIOS-to-UEFI**.
2. No separador **Opções** do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **_SMSTSBootUEFI** não é **igual** a **verdadeiro**. Isto impede que os passos do grupo sejam funcionados quando um computador já se encontra no modo UEFI.
![BIOS para o grupo UEFI](media/BIOS-to-UEFI-group.png)
3. Sob o novo grupo, adicione o passo da sequência de tarefas **restart Computer.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada** para iniciar o computador no Windows PE.  
4. No separador **Opções,** adicione uma variável de sequência de tarefas como uma condição em que **_SMSTSInWinPE é igual a falso**. Isto impede que este passo seja decorrido se o computador já estiver no Windows PE.

    ![Reiniciar passo do computador](media/Restart-in-Windows-PE.png)
5. Adicione um passo para iniciar a ferramenta OEM que converterá o firmware de BIOS para UEFI. Este será normalmente um passo de sequência de tarefa de Linha de **Comando de Execução** com uma linha de comando para iniciar a ferramenta OEM.
5. Adicione o passo de sequência de tarefas do Formato e do Disco de Partição que irá dividir e formatar o disco rígido. No passo, faça o seguinte:
    1. Crie a partição FAT32 que será convertida para UEFI antes da instalação do sistema operativo. Escolha **GPT** para **o tipo de disco**.
    ![Passo do disco de formato e divisória](media/Format-and-partition-disk.png)
    2. Vá para as propriedades para a partição FAT32. Introduza **o TSUEFIDrive** no campo **Variável.** Quando a sequência de tarefas detetar esta variável, preparar-se-á para a transição UEFI antes de reiniciar o computador.
    ![Propriedades de partição](media/Partition-properties.png)
    3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para salvar o seu estado e armazenar ficheiros de registo.
6. Adicione o passo da sequência de tarefas **do Computador Restart.** Em **Especificar o que executar após o reinício,** selecione A imagem de arranque atribuída a esta sequência de **tarefas é selecionada** para iniciar o computador no Windows PE.  




## <a name="intune-compliance-charts"></a>Gráficos de conformidade intune
Nesta versão, pode obter uma visão rápida da conformidade geral dos dispositivos e das principais razões para o incumprimento utilizando novas tabelas no âmbito do espaço de **trabalho de Monitorização** na consola Do Gestor de Configuração.

#### <a name="to-view-the-intune-compliance-charts"></a>Para ver as tabelas de conformidade intune
1. Na consola 'Gestor de Configuração', vá a **monitorizar** > **as definições**de conformidade da**visão geral** > .
2. A tabela geral de conformidade com o **dispositivo** é apresentada.
3. Clique no nó de Política de **Conformidade** para ver os gráficos **de conformidade geral** do dispositivo e **principais razões de incumprimento.**

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitações dos gráficos de conformidade intune em TP 1609
- A perfuração para a tabela global de conformidade com o **dispositivo** produz atualmente um erro.
- O gráfico **principais motivos de incumprimento** lista o nome da apólice e não as razões individuais de incumprimento. Pode clicar na política para perfurar e ver os dispositivos que não estão em conformidade com essa política.

### <a name="try-it-out"></a>Experimente
Complete as seguintes secções por ordem:

#### <a name="check-overall-compliance-chart"></a>Verifique o gráfico geral de conformidade
1. Adicione em duas políticas de conformidade iOS no Gestor de Configuração. Uma das definições deve ter um conjunto de definições para dispositivos (por exemplo, definir o comprimento PIN para 6). A outra política deve ter outro conjunto de configurações (por exemplo, complexidade PIN). As definições políticas não devem sobrepor-se ou estar em conflito.
2. Implemente as duas políticas para um conjunto de utilizadores.
3. Inscreva dois dispositivos iOS em Intune utilizando a mesma conta de utilizador, e uma conta que recebeu as apólices no escalão anterior. Os dispositivos não devem satisfazer os critérios da política de conformidade.
4. No 'Gestor de Configuração', verifique o gráfico geral de conformidade do **dispositivo.** Ambos os dispositivos devem apresentar-se como incompatíveis.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Consulte o gráfico das principais razões de incumprimento
5. Verifique o gráfico **principais motivos de incumprimento.** Este gráfico enumera as 5 principais razões para o incumprimento, mas quando apenas duas definições de conformidade foram definidas entre as políticas, apenas são apresentadas as 2 principais razões de incumprimento.
6. Clique numa das secções da tabela. Ambos os dispositivos devem aparecer na vista filtrada no dispositivo de**visão geral** >  **de Ativos e Conformidade** > **.**

#### <a name="make-devices-compliant-and-check-the-charts"></a>Tornar os dispositivos conformes e verificar os gráficos
7. Faça um dos dispositivos em conformidade com uma das políticas. Volte a verificar a tabela de conformidade geral do **dispositivo.** O gráfico deve apresentar um dispositivo compatível e um dispositivo não conforme.
8. Faça com que o outro dispositivo cumpra a mesma política. Isto fará com que um dispositivo seja compatível com ambas as políticas e um dispositivo em conformidade com apenas uma das políticas.
9. Verifique o gráfico **principais motivos de incumprimento.** Só deve haver uma razão de incumprimento enumerada.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Veja também
[Pré-visualização técnica para gestor de configuração](../../core/get-started/technical-preview.md)
