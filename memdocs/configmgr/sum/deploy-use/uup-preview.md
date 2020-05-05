---
title: Pré-visualização do UUP
titleSuffix: Configuration Manager
description: Instruções para pré-visualização da integração do UUP
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719737"
---
# <a name="uup-private-preview-instructions"></a>Instruções de pré-visualização privadas da UUP

> [!Note]  
> Esta informação diz respeito a uma funcionalidade de pré-visualização que pode ser substancialmente modificada antes de ser lançada comercialmente. A Microsoft não faz garantias, de forma expressa ou implícita, em relação à informação aqui apresentada.  

## <a name="introduction"></a>Introdução

A Plataforma de Atualização Unificada (UUP) é a plataforma de embalagem e publicação que os dispositivos de consumo e empresa utilizam para receber atualizações do Windows Update for Business. O programa de pré-visualização privada da UUP destina-se a clientes que concordaram em ajudar a Microsoft a validar o uso de atualizações uUP no 'Gestor de Configuração' para ajudar a resolver problemas que os clientes reportam hoje com o serviço ao Windows. Estas atualizações não estão atualmente disponíveis ao público.

Para mais informações sobre o UUP, consulte a seguinte publicação do blog do Windows: [Uma atualização na nossa Plataforma de Atualização Unificada (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Benefícios

A funcionalidade de UUP do Windows 10 e atualizações cumulativas ajudam a resolver múltiplos problemas que os clientes reportam hoje com a manutenção do Windows.

### <a name="feature-updates"></a>Atualizações de funcionalidades

- Com uma atualização de funcionalidades UUP, o processo de atualização do Windows preserva funcionalidades sobre procura (FOD) e pacotes de idiomas.

- Atualize diretamente para o último nível de conformidade de segurança. Não necessita de instalar atualizações de segurança imediatamente após uma atualização da funcionalidade. A Microsoft publica uma nova atualização de funcionalidades todos os meses com a mais recente atualização de segurança cumulativa. Não precisa de descarregar ou distribuir a maior parte dos conteúdos da atualização de funcionalidades todos os meses. Apenas descarrega a atualização de segurança, que a UUP partilha com a atualização cumulativa.

### <a name="cumulative-updates"></a>Atualizações cumulativas

- As atualizações cumulativas com a UUP incluem atualizações de pilhas de manutenção (SSU) com atualizações de segurança acumuladas mensais. Este comportamento resolve dificuldades em orquestrar estas duas atualizações. Certifica-se de que as atualizações da pilha de manutenção estão em vigor para instalar atualizações cumulativas. Não precisas de gerir e orquestrar estas relações.

- As atualizações cumulativas com a UUP permitem-lhe distribuir conteúdo de FOD e pack de idiomas offline. Este comportamento permite que os utilizadores os adicionem a pedido. Os utilizadores não precisam de descarregar a partir da internet, e você não precisa descobrir como pré-encenar este conteúdo.

## <a name="set-up"></a>Configurar

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. Envie o seu ID WSUS para a Microsoft

Para participar na pré-visualização privada da UUP, partilhe o seu ID WSUS com o seu contacto de pré-visualização UUP. A Microsoft aprova o seu ambiente WSUS no programa de pré-visualização da UUP. Sem esta identificação, não pode ver nenhuma atualização da UUP até que a pré-visualização seja pública.

Para obter o seu ID WSUS, execute o seguinte script PowerShell:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

A propriedade **MUUrl** deve ser `https://sws.update.microsoft.com`. Para alterá-la, consulte a resolução no seguinte artigo de suporte: A [sincronização da WSUS falha com a SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. Gestor de Configuração de Atualizações

Faça as seguintes alterações no site do Seu Gestor de Configuração para suportar esta pré-visualização da UUP:

#### <a name="diagnostics-and-usage-data-level"></a>Diagnósticos e nível de dados de utilização

Considere aumentar o nível de diagnóstico e utilização de dados do Gestor de Configuração durante esta pré-visualização. O nível **completo** ajuda a Microsoft a analisar melhor e a resolver problemas com esta nova funcionalidade. Para obter mais informações, consulte [Níveis de recolha de dados de utilização de diagnóstico para a versão 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Instale a última atualização

1. Atualize o site com uma das seguintes atualizações:

    - Versão 1902 com a [atualização rollup](https://support.microsoft.com/help/4500571)
    - [Versão 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Para mais informações, consulte [Instalar atualizações na consola](../../core/servers/manage/install-in-console-updates.md).

2. Atualizar clientes.  

    - Para simplificar este processo, considere utilizar a atualização automática do cliente. Para mais informações, consulte [os clientes de Upgrade](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - Para evitar *o desnecessariamente download de cerca* de 6 GB de conteúdo não utilizado para o cliente, atualize todos os clientes para os quais direciona as atualizações da UUP.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Atualizar os clientes do Windows para uma versão suportada

Para que as atualizações da UUP se instalem com sucesso, instale ambas as seguintes atualizações:

1. Um nível mínimo acumulado de conformidade mensal acumulada.

2. Uma atualização específica não cumulativa e não-segurança do Catálogo de Atualizações da Microsoft. Para importar a atualização para o Gestor de Configuração para implementação, consulte [as atualizações de Import do Catálogo de Atualizações da Microsoft](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Versões suportadas do Windows 10 e atualizações necessárias

| Versão do Windows 10 | Nível mínimo de conformidade | Atualização adicional do catálogo |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, versão 1903** | RTM | 7 de novembro de 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, versão 1809** | agosto de 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 de novembro de 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, versão 1803** | Abril 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 de novembro de 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, versão 1709** | Abril 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 de novembro de 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Se aplicar as atualizações de 12 de novembro de 2019 ao cliente antes de aplicar a atualização adicional do catálogo de 7 de novembro de 2019, as alterações necessárias ao Windows Update Agent necessárias para suportar a UUP serão substituídas. Para remediar os clientes nesse cenário, aplique a atualização adicional do catálogo após a instalação das atualizações de 12 de novembro de 2019.
> - Se aplicar uma atualização de funcionalidade ao cliente, terá de reinstalar a atualização adicional do catálogo após a atualização estar concluída.
> - Para facilitar o teste das atualizações de funcionalidades, importe as atualizações para o Gestor de Configuração. Para mais informações, consulte [as atualizações da Import a partir do Catálogo de Atualizações da Microsoft](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Após a atualização da funcionalidade estar concluída, a atualização adicional do catálogo **mostra-** o que permite a implementação automática para a versão de alto nível do SISTEMA.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Permitir que os clientes descarreguem conteúdo delta quando disponíveis

Para que as atualizações da UUP baixem corretamente, ative a definição do cliente para permitir que os **clientes descarreguem conteúdo delta quando disponíveis**. Esta definição permite ao Gestor de Configuração permitir que o Agente de Atualização do Windows (WUA) determine o conteúdo necessário para descarregar para os clientes. Este comportamento é em vez do padrão em que o cliente do Gestor de Configuração descarrega todos os conteúdos associados à atualização uUP. Quando ativa esta definição, a WUA determina o conteúdo adicional necessário a cada atualização uup. Por exemplo, apenas os pacotes de FOD e linguísticos necessários.

Quando ativa esta definição, não afeta os downloads de conteúdos do servidor a partir da internet. Aplica-se apenas aos downloads dos clientes. Antes de implementar atualizações da UUP para clientes, aplique esta definição aos clientes que conheçam as versões suportadas para a UUP. As atualizações pré-requisitos do cliente fixam problemas de compatibilidade para atualizações de UUP no WSUS e No Gestor de Configuração.

Para mais informações sobre esta definição de cliente, consulte [sobre as definições do cliente - Atualizações de software](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)

### <a name="5-review-your-software-update-infrastructure"></a>5. Reveja a sua infraestrutura de atualização de software

Antes de sincronizar as atualizações da UUP, reveja as suas regras de implementação automática (ADR) e os planos de manutenção. Se não quiser que estas atualizações se implementem automaticamente, reveja os seus ADRs para filtrar. Para mais informações, consulte [Como encontrar atualizações de UUP sincronizadas](#how-to-find-synced-uup-updates). Por predefinição, os planos de manutenção existentes apenas implementam atualizações não UUP. Pode modificar os planos de manutenção para alterar este comportamento.

Reveja os seus relatórios de conformidade e reveja conforme necessário. Por exemplo, se medir a conformidade com todos os produtos, verá agora atualizações cumulativas uup e não-UUP. Os dispositivos reportarão a conformidade com ambos os tipos de atualizações. Certifique-se de que os seus relatórios de conformidade abordam esta alteração.

## <a name="enable-uup-and-start-testing"></a>Ativar uUP e começar a testar

### <a name="select-products-and-classifications-to-sync"></a>Selecione produtos e classificações para sincronizar

Assim que estiver pronto para começar a sincronizar as atualizações do UUP, e a Microsoft tiver aprovado o seu ID WSUS, ative os novos produtos:

1. [Sincronizar atualizações](../get-started/synchronize-software-updates.md) de software para povoar os novos produtos.  

2. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**

3. Selecione o seu site de alto nível, que é ou um site de administração central (CAS) ou site primário autónomo.

4. Na fita, **selecione Configurar componentes**do site , e escolha o Ponto de **Atualização**do Software .

5. Mude para o separador **Produtos** e selecione um ou mais dos seguintes produtos: 

    - **Pré-visualização do Windows 10 UUP**
    - **Pré-visualização uup do servidor do Windows**

6. Mude para o separador Classificações e selecione as **seguintes** opções:  

    - **Atualizações de Segurança**: Para ver as atualizações cumulativas da UUP  
    - **Upgrades**: Para ver as atualizações da funcionalidade UUP  

7. Sincronizar novamente as atualizações de software para ver as novas atualizações da UUP.

### <a name="how-to-find-synced-uup-updates"></a>Como encontrar atualizações de UUP sincronizadas

Depois de ter sincronizado as atualizações da UUP no seu ambiente, encontre-as na consola Do Gestor de Configuração para testar. Existem duas formas de encontrar as atualizações de pré-visualização:

- Como estas atualizações de pré-visualização estão num produto separado, utilize o produto para filtrar para encontrar estas atualizações. Utilize o filtro do produto do plano de manutenção para implementar atualizações de funcionalidades UUP ou não UUP.  

- Nas **atualizações** de software e em todos os salões **de**atualizações do **Windows 10,** há uma nova coluna opcional **Tag**. Esta propriedade também está disponível como um filtro em ADRs. Para atualizações da UUP, `UUP`procure neste campo . Está em branco para atualizações não-UUP.  

### <a name="updates-available-during-preview"></a>Atualizações disponíveis durante a pré-visualização

Para obter mais informações sobre todas as atualizações do Windows 10 lançadas pela Microsoft, consulte [as informações de lançamento do Windows 10.](https://docs.microsoft.com/windows/release-information/)

#### <a name="cumulative-updates-to-test"></a>Atualizações cumulativas a testar

Embora possa ver várias atualizações com etiquetas UUP disponíveis, comece com a atualização **de setembro de 2019** (2019-09) ou uma versão posterior. Por exemplo:

- Atualização cumulativa 2019-09 para o Windows 10 Versão 1809 para sistemas x64 baseados em x64 (KB4512578)
- Atualização cumulativa 2019-09 para o Windows 10 Versão 1803 para sistemas x64 baseados em x64 (KB4516058)
- Atualização cumulativa 2019-09 para o Windows 10 Versão 1709 para sistemas x64 baseados em x64 (KB4516066)

#### <a name="feature-updates-to-test"></a>Atualizações de funcionalidades para testar

Embora possa ver várias atualizações com etiquetas UUP disponíveis, comece com a atualização **de setembro de 2019** (2019-09B) ou uma versão posterior. Por exemplo:

- Atualização de funcionalidades para o Windows 10, versão 1809 x64 2019-09B
- Atualização de funcionalidades para o Windows 10, versão 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Cenários para testar

### <a name="test-feature-updates"></a>Atualizações de funcionalidades de teste

- Atualize diretamente para o seu nível de conformidade de segurança escolhido  

- Instale FODs e pacotes de idiomas antes da atualização. Certifique-se de que a atualização preserva estes componentes.  

### <a name="test-cumulative-updates"></a>Teste de atualizações cumulativas

Durante a pré-visualização, mantenha os clientes em conformidade utilizando a atualização do tipo UUP para várias atualizações consecutivas. Este teste ajuda-o a entender o comportamento contínuo.

### <a name="test-content"></a>Conteúdo de teste

A primeira atualização para cada versão principal (1809, 1803, 1709), arquitetura e combinação de linguagem parecerão grandes. Este tamanho está tanto em número de ficheiros como em espaço de disco, em comparação com o que viu anteriormente com atualizações não-UUP. Este conteúdo extra destina-se principalmente a todos os pacotes de FOD e idiomas para atualizações cumulativas. Para atualizações de funcionalidades, há um grande conteúdo adicional para a primeira atualização.

Para futuras atualizações cumulativas e de funcionalidades, a quantidade de novos conteúdos que o site descarrega e distribui é muito menor. A UUP partilha inteligentemente todos os conteúdos fod e pack de idiomas entre atualizações. Não precisa de rebaixar ou redistribuir este conteúdo partilhado. Durante a pré-visualização, nas versões 1709 e 1803 do Windows, este download mensal é quase o mesmo que o tamanho das atualizações cumulativas em cenários não-UUP. Na versão 1809 do Windows 10 e posteriormente, o download incremental da atualização cumulativa é muito menor a cada mês.

Quando se olha para o conteúdo total que é descarregado e distribuído durante um período de 12 meses para *não-expresso*, a versão 1803 do Windows 10 sem UUP deve ser quase igual à versão 1809 com UUP. O conteúdo total descarregado e distribuído ao longo de todo o tempo de vida do lançamento é menor na versão 1809 com uUP.

### <a name="supported-content-channels"></a>Canais de conteúdo suportados

Para a pré-visualização, teste os seus cenários típicos do mundo real. A UUP suporta todos os canais de conteúdo, incluindo:

- Otimização de Entrega do Windows (DO)
  - Ao utilizar o DO, certifique-se de que está configurado corretamente. Para mais informações, consulte [otimize a entrega da atualização do Windows 10.](optimize-windows-10-update-delivery.md)
- Cache de pares do Gestor de Configuração
- Windows BranchCache
- Utilize a opção **no pacote de implementação** e os clientes descarregam diretamente a partir do Microsoft Update. Utilize esta opção com otimização de entrega.
- Fornecedores de conteúdos alternativos de terceiros

Para obter mais informações sobre os canais de conteúdo, consulte [otimize a entrega da atualização do Windows 10.](optimize-windows-10-update-delivery.md)

<!-- TODO: Addlink to WSUS Perf documentation-->
