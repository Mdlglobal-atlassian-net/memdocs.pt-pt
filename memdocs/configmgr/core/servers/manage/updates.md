---
title: Atualizações e manutenção
titleSuffix: Configuration Manager
description: Conheça o método de serviço na consola chamado Updates and Servicing que facilita a localização e instalação de atualizações recomendadas.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ffee9d851f00bcac5ed7ba562bdc9db8e0fa2767
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903946"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Atualizações e manutenção para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Gestor de Configuração utiliza um método de serviço na consola chamado **Atualizações e Manutenção**. Este método na consola facilita a descoberta e instalação de atualizações recomendadas para a sua infraestrutura de Gestor de Configuração. A manutenção na consola é complementada por atualizações fora da banda, tais como hotfixes. As atualizações fora da banda destinam-se a clientes que precisam de resolver problemas que possam ser específicos do seu ambiente.  

> [!TIP]  
> Os termos *de atualização,* *atualização*e *instalação* são usados para descrever três conceitos separados no Gestor de Configuração. Para obter mais informações sobre como cada termo é usado, consulte [sobre atualização, atualização e instalação](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  

Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia.

- Use também uma versão de base para atualizar a partir do System Center 2012 Configuration Manager.  

- Depois de atualizar para o ramo atual do Gestor de Configuração, não utilize versões de base para se manter atual. Em vez disso, utilize apenas [atualizações na consola](install-in-console-updates.md) para atualizar para a versão mais recente.  

- Periodicamente, são lançadas versões de base adicionais. Quando utiliza a versão base mais recente para instalar uma nova hierarquia, evita instalar uma versão desatualizada ou não suportada do 'Gestor de Configuração', seguida de um upgrade adicional da sua infraestrutura para a atualizar.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

- Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

- Atualizações que instala no site da administração central instalam automaticamente em locais primários infantis. Controle este tempo utilizando uma janela de manutenção no local primário.  

- Atualize manualmente os sites secundários para uma nova versão de atualização a partir da consola.  

Quando instala uma atualização, a atualização armazena ficheiros de instalação para essa versão no servidor do site numa pasta chamada **CD. Mais recente.** Para mais informações sobre estes ficheiros, consulte [o CD. Última pasta.](the-cd.latest-folder.md)  

- Use os ficheiros no CD. Última pasta durante a recuperação do site. Além disso, quando a sua hierarquia já não executa uma versão de base, utilize estes ficheiros para instalar sites adicionais.  

- Não pode usar ficheiros de instalação a partir de CD. Mais recente para instalar o primeiro site de uma nova hierarquia, ou para atualizar um site do System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Detalhes da versão

Algumas atualizações do Configuration Manager estão disponíveis tanto como versões de atualização na consola para uma infraestrutura existente, como novas versões de linha de base.  

#### <a name="supported-versions"></a>Versões suportadas

As seguintes versões suportadas do Gestor de Configuração estão atualmente disponíveis como base, uma atualização ou ambas:  

| Versão | Data de disponibilidade | [Data de fim do suporte](current-branch-versions-supported.md) | Linha de base | Atualização in-consola |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1 de abril de 2020 | 1 de outubro de 2021 | Nota sim<sup>[1](#bkmk_note1)</sup> | Sim |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29 de novembro de 2019 | 29 de maio de 2021 | Não | Sim |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26 de julho de 2019 | 26 de janeiro de 2021 | Não | Sim |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27 de março de 2019 | 27 de setembro de 2020 | Nota sim<sup>[1](#bkmk_note1)</sup> | Sim |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27 de novembro de 2018 | 1 de dezembro de 2020 | Não | Sim |

A **data de disponibilidade** é quando o anel de [atualização precoce](checklist-for-installing-update-2002.md#early-update-ring) é lançado. Os meios de base estarão disponíveis no Centro de Serviços de Licença de Volume após a atualização estar disponível globalmente.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Nota 1:**</sup> Os meios de base estão disponíveis como parte das seguintes versões no Centro de Serviço seleções de Licença de [Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Centro de Sistema Config Mgr (ramo atual)
> - Centro de Sistema2016 Datacenter
> - System Center 2016 Standard  
>
> Por exemplo, procure no VLSC `System Center Config Mgr (current branch)` . Encontre os meios de base na lista de ficheiros e descarregue para esse lançamento.  

#### <a name="historical-versions"></a>Versões históricas

A tabela seguinte lista versões históricas do ramo atual do Gestor de Configuração que estão fora de suporte:

| Versão | Data de disponibilidade | Data de fim do suporte | Linha de base | Atualização in-consola |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31 de julho de 2018 | 31 de janeiro de 2020 | Não | Sim |
| **1802** <br /> (5.00.8634) | 22 de março de 2018 | 22 de setembro de 2019 | Sim | Sim |
| **1710** <br /> (5.00.8577) | 20 de novembro de 2017 | 20 de maio de 2019 | Não | Sim |
| **1706** <br /> (5.00.8540) | 31 de julho de 2017 | 31 de julho de 2018 | Não | Sim |
| **1702** <br /> (5.00.8498) | 27 de março de 2017 | 27 de março de 2018 | Sim | Sim |
| **1610** <br /> (5.00.8458) | 18 de novembro de 2016 | 18 de novembro de 2017 | Não | Sim |
| **1606** <br /> (5.00.8412.1000) | 22 de julho de 2016 | 22 de julho de 2017 | Não | Sim |
| **1606 com KB3186654** <br />5.00.8412.1307) | 12 de outubro de 2016 | 12 de outubro de 2017 | Sim | Não |
| **1602** <br /> (5.00.8355) | 11 de março de 2016 | 11 de março de 2017 | Não | Sim |
| **1511** <br /> (5.00.8325) | 8 de dezembro de 2015 | 8 de dezembro de 2016 | Sim | Não |  

#### <a name="how-to-check-the-version"></a>Como verificar a versão

Para verificar a versão do seu site de Configuração Manager, na consola vá ao **About Configuration Manager** no canto superior esquerdo da consola. Este diálogo exibe as versões do site e da consola.  

> [!Note]  
> A versão da consola é ligeiramente diferente da versão do site. A versão menor da consola corresponde à versão de lançamento do Gestor de Configuração. Por exemplo, na versão 1802 do Configuration Manager a versão inicial do site é de 5.0.8634.1000, e a versão inicial da consola é de 5. **1802**.1082.1700. Os números de construção (1082) e revisão (1700) podem mudar com futuros hotfixos.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  

Quando utiliza uma instalação pronta para a produção do ramo atual do Diretor de Configuração, a maioria das atualizações estão disponíveis através do canal **de atualizações e manutenção.** Este método identifica, descarrega e disponibiliza as atualizações que se aplicam à sua versão e configuração de infraestrutura atual. Inclui apenas atualizações que a Microsoft recomenda para todos os clientes.

Estas atualizações incluem:  

- Novas versões, como a versão 1906, 1910 ou 2002.

- Atualizações que incluem novas funcionalidades para a sua versão atual.

- Hotfixes para a sua versão de Gestor de Configuração e que todos os clientes devem instalar.

    > [!Note]  
    > A partir da versão 1902, os hotfixos nas consolas têm agora relações de supersedência. Para mais informações, consulte [A Supersedence para os hotfixes na consola](#bkmk_supersede).

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Substituem os tipos de atualização vistos para versões de produtos anteriores, tais como pacotes de serviços, atualizações cumulativas, hotfixes aplicáveis a todos os clientes, e a extensão para microsoft Intune.

As atualizações na consola podem aplicar-se a um ou mais dos seguintes sistemas:  

- Servidores de sites primário e de administração central  

- Funções de sistema de sites e servidores de sistema de sites  

- Instâncias do Fornecedor de SMS  

- Consolas de Gestor de Configuração  

- Clientes do Gestor de Configuração  

O Gestor de Configuração descobre novas atualizações para si. Sincronizar o seu ponto de ligação do Gestor de Configuração com o serviço de nuvem da Microsoft, observando os seguintes comportamentos:  

- Quando o seu ponto de ligação de serviço está em modo online, o seu site sincroniza-se com a Microsoft todos os dias. Identifica automaticamente novas atualizações que se aplicam à sua infraestrutura. Para descarregar atualizações e ficheiros redistribuíveis, o computador que acolhe a função do sistema de pontode ligação de serviço utiliza o contexto **do Sistema** para aceder aos seguintes locais da Internet: go.microsoft.com e download.microsoft.com. Para obter mais informações sobre locais adicionais utilizados pelo ponto de ligação ao serviço, consulte os requisitos de [acesso à Internet.](../deploy/configure/about-the-service-connection-point.md#bkmk_urls)  

- Quando o seu ponto de ligação de serviço estiver em modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a nuvem da Microsoft. Para mais informações, consulte [Utilize a ferramenta de ligação de serviço](use-the-service-connection-tool.md).  

- As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

- Instale apenas as atualizações na consola que escolher. Ao instalar algumas atualizações, pode selecionar funcionalidades individuais para ativar e utilizar. Para mais informações, consulte [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

Quando instala uma atualização na consola, ocorre o seguinte processo:  

- Esta executa automaticamente uma verificação de pré- requisitos. Também pode executar manualmente esta verificação antes de iniciar a instalação.  

- Instala-se no local de alto nível do seu ambiente. Este site é o site da administração central, se tiver um. Numa hierarquia, a atualização instala-se automaticamente em locais primários. Controlar quando cada servidor de site primário é autorizado a atualizar utilizando [janelas de serviço para servidores](service-windows.md)do site .  

- Após atualizações do servidor do site, todas as funções do sistema do site afetadas atualizam automaticamente. Estas funções incluem instâncias do Fornecedor sms. Depois de o site instalar a atualização, as consolas do Gestor de Configuração também levam o utilizador da consola a atualizar a consola.  

- Se uma atualização incluir o cliente do Gestor de Configuração, é-lhe oferecida a opção de testar a atualização em pré-produção ou de aplicar a atualização a todos os clientes imediatamente.  

- Depois de um site primário ser atualizado, os sites secundários não atualizam automaticamente. Em vez disso, deve iniciar manualmente a atualização do site secundário.  

> [!NOTE]  
> O ramo atual do Gestor de Configuração, o ramo de manutenção a longo prazo, e o ramo de pré-visualização técnica são diferentes lançamentos. As atualizações que se aplicam a uma sucursal não estão disponíveis como atualizações na consola para os outros balcões. Para obter mais informações sobre os balcões disponíveis, consulte [qual o ramo do Gestor de Configuração que devo usar?](../../understand/which-branch-should-i-use.md)

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Supersedência para hotfixos na consola

<!-- 3229613 -->
A partir da versão 1902, os hotfixos nas consolas têm agora relações de supersedência. Quando a Microsoft publica um novo hotfix do Gestor de Configuração, a consola não exibe quaisquer hotfixes que sejam substituídos por este novo hotfix. Este novo comportamento ajuda-o a determinar melhor quais os hotfixes a instalar.

### <a name="supersedence-example"></a>Exemplo de supersedência

Existem três hotfixes disponíveis: Hotfix-A, Hotfix-B e Hotfix-C. Hotfix-A é substituído por Hotfix-B, e Hotfix-B é substituído por Hotfix-C.

|Hotfix-A|Hotfix-B|Hotfix-C|Vista na consola|
|--------|--------|--------|---------------|
|Não instalado|Não instalado|Não instalado|Mostre os três hotfixs|
|Instalado|Instalado|Não instalado|Hotfix-B mostra como instalado<br/>Hotfix-C mostra como pronto para instalar|
|Não instalado|Não instalado|Instalado|Hotfix-C mostra como instalado|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Correções fora de banda  

Alguns hotfixes libertam com disponibilidade limitada para resolver questões específicas. Outros hotfixes são aplicáveis a todos os clientes, mas não podem instalar usando o método da consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, quando procura corrigir ou resolver um problema com a sua implementação do 'Gestor de Configuração', pode aprender sobre hotfixes fora de banda a partir de serviços de suporte ao cliente da Microsoft, um artigo de base de suporte da Microsoft ou o blog da equipa do Gestor de [Configuração](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Instale estas correções manualmente, utilizando um dos dois seguintes métodos:  

### <a name="update-registration-tool"></a>Ferramenta de registo de atualização

Esta ferramenta importa manualmente o hotfix na consola do Gestor de Configuração. Em seguida, instale a atualização como faria na consola atualizações que são descobertas automaticamente.  

Este método é utilizado para fixações que utilizam a seguinte estrutura de nome de ficheiro:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Para mais informações, consulte [Utilize a ferramenta de registo de atualização para importar hotfixes](use-the-update-registration-tool-to-import-hotfixes.md).  

### <a name="hotfix-installer"></a>Instalador hotfix

Utilize esta ferramenta para instalar manualmente um hotfix que não pode ser instalado utilizando o método da consola.  

Este método é utilizado para correções que utilizam a seguinte estrutura de nome de ficheiro:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Para mais informações, consulte [Utilize o instalador de hotfix para instalar atualizações](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Próximos passos

Os seguintes artigos podem ajudá-lo a entender como encontrar e instalar os diferentes tipos de atualização para O Gestor de Configuração:  

- [Instalar atualizações na consola](install-in-console-updates.md)  

- [Utilizar a ferramenta de ligação de serviços](use-the-service-connection-tool.md)  

- [Utilize a ferramenta de registo de atualização para importar hotfixes](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Utilize o instalador hotfix para instalar atualizações](use-the-hotfix-installer-to-install-updates.md)  

Para mais informações sobre o ramo de pré-visualização técnica, consulte [A pré-visualização técnica](../../get-started/technical-preview.md).
