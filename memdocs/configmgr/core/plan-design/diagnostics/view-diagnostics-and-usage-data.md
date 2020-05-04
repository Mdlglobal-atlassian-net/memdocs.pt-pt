---
title: Ver dados de diagnóstico
titleSuffix: Configuration Manager
description: Consulte os dados de diagnóstico e utilização para confirmar que a sua hierarquia do Gestor de Configuração não contém nenhuma informação sensível.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712541"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Como visualizar diagnósticos e dados de utilização para O Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode ver dados de diagnóstico e utilização da hierarquia do Gestor de Configuração para confirmar que não inclui nenhuma informação sensível ou identificável. O site resume e armazena os seus dados de diagnóstico na tabela **TEL_TelemetryResults** da base de dados do site. Forma os dados para serem programáticamente utilizáveis e eficientes.

As informações deste artigo dão-lhe uma visão dos dados exatos enviados à Microsoft. Não se destina a ser usado para outros fins, como a análise de dados.  

## <a name="view-data-in-database"></a>Ver dados na base de dados

Utilize o seguinte comando SQL para visualizar o conteúdo desta tabela e mostrar os dados exatos que são enviados:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>Exportar os dados

Quando o ponto de ligação ao serviço estiver em modo offline, utilize a ferramenta de ligação de serviço para exportar os dados atuais para um ficheiro de valores separados pela vírlém (CSV). Executar a ferramenta de ligação de serviço no ponto de ligação de serviço com o parâmetro **-Export.**

Para mais informações, consulte [Utilize a ferramenta de ligação de serviço](../../servers/manage/use-the-service-connection-tool.md).

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a>Hashes de ida

Alguns dados consistem em cadeias de caracteres alfanuméricos aleatórios. O Gestor de Configuração usa o algoritmo SHA-256 para criar hashes de ida. Este processo garante que a Microsoft não recolhe dados potencialmente sensíveis. Os dados hashed ainda podem ser utilizados para fins de correlação e comparação.

Por exemplo, em vez de recolher os nomes das tabelas na base de dados do site, captura o hash de sentido único para cada nome de mesa. Este comportamento garante que quaisquer nomes de mesa personalizados não são visíveis. A Microsoft faz então o mesmo processo de hash one-way dos nomes de tabela SQL padrão. Comparar os resultados das duas consultas determina o desvio do esquema da sua base de dados do padrão do produto. Esta informação é então utilizada para melhorar as atualizações que requerem alterações ao esquema SQL.  

Quando se vê os dados brutos, aparece um valor hashed comum em cada linha de dados. Este hash é a identidade da hierarquia. É usado para correlacionar dados com a mesma hierarquia sem identificar o cliente ou fonte.

### <a name="how-the-one-way-hash-works"></a>Como funciona o hash de sentido único

1. Obtenha o seu ID de hierarquia executando a seguinte consulta SQL no SQL Management Studio contra a base de dados do Gestor de Configuração:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Utilize o seguinte script Windows PowerShell para fazer o haxixe de ida e outro do seu ID da hierarquia.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Compare a saída do script com o GUID nos dados brutos. Este processo mostra como os dados são obscurecidos.

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Níveis de dados de utilização de diagnóstico](levels-overview.md)
