---
title: Como gerir o Controlo de Aplicações do Windows Defender
titleSuffix: Configuration Manager
description: Aprenda a utilizar o Gestor de Configuração para gerir o Controlo de Aplicações do Windows Defender.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f9aff29d2773c4994272317d5fcd486b83cba8d7
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210184"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Gestão de controlo de aplicações do Windows Defender com Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

## <a name="introduction"></a>Introdução
O Windows Defender Application Control foi concebido para proteger os Computadores contra malware e outros softwares não confiáveis. Impede que o código malicioso seja executado garantindo que apenas o código aprovado, que sabe, pode ser executado.

O Windows Defender Application Control é uma camada de segurança baseada em software que aplica uma lista explícita de software que é permitida a ser executada num PC. Por si só, o Controlo de Aplicações não dispõe de quaisquer pré-requisitos de hardware ou firmware. As políticas de Controlo de Aplicações implementadas com o Gestor de Configuração permitem uma política em PCs em coleções direcionadas que satisfaçam os requisitos mínimos de versão windows e SKU descritos neste artigo. Opcionalmente, a proteção baseada em hipervisores das políticas de controlo de aplicações implementadas através do Gestor de Configuração pode ser ativada através da Política de Grupo em hardware capaz.

Para saber mais sobre o Controlo de Aplicações do Windows Defender, leia o guia de implementação do Controlo de [Aplicações do Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - Começando pelo Windows 10, versão 1709, as políticas de integridade do código configuráveis são conhecidas como Controlo de Aplicações do Windows Defender.
   > - Começando na versão 1710 do Gestor de Configuração, as políticas de Guarda de Dispositivos foram renomeadas para as políticas de Controlo de Aplicações do Windows Defender.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Utilização do Controlo de Aplicações do Windows Defender com Gestor de Configuração

Pode utilizar o Gestor de Configuração para implementar uma política de controlo de aplicações do Windows Defender. Esta política permite configurar o modo em que o Windows Defender Application Control é executado em PCs numa coleção. 

Pode configurar um dos seguintes modos:

1. **Aplicação ativada** - Só podem correr executáveis fidedignos.
2. **Auditoria apenas** - Permita que todos os executáveis executem, mas faça log executables não confiáveis que executem no registo de eventos de cliente local.

> [!Tip]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1702 como [uma funcionalidade de pré-lançamento.](../../core/servers/manage/pre-release-features.md) Começando com a versão 1906, já não é uma funcionalidade de pré-lançamento.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>O que pode ser executado quando implementa uma política de Controlo de Aplicações do Windows Defender?

O Windows Defender Application Control permite controlar fortemente o que pode ser executado em PCs que gere. Esta funcionalidade pode ser útil para computadores em departamentos de alta segurança, onde é vital que o software indesejado não possa ser executado.

Quando implementa uma política, normalmente, os seguintes executáveis podem executar:

- Componentes do sistema operativo Windows
- Controladores do Hardware Dev Center (que têm assinaturas de Laboratórios de Qualidade de Hardware do Windows)
- Aplicativos windows store
- O cliente do Gestor de Configuração 
- Todo o software implementado através do Configuracion Manager que os PCs instalam após a política de Controlo de Aplicações do Windows Defender ser processada. 
- Atualizações aos componentes do Windows a partir de:
    - Windows Update
    - Windows Update para Empresas
    - Windows Server Update Services
    - Gestor de configuração
    - Opcionalmente, software com uma boa reputação determinada pelo Microsoft Intelligent Security Graph (ISG). O ISG inclui o Windows Defender SmartScreen e outros serviços da Microsoft. O dispositivo deve estar a executar o Windows Defender SmartScreen e a versão 1709 do Windows 10 ou mais tarde para que este software seja de confiança.

>[!IMPORTANT]
>Estes itens não incluem qualquer software que *não* esteja integrado no Windows que atualize automaticamente a partir de atualizações de software de internet ou de terceiros, quer sejam instalados através de algum dos mecanismos de atualização mencionados anteriormente, ou da internet. Apenas alterações de software que são implementadas embora o cliente do Gestor de Configuração possa executar.

## <a name="before-you-start"></a>Antes de começar

Antes de configurar ou implementar as políticas de Controlo de Aplicações do Windows Defender, leia as seguintes informações:

- A gestão do Controlo de Aplicações do Windows Defender é uma funcionalidade de pré-lançamento para O Gestor de Configuração, e está sujeita a alterações.
- Para utilizar o Controlo de Aplicações do Windows Defender com o Gestor de Configuração, os PCs que gere devem estar a executar a versão 1703 do Windows 10 Enterprise, ou mais tarde.
- Uma vez que uma apólice é processada com sucesso num PC cliente, o Gestor de Configuração é configurado como um Instalador Gerido nesse cliente. O software implementado através dele, após os processos de política, é automaticamente fidedigno. O software instalado pelo Gestor de Configuração antes dos processos de controlo de aplicações do Windows Defender não é automaticamente fidedigno.
- O calendário de avaliação de conformidade predefinido para as políticas de Controlo de Aplicações, configurável durante a implementação, é todos os dias. Se forem observadas questões no processamento de políticas, pode ser benéfico configurar o calendário de avaliação de conformidade para ser mais curto, por exemplo, a cada hora. Este calendário dita a frequência com que os clientes tentam processar uma política de Controlo de Aplicações do Windows Defender se ocorrer uma falha.
- Independentemente do modo de execução que selecione, quando implementa uma política de Controlo de Aplicações do Windows Defender, os Computadores do Cliente não podem executar aplicações HTML com a extensão .hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Como criar uma política de controlo de aplicações do Windows Defender
1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. No espaço de trabalho **de Ativos e Compliance,** expanda a **Proteção do Ponto Final**e, em seguida, clique no Controlo de **Aplicações do Windows Defender**.
3. No separador **Home,** no grupo **Criar,** clique em Criar a política de Controlo de **Aplicações**.
4. Na página **geral** do Assistente de Política de Controlo de **Aplicações ,** especifique as seguintes definições:
    - **Nome** - Introduza um nome único para esta política de Controlo de Aplicações do Windows Defender. 
    - **Descrição** - Opcionalmente, introduza uma descrição para a política que o ajuda a identificá-la na consola 'Gestor de Configuração'.
    - **Impor um reinício de dispositivos para que esta política possa ser aplicada para todos os processos** - Depois de a apólice ser processada num PC cliente, está agendado um reinício no cliente de acordo com as **Definições** do Cliente para reiniciar o **computador**.
        - Os dispositivos que executam o Windows 10 versão 1703 ou mais cedo serão sempre reiniciados automaticamente.
        - A partir da versão 1709 do Windows 10, as aplicações atualmente em funcionamento no dispositivo só terão a nova política de Controlo de Aplicações aplicada após o reinício. No entanto, as candidaturas lançadas após a aplicação da política irão honrar a nova política de Controlo de Aplicações. 
    - **Modo de execução** - Escolha um dos seguintes métodos de aplicação para o Windows Defender Application Control no PC cliente.
        - **Enforcement Enabled** - Só permite que executáveis fidedignos possam ser executados.
        - **Auditoria Apenas** - Permita que todos os executáveis executem, mas faça log executables não confiáveis que executem no registo de eventos de cliente local.
5. No separador **Inclusão si** do Assistente de Política de Controlo de **Aplicações Create,** escolha se pretende **autorizar software fidedigno pelo Gráfico**de Segurança Inteligente .
6. Clique em **Adicionar** se quiser adicionar confiança a ficheiros ou pastas específicos em PCs. Na caixa de diálogo **'Ficheiro fidedigno' ou de pasta Adicionar,** pode especificar um ficheiro local ou um caminho de pasta para confiar. Também pode especificar um ficheiro ou um caminho de pasta num dispositivo remoto no qual tem permissão para se ligar. Quando adicionar confiança para ficheiros ou pastas específicos numa política de Controlo de Aplicações do Windows Defender, pode:
    - Superar problemas com comportamentos instaladores geridos
    - Aplicativos de linha de negócio sintetizados que não podem ser implementados com O Gestor de Configuração
    - Confie em aplicativos que estão incluídos numa imagem de implementação do sistema operativo. 
8. Clique **em Seguir,** para completar o assistente.

>[!IMPORTANT]
>A inclusão de ficheiros ou pastas fidedignos só é suportada nos Computadores de clientes que executam a versão 1706 ou posteriordo do cliente do Gestor de Configuração. Se quaisquer regras de inclusão forem incluídas numa política de Controlo de Aplicações do Windows Defender e a apólice for então implementada para um PC cliente que executa uma versão anterior no cliente Do Gestor de Configuração, a apólice não será aplicada. A atualização destes clientes mais velhos resolverá este problema. As políticas que não incluam quaisquer regras de inclusão podem ainda ser aplicadas em versões mais antigas do cliente do Gestor de Configuração.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Como implementar uma política de controlo de aplicações do Windows Defender
1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. No espaço de trabalho **de Ativos e Compliance,** expanda a **Proteção do Ponto Final**e, em seguida, clique no Controlo de **Aplicações do Windows Defender**.
3. A partir da lista de políticas, selecione a que pretende implementar e, em seguida, no separador **Home,** no grupo **Deimplantação,** clique em Implementar a Política de Controlo de **Aplicações**.
4. Na caixa de diálogo de controlo de aplicações de **implementação,** selecione a recolha para a qual pretende implementar a política. Em seguida, configure um horário para quando os clientes avaliarem a apólice. Por fim, selecione se o cliente pode avaliar a apólice fora de quaisquer janelas de manutenção configuradas.
5. Quando terminar, clique em **OK** para implementar a política. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Como monitorizar uma política de controlo de aplicações do Windows Defender

Utilize as informações no artigo de [definições](../../compliance/deploy-use/monitor-compliance-settings.md) de conformidade do Monitor para ajudá-lo a monitorizar que a política implementada foi aplicada corretamente a todos os Computadores.

Para monitorizar o processamento de uma política de Controlo de Aplicações do Windows Defender, utilize o seguinte ficheiro de registo nos Computadores do Cliente:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para verificar se o software específico está bloqueado ou auditado, consulte os seguintes registos de eventos de clientes locais:

1. Para bloquear e auditar ficheiros executáveis, utilize **aplicações e registos** > de registos**microsoft** > **Windows** > **Code Integrity** > **Operacional**.
2. Para bloquear e auditar ficheiros do Instalador e script do Windows, utilize **aplicações e registos** > de registos**Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Informações de segurança e privacidade para o Windows Defender Application Control

- Nesta versão de pré-lançamento, não implemente políticas de Controlo de Aplicações do Windows Defender com o modo de execução **Audit apenas** num ambiente de produção. Este modo destina-se a ajudá-lo a testar a capacidade apenas numa configuração de laboratório.
- Os dispositivos que tenham uma política implantada **apenas** no modo Audit Ou **Enforcement Enabled** que não tenham sido reiniciados para fazer cumprir a política, são vulneráveis à instalação de software não confiável.
Nesta situação, o software pode continuar a ser autorizado a funcionar mesmo que o dispositivo reinicie, ou receba uma política no modo Ativado pela **Aplicação.**
- Para garantir que a política de Controlo de Aplicações do Windows Defender é eficaz, prepare o dispositivo num ambiente de laboratório. Em seguida, implemente a política Ativada pela **Execução** e, finalmente, reinicie o dispositivo antes de dar o dispositivo a um utilizador final.
- Não implemente uma política com a **Enforcement Enabled**, e depois implemente uma política com **auditoria apenas** para o mesmo dispositivo. Esta configuração pode resultar na permissão de software não confiável.
- Quando utiliza o Gestor de Configuração para ativar o Controlo de Aplicações do Windows Defender em Computadores de Cliente, a política não impede que os utilizadores com direitos de administrador local contornem as políticas de Controlo de Aplicações ou executem software não confiável. 
- A única forma de evitar que os utilizadores com direitos de administrador local desacionem o Controlo de Aplicações é implementar uma política binária assinada. Esta implementação é possível através da Política de Grupo, mas não atualmente suportada no Gestor de Configuração.
- Configurar o Gestor de Configuração como instalador gerido em Computadores de cliente utiliza a política AppLocker. O AppLocker só é utilizado para identificar instaladores geridos e toda a aplicação acontece com o Controlo de Aplicações do Windows Defender. 

## <a name="next-steps"></a>Passos seguintes

 [Gerir políticas antimalware e definições de firewall](endpoint-antimalware-firewall.md)



