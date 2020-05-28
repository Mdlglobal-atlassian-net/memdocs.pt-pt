---
title: Notas de versão
titleSuffix: Configuration Manager
description: Conheça questões urgentes que ainda não estão corrigidas no produto ou abrangidas por um artigo de base de conhecimento do Microsoft Support.
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823967"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de lançamento para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Com o Gestor de Configuração, as notas de lançamento do produto limitam-se a problemas urgentes. Estes problemas ainda não estão corrigidos no produto, nem detalhados num artigo de base de conhecimento do Microsoft Support.  

A documentação específica de funcionalidades inclui informações sobre questões conhecidas que afetam cenários fundamentais.  

Este artigo contém notas de lançamento para o atual ramo do Gestor de Configuração. Para obter informações sobre o ramo de pré-visualização técnica, consulte [Pré-visualização Técnica](../../../get-started/technical-preview.md)  

Para obter informações sobre as novas funcionalidades introduzidas com diferentes versões, consulte os seguintes artigos:

- [Novidades na versão 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Novidades na versão 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Novidades na versão 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [Novidades na versão 1902](../../../plan-design/changes/whats-new-in-version-1902.md)

Para obter informações sobre as novas funcionalidades no Desktop Analytics, consulte [as novidades no Desktop Analytics.](../../../../desktop-analytics/whats-new.md)

> [!Tip]  
> Para ser notificado quando esta página for atualizada, copie e cole o seguinte URL no seu leitor de feed RSS:`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Configurar e atualizar  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>Atualização automática do cliente acontece imediatamente para todos os clientes

<!-- 6040412 -->

*Aplica-se à versão 1910*

Se o seu site utilizar a [atualização automática](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)do cliente , quando atualizar o site para a versão 1910, todos os clientes atualizam imediatamente após as atualizações do site com sucesso. A única aleatoriedade é quando os clientes recebem a apólice, que por defeito é a cada hora. Para um grande site com muitos clientes, este comportamento pode consumir uma quantidade significativa de tráfego de rede e pontos de distribuição de stress.

Para obter mais informações sobre as versões afetadas, consulte a atualização do Cliente para o atual ramo do Gestor de [Configuração, versão 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Servidor do site em modo passivo não atualiza configuração.mof

<!-- 5787848 -->

*Aplica-se à versão 1910*

Se o seu site incluir um servidor de [site em modo passivo,](../configure/site-server-high-availability.md)poderá perder personalizações de inventário quando atualizar o site. O site não sincroniza a configuração.mof quando falha nos servidores do site.

Para contornar este problema, volte manualmente e restaure a configuração do site.mof.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Configuração pré-requisito aviso no nível funcional de domínio no Servidor 2019

<!-- 4904376 -->

*Aplica-se à versão 1906*

Ao instalar a atualização para a versão 1906 num ambiente com controladores de domínio a executar o Windows Server 2019, a verificação prévia para o nível funcional do domínio devolve o seguinte aviso:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Para contornar esta questão, ignore o aviso.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>A descoberta de utilizadores da AD Azure e a sincronização do grupo de recolha não funcionam após a expansão do site

<!-- 4797313 -->
*Aplica-se à versão 1906*

Depois de configurar qualquer uma das seguintes funcionalidades:

- Descoberta do grupo de utilizadores do Diretório Ativo Azure
- Sincronizar os resultados da adesão à coleção aos grupos de Diretórios Ativos da Azure

Se expandir um local primário autónomo para uma hierarquia com um site de administração central, verá o seguinte erro em SMS_AZUREAD_DISCOVERY_AGENT.log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Para resolver este problema, renovar a chave associada ao registo de aplicações em Azure AD. Para mais informações, consulte [Renovar a chave secreta.](../configure/azure-services-wizard.md#bkmk_renew)

## <a name="role-based-administration"></a>Administração baseada em funções

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Os âmbitos de segurança de certas pastas não se replicam do CAS para os sites primários
<!--6306759-->
*Aplica-se à versão 1910*

Após o upgrade para a versão 1910, os âmbitos de [segurança para pastas](../configure/configure-role-based-administration.md#bkmk_config-folder) em coleções de utilizadores e coleções de dispositivos não são replicados do CAS para sites primários.

## <a name="application-management"></a>Gestão de aplicações

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Incapaz de obter certificado de erro PowerShell ao implementar O Microsoft Edge, versão 77 e mais tarde
<!--5769384-->
*Aplica-se a: Versão do Gestor de Configuração 1910*

Se estiver a executar a consola do Gestor de Configuração num SISTEMA onde o idioma é sueco, húngaro ou japonês, receberá o seguinte erro ao implementar o Microsoft Edge, versão 77 e mais tarde:

`Unable to get certificate for Powershell`

Este erro ocorre porque uma `scripts` pasta não existe sob o `AdminConsole\bin` diretório para línguas sueca, húngara ou japonesa. A pasta de scripts está localizada nestas línguas de SO.

Para resolver este problema, crie uma pasta chamada `scripts` no `AdminConsole\bin` diretório. Copie os ficheiros da pasta localizada para a `scripts` pasta recém-criada. Implemente o Microsoft Edge, a versão 77 e, mais tarde, uma vez copiados os ficheiros.

## <a name="os-deployment"></a>Implementação de SO

### <a name="task-sequences-cant-run-over-cmg"></a>Sequências de tarefas não podem passar por cima da CMG

*Aplica-se a: Versão de Gestor de Configuração 2002*

Existem dois casos em que as sequências de tarefas não podem ser executadas num dispositivo que comunica através de um portal de gestão de nuvens (CMG):

- Configura o site para Enhanced HTTP e o ponto de gestão é HTTP.<!-- 6358851 -->

    Para resolver este problema, configure o ponto de gestão para HTTPS.

- Instalou e registou o cliente com um sinal de registo a granel para autenticação.<!-- 6377921 -->

    Para resolver este problema, utilize um dos seguintes métodos de autenticação:

  - Pré-registar o dispositivo na rede interna
  - Configure o dispositivo com um certificado de autenticação do cliente
  - Junte-se ao dispositivo para a Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Após a promoção do servidor passivo do site, os pacotes de imagem de boot padrão ainda têm fonte de pacote no servidor ativo anterior

<!--3453224, SCCMDocs-pr issue 3097-->
*Aplica-se a: Versão 1810 do Gestor de Configuração*

Se tiver um servidor de site em modo passivo (servidor B), quando o promove para ativo, a localização do conteúdo das imagens de boot predefinidas continua a fazer referência ao servidor anteriormente ativo (servidor A). Se o servidor A tiver uma falha de hardware, não pode atualizar ou alterar as imagens de boot predefinidas.

Não há sobra para esta questão.

## <a name="software-updates"></a>Atualizações de software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Faltam funções de segurança para implementações faseadas

<!--3479337, SCCMDocs-pr issue 3095-->
*Aplica-se a: Configuração Manager versões 1810, 1902*

O gestor de **implementação** do OS tem permissões para [implementações faseadas.](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) Faltam estas permissões:  

- **Administrador de Aplicações**  
- **Gestor de Implementação de Aplicações**  
- **Gestor de atualização de software**  

O papel de Autor da **Aplicação** pode parecer ter algumas permissões para implementações faseadas, mas não deve ser capaz de criar implementações.

Um utilizador com uma destas funções pode iniciar o assistente de implementação faseada create, e pode ver implementações faseadas para uma aplicação ou atualização de software. Não podem completar o assistente, nem fazer alterações a uma implementação existente.

Para contornar esta questão, crie um papel de segurança personalizado. Copie uma função de segurança existente e adicione as seguintes permissões na classe de objetos de **implantação faseada:**

- Criar  
- Eliminar  
- Modificar  
- Leitura  

Para mais informações, consulte [Criar funções de segurança personalizadas](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)

## <a name="desktop-analytics"></a>Análise de Computadores

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a>Uma atualização de segurança alargada para o Windows 7 faz com que se mostrem incapazes de **se inscreverem**

<!-- 7283186 -->
_Aplica-se a: Configuração Manager versões 1902, 1906, 1910 e 2002_

A atualização de segurança estendida de abril de 2020 (ESU) para o Windows 7 alterou a versão mínima exigida do diagtrack.dll de 10586 para 10240. Esta alteração faz com que os dispositivos do Windows 7 apareçam como Incapazes de se inscrever no painel de saúde de **ligação** a análise do ambiente de **trabalho.** Quando se aprofunda na vista do dispositivo para este estado, a propriedade de configuração do **serviço DiagTrack** apresenta o seguinte estado:`Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

Não é necessária qualquer sucução para esta questão. Não desinstale a ESU de abril. Caso contrário configurado corretamente, os dispositivos do Windows 7 ainda reportam dados de diagnóstico ao serviço Desktop Analytics e ainda aparecem no portal.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Se utilizar o inventário de hardware para visualizações distribuídas, não pode embarcar para desktop Analytics

<!-- 4950335 -->
*Aplica-se a: Configuração Manager versão 1902 com rollup de atualização e versão 1906*

Se tiver uma hierarquia e ativar os dados do site de inventário de **hardware** para [visualizações distribuídas](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) em quaisquer links de replicação do site, depois de configurar a ligação Desktop Analytics no Gestor de Configuração, verá o seguinte erro em M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Para resolver este problema, desative os dados do site de inventário de **Hardware** para visualizações distribuídas em cada link de replicação do site.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>Consola fecha inesperadamente ao remover coleções

<!-- 4749443 -->
*Aplica-se a: Versão do Gestor de Configuração 1902 com rollup de atualização*

Depois de ligar o site ao [Desktop Analytics,](../../../../desktop-analytics/connect-configmgr.md)pode **selecionar coleções específicas para sincronizar com desktop Analytics**. Se remover uma coleção e aplicar as alterações, adicionar imediatamente uma nova coleção causa uma exceção não tratada. A consola fecha inesperadamente.

Para resolver este problema, quando remover uma coleção, selecione **OK** para fechar a janela de propriedades. Em seguida, abra novamente as propriedades para adicionar uma nova coleção no separador **Desktop Analytics Connection.**

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>O azulejo do estado do piloto mostra alguns dispositivos como "indefinidos"

<!-- 4547783 -->
*Aplica-se a: Versão do Gestor de Configuração 1902 com rollup de atualização*

Quando utiliza a consola Do Gestor de Configuração para monitorizar o estado de implementação do piloto, os dispositivos-piloto que estão atualizados na versão-alvo do Windows para esse plano de implementação mostram-se **indefinidos** no azulejo de estado do Piloto.  

Estes dispositivos **indefinidos** estão **atualizados** com a versão-alvo do Sistema operativo para esse plano de implementação. Não são necessárias mais ações.

## <a name="cloud-services"></a>Serviços em nuvem

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>Serviço azure para nuvem do Governo dos EUA mostra-se como nuvem pública

<!-- 6036748 -->

*Aplica-se à versão 1910*

Se criar uma ligação a um serviço Azure, e colocar o **ambiente Azure** na nuvem governamental, as propriedades da ligação mostram o ambiente como a nuvem pública de Azure. Este problema é apenas um problema de exibição na consola, o serviço está na nuvem do governo. Para confirmar a configuração, ecorra a seguinte consulta SQL na base de dados do site:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

Para a nuvem do governo, o resultado desta consulta é `2` para o inquilino específico.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Não é possível descarregar conteúdo de um portal de gestão de nuvem ativado para TLS 1.2

<!-- 5771680 -->

*Aplica-se à versão 1906, 1910 early update ring*

Se permitir que um portal de gestão de nuvem (CMG) funcione como um ponto de distribuição na **nuvem e sirva conteúdo do armazenamento Azure** e enforce **tLS 1.2,** poderá ver os downloads de conteúdos falharem.

Os seguintes erros mostram no DataTransferService.log no cliente:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Os seguintes erros mostram no CMGContentService.log no servidor:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Para contornar este problema:

- Atualize o site para a versão globalmente disponível de 1910, lançada a 20 de dezembro de 2019. (Se tiver atualizado previamente o anel de atualização inicial de 1910, precisa de atualizar para esta construção quando estiver disponível.)

- Em alternativa, utilize um ponto de distribuição tradicional de [nuvem.](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) Esta função não aplica tLS 1.2, mas é compatível com clientes que requerem TLS 1.2.

## <a name="protection"></a>Proteção

### <a name="bitlocker-management-appears-in-version-1906"></a>A gestão bitLocker aparece na versão 1906

*Aplica-se à versão 1906*

<!-- 5984688 -->

Depois de 21 de novembro de 2019, se atualizar para a versão 1906 a partir da versão 1902 ou mais cedo, a funcionalidade de gestão BitLocker será ligada e disponível. Esta funcionalidade é uma funcionalidade opcional a partir da versão 1910. Não é suportado na versão de 1906. Se tentar usá-lo na versão 1906, poderá experimentar resultados inesperados. Se não usar a funcionalidade, não há impacto.

Para utilizar a funcionalidade de [gestão BitLocker,](../../../../protect/plan-design/bitlocker-management.md)atualize para a versão 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
