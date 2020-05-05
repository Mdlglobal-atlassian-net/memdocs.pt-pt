---
title: Autenticação à base de token para CMG
titleSuffix: Configuration Manager
description: Registe um cliente na rede interna para obter um símbolo único ou crie um sinal de registo a granel para dispositivos baseados na Internet.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3a05c10d1f73fa0817febdd591190f6bc2ff0a0e
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587269"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticação baseada em token para gateway de gestão de nuvem

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--5686290-->

O gateway de gestão de nuvem (CMG) suporta muitos tipos de clientes, mas mesmo com [o Enhanced HTTP,](../../plan-design/hierarchy/enhanced-http.md)estes clientes requerem um certificado de [autenticação do cliente.](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway) Este requisito de certificado pode ser um desafio para a disponibilização de clientes baseados na Internet que muitas vezes não se conectam à rede interna, não são capazes de aderir ao Azure Ative Directory (Azure AD), e não têm um método para instalar um certificado emitido pelo PKI.

A partir da versão 2002, o Gestor de Configuração alarga o suporte do dispositivo com os seguintes métodos:

- Registe-se na rede interna para um símbolo único

- Criar um símbolo de registo a granel para dispositivos baseados na Internet

Para tirar o máximo partido desta funcionalidade, depois de atualizar o site, também atualize os clientes para a versão mais recente. O cenário completo não é funcional até que a versão do cliente seja também a mais recente. Se necessário, certifique-se de [promover a nova versão cliente à produção.](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)

O cliente do Gestor de Configuração juntamente com o ponto de gestão gerem este símbolo, por isso não há dependência da versão S. Esta funcionalidade está disponível para qualquer [versão ossia do cliente suportada.](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)

> [!NOTE]
> Estes métodos suportam apenas cenários de gestão centrados em dispositivos.
>
> A Microsoft recomenda a adesão de dispositivos à Azure AD. Os dispositivos baseados na Internet podem usar a AD Azure para autenticar com o Gestor de Configuração. Também permite tanto os cenários do dispositivo como do utilizador, quer o dispositivo esteja na internet ou ligado à rede interna. Para mais informações, consulte [Instalar e registar o cliente utilizando a identidade Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Registo na rede interna

Este método exige que o cliente se registe primeiro com o ponto de gestão da rede interna. O registo do cliente normalmente acontece logo após a instalação. O ponto de gestão dá ao cliente um símbolo único que mostra que está a usar um certificado auto-assinado. Quando o cliente vagueia pela internet, para comunicar com a CMG emparelha o seu certificado auto-assinado com o símbolo emitido por ponto de gestão. O cliente renova o símbolo uma vez por mês, e é válido por 90 dias.

O site permite este comportamento por defeito.

## <a name="create-a-bulk-registration-token"></a>Criar um símbolo de registo a granel

Se não conseguir instalar e registar clientes na rede interna, crie um sinal de registo a granel. Utilize este símbolo quando o cliente instala num dispositivo baseado na Internet e se registe através da CMG. O sinal de registo a granel tem um período de validade curta, e não está armazenado no cliente ou no site. Permite ao cliente gerar um símbolo único, que emparelhado com o seu certificado auto-assinado, permite autenticar com a CMG.

1. Inscreva-se no servidor de topo do site na hierarquia com privilégios de administrador local.

1. Abra uma linha de comandos como administrador.

1. Executar a ferramenta `\bin\X64` a partir da pasta do diretório `BulkRegistrationTokenTool.exe`de instalação do Gestor de Configuração no servidor do site: . Crie um novo `/new` símbolo com o parâmetro. Por exemplo, `BulkRegistrationTokenTool.exe /new`. Para mais informações, consulte o uso da [ferramenta token de registo a granel](#bulk-registration-token-tool-usage).

1. Copie o símbolo e guarde-o num local seguro.

1. Instale o cliente do Gestor de Configuração num dispositivo baseado na Internet. Incluir o parâmetro de instalação do cliente: [**/regtoken**](about-client-installation-properties.md#regtoken). A seguinte linha de comando exemplo inclui os outros parâmetros e propriedades de configuração necessários:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Para obter mais informações sobre esta linha de comando, consulte [Instalar e registar o cliente utilizando a identidade Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Este processo é semelhante, apenas não usa as propriedades da AD Azure.

### <a name="known-issues"></a>Problemas conhecidos

Não é possível criar um sinal de registo em massa num site que tenha um servidor de site em modo passivo.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Utilização da ferramenta simbólica de registo a granel

A `BulkRegistrationTokenTool.exe` ferramenta está `\bin\X64` na pasta do diretório de instalação do Gestor de Configuração no servidor do site. Inscreva-se no servidor do site e execute-o como administrador. Suporta os seguintes parâmetros de linha de comando:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Mostre esta informação de utilização.

Exemplo: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/novo

Crie um novo símbolo de registo a granel.

Exemplo: `BulkRegistrationTokenTool.exe /new`

A ferramenta apresenta as seguintes informações:
  
- Um GUID que o site usa para rastrear tokens emitidos
- O período de validade do símbolo, que é de três dias por defeito.
- O símbolo de registo a granel.

O símbolo não está guardado no cliente ou no site. Certifique-se de copiar o símbolo do pedido de comando e armazenar num local seguro.

#### <a name="lifetime"></a>/vida útil

Utilize `/new` com parâmetro para especificar o período de validade do símbolo. Especifique um valor inteiro em minutos. O valor predefinido é de 4.320 (três dias). O valor máximo é de 10.080 (sete dias).

Exemplo: `BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>Consulte também

- [Plano para o gateway de gestão de nuvem](../manage/cmg/plan-cloud-management-gateway.md)

- [Instalar e atribuir clientes do Gestor de Configuração do Windows 10 utilizando a AD Azure para autenticação](deploy-clients-cmg-azure.md)
