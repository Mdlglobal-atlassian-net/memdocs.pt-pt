---
title: Create a lab in Azure (Criar um laboratório no Azure)
titleSuffix: Configuration Manager
description: Automatizar a criação de um laboratório de pré-visualização técnica do Gestor de Configuração ou de um laboratório de avaliação de ramo atual utilizando modelos Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 23cc7d0c642637a310f53280bafed6a2a28d2834
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406675"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Criar um laboratório de Gestor de Configuração em Azure

*Aplica-se a: Gestor de Configuração (ramo atual, ramo de pré-visualização técnica)*

<!--3556017-->

Este guia descreve como construir um ambiente de laboratório do Gestor de Configuração no Microsoft Azure. Utiliza modelos Azure para simplificar e automatizar a criação de um laboratório utilizando recursos Azure. São fornecidos dois modelos Azure: 

- Configuração Manager modelo de pré-visualização técnica Azure instala a versão mais recente do ramo de pré-visualização técnica do Gestor de Configuração.
- Configuração Manager atual ramo de ramo De modelo Azure instala a avaliação da versão mais recente do ramo atual do Gestor de Configuração. 

Para mais informações, consulte [O Gestor de Configuração no Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Pré-requisitos

Este processo requer uma subscrição Azure na qual pode criar os seguintes objetos: 
- Duas Standard_B2s máquinas virtuais para controlador de domínio, ponto de gestão e ponto de distribuição.
- Uma Standard_B2ms máquina virtual para o servidor principal do site e o servidor de base de dados SQL.
- conta de armazenamento Standard_LRS

> [!Tip]  
> Para ajudar a determinar os custos potenciais, consulte a calculadora de [preços Azure](https://azure.microsoft.com/pricing/calculator/).  



## <a name="process"></a>Processo

1. Vá ao modelo de [pré-visualização técnica do Gestor](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) de Configuração ou ao modelo de [ramo atual do Gestor](https://azure.microsoft.com/resources/templates/sccm-currentbranch/)de Configuração .  

2. Selecione **Deploy para Azure,** que abre o portal Azure.  

3. Complete o modelo de quickstart Azure com as seguintes informações:

    - Noções básicas  

        - **Subscrição**: O nome da subscrição para criar os VMs  

        - **Grupo de recursos**: Selecione um grupo de recursos para usar para estes VMs  

        - **Localização**: Selecione um centro de dados Azure para acolher este ambiente de laboratório  

    - Definições  

        - **Prefixo**: O nome prefixo das máquinas. Para mais informações, consulte [a infom A. Azure.](#azure-vm-info)  

        - **Nome de utilizador :** O nome de um utilizador nas VMs com direitos administrativos. Usa este utilizador para iniciar sessão nos VMs.  

        - **Palavra-passe do Administrador**: A palavra-passe deve satisfazer os requisitos de complexidade do Azure. Para mais informações, consulte [o administradorPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > As seguintes definições são exigidas pelo Azure. Utilize os valores predefinidos. Não mude estes valores.  
    > 
    > - Localização dos ** \_ artefactos**: A localização dos scripts para este modelo <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - ** \_ Artefactos Localização Sas Token**: O sasToken é necessário para aceder à localização dos artefactos  
    > 
    > - **Localização**: A localização de todos os recursos

4. Leia os termos e condições. Se concordar, selecione **concordo com os termos e condições acima indicados**. Em seguida, selecione **Comprar** para continuar. 

O Azure valida as definições e inicia a implementação. Verifique o estado da implantação no portal Azure. 

> [!NOTE]
> O processo pode demorar 2 a 4 horas. Mesmo quando o portal Azure mostra uma implementação bem sucedida, os scripts de configuração continuam a ser executados. Não reinicie os VMs durante o processo.

Para ver o estado dos scripts de configuração, ligue-se ao `<prefix>PS1` servidor e veja o seguinte ficheiro: `%windir%\TEMP\ProvisionScript\PS1.json` . Se mostrar todos os passos como completos, o processo está concluído.

Para ligar aos VMs, obtenha primeiro do portal Azure os endereços IP públicos para cada VM. Quando se liga ao VM, o nome de domínio é `contoso.com` . Utilize as credenciais que especificou no modelo de implantação. Para mais informações, consulte [Como ligar e iniciar sessão numa máquina virtual Azure que executa o Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informação azure VM

Os Três VMs têm as seguintes especificações:
- 150 GB de espaço em disco
- Um endereço IP público e privado. Os IPs públicos estão num grupo de segurança de rede que só permite ligações remotas de ambiente de trabalho na porta TCP 3389. 

O prefixo que especificou no modelo de implementação é o prefixo de nome VM. Por exemplo, se definir "contoso" como prefixo, então o nome da máquina do controlador de domínio é `contosoDC` .


### `<prefix>DC01`

- Controlador de domínio do Active Directory
- Standard_B2s, que tem dois processadores e 4 GB de memória
- Edição do Windows Server 2019 Datacenter

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- Serviços de Domínio de Diretório Ativo (ADDS)
- .NET
- Compressão diferencial remota (RDC)


### `<prefix>PS01`

- Standard_B2ms, que tem dois processadores e 8 GB de memória
- Edição do Datacenter do Windows Server 2016
- SQL Server
- Windows 10 ADK com Windows PE 
- Site primário do Gestor de Configuração

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- .NET
- Compressão diferencial remota (RDC) 
- Serviço de Informação na Internet (IIS)


### `<prefix>DPMP01`

- Standard_B2s, que tem dois processadores e 4 GB de memória
- Edição do Windows Server 2019 Datacenter
- Ponto de distribuição
- Ponto de gestão

#### <a name="windows-features-and-roles"></a>Funcionalidades e funções do Windows
- .NET
- Compressão diferencial remota (RDC) 
- Serviço de Informação na Internet (IIS)
- Serviço de transferência inteligente de fundo (BITS)

### `<prefix>CL01`

- Apenas para o modelo de avaliação do ramo atual do Gestor de Configuração
- Windows 10
- Cliente do Gestor de Configuração
