---
title: Licensing and branches (Licenciamento e ramos)
titleSuffix: Configuration Manager
description: Conheça os requisitos de licenciamento das opções de instalação disponíveis com o Gestor de Configuração
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906054"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licenciamento e balcões para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual), & System Center Configuration Manager (ramo de manutenção a longo prazo)*

Utilize este artigo para conhecer os requisitos de licenciamento para as opções de instalação disponíveis com o Gestor de Configuração. Estas opções de instalação incluem os seguintes ramos:

- Ramo atual
- Ramo de manutenção a longo prazo (LTSB)
- Instalação de avaliação do ramo atual
- Ramo de pré-visualização técnica

## <a name="licensing-overview"></a>Descrição geral do licenciamento

Os clientes com garantia de software ativa (SA) em licenças de Gestor de Configuração ou com direitos de subscrição equivalentes a partir de 1 de outubro de 2016 têm direitos de utilização da versão 1606 de outubro de 2016 do Diretor de Configuração. Os clientes com direitos de Configuração Em ou depois de 1 de outubro de 2016 encontrarão duas opções licenciadas após a instalação: filial atual e ramo de manutenção de longo prazo (LTSB).

Para os termos e condições completos para os produtos que compra através de programas de licenciamento de volume da Microsoft, consulte [Termos e Documentação de Licenciamento.](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)


## <a name="licensed-branches"></a>Sucursais licenciadas

Este artigo refere-se ao acordo de Garantia de Software ou direitos de subscrição equivalentes. Este contrato de licenciamento da Microsoft concede direitos de instalação e utilização do Gestor de Configuração.

### <a name="current-branch"></a>Ramo atual

A sucursal atual requer um acordo ativo de garantia de software ou direitos equivalentes ao Gestor de Configuração. Para mais informações, consulte [software assurance e a Filial Atual](#software-assurance-and-the-current-branch).

Este ramo é suportado para uso em ambientes de produção que querem receber atualizações regulares de qualidade e funcionalidades da Microsoft. Proporciona acesso a todas as funcionalidades e melhorias.

A partir do lançamento de 1710, cada versão de atualização permanece em suporte durante 18 meses a partir da data de lançamento da sua disponibilidade geral. Para mais informações, consulte as [versões atuais](../servers/manage/current-branch-versions-supported.md)do Suporte para O Gestor de Configuração .

### <a name="long-term-servicing-branch-ltsb"></a>Ramo de manutenção a longo prazo (LTSB)

O LTSB requer um atual acordo de Garantia de Software com a Microsoft a partir de 1 de outubro de 2016. Para mais informações, consulte [software assurance e o LTSB](#software-assurance-and-the-ltsb).

Este ramo é suportado para uso em ambientes de produção. Destina-se a ser utilizado por clientes que permitiram que os seus direitos de Garantia de Software (SA) ou direitos de subscrição equivalentes ao Gestor de Configuração expirem após 1 de outubro de 2016. Este ramo é limitado quando comparado com o Ramo Atual.

As atualizações críticas de segurança para o Gestor de Configuração são disponibilizadas para este ramo, mas não são disponibilizadas novas funcionalidades.

### <a name="evaluation-installation-of-the-current-branch"></a>Instalação de avaliação do ramo atual

A versão de avaliação não requer um acordo de Garantia de Software com a Microsoft. [As instalações](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) de avaliação são sempre o ramo atual, podendo usá-las durante 180 dias.

Pode atualizar a instalação de avaliação para uma instalação completa do ramo atual. Não é possível atualizar uma instalação de avaliação para o ramo de manutenção a longo prazo.

### <a name="technical-preview-branch"></a>Ramo de pré-visualização técnica

O [ramo técnico de pré-visualização](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) também está disponível. Este ramo é uma construção limitada de Configuração Manager que permite experimentar novas funcionalidades. Instala a pré-visualização técnica utilizando diferentes suportes que as versões licenciadas. Para mais informações, consulte [A Pré-Visualização Técnica](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Acordos de Garantia de Software

O estado da Garantia de Software nas suas licenças de Gestor de Configuração, ou direitos de subscrição equivalentes, em ou depois de 1 de outubro de 2016, determina a sucursal que pode instalar e utilizar.

### <a name="software-assurance-and-the-current-branch"></a>Garantia de Software e a filial atual

Os direitos de utilização do gestor de configuração podem ser fornecidos por:

- **Centro de Sistema:** Os clientes com Licenças SA ativas em System Center Standard ou Datacenter podem instalar e utilizar a opção atual de gestão de Configuração Manager.

- **Gestor de configuração do centro de sistemas:** Os clientes com Licenças SA ativas em Configuração Manager, ou com direitos de subscrição equivalentes, podem instalar e utilizar a opção atual de gestão de Configuração Manager.

Se tiver licenças ativas sa em Configuração Manager ou direitos de subscrição equivalentes em ou depois de 1 de outubro de 2016:

- Pode instalar e utilizar o ramo atual.
- Se permitir que a SA ou a subscrição caducem, tem de desinstalar o ramo atual.

### <a name="software-assurance-and-the-ltsb"></a>Garantia de Software e LTSB

Se tiver uma SA ativa em licenças de Gestor de Configuração ou direitos de subscrição equivalentes em ou depois de 1 de outubro de 2016:

- Pode instalar e utilizar o LTSB. Os clientes que tenham direitos perpétuos ao Gestor de Configuração, ou que permitam que a sua SA ou subscrição caducem, podem instalar a versão do Gestor de Configuração LTSB que está atual no momento do lapso.

LtSB baseia-se na versão atual da sucursal 1606, e tem as seguintes limitações:

- Não há suporte para converter uma filial atual para o LTSB. Se tem atualmente um site de sucursais atual, tem de instalar o LTSB como um novo site.  

- A LTSB não suporta todas as capacidades do ramo atual. Para mais informações, consulte [Introdução ao ramo](introduction-to-the-ltsb.md)de manutenção a longo prazo . Estas limitações incluem um conjunto de funcionalidades limitada, opções de upgrade limitadas e um ciclo de vida de suporte de produto separado.  

### <a name="software-assurance-expiration-date"></a>Data de validade da garantia de software

A partir do lançamento de outubro de 2016 do meio de base da versão 1606 para O Gestor de Configuração, pode especificar a data de validade do seu contrato de Garantia de Software. A data de validade da Garantia de **Software** é um valor opcional como um lembrete conveniente. Adicione-o quando executar configuração do Gestor de Configuração ou mais tarde a partir da consola 'Gestor de Configuração'.

> [!NOTE]
> A Microsoft não valida a data de validade que especifica e não utiliza esta data para validação da licença. Use-o como um lembrete da sua data de validade. Este valor é útil quando o Gestor de Configuração verifica periodicamente novas atualizações de software oferecidas online. O estado da licença de garantia de software deve ser atual para ser elegível para usar estas atualizações adicionais.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Para especificar a data de validade da Garantia de Software

- Quando executar a Configuração a partir dos meios de Configuração Manager, especifique o valor na página chave do **produto** do assistente de configuração.

- Na consola 'Gestor de Configuração', em **Definições de Hierarquia,** especifique o valor no separador **Licenciamento.**


## <a name="licensing-resources"></a>Recursos de licenciamento

Para saber mais sobre os detalhes de licenciamento de produtos, utilize os seguintes recursos.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Visão geral do VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Termos do produto de licenciamento de volume da Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Os clientes da licença de volume podem obter um resumo das suas licenças no Centro de Serviços de Licença de [Volume.](https://www.microsoft.com/Licensing/servicecenter/default.aspx) Vá ao menu **Licenças** e selecione Resumo das **Licenças.**

### <a name="vlsc-videos"></a>Vídeos VLSC

- Para treinar vídeos sobre como funciona o VLSC, vá ao [microsoft Volume Licensing Service Center treinando e recursos](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) e selecione vídeos **How-to**.

- [Onde procurar o seu contrato ativo](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) de Garantia de Software (a partir de 43 segundos)  

- [Como obter permissões para VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Pode delegar a VLSC a ler e a escrever permissões a outras pessoas da sua organização.
