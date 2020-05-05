---
title: Segurança e privacidade para atualizações de software
titleSuffix: Configuration Manager
description: Siga estas boas práticas de segurança para atualizações de software e saiba como o Gestor de Configuração lida com informações de privacidade.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5c7a1ac5e88aa669ae1d5e6bb9333e1f54fb5980
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724007"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Segurança e privacidade para atualizações de software no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém informações de segurança e privacidade para atualizações de software no Gestor de Configuração.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Procedimentos recomendados de segurança para atualizações de software  
 Utilize os seguintes procedimentos recomendados de segurança para implementar atualizações de software em clientes:  

-   Não altere as permissões predefinidas nos pacotes de atualização de software.  

     Por predefinição, os pacotes de atualização de software são configurados para permitir **Controlo Total** aos administradores e acesso de **Leitura** aos utilizadores. Se alterar estas permissões, poderá permitir que um intruso adicione, remova ou elimine as atualizações de software.  

-   Controle o acesso à localização de transferência de atualizações de software.  

     As contas de computador do Fornecedor de SMS, o servidor do site e o utilizador administrativo que efetivamente transferem atualizações de software para a localização de transferência necessitam de acesso de **Escrita** a essa mesma localização. Restrinja o acesso à localização de transferência para reduzir o risco de adulteração dos ficheiros de origem das atualizações de software por parte de intrusos.  

     Além disso, se utilizar uma partilha UNC na localização de transferência, proteja o canal de rede utilizando o IPsec ou a assinatura SMB para evitar a adulteração dos ficheiros de origem de atualizações de software quando forem transferidos através da rede.  

-   Utilize a UTC para avaliar a tempos de implementação.  

     Se utilizar a hora local em vez da UTC, os utilizadores poderão atrasar a instalação das atualizações de software alterando o fuso horário nos respetivos computadores  

-   Ative SSL no WSUS e siga os procedimentos recomendados para proteger o Windows Server Update Services (WSUS).  

     Identifique e siga as melhores práticas de segurança para a versão do WSUS que utiliza com o Gestor de Configuração.  

    > [!IMPORTANT]  
    >  Se configurar o ponto de atualização de software para ativar as comunicações SSL no servidor WSUS, tem de configurar as raízes virtuais para SSL no servidor WSUS.  

-   Ative a verificação CRL.  

     Por predefinição, o Gestor de Configuração não verifica a lista de revogação do certificado (CRL) para verificar a assinatura nas atualizações de software antes de serem implementadas nos computadores. A verificação da CRL sempre que é utilizado um certificado oferece mais segurança contra a utilização de um certificado revogado, mas provoca um atraso de ligação e implica um processamento adicional no computador que a está a efetuar.  

     Para obter mais informações sobre como permitir a verificação de CRL para atualizações de software, consulte como permitir a verificação de [CRL para atualizações](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates)de software .  

-   Configure o WSUS para utilizar um Web site personalizado.  

     Quando instala o WSUS no ponto de atualização de software, pode optar por utilizar o Web site predefinido do IIS existente ou por criar um Web site do WSUS personalizado. Crie um website personalizado para o WSUS para que o IIS aconselhe os serviços WSUS num site virtual dedicado em vez de partilhar o mesmo site que é usado pelos outros sistemas de site do Gestor de Configuração ou outras aplicações.  

     Para mais informações, consulte [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a>Informações de privacidade para atualizações de software  
 As atualizações de software analisam os computadores cliente para determinar que atualizações de software são necessárias e, em seguida, devolvem as informações à base de dados do site. Durante o processo de atualizações de software, o Gestor de Configuração pode transmitir informações entre clientes e servidores que identifiquem as contas de computador e logon.  

 O Gestor de Configuração mantém informações do Estado sobre o processo de implementação do software. As informações de estado não são encriptadas durante a transmissão ou o armazenamento. As informações do Estado são armazenadas na base de dados do Gestor de Configuração e são eliminadas pelas tarefas de manutenção da base de dados. Não são enviadas informações de estado à Microsoft.  

 A utilização de atualizações de software do Gestor de Configuração para instalar atualizações de software em computadores clientes pode estar sujeita a termos de licença de software para essas atualizações, que é separada dos Termos de Licença de Software para Gestor de Configuração. Reveja sempre e concorde com os Termos de Licenciamento de Software antes de instalar as atualizações do software utilizando o Gestor de Configuração.  

 O Gestor de Configuração não implementa atualizações de software por padrão e requer vários passos de configuração antes de a informação ser recolhida.  

 Antes de configurar as atualizações de software, considere os requisitos de privacidade.  
