---
title: Gerir as políticas da Guarda de Aplicações
titleSuffix: Configuration Manager
description: Saiba como criar e implementar políticas de Guarda de Aplicações do Windows Defender
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b691004742def4c126ba82b07cad1651cbe822f8
ms.sourcegitcommit: 13ceb4e1cc8c2a10bfa199e301bf9bada8ceb268
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82923431"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política de guarda de aplicações do Windows Defender

*Aplica-se a: Gestor de Configuração (ramo atual)*
<!-- 1351960 -->  
Pode criar e implementar as políticas de Guarda de [Aplicações do Windows Defender (Application Guard)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) utilizando a proteção do ponto final do Gestor de Configuração. Estas políticas ajudam a proteger os seus utilizadores abrindo web sites não confiáveis num recipiente isolado seguro que não é acessível por outras partes do sistema operativo.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implementar uma política de Guarda de Aplicações Do Windows Defender, tem de utilizar a Atualização do Criador de outono do Windows 10 (1709). Os dispositivos Windows 10 para os quais implementa a política devem ser configurados com uma política de isolamento de [rede](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard#network-isolation-settings). Para mais informações, consulte a visão geral do [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Criar uma política e navegar nas definições disponíveis

1. Na consola 'Gestor de Configuração', escolha **Ativos e Conformidade.**
2. No espaço de trabalho **de Ativos e Compliance,** escolha **A**Proteção de  >  **Pontos Finais**guarda de  >  **aplicação Windows Defender**.
3. No separador **Home,** no grupo **Criar,** clique em Criar a Política de Guarda de **Aplicações do Windows Defender**.
4. Usando o [artigo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como referência, pode navegar e configurar as definições disponíveis. O Gestor de Configuração permite-lhe definir determinadas definições de política:
   - [Configurações de interação do anfitrião](#bkmk_HIS)
   - [Comportamento de aplicação](#bkmk_ABS)
   - [Gestão de ficheiros](#bkmk_FM)
5. Na página Definição de **Rede,** especifique a identidade corporativa e defina o limite da sua rede corporativa.

    > [!NOTE]
    > Os PCs windows 10 armazenam apenas uma lista de isolamento de rede no cliente. Pode criar dois tipos diferentes de listas de isolamento de rede e implantá-las ao cliente:
    >
    >  - um da Proteção de Informação do Windows
    >  - um do Windows Defender Application Guard
    >
    > Se implementar ambas as políticas, estas listas de isolamento da rede devem coincidir. Se implementar listas que não correspondam ao mesmo cliente, a implementação falhará. Para mais informações, consulte a documentação de [Proteção de Informação do Windows](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Quando terminar, complete o assistente e implemente a política para um ou mais dispositivos Windows 10 1709.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a>Configurações de interação do anfitrião

Configura as interações entre os dispositivos hospedeiros e o recipiente da Guarda de Aplicação. Antes da versão 1802 do Gestor de Configuração, tanto o comportamento da aplicação como a interação do anfitrião estavam no separador **Definições.**

- **Clipboard** - Abaixo das definições antes do Gestor de Configuração 1802
  - Tipo de conteúdo permitido
    - Texto
    - Imagens
- **Impressão:**
  - Ativar a impressão para XPS
  - Ativar a impressão para PDF
  - Ativar a impressão para impressoras locais
  - Ativar a impressão para impressoras de rede
- **Gráficos:** (começando com a versão 1802 do Gestor de Configuração)
  - Acesso ao processador gráfico virtual
- **Ficheiros:** (começando com a versão 1802 do Gestor de Configuração)
  - Guardar ficheiros descarregados para hospedar

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a>Configurações de comportamento de aplicação

Configura o comportamento da aplicação dentro da sessão da Guarda de Aplicações. Antes da versão 1802 do Gestor de Configuração, tanto o comportamento da aplicação como a interação do anfitrião estavam no separador **Definições.**

- **Conteúdo:**
  - Os sites empresariais podem carregar conteúdo não empresarial, como plug-ins de terceiros.
- **Outros:**
  - Reter dados de navegador gerados pelo utilizador
  - Auditar eventos de segurança na sessão isolada de guarda de aplicações

### <a name="file-management"></a><a name="bkmk_FM"></a>Gestão de ficheiros
<!--3555858-->
A partir da versão 1906 do Gestor de Configuração, existe uma definição de política que permite aos utilizadores confiar em ficheiros que normalmente se abrem no Application Guard. Após a conclusão com sucesso, os ficheiros serão abertos no dispositivo de hospedar em vez de no Application Guard. Para obter mais informações sobre as políticas do Application Guard, consulte [configurar as definições](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard)de política do Windows Defender Application Guard .

- **Permitir que os utilizadores confiem** em ficheiros que se abrem no Windows Defender Application Guard - Ative o utilizador a marcar ficheiros como confiável. Quando um ficheiro é de confiança, abre-se no hospedeiro e não na Guarda de Aplicações. Aplica-se à versão 1809 do Windows 1809 ou superior.
  - **Proibido:** Não permita que os utilizadores marquem ficheiros como confiáveis (predefinido).
  - **Ficheiro verificado por antivírus:** Permitir que os utilizadores marquem ficheiros como confiáveis após uma verificação antivírus.
  - **Todos os ficheiros:** Permitir que os utilizadores marquem qualquer ficheiro como confiável.

Quando ativa a gestão de ficheiros, poderá ver erros registados no DCMReporting.log do cliente. Os erros abaixo normalmente não efetuam a funcionalidade: <!--4619457-->

- Em dispositivos compatíveis:
  - FileTrustCriteria_condition não encontrado
- Em dispositivos não compatíveis:
  - FileTrustCriteria_condition não encontrado
  - FileTrustCriteria_condition não poderia estar localizado no mapa
  - FileTrustCriteria_condition não encontrados na digestão

Para editar as definições do Application Guard, expanda a **Proteção do Ponto Final** no espaço de trabalho **de Ativos e Compliance** e, em seguida, clique no nó de Proteção de **Aplicações do Windows Defender.** Clique na política que pretende editar e, em seguida, selecione **Propriedades**.

## <a name="next-steps"></a>Próximos passos

Para ler mais sobre o Windows Defender Application Guard: [Windows Defender Application Guard View](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Guarda de aplicações Do Windows Defender FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
