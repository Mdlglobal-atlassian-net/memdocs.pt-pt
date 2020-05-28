---
title: Pré-requisitos para atualizações de software
titleSuffix: Configuration Manager
description: Conheça os pré-requisitos para atualizações de software no Gestor de Configuração.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906705"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Pré-requisitos para atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo lista os pré-requisitos para atualizações de software no Gestor de Configuração. Para cada um dos pré-requisitos, as dependências externas e as dependências internas estão listadas em tabelas separadas.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dependências de atualização de software que são externas ao Gestor de Configuração  
 As seguintes secções listam as dependências externas para atualizações de software.  

### <a name="internet-information-services"></a>Internet Information Services  
 Os Serviços de Informação de Internet (IIS) devem ser instalados nos servidores do sistema do site para executar o ponto de atualização do software, o ponto de gestão e o ponto de distribuição. Para obter mais informações, veja [Pré-requisitos das funções do sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Os Serviços de Atualização do Servidor do Windows (WSUS) são necessários para a sincronização de atualizações de software e para as atualizações de software que a aplicabilidade dos clientes podem fazer. O servidor WSUS deve ser instalado antes de criar a função de ponto de atualização de software. As seguintes versões da WSUS são suportadas para um ponto de atualização de software:  

- WSUS 10.0.14393 (função no Windows Server 2016)
- WSUS 10.0.17763 (função no Windows Server 2019) (Requer o Gestor de Configuração 1810 ou mais tarde)
- WSUS 6.2 e 6.3 (função no Windows Server 2012 e Windows Server 2012 R2)
  - [KB 3095113 e KB 3159706 (ou uma atualização equivalente)](#BKMK_wsus2012) são necessários para wSUS 6.2 e 6.3 se implementar atualizações do Windows 10.

> [!NOTE]
> - Quando tiver vários pontos de atualização de software num site, certifique-se de que todos estão a executar a mesma versão do WSUS.

### <a name="wsus-administration-console"></a>Consola de Administração do WSUS  
A Consola de Administração WSUS é necessária no servidor do site do Gestor de Configuração quando o ponto de atualização do software está num servidor de sistema de site remoto e o WSUS ainda não está instalado no servidor do site.  

> [!IMPORTANT]  
> - A versão WSUS no servidor do site deve ser a mesma que a versão WSUS que está a ser recorrida nos pontos de atualização do software.
> - Não utilize a Consola de Administração WSUS para configurar as definições do WSUS. O Gestor de Configuração liga-se à instância do WSUS que está a ser recorrida no ponto de atualização do software e configura as definições apropriadas.  


### <a name="windows-update-agent"></a>Windows Update Agent  
 O cliente do Windows Update Agent (WUA) é necessário nos clientes para que possam ligar-se ao servidor WSUS. A WUA recupera a lista de atualizações de software que devem ser digitalizadas para o cumprimento.  

 Quando instala o Gestor de Configuração, a versão mais recente da WUA é descarregada. Em seguida, quando instala o cliente do Gestor de Configuração, a WUA é atualizada se necessário. Se a instalação falhar, deve utilizar um método diferente para atualizar a WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dependências de atualização de software que são internas para O Gestor de Configuração  
 As seguintes secções listam as dependências internas para atualizações de software no Gestor de Configuração.  

### <a name="management-points"></a>Pontos de gestão  
 Pontos de gestão transferem informações entre computadores clientes e o site do Gestor de Configuração. Os pontos de gestão são necessários para atualizações de software.  

### <a name="software-update-points"></a>Pontos de atualização de software  
 Tem de instalar um ponto de atualização de software no servidor WSUS para implementar atualizações de software no 'Gestor de Configuração'. Para mais informações, consulte [Instalar e configurar um ponto](../get-started/install-a-software-update-point.md)de atualização de software .

### <a name="distribution-points"></a>Pontos de distribuição  
 Os pontos de distribuição são necessários para armazenar o conteúdo para atualizações de software. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdos, consulte Gerir a infraestrutura de [conteúdos e conteúdos.](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

### <a name="client-settings-for-software-updates"></a>Definições de cliente para atualizações de software  
As atualizações de software são ativadas para clientes por padrão. Existem outras definições disponíveis que controlam como e quando os clientes avaliam a conformidade com as atualizações do software e controlam a forma como as atualizações do software são instaladas.  

 Para obter mais informações, veja os seguintes artigos:  

- [Definições de cliente para atualizações de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Software atualiza as definições do cliente](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Pontos do Reporting Services  
 A função do sistema de sites do ponto do Reporting Services pode apresentar relatórios de atualizações de software. Este papel é opcional, mas recomendado. Para obter mais informações sobre como criar um ponto de serviços de reporte, consulte [a Configuração de relatórios](../../core/servers/manage/configuring-reporting.md).  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>Quais as atualizações necessárias nos WSUS 6.2 e 6.3?

São necessárias duas atualizações para sincronizar a classificação de **Upgrades** em WSUS 6.2 e 6.3. Ocasionalmente, pode ver um erro a descarregar ou implementar upgrades se sincronizarem antes de kB3095113 e KB3159706 terem sido instalados. A informação sobre possíveis problemas está na próxima secção.  

- Tem de instalar o [KB 3095113,](https://support.microsoft.com/kb/3095113)lançado em outubro de 2015, nos pontos de atualização do software e servidores do site antes de sincronizar a classificação **de Upgrades.**
  - Esta atualização permite a classificação **de Upgrades.**
- Para requerer o Windows 10 versão 1607 e mais tarde, tem de instalar e configurar [o KB 3159706](https://support.microsoft.com/help/3159706). KB 3159706 foi lançado em maio de 2016.
  - Esta atualização permite ao WSUS desencriptar de forma nativa os ficheiros utilizados para atualizar a versão 1607 do Windows 1607 e posteriormente.

>[!IMPORTANT]
> Tanto o KB 3095113 como o KB 3159706 estão incluídos no **Rollup** mensal de qualidade de segurança a partir de julho de 2017. Isto significa que pode não ver KB 3095113 e KB 3159706 como atualizações instaladas, uma vez que podem ter sido instaladas com um rollup. No entanto, se precisar de qualquer uma destas atualizações, recomendamos a instalação de um **Rollup** de Qualidade Mensal de Segurança lançado após outubro de 2017, uma vez que contêm uma atualização adicional da WSUS para diminuir a utilização da memória no serviço de clientela da WSUS.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Download de atualizações do Windows 10 falha com "Error: Invalid certificate signature" ou 0xc1800118

As atualizações e problemas descritos nesta secção aplicam-se apenas ao WSUS que funciona no Windows Server 2012 ou no Windows Server 2012 Máquinas R2 (WSUS 6.2 e 6.3). Normalmente, só verá os problemas descritos nesta secção se instalou o WSUS antes de julho de 2017 e recentemente ativou a classificação **de Upgrades.** No entanto, é possível ver estas questões em outras situações também.

### <a name="historical-information-about-kb-3095113"></a>Informação histórica sobre kB 3095113

 [O KB 3095113](https://support.microsoft.com/kb/3095113) foi [lançado como um hotfix](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113) em outubro de 2015 para adicionar suporte para atualizações do Windows 10 à WSUS. A atualização permite à WSUS sincronizar e distribuir atualizações na classificação **de Atualizações** para windows 10.

Se sincronizar quaisquer atualizações sem ter instalado pela primeira vez [o KB 3095113,](https://support.microsoft.com/kb/3095113)povoa a base de dados WSUS (SUSDB) com dados inutilizáveis. Esses dados devem ser limpos antes de as atualizações poderem ser corretamente implementadas. As atualizações do Windows 10 neste estado não podem ser descarregadas utilizando o Descarregamento software Updates Wizard.

Erros que se assemelham aos seguintes aparecem na página de conclusão do Assistente de Atualizações de Software de Descarregamento:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Além disso, erros que se assemelham aos seguintes são registados no ficheiro PatchDownloader.log:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Historicamente, quando estes erros ocorreram, seriam resolvidos através da realização de uma versão modificada dos passos de resolução para a [WSUS.](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus) Como estes passos são semelhantes à resolução para não fazer os passos manuais necessários após a instalação do KB 3159706, combinamos ambos os conjuntos de passos numa única resolução na secção abaixo:

- [Para recuperar da sincronização das atualizações antes de instalar kB 3095113 ou KB 3159706](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>Informação histórica sobre kB 3159706

O KB 3148812 foi inicialmente lançado em abril de 2016 para permitir à WSUS desencriptar de forma nativa os ficheiros .esd utilizados para a atualização dos pacotes do Windows 10. [KB 3148812 causou problemas a alguns clientes](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) e foi substituído por [KB 3159706](https://support.microsoft.com/help/3159706). O KB 3159706 precisa de ser instalado em todos os pontos de atualização de software e servidores do site antes de poder repor o Windows 10 Version 1607 e dispositivos posteriores. No entanto, podem surgir problemas se não se aperceber que o KB necessita dos seguintes passos manuais após a instalação:

1. De uma corrida rápida de comando elevado `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` .
1. Reinicie o serviço WSUS em todos os servidores WSUS.

Se não perceber que o KB 3159706 tinha passos manuais após a instalação, ou sincronizado na atualização para o Windows 10 1607 antes de instalar o KB 3159706, terá problemas de ligação à consola WSUS e implementando a atualização respectivamente. Quando um cliente descarregou o ficheiro de upgrade, receberia um código de erro [ **0xC1800118** ](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Como os passos de resolução são semelhantes à resolução para sincronizar atualizações antes da instalação do KB 3095113, combinamos ambos os conjuntos de passos numa única resolução na secção seguinte.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>Para recuperar da sincronização das atualizações antes de instalar kB 3095113 ou KB 3159706

Siga os passos abaixo para resolver tanto o erro 0xc1800118 como "Error: Invalid certificate signature":

1. Desative a classificação de **Upgrades** tanto no WSUS como no Gestor de Configuração. Não quer que ocorra uma sincronização até que seja direcionado por estas instruções.  
   - Desmarque a classificação de **Upgrades** nas propriedades do componente de ponto de atualização de software no site de alto nível.
     - Para mais informações, consulte [classificações e produtos de Configuração.](../get-started/configure-classifications-and-products.md)
   - Desfaça a classificação de **Upgrades** da WSUS em produtos **e classificações** na página [ **Opções,** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)ou utilize o PowerShell ISE funcionando como administrador.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - Se partilhar a base de dados wSUS entre vários servidores WSUS, só precisa de **desmarcar atualizações** uma vez para cada base de dados.  
1. Em cada servidor WSUS, a partir de uma execução rápida de comando elevado: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` . Em seguida, reinicie o serviço WSUS em todos os servidores WSUS.
   -  A WSUS coloca a base de dados no [modo de utilizador único](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) antes de verificar se é necessário fazer manutenção. A manutenção corre ou não funciona com base nos resultados da verificação. Em seguida, a base de dados é reposta no modo multiutilizador. 
   - Se partilhar a base de dados wSUS entre vários servidores WSUS, só precisa de fazer esta manutenção uma vez para cada base de dados.
1. Elimine todas as atualizações do Windows 10 de cada base de dados wSUS utilizando o PowerShell ISE como administrador.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Elimine ficheiros da tabela tbFile de cada uma das bases de dados wSUS utilizadas pelos pontos de atualização do software. Na base de dados wSUS, execute os seguintes comandos do Estúdio de Gestão de Servidores SQL:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Inicie a sincronização das atualizações de software no seu site de alto nível no 'Gestor de Configuração' e aguarde que esteja concluído. Uma sincronização completa ocorre porque fizemos uma alteração no Gestor de Configuração de Classificações quando removemos **upgrades**. (Para obter mais informações, consulte as atualizações de [software Synchronize](../get-started/synchronize-software-updates.md).
1. Selecione a classificação **de Upgrades** nas propriedades do componente de ponto de atualização de software. Em seguida, inicie outra sincronização de atualizações de software para trazer as **Atualizações** de volta ao WSUS e Ao Gestor de Configuração. Não é preciso ativar a classificação de **Upgrades** no WSUS, uma vez que o Gestor de Configuração o fará por si.
1. Se os seus clientes receberam o código de erro **0xC1800118** ao descarregar uma atualização, terá de eliminar a loja de dados utilizada pelo Windows Update Agent. Pode também ter de apagar a pasta ~BT escondida no dispositivo. Da próxima vez que o cliente digitalizar, será uma varredura completa contra o servidor WSUS em vez de um delta. Pode utilizar um script PowerShell semelhante ao seguinte script de amostra:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Próximos passos
[Preparar a gestão de atualizações de software](../get-started/prepare-for-software-updates-management.md)
