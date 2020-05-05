---
title: Sincronizar as atualizações do Office 365 sem ligação à Internet
titleSuffix: Configuration Manager
description: Sincronizar as atualizações do Office 365 no ponto de atualização de software de alto nível que está desligado da Internet.
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110360"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a>Sincronizar as atualizações do Office 365 a partir de um ponto de atualização de software desligado

*Aplica-se a: Gestor de Configuração (ramo atual)*
<!--4065163-->
A partir da versão de 'Gestor de Configuração' de 2002, pode utilizar uma ferramenta para importar atualizações do Office 365 a partir de um servidor WSUS ligado à Internet para um ambiente de Gestor de Configuração desligado. Anteriormente, quando exportou e importou metadados para software atualizado em ambientes desligados, não foi capaz de implementar atualizações do Office 365. As atualizações do Office 365 requerem metadados adicionais descarregados de uma API do Office e do Office CDN, o que não é possível para ambientes desligados.

> [!Note]
> A partir de 21 de abril de 2020, o Office 365 ProPlus está a ser renomeado para **microsoft 365 Apps para empresa**. Para mais informações, consulte [a alteração de nome para o Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Ainda pode ver referências ao nome antigo na consola do Gestor de Configuração e documentação de suporte enquanto a consola está a ser atualizada.

## <a name="prerequisites"></a>Pré-requisitos

- Um servidor WSUS ligado à Internet executa um mínimo de Windows Server 2012.
- O servidor WSUS precisa de conectividade com estes dois pontos finais da Internet:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Copie a ferramenta OfflineUpdateExporter e as suas dependências para o servidor WSUS ligado à Internet.
  - A ferramenta e as suas dependências estão no ** &lt;diretório ConfigMgrInstallDir>/tools/OfflineUpdateExporter.**
- O utilizador que executa a ferramenta deve fazer parte do grupo de **administradores da WSUS.**
- O diretório criado para armazenar os metadados e conteúdos de atualização do Office deve ter listas de controlo de acesso adequadas (ACLs) para proteger os ficheiros.
    - Este diretório também deve estar vazio.
- Os dados que estão a ser transferidos do servidor WSUS online para o ambiente desligado devem ser movidos de forma segura.

> [!IMPORTANT]
> Os conteúdos serão descarregados para todos os idiomas do Office 365. Cada atualização pode ter aproximadamente 10 GB de conteúdo.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Sincronizar edepois recusar atualizações desnecessárias do Office 365

1. Na sua Internet ligada à WSUS, abra a consola WSUS.
1. Selecione **opções** e, em seguida, **Produtos e Classificações**.
1. No separador **Produtos,** selecione **Office 365 Client** e selecione **Atualizações** no separador **Classificações.** [ ![Produtos e classificações para as atualizações do Office 365 no WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Vá a **Sincronizações** e selecione **Synchronize Now** para obter as atualizações do Office 365 no WSUS.
1. Quando a sincronização estiver concluída, recuse quaisquer atualizações do Office 365 que não queira implementar com o Gestor de Configuração. Não precisa de aprovar atualizações do Office 365 para que sejam descarregadas.  
   - A diminuição das atualizações indesejadas do Office 365 na WSUS não impede que sejam exportadas durante uma exportação WsusUtil.exe, mas impede que a ferramenta OfflineUpdateExport descarregue o conteúdo para eles.
   - A ferramenta OfflineUpdateExporter faz o download das atualizações do Office 365 para si. Outros produtos ainda terão de ser aprovados para download se estiver a exportar atualizações para os mesmos.
    - Crie uma nova visão de [atualização no WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus) para ver e recusar facilmente atualizações desnecessárias do Office 365 no WSUS.
1. Se estiver a aprovar outras atualizações de produtos para download e exportação, aguarde que o download de conteúdo seja concluído antes de executar a exportação wsusUtil.exe e copiar o conteúdo da pasta WSUSContent. Para mais informações, consulte [as atualizações de software Synchronize a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md)

## <a name="exporting-the-office-365-updates"></a>Exportação das atualizações do Office 365

1. Copie a pasta OfflineUpdateExporter do Gestor de Configuração para o servidor WSUS ligado à Internet.
    - A ferramenta e as suas dependências estão no ** &lt;diretório ConfigMgrInstallDir>/tools/OfflineUpdateExporter.**
1. A partir de um pedido de comando no servidor WSUS ligado à Internet, execute a ferramenta com a seguinte utilização: **OfflineUpdateExporter.exe -O -D &lt;destino>**

   |Parâmetro de Exportador offlineUpdate|Descrição|
   |---|---|
   |**- O**|  **- Escritório.** Especifica o produto para atualizações exportação é Office 365|
   |**-D**|**-Destino**. O destino é um parâmetro necessário e todo o caminho para a pasta de destino é necessário.|

   - A ferramenta **OfflineUpdateExporter** faz o seguinte:
      - Liga-se ao WSUS
      - Lê os metadados de atualização do Office 365 no WSUS
      - Descarrega o conteúdo e quaisquer metadados adicionais necessários pelas atualizações do Office 365 para a pasta de destino

1. No pedido de comando no servidor WSUS ligado à Internet, navegue para a pasta que contém WsusUtil.exe. Por padrão, a ferramenta está localizada em %*ProgramFiles*%\Update Services\Tools. Por exemplo, se a ferramenta estiver localizada na localização predefinida, escreva **cd %ProgramFiles%\Update Services\Tools**.
   - Se estiver a utilizar o Windows Server 2012, certifique-se de que o [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) está instalado nos servidores WSUS.
   - O utilizador que executa a ferramenta WsusUtil deve ser um membro do grupo de Administradores locais no servidor.

1. Escreva o seguinte para exportar os metadados de atualizações de software para um ficheiro GZIP:  

    Ficheiro de*logfile* de*pacote*de **exportação WsusUtil.exe**      

    Por exemplo:  

    **WsusUtil.exe exportação exportação.xml.gz exportação.log**

1. Copie o ficheiro **export.xml.gz** para o servidor WSUS de alto nível na rede desligada.
1. Se aprovou atualizações para outros produtos, copie o conteúdo da pasta WSUSContent para a pasta WSUSContent desligada de nível superior.
1. Copie a pasta de destino utilizada para o **OfflineUpdateExporter** para o servidor de site do Gestor de Configuração de topo na rede desligada.

## <a name="import-the-office-365-updates"></a>Importar as atualizações do Office 365

1. No servidor WSUS de alto nível desligado, importe os metadados da atualização do **export.xml.gz** gerado no servidor WSUS ligado à Internet.
   
    Por exemplo:  

    **WsusUtil.exe importação export.xml.gz import.log**
    
    Por predefinição, a ferramenta WsusUtil.exe está localizada em %*ProgramFiles*%\Update Services\Tools.

1. Uma vez concluída a importação, terá de configurar uma propriedade de controlo de site no servidor de site do Gestor de Configuração de alto nível desligado. Esta configuração de alteração aponta o Gestor de Configuração para o conteúdo do Office 365. Para alterar a configuração da propriedade:
   1. Copie o [script O365OflBaseUrlConfigurado PowerShell](#bkmk_o365_script) para o servidor de site do Gestor de Configuração desligado de nível superior.
   1. Altere `"D:\Office365updates\content"` para o percurso completo do diretório copiado que contém o conteúdo do Office e os metadados gerados pelo OfflineUpdateExporter.
      > [!IMPORTANT]
      > Apenas os caminhos locais funcionam para a propriedade O365OflBaseUrlConfigured.
   1. Salvar o script como`O365OflBaseUrlConfigured.ps1`
   1. A partir de uma janela powerShell elevada no servidor de `.\O365OflBaseUrlConfigured.ps1`site de configuração de nível superior desligado, executar .
   1. Reinicie o serviço **SMS_Executive** no servidor do site.
1. Na consola de Gestor de **Configuração,** navegue para**sites**de**configuração** > do site **da administração.** > 
1. Clique à direita no seu site de nível superior e, em seguida, selecione **Configure Site Components** > **Software Update Point**.
1. No separador **Classificações,** selecione *Atualizações*. No separador **Produtos,** selecione *Office 365 Client*.
1. [Sincronizar atualizações](synchronize-software-updates.md#manually-start-software-updates-synchronization) de software para O Gestor de Configuração
1. Quando a sincronização estiver concluída, utilize o seu processo normal para implementar atualizações do Office 365.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a>Configuração proxy

- A configuração proxy não é incorporada nativamente na ferramenta. Se o proxy estiver definido nas Opções de Internet no servidor onde a ferramenta está em execução, em teoria, será utilizada e deve funcionar corretamente.
   - A partir de `netsh winhttp show proxy` um pedido de comando, corra para ver o proxy configurado.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a>Modificar propriedade O365OflBaseUrlConfigured

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Passos seguintes

[Adicione atualizações de software a um grupo de atualização](../deploy-use/add-software-updates-to-an-update-group.md)