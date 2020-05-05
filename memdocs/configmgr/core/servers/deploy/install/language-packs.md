---
title: Pacotes de idiomas
titleSuffix: Configuration Manager
description: Conheça o suporte linguístico disponível no Gestor de Configuração.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ec5581567925ee57300274e50288058e06d80ec0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718190"
---
# <a name="language-packs-in-configuration-manager"></a>Pacotes de idiomas no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo fornece detalhes técnicos sobre o suporte linguístico no Gestor de Configuração. Os servidores e clientes do Gestor de Configuração são considerados neutros em termos de linguagem. Adicione suporte para idiomas de exibição instalando **pacotes** de idiomas de servidor ou pacotes de **idiomas de cliente** num site de administração central e em sites primários. Seleciona os idiomas do servidor e do cliente para suportar num site a partir dos ficheiros de pack de idiomas disponíveis durante o processo de instalação do site.
 
Instale vários idiomas em cada site. Só precisa de instalar os idiomas que utiliza.  

- Cada site suporta vários idiomas para consolas de Configuração Manager.  

- Adicione suporte apenas para as línguas do cliente que pretende suportar instalando pacotes individuais de idioma de cliente em cada site.  

Quando instala suporte para um idioma que corresponda aos seguintes componentes:  

- O idioma de exibição de um computador: Tanto a consola Do Gestor de Configuração como a interface do utilizador cliente que funciona nesse computador exibem informações nesse idioma.  

- A preferência linguística que está a ser utilizada pelo navegador web de um computador: Conexões a informações baseadas na Web, incluindo o Catálogo de Aplicações ou serviços de reporte de servidores SQL, exibem nesse idioma.  


Ao executar a configuração do 'Gestor de Configuração', descarrega ficheiros de pack de idiomas como parte dos pré-requisitos e ficheiros redistribuíveis. Também pode utilizar o downloader de [configuração](setup-downloader.md) para descarregar estes ficheiros antes de executar a configuração.   



## <a name="server-languages"></a>Idiomas do servidor  

Utilize a tabela seguinte para mapear uma identificação local para um idioma que pretende suportar nos servidores. Para obter mais informações sobre iDs locais, consulte [iDs locais atribuídos pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Idioma do servidor|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENU|  
|Chinês (Simplificado)|0804|CHS|  
|Chinês (Tradicional, Taiwan)|0404|CHT|  
|Checo|0405|CSY|  
|Neerlandês (Países Baixos)|0413|NLD|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Húngaro|040e|HUN|  
|Italiano (Itália)|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Polaco|0415|PLK|  
|Português (Brasil)|0416|PTB|  
|Português (Portugal)|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol (Espanha)|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  



## <a name="client-languages"></a>Línguas de cliente  

Use a tabela seguinte para mapear uma identificação local para um idioma que pretende suportar nos computadores dos clientes. Para obter mais informações sobre iDs locais, consulte [iDs locais atribuídos pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Idioma do cliente|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENG|  
|Chinês (Simplificado)|0804|CHS|  
|Chinês (Tradicional, Taiwan)|0404|CHT|  
|Checo|0405|CSY|  
|Dinamarquês|0406|DAN|  
|Neerlandês (Países Baixos)|0413|NLD|  
|Finlandês|040b|FIN|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Grego|0408|ELL|  
|Húngaro|040e|HUN|  
|Italiano (Itália)|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Norueguês|0414|NOR|  
|Polaco|0415|PLK|  
|Português (Brasil)|0416|PTB|  
|Português (Portugal)|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol (Espanha)|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Idiomas de clientes de dispositivomóvel  
Quando adiciona suporte para idiomas de dispositivos móveis, todas as línguas de cliente de dispositivos móveis suportadas estão incluídas. Não é possível selecionar pacotes de idiomas individuais para suporte a dispositivos móveis.  



## <a name="identify-installed-language-packs"></a>Identificar pacotes de idiomas instalados  
Para identificar os pacotes de idiomas instalados num computador que executa o cliente do Gestor de Configuração, procure o ID local (LCID) dos pacotes de idiomas instalados no registo do computador. Esta informação está disponível na seguinte via de registo:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personalize o inventário de hardware para recolher esta informação. Em seguida, construa um relatório personalizado para ver os detalhes da linguagem. Para obter mais informações sobre a recolha de inventário de hardware personalizado, consulte [como configurar o inventário](../../../clients/manage/inventory/configure-hardware-inventory.md)de hardware . Para mais informações, consulte [Criar relatórios](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
