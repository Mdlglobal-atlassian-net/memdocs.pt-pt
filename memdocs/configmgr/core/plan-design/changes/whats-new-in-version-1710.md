---
title: Nova versão 1710 / Microsoft Docs
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas capacidades introduzidas na versão 1710 do Gestor de Configuração.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073624"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>O que&#39;novo na versão 1710 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A atualização 1710 para o espaço atual do Gestor de Configuração está disponível como uma atualização na consola para sites previamente instalados que executam a versão 1610, 1702 ou 1706.

Além de novas funcionalidades, esta versão também inclui alterações adicionais, tais como correções de bugs. Para mais informações, consulte [resumo das alterações no atual ramo do Gestor de Configuração, versão 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

As seguintes atualizações adicionais para esta versão também estão disponíveis:
- [Rollup de atualização para o ramo atual do Gestor de Configuração, versão 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Atualização rollup 2 para configuração manager atual ramo, versão 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de base do 'Gestor de Configuração'.  
>
> Saiba mais sobre:    
> - [Instalação de novos sites](../../servers/deploy/install/installing-sites.md)  
> - [Instalação de atualizações nos sites](../../servers/manage/updates.md)  
> - [Versões de base e atualização](../../servers/manage/updates.md#bkmk_Baselines)

As seguintes secções fornecem detalhes sobre alterações e novas capacidades introduzidas na versão 1710 do Gestor de Configuração.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do local

### <a name="updates-for-peer-cache-----sms500850---"></a>Atualizações para Peer Cache  <!-- sms500850 -->
A partir deste lançamento, peer Cache já não é uma funcionalidade de pré-lançamento.  Não são introduzidas outras alterações para o Peer Cache com esta versão. Para mais informações, consulte [peer cache para clientes do Gestor de Configuração](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Suporte de ponto de distribuição em nuvem para nuvem do governo de Azure   <!-- sms491428 -->
Agora pode usar [pontos de distribuição baseados em nuvem](../hierarchy/use-a-cloud-based-distribution-point.md) na nuvem do Governo de Azure.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisão da unidade de padrão de inventário <!-- sms503697 -->
Como os dispositivos agora incluem discos rígidos com tamanhos no gigabyte (GB), terabyte (TB) e escalas maiores, esta libertação altera a unidade padrão (SMS_Units) usada em muitas vistas de megabytes (MB) a GB. Por exemplo, o valor v_gs_LogicalDisk.FreeSpace reporta agora unidades GB.


<!-- ## Migration  -->


## <a name="client-management"></a>Gestão de clientes

### <a name="co-management-for-windows-10-devices"></a>Cogestão para os dispositivos com Windows 10    
<!-- 1350871 -->
Nas atualizações anteriores do Windows 10, já pode juntar-se a um dispositivo Windows 10 para o Ative Directory (AD) e o Azure AD baseado na nuvem ao mesmo tempo (AD Azure híbrido). Começando com os dispositivos 1710 do Gestor de Configuração, a cogestão aproveita esta melhoria e permite-lhe gerir simultaneamente os dispositivos do Windows 10, versão 1709 (também conhecido como Atualização de Criadores de outono) utilizando tanto o Gestor de Configuração como o Intune. É uma solução que fornece uma ponte da gestão tradicional à gestão moderna e lhe dá um caminho para fazer a transição usando uma abordagem faseada. Para mais detalhes, consulte [a Co-management para dispositivos Windows 10](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Reiniciar computadores a partir da consola 'Gestor de Configuração'  <!-- 1356283 -->
A partir desta versão, pode utilizar a consola 'Gestor de Configuração' para identificar dispositivos clientes que requerem um reinício e, em seguida, utilizar uma ação de notificação do cliente para os reiniciar.

Ver [Como gerir clientes](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Gestão de Aplicações
### <a name="improvements-for-run-scripts------1236459---"></a>Melhorias para Scripts de Execução   <!-- 1236459 -->
Esta versão traz várias melhorias na funcionalidade **Executar Scripts,** que permite implementar scripts PowerShell para executar em dispositivos geridos. Esta funcionalidade foi introduzida pela primeira vez na versão 1706.

As melhorias incluem:
- Utilize os Âmbitos de Segurança para ajudar a controlar quem pode usar scripts de execução
- Monitorização em tempo real dos scripts que executa
- Os parâmetros para o ecrã do script no Create Script Wizard, validação de suporte, e são identificados como obrigatórios ou opcionais.

Para mais informações sobre a utilização de Scripts run, consulte [Criar e executar scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Novas definições de política de gestão de aplicações móveis
<!-- 1324760 -->
Foram adicionadas as seguintes definições às definições da política de gestão de aplicações móveis:
- **Desative**a sincronização de contacto : Impede que a aplicação guarde dados para a aplicação Contactos nativos no dispositivo.
- **Impressão desativação**: Impede que a aplicação de impressão de trabalhoou dados escolares.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center já não distorce ícones maiores do que 250x250  
<!-- 1356194 -->

Com esta versão, o Software Center deixará de distorcer ícones que sejam maiores do que 250x250. O Centro de Software fez com que tais ícones parecessem desfocados. Agora pode definir um ícone com dimensões de pixel até 512x512, e exibe sem distorção.

Para adicionar um ícone para a sua aplicação no Software Center, consulte [Criar aplicações.](../../../apps/deploy-use/create-applications.md)

## <a name="operating-system-deployment"></a>Implementação do sistema operativo
 > [!TIP]   
 > <!-- 1354281 -->
 > A partir do lançamento do Windows 10, versão 1709 (também conhecida como Atualização de Criadores de outono), os meios de comunicação windows incluem várias edições. Ao configurar uma sequência de tarefas para utilizar um pacote de atualização do sistema operativo ou imagem do sistema operativo, certifique-se de selecionar uma [edição que seja suportada para utilização pelo Select Manager](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Adicione sequências de tarefas infantis a uma sequência de tarefas
<!-- 1261338 -->

Pode adicionar um novo passo de sequência de tarefas que executa outra sequência de tarefas, que cria uma relação pai/filho entre as sequências de tarefas. Isto permite-lhe criar mais sequências de tarefas modulares que pode reutilizar.  

Para saber mais sobre a sequência de tarefas da criança, consulte a sequência de [tarefas da criança](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Personalização do Centro de Software
<!-- 1351224 -->
Pode adicionar elementos de marca empresarial e especificar a visibilidade dos separadores no Software Center. Pode adicionar o nome específico da empresa do Software Center, definir um tema de cores de configuração do Software Center, definir um logotipo da empresa e definir os separadores visíveis para dispositivos clientes.

Para mais informações, consulte Plan para e configure a gestão de [aplicações.](../../../apps/plan-design/plan-for-and-configure-application-management.md)

## <a name="software-updates"></a>Atualizações de software

### <a name="surface-driver-updates-----1098490---"></a>Atualizações do condutor de superfície  <!-- 1098490 -->
A partir desta versão, gerir as atualizações do controlador surface já não é uma funcionalidade de pré-lançamento.  


## <a name="reporting"></a>Relatórios

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limite os dados melhorados do Windows 10 para apenas enviar dados relevantes para a Saúde do Dispositivo Windows Analytics
<!-- 1356148 -->

Agora pode definir o nível de recolha de dados de diagnóstico do Windows 10 para **Enhanced (Limited)**. Esta definição permite-lhe obter informações acionáveis sobre dispositivos no seu ambiente sem que os dispositivos reportem todos os dados ao nível **do Enhanced** com a versão 1709 do Windows 10 ou mais tarde.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gestão de dispositivos móveis

### <a name="actions-for-non-compliance"></a>Ações de não conformidade 
<!--1321366 -->    
Agora pode configurar uma sequência de ações ordenadas pelo tempo que são aplicadas a dispositivos que não cumprem o cumprimento. Por exemplo, pode notificar os utilizadores de dispositivos não conformes por e-mail ou marcar esses dispositivos sem conformidade.

### <a name="windows-10-arm64-device-support"></a>Suporte ao dispositivo ARM64 do Windows 10
<!-- 1355000 -->

Os cenários de gestão de dispositivos móveis híbridos (MDM) serão suportados em dispositivos ARM64 que executam o Windows 10 quando estes dispositivos estiverem disponíveis.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Experiência melhorada de perfil VPN na consola de gestor de configuração 
<!-- 1318232 -->

Com esta versão, atualizámos o assistente de perfil VPN e as páginas de propriedades para exibir as definições apropriadas para a plataforma selecionada:


- Cada plataforma tem o seu próprio fluxo de trabalho, o que significa que os novos perfis VPN contêm apenas a definição suportada pela plataforma.
- A página **Plataformas Suportadas** aparece agora após a página **Geral.**  Agora escolhe a plataforma antes de definir os valores de propriedade.
- Quando a plataforma está definida para **Android**, **Android for Work**, ou Windows Phone **8.1**, a página de **plataformas suportadas** não é necessária e não é exibida.
- O fluxo de trabalho baseado no cliente do Gestor de Configuração foi combinado com os fluxos de trabalho do Dispositivo Móvel Híbrido (MDM) baseados no cliente do Windows 10; suportam as mesmas configurações.
- Cada fluxo de trabalho da plataforma inclui apenas as definições adequadas para esse fluxo de trabalho.  Por exemplo, o fluxo de trabalho Android contém configurações adequadas para Android; As definições adequadas para iOS ou Windows 10 Mobile já não aparecem no fluxo de trabalho Android.
- A página VPN automática é obsoleta e foi removida.

Estas alterações aplicam-se aos novos perfis VPN.  

Para minimizar o risco de compatibilidade, os perfis VPN existentes são inalterados.  Quando edita um perfil existente, as definições aparecem como quando o perfil foi criado.  

Para mais informações, consulte [perfis VPN em dispositivos móveis](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Suporte limitado à Criptografia: Certificados de próxima geração (GNC) <!-- 1356191 -->

O Gestor de Configuração tem suporte limitado para os certificados de Criptografia: Certificados de Próxima Geração (CNG). Os clientes do Gestor de Configuração podem utilizar o certificado de autenticação do cliente PKI com chave privada no Fornecedor de Armazenamento de Chaves CNG (KSP). Com suporte kSP, os clientes do Gestor de Configuração suportam a chave privada baseada em hardware, como tPM KSP para certificados de autenticação de clientes PKI.

Para mais informações, consulte a visão geral dos [certificados de CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteger dispositivos

### <a name="create-and-deploy-exploit-guard-policies"></a>Criar e implementar políticas da Guarda de Exploração
<!-- 1355468 -->

Pode [criar e implementar políticas](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) que gerem os quatro componentes do Windows Defender Exploit Guard, incluindo a redução de superfície de ataque, acesso controlado a pastas, proteção de exploração e proteção de rede.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Criar e implementar a política de guarda de aplicações do Windows Defender
<!-- 1351960 -->

Pode [criar e implementar as políticas](../../../protect/deploy-use/create-deploy-application-guard-policy.md) de Proteção de Aplicações do Windows Defender utilizando a proteção do ponto final do Gestor de Configuração.

### <a name="device-guard-policy-changes"></a>Alterações na política da Guarda de Dispositivos
<!-- 1355092 -->
Foram feitas as três alterações que se seguiram em relação às políticas da Guarda de Dispositivos:

- As políticas de Guarda de Dispositivos foram renomeadas para as políticas de Controlo de Aplicações do Windows Defender. Assim, por exemplo, o assistente de **política Create Device Guard** é agora nomeado assistente de política de controlo de **aplicações do Windows Defender**.
- Os dispositivos que utilizam a Atualização dos Criadores de outono para a versão 1709 do Windows não necessitam de um reinício para aplicar as políticas de Controlo de Aplicações do Windows Defender. Reiniciar ainda é o padrão, mas pode [desligar os reinícios](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- Pode [definir dispositivos para executar automaticamente software](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) fidedigno pelo Gráfico de Segurança Inteligente.





## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [Atualizações para 'Gestor](../../servers/manage/updates.md)de Configuração'.
