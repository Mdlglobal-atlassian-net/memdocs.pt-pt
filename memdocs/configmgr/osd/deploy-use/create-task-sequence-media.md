---
title: Criar um suporte de dados de sequência de tarefas
titleSuffix: Configuration Manager
description: Crie meios de sequência de tarefas para implantar um SISTEMA para um computador de destino no ambiente do Seu Gestor de Configuração.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711029"
---
# <a name="create-task-sequence-media"></a>Criar um suporte de dados de sequência de tarefas

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar os meios de comunicação para capturar uma imagem de OS a partir de um computador de referência ou para implementar um SISTEMA para um computador de destino no ambiente do Gestor de Configuração. O suporte de dados criado pode ser um conjunto de CD, DVD ou uma unidade flash USB.  

Os meios de comunicação são utilizados principalmente para implementar sistemas operativos em computadores de destino que não tenham uma ligação de rede ou que tenham uma ligação de baixa largura de banda ao site do Seu Gestor de Configuração. No entanto, também pode utilizar meios de comunicação para iniciar uma implementação de OS fora de um Sistema operativo windows existente. Este método é útil quando não existe um Sistema operativo, o Sistema operativo não está a funcionar, ou quer repartipartição do disco rígido.  

O suporte de dados de implementação inclui suportes de dados de arranque, suportes de dados autónomos e suportes de dados pré-configurados. O conteúdo dos meios varia, dependendo do tipo de meios que utiliza. Por exemplo, os meios de comunicação autónomos contêm a sequência de tarefas que implanta o Sistema Operativo. Outros tipos de meios de comunicação recuperam sequências de tarefas a partir do ponto de gestão.  

> [!IMPORTANT]  
> Para criar meios de sequência de tarefas, deve ser um administrador no computador onde executa a consola 'Gestor de Configuração'. Se não for administrador, é solicitado credenciais de administrador quando iniciar o assistente de "Create Task Sequence Media".  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Capturar meios de comunicação

Os meios de captura permitem-lhe capturar uma imagem de OS a partir de um computador de referência. Os meios de captura contêm a imagem de arranque que inicia o computador de referência e a sequência de tarefas que captura a imagem de OS.

Para obter mais informações sobre como criar meios de captura, consulte [Create capture media](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Meios de comunicação sinuosos

Os meios de arranque contêm os seguintes componentes:

- A imagem da bota
- Comandos de [prestação](../understand/prestart-commands-for-task-sequence-media.md) opcionais e os seus ficheiros necessários
- Binários de Gestor de Configuração

Quando o computador de destino começa, liga-se à rede e recupera a sequência de tarefas, a imagem de OS e qualquer outro conteúdo necessário da rede. Como a sequência de tarefas não está nos meios de comunicação, pode alterar a sequência de tarefas ou o conteúdo sem ter de recriar os meios de comunicação.  

> [!IMPORTANT]  
> Os pacotes nos meios de comunicação não estão encriptados. Tome as medidas de segurança adequadas, tais como a adição de uma palavra-passe aos meios de comunicação, para garantir que o conteúdo do pacote é protegido de utilizadores não autorizados.  

Para mais informações sobre como criar meios de sinuoso, [Crie meios de sabotados.](create-bootable-media.md)  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Meios de comunicação pré-encenados

Os meios de comunicação pré-encenados permitem-lhe aplicar meios de sinuoso e uma imagem de SO num disco rígido antes do processo de provisionamento. Os meios de comunicação pré-encenados são um ficheiro Windows Image (WIM). Pode ser instalado num computador de metal nu pelo fabricante ou no seu centro de paragem que não esteja ligado ao ambiente do Gestor de Configuração de Produção.  

Os meios de comunicação pré-encenados contêm a imagem de arranque usada para iniciar o computador de destino e a imagem de OS que é aplicada ao computador de destino. Também pode especificar aplicações, pacotes e pacotes de controladores para incluir como parte do suporte de dados pré-configurado. A sequência de tarefas que implanta o Sistema operativo não está incluída nos meios de comunicação. Ao implementar uma sequência de tarefas que utiliza meios pré-encenados, o cliente verifica primeiro a cache da sequência de tarefas local para obter conteúdo válido. Se o conteúdo não puder ser encontrado ou tiver sido revisto, o cliente descarrega o conteúdo a partir de um ponto de distribuição ou de um par.  

O suporte de dados pré-configurado é aplicado no disco rígido do computador novo antes do seu envio para o utilizador final. Quando o computador começa pela primeira vez depois de ter aplicado os meios pré-encenados, o computador começa no Windows PE. Liga-se a um ponto de gestão para localizar a sequência de tarefas que completa o processo de implementação do SO.  

> [!IMPORTANT]  
> Os pacotes em meios pré-encenados não estão encriptados. Tome as medidas de segurança adequadas, tais como a adição de uma palavra-passe aos meios de comunicação, para garantir que o conteúdo do pacote é protegido de utilizadores não autorizados.  

Para obter mais informações sobre como criar meios de comunicação pré-encenados, consulte [Criar meios pré-encenados.](create-prestaged-media.md)  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Meios de comunicação autónomos

Os meios de comunicação autónomos contêm tudo o que é necessário para implantar o Sistema Operativo. Este conteúdo inclui a sequência de tarefas e qualquer outro conteúdo necessário. Como tudo o que é necessário para implementar o SISTEMA é armazenado nos meios autónomos, o espaço de disco necessário para meios autónomos é maior do que para outros tipos de meios de comunicação.  

Para obter mais informações sobre como criar meios de comunicação autónomos, consulte [Create stand-alone media](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Considerações ao utilizar HTTPS

Quando configurar os seus pontos de gestão e pontos de distribuição para utilizar HTTPS, crie meios de arranque e meios pré-encenados num site primário, e não no site da administração central. Além disso, considere o seguinte ponto para ajudá-lo a determinar se configura os meios como dinâmicos ou baseados no site:  

- Para configurar os meios de comunicação como meios dinâmicos, todos os sites primários devem ter a autoridade do certificado de raiz (CA) do site a partir do qual criou os meios de comunicação. Pode importar a AC de raiz para todos os sites principais da hierarquia.  

- Quando os sites primários da hierarquia do Gestor de Configuração usam diferentes CAs de raiz, deve utilizar os meios baseados no site em cada site.  
