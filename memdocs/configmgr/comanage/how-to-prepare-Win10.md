---
title: Cogerir dispositivos baseados na Internet
titleSuffix: Configuration Manager
description: Saiba como preparar os seus dispositivos baseados na Internet do Windows 10 para cogestão.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 59ca1006d8700e52b3f3fb703f8896ce9fa8b9b7
ms.sourcegitcommit: 3ff33493c3f93bf06fdc942d30958a2a4ad03529
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82137920"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Como preparar dispositivos baseados na Internet para cogestão

Este artigo centra-se no segundo caminho para a cogestão, para novos dispositivos baseados na Internet. Este cenário é quando tem novos dispositivos Windows 10 que se juntam ao Azure AD e se inscrevem automaticamente no Intune. Instala o cliente do Gestor de Configuração para chegar a um estado de cogestão.  

## <a name="windows-autopilot"></a>Windows Autopilot

Para novos dispositivos Windows 10, pode utilizar o serviço Autopilot para configurar a experiência fora da caixa (OOBE). Este processo inclui a junção do dispositivo à AD Azure e a inscrição do dispositivo em Intune.  

Para mais informações, consulte a [visão geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).

Para configurar os seus dispositivos para serem automaticamente inscritos no Intune quando se juntarem ao Azure AD, consulte [os dispositivos DoWindows para](https://docs.microsoft.com/intune/windows-enroll)o Microsoft Intune .  

### <a name="gather-information-from-configuration-manager"></a>Recolher informações do Gestor de Configuração

Utilize o Gestor de Configuração para recolher e reportar as informações do dispositivo exigidas pela Intune. Estas informações incluem o número de série do dispositivo, identificador de produto Windows e um identificador de hardware. É usado para registar o dispositivo em Intune para suportar o Windows Autopilot.

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **de Monitorização,** expanda o nó **reporte,** expanda **relatórios**e selecione o **Hardware -** Nó Geral.  

2. Executar o relatório, **Windows Autopilot Device Information**, e ver os resultados.  

3. No visualizador do relatório, selecione o ícone **Export** e escolha a opção **CSV (vírposta-delimitada).**  

4. Depois de guardar o ficheiro, faça o upload dos dados para Intune.  

Para mais informações, consulte [Adicionar dispositivos em Intune](https://docs.microsoft.com/intune/enrollment-autopilot#add-devices).

### <a name="autopilot-for-existing-devices"></a>Piloto automático para dispositivos existentes
<!--1358333-->

[O Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível no Windows 10, versão 1809 ou posterior. Esta funcionalidade permite-lhe reimagem e fornecer um dispositivo Windows 7 para o [modo de utilização do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma única sequência de tarefas nativa do Gestor de Configuração.

Para obter mais informações, consulte o Windows Autopilot para obter a sequência de [tarefas dos dispositivos existentes](../osd/deploy-use/windows-autopilot-for-existing-devices.md).

## <a name="install-the-configuration-manager-client"></a>Instalar o cliente do Gestor de Configuração

Para dispositivos baseados na Internet no segundo caminho, você precisa criar uma aplicação em Intune. Implemente esta aplicação para dispositivos Windows 10 que ainda não são clientes do Gestor de Configuração.

> [!NOTE]
> Antes de atribuir esta aplicação a dispositivos em Intune, certifique-se de que os dispositivos confiam no certificado de autenticação do servidor CMG. Para mais informações, consulte [o certificado raiz fidedigno da CMG aos clientes.](../core/clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) Se um dispositivo não confiar no certificado de autenticação do servidor CMG, verá um erro WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA no ccmsetup.log no cliente.

### <a name="get-the-command-line-from-configuration-manager"></a>Obtenha a linha de comando do Gestor de Configuração

1. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud**e selecione o nó **de cogestão.**  

2. Selecione o objeto de cogestão e, em seguida, escolha **propriedades** na fita.  

3. No separador **Habilitação,** copie a linha de comando. Colá-lo no Bloco de Notas para economizar para o próximo processo.  

A seguinte linha de comando é um exemplo:`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC"`

<!--1358215-->
Decida quais as propriedades da linha de comando que necessita para o seu ambiente:  

- As seguintes propriedades da linha de comando são necessárias em todos os cenários:  
  - CCMHOSTNAME  
  - SMSSITECODE  

- São necessárias as seguintes propriedades ao utilizar a AD Azure para autenticação de clientes em vez de certificados de autenticação de clientes baseados em PKI:  
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

- Se o cliente voltar à intranet, é necessário o seguinte imóvel:  
  - SMSMP  

- Se utilizar o seu próprio certificado PKI, e o seu CRL não for publicado na internet, é necessário o seguinte parâmetro:  
  - /noCRLCheck  

    Para mais informações, consulte [Planeamento para CRLs](../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

- A partir da versão 2002, utilize a seguinte propriedade para iniciar uma sequência de tarefas imediatamente após o registo do cliente:
  - PROVISÕES

    Para mais informações, consulte sobre as propriedades de [instalação do cliente - PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts).

O site publica informações adicionais da Azure AD para o gateway de gestão de nuvem (CMG). Um cliente azure-joined ad obtém esta informação da CMG durante o processo ccmsetup, usando o mesmo inquilino ao qual se juntou. Este comportamento simplifica ainda mais os dispositivos de inscrição para a cogestão num ambiente com mais de um inquilino da AD Azure. As duas únicas propriedades ccmsetup necessárias são **CCMHOSTNAME** e **SMSSITECODE**.<!--3607731-->

> [!NOTE]
> Se já está a implementar o cliente do Gestor de Configuração a partir do Intune, atualize a aplicação Intune com uma nova linha de comando e um novo MSI. <!-- SCCMDocs-pr issue 3084 -->

O exemplo seguinte inclui todas estas propriedades:

`CCMSETUPCMD="CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSITECODE=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com PROVISIONTS=PRI20001"`

Para mais informações, consulte as propriedades de [instalação do Cliente.](../core/clients/deploy/about-client-installation-properties.md)

### <a name="create-the-app-in-intune"></a>Crie a app em Intune

1. Vá ao [portal Azure](https://portal.azure.com)e abra a página Intune.  

2. Selecione > **Aplicações** >  **de Clientes****Adicionar**.  

3. Em **Outros**, selecione **app Line-of-business**.  

4. Faça upload do ficheiro de pacote de **aplicativos ccmsetup.msi.** Encontre este ficheiro na seguinte pasta no `<ConfigMgr installation directory>\bin\i386`servidor do site do Gestor de Configuração: .  

    > [!Tip]  
    > Ao atualizar o site, certifique-se de que também atualiza esta aplicação em Intune.  

5. Depois de atualizada a aplicação, configure as informações da aplicação com a linha de comando que copiou do Gestor de Configuração.  

> [!IMPORTANT]
> Se personalizar esta linha de comando, certifique-se de que não tem mais de 1024 caracteres. Quando o comprimento da linha de comando é superior a 1024 caracteres, a instalação do cliente falha.
