---
title: Autenticação baseada em token para CMG
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
ms.openlocfilehash: c6b33027d67329b883f401168795c1b466ded1a7
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709401"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Autenticação baseada em token para gateway de gestão de nuvem

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--5686290-->

O gateway de gestão de nuvem (CMG) suporta muitos tipos de clientes, mas mesmo com [o Enhanced HTTP,](../../plan-design/hierarchy/enhanced-http.md)estes clientes requerem um certificado de [autenticação do cliente.](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway) Este requisito de certificado pode ser um desafio para a disponibilização de clientes baseados na Internet que muitas vezes não se conectam à rede interna, não são capazes de aderir ao Azure Ative Directory (Azure AD), e não têm um método para instalar um certificado emitido pelo PKI.

Para superar estes desafios, a partir da versão 2002, o Configuração Manager alarga o suporte do seu dispositivo com os seguintes métodos:

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

1. Executar a ferramenta a partir `\bin\X64` da pasta do diretório de instalação do Gestor de Configuração no servidor do site: `BulkRegistrationTokenTool.exe` . Crie um novo símbolo com o `/new` parâmetro. Por exemplo, `BulkRegistrationTokenTool.exe /new`. Para mais informações, consulte o uso da [ferramenta token de registo a granel](#bulk-registration-token-tool-usage).

1. Copie o símbolo e guarde-o num local seguro.

1. Instale o cliente do Gestor de Configuração num dispositivo baseado na Internet. Incluir o parâmetro de instalação do cliente: [**/regtoken**](about-client-installation-properties.md#regtoken). A seguinte linha de comando exemplo inclui os outros parâmetros e propriedades de configuração necessários:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Para obter mais informações sobre esta linha de comando, consulte [Instalar e registar o cliente utilizando a identidade Azure AD](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Este processo é semelhante, apenas não usa as propriedades da AD Azure.

### <a name="known-issues"></a>Problemas conhecidos

Não é possível criar um sinal de registo em massa num site que tenha um servidor de site em modo passivo.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Utilização da ferramenta simbólica de registo a granel

A `BulkRegistrationTokenTool.exe` ferramenta está na pasta do `\bin\X64` diretório de instalação do Gestor de Configuração no servidor do site. Inscreva-se no servidor do site e execute-o como administrador. Suporta os seguintes parâmetros de linha de comando:

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

Utilize com `/new` parâmetro para especificar o período de validade do símbolo. Especifique um valor inteiro em minutos. O valor predefinido é de 4.320 (três dias). O valor máximo é de 10.080 (sete dias).

Exemplo: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Gestão simbólica de registo a granel

Pode ver fichas de registo a granel previamente criadas e suas vidas na consola Do Gestor de Configuração e bloquear o seu uso se necessário. A base de dados do site, no entanto, não armazena fichas de registo a granel.

#### <a name="to-review-a-bulk-registration-token"></a>Para rever um símbolo de registo a granel

1. Na consola do Configuration Manager, clique em **Administração**.

2. No espaço de trabalho da Administração, expandir **segurança,** clicar **em Certificados.** A consola lista todos os certificados relacionados com o site e fichas de registo a granel no painel de detalhes.

3. Selecione o símbolo de registo a granel para rever.

Pode identificar fichas específicas de registo a granel com base no seu GUID. Os GUIDs para fichas de registo a granel são apresentados no tempo de criação do símbolo. Também pode filtrar ou classificar na coluna **Tipo,** se necessário.

#### <a name="to-block-a-bulk-registration-token"></a>Para bloquear um sinal de registo a granel

1. Na consola do Configuration Manager, clique em **Administração**.

2. No espaço de trabalho da Administração, expandir **Segurança,** clicar **em Certificados,** e selecionar o símbolo de registo a granel para bloquear.

3. No separador **Home** da barra de fita ou no menu de conteúdo do clique direito, selecione **Bloquear**. Inversamente, pode desbloquear fichas de registo a granel previamente bloqueadas selecionando **Desbloquear** o separador **Home** da barra de fita ou o menu de conteúdo do clique direito.

## <a name="see-also"></a>Consulte também

- [Plano para o gateway de gestão de nuvem](../manage/cmg/plan-cloud-management-gateway.md)

- [Instalar e atribuir clientes do Gestor de Configuração do Windows 10 utilizando a AD Azure para autenticação](deploy-clients-cmg-azure.md)
