---
title: Arranque rápido do Centro de Apoio
titleSuffix: Configuration Manager
description: Capture rapidamente o estado de um cliente do Gestor de Configuração para resolução de problemas.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723118"
---
# <a name="support-center-quickstart-guide"></a>Guia quickstart do Centro de Apoio

*Aplica-se a: Gestor de Configuração (ramo atual)*

O Centro de Suporte tem capacidades poderosas, incluindo resolução de problemas e visualização de registoem em tempo real. Também pode ser usado em apenas alguns minutos para capturar o estado de um computador cliente do Gestor de Configuração. Esta capacidade inclui o acesso a clientes remotos.

Crie um ficheiro completo de resolução de *problemas* (.zip) que capture o estado do cliente. O pacote não contém apenas ficheiros de registo. Pode incluir outros tipos de dados, tais como configurações de registo e configurações de clientes. Forneça o pacote a um técnico de suporte que utilize o Espectador do Centro de Suporte.



## <a name="prerequisites"></a>Pré-requisitos

- Direitos administrativos locais para um cliente do Gestor de Configuração  

- O instalador do Centro de Suporte. Este ficheiro está no servidor do site em `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` . Para mais informações, consulte [Suporte Centro - Instale](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Passo 1: Criar um pacote de dados sobre um cliente local

1.  Instale o Centro de Suporte no cliente do Gestor de Configuração.  

2.  Vá ao menu **Iniciar,** no grupo **Microsoft System Center,** selecione **Support Center**.  

3.  No separador Casa da fita, **selecione Recolher Dados Selecionados**. Por predefinição, o Support Center apenas recolhe o conjunto de dados mínimos: ficheiros de registo, configuração do cliente e sistema operativo.  

4.  Guarde o ficheiro de pacote de resolução de problemas (.zip) para uma pasta no computador. Por predefinição, o nome do ficheiro é semelhante ao seguinte exemplo: `Support_c885cdfed3c7482bba4f9e662978ec07.zip` .  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Passo 2: Ver o pacote de dados usando o Espectador do Centro de Suporte

1.  Iniciar **o Espectador do Centro**de Suporte . Esta ação pode acontecer em qualquer computador no qual instale o Centro de Suporte.  

2.  **Selecione abra o pacote,** navegue para o ficheiro de pacote e selecione **Open**.  

3.  Depois de o Espectador do Centro de Suporte processar o ficheiro, mude para cada separador disponível. Ver os tipos de dados que o Centro de Suporte recolhe por defeito:  

    - **Configuração**  

        - Configuração do cliente do Gestor de Configuração  

        - Sistema operativo  

        - Computador  

        - Serviços  

        - Placas de rede  

    - **Registos**: Escolha uma ou mais entradas na lista e selecione **Open**. Esta ação abre os ficheiros de registo selecionados no Visualizador de Registo. Utilize esta funcionalidade para procurar códigos de erro e utilize filtros avançados para o ajudar a analisar mais rapidamente ficheiros de registo.  



## <a name="collect-more-data"></a>Recolher mais dados

Além destas capacidades básicas, o Support Center também pode recolher uma grande variedade de outras informações do Estado cliente. Open **Support Center** e selecione Recolher Todos os **Dados**. Este processo normalmente dura vários minutos, mesmo em computadores mais recentes. O Centro de Suporte recolhe os seguintes dados adicionais:

- **Política**: Definições de política do Gestor de Configuração, incluindo tanto a configuração de política solicitada como a configuração real da política  

- **Certificados**: Informação chave pública para certificados de cliente. O Centro de Apoio não recolhe chaves privadas de certificado.  

- **Registo do cliente**: Recolhe informações de configuração do cliente a partir do registo. O Centro de Suporte recolhe apenas informações sobre o registo do Gestor de Configuração.  

- **Client WMI**: Informação de configuração do cliente da WMI. O Centro de Apoio não recolhe a política do cliente.  

- **Resolução de problemas**: Dados de resolução de problemas em tempo real para ajudar a diagnosticar problemas comuns de clientes com Diretório Ativo, pontos de gestão, networking, atribuições de políticas e registo.  

- **Despejos de depuração**: Realizar despejo de depuração de clientes e processos relacionados. As lixeiras de depuração podem ser grandes. Só ative esta opção quando resolver problemas com o desempenho do cliente.  

