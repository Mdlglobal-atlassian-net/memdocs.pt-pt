---
title: Ferramentas do Configuration Manager
titleSuffix: Configuration Manager
description: Aprenda sobre as ferramentas para ajudá-lo a gerir e resolver problemas a sua infraestrutura de Gestor de Configuração.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718568"
---
# <a name="configuration-manager-tools"></a>Ferramentas do Configuration Manager

*Aplica-se a: Gestor de Configuração (ramo atual)*

As ferramentas do Gestor de Configuração incluem ferramentas [baseadas no cliente](#client-tools) e [baseadas no servidor.](#server-tools) Utilize estas ferramentas para ajudar a suportar e resolver problemas na sua infraestrutura de Gestor de Configuração.

A partir da versão 1806 do Gestor de `CD.Latest\SMSSETUP\Tools` Configuração, estas ferramentas estão incluídas na pasta no servidor do site. Não é necessária mais nenhuma instalação.<!--1357145--> Utilize estas versões das ferramentas com a versão 1806 do Gestor de Configuração.

Todos os sistemas operativos Windows listados como clientes suportados em [sistemas operativos suportados para clientes e dispositivos](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportados para uso com estas ferramentas.

> [!Note]  
> O [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) ainda está disponível no Microsoft Download Center. Para configuração da versão 1806 e posterior, utilize as versões das ferramentas no CD. Última pasta no servidor do site. Algumas ferramentas estavam anteriormente no kit de ferramentas, mas não incluídas na versão 1806. Estas ferramentas antigas já não são apoiadas.


## <a name="client-tools"></a>Ferramentas de cliente

Estas ferramentas `ClientTools` estão na subpasta:

- [CMTrace](cmtrace.md): Visualizar, monitorizar e analisar ficheiros de registo do Gestor de Configuração  

- [Client Spy](clispy.md): Problemas relacionados com distribuição de software, inventário e medição

- [Ferramenta de monitorização](deployment-monitoring-tool.md)de implementação : Aplicações de resolução de problemas, atualizações e implementações de base  

- [Policy Spy](policy-spy.md): Ver atribuições políticas  

- [Ferramenta power viewer](power-viewer-tool.md): Ver estado da funcionalidade de gestão de energia  

- [Ferramenta de envio](send-schedule-tool.md)de horários : Horários de disparo e avaliações das linhas de base de configuração  

> [!Note]  
> A `ClientTools` pasta também inclui o ficheiro Microsoft.Diagnostics.Tracing.EventSource.dll. Várias ferramentas de cliente requerem esta biblioteca. Não pode usá-lo diretamente.  


## <a name="server-tools"></a>Ferramentas de servidor

Estas ferramentas `ServerTools` estão na subpasta:

- [DP Job Queue Manager](dp-job-manager.md): Troubleshoots empregos de distribuição de conteúdos para pontos de distribuição  

- [Avaliação de avaliação de recolha Espectador](ceviewer.md): Ver detalhes da avaliação da coleção  

- [Explorador de Biblioteca](content-library-explorer.md)de Conteúdos : Ver conteúdos da loja de instâncias únicas da biblioteca de conteúdos  

- [Transferência da Biblioteca de Conteúdos](content-library-transfer.md): Transfere biblioteca de conteúdos entre unidades  

- [Ferramenta de propriedade de conteúdo](content-ownership-tool.md): Altera a propriedade de pacotes órfãos. Estes pacotes existem no site sem um servidor de site próprio.

- [Ferramenta de Administração e Auditoria baseada em funções](rbaviewer.md): Ajuda administradores a auditar funções  

- Ferramenta de [sumreização do medidor](run-meter-summ.md)de execução : Executar tarefa de sumreização de medição e analisar dados de medição

> [!Note]  
> A pasta ServerTools também inclui os seguintes ficheiros:
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Várias ferramentas de servidor requerem estas bibliotecas. Não pode usá-los diretamente.  

## <a name="other-tools-and-toolkits"></a>Outras ferramentas e kits de ferramentas

- [Centro de Suporte](support-center.md): Recolha informações dos clientes para uma análise mais fácil ao resolver problemas.

    A partir da versão 1906, o **OneTrace** é um novo espectador de log com Support Center. Funciona da mesma forma com a CMTrace, com melhorias. Para mais informações, consulte [o Suporte Center OneTrace](support-center-onetrace.md).

- [Alargar e migrar o site no local para o Microsoft Azure](azure-migration-tool.md): Ajuda-o a criar programáticamente máquinas virtuais Azure (VMs) para O Gestor de Configuração. <!--3556022--> 

- [Ferramenta](../plan-design/hierarchy/content-library-cleanup-tool.md)de limpeza da biblioteca de conteúdos : `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` Utilize **contentLibraryCleanup.exe** para remover conteúdo órfão de um ponto de distribuição.  

- [Ferramenta](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)de Manutenção da Hierarquia : Utilize **preinst.exe** na pasta `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` partilhada no servidor do site para passar comandos para a componente do gestor da hierarquia.  

- Ferramenta de reset de [atualização](../servers/manage/update-reset-tool.md): `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` Utilize **CMUpdateReset.exe** para corrigir problemas quando as atualizações na consola tiverem problemas de descarregamento ou replicação.  

- [Ferramenta de ligação ao serviço](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md): `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` Utilize **serviceConnectionTool.exe** para manter o seu site atualizado quando o seu ponto de ligação de serviço estiver offline.   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md): Uma coleção de ferramentas, processos e orientação para automatizar implementações de desktop e servidor.

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md): Uma ferramenta autónoma para gerir e importar atualizações de software personalizadas.

- [Gestor de Conversão](../../apps/pcm/package-conversion-manager.md)de Pacotes : Converter pacotes legados em aplicações.
