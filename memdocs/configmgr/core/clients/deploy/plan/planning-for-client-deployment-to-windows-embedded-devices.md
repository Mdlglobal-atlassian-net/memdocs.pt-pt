---
title: Planejar a implementação de clientes para dispositivos Incorporados do Windows
titleSuffix: Configuration Manager
description: Plano para implementação de clientes para dispositivos Incorporados do Windows em ' Gestor de Configuração.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7848e3c0c38391ab61d10ad46cbb772c812539c7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906646"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Planeamento para implementação de clientes para dispositivos Incorporados do Windows em ' Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

<a name="BKMK_DeployClientEmbedded"></a>Se o seu dispositivo Windows Embedded não incluir o cliente do Gestor de Configuração, pode utilizar qualquer um dos métodos de instalação do cliente se o dispositivo cumprir as dependências exigidas. Se o dispositivo incorporado suportar filtros de escrita, terá de desativar esses filtros antes de instalar o cliente e, em seguida, de reativar novamente os filtros após a instalação do cliente e da atribuição do mesmo a um site.  

 Tenha em atenção que, ao desativar os filtros, não deve desativar os controladores dos filtros. Normalmente, estes controladores são iniciados automaticamente quando o computador é iniciado. Desativar os controladores irá impedir a instalação do cliente ou irá interferir com a orquestração do filtro de escrita, o que fará com que as operações do cliente falhem. Eis os serviços associados a cada um dos tipos de filtro de escrita que têm de ser mantidos em execução:  

|Tipo de Filtro de Escrita|Controlador|Tipo|Descrição|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementa um redirecionamento de E/S ao nível dos setores em volumes protegidos.|  
|FBWF|FBWF|Sistema de ficheiros|Implementa um redirecionamento de E/S ao nível dos ficheiros em volumes protegidos.|  
|UWF|uwfreg|Kernel|Redirecionador de Registo UWF|  
|UWF|uwfs|Sistema de Ficheiros|Redirecionador de Ficheiros UWF|  
|UWF|uwfvol|Kernel|Gestor de Volumes UWF|  

 Os filtros de escrita controlam a forma como o sistema operativo no dispositivo incorporado é atualizado quando efetuar alterações, por exemplo quando instalar software. Se os filtros de escrita estiverem ativados, em vez de serem efetuadas diretamente no sistema operativo, estas alterações serão redirecionadas para uma sobreposição temporária. Se as alterações apenas forem escritas na sobreposição, serão perdidas quando o dispositivo incorporado for encerrado. No entanto, caso os filtros de escrita sejam temporariamente desativados, as alterações poderão tornar-se permanentes, evitando a necessidade de voltar a efetuar essas alterações (ou de reinstalar o software) sempre que o dispositivo incorporado for reiniciado. No entanto, a desativação temporária e posterior reativação dos filtros de escrita implicará uma ou mais reinicializações, pelo que, em condições normais, será preferível controlar o momento em que esta operação irá decorrer, configurando janelas de manutenção que permitam as reinicializações fora do horário de expediente.  

 Pode configurar opções para desativar e reativar automaticamente os filtros de escrita quando implementar software como aplicações, sequências de tarefas, atualizações de software e o cliente do Endpoint Protection. A exceção são as linhas de base de configuração com itens de configuração que utilizem a remediação automática. Neste cenário, a remediação ocorre sempre ao nível da sobreposição, pelo que apenas ficará disponível até o dispositivo ser reiniciado. A remediação é novamente aplicada durante o ciclo de avaliação seguinte, mas apenas ao nível da sobreposição, cujos dados são eliminados durante o reinício. Para forçar o Gestor de Configuração a comprometer as alterações de reparação, pode implementar a linha de base de configuração e, em seguida, outra implementação de software que suporte a comprometer a mudança o mais rapidamente possível.  

 Se os filtros de escrita estiverem desativados, poderá instalar software nos dispositivos Windows Embedded utilizando o Centro de Software. No entanto, se os filtros de escrita estiverem ativados, a instalação falha e o Gestor de Configuração apresenta uma mensagem de erro de que não tem permissões suficientes para instalar a aplicação.  

> [!WARNING]  
>  Mesmo que não selecione as opções do Gestor de Configuração para cometer as alterações, as alterações poderão ser cometidas se for feita outra instalação ou alteração de software que cometa alterações. Neste cenário, as alterações originais serão confirmadas para além das novas alterações.  

 Quando o Gestor de Configuração desativa os filtros de escrita para tornar as alterações permanentes, apenas os utilizadores que possuem direitos administrativos locais podem iniciar sessão e utilizar o dispositivo incorporado. Durante este período, os utilizadores com direitos restritos são bloqueados e recebem uma mensagem a informar que o computador está indisponível por estar em manutenção. Isto ajuda a proteger o dispositivo enquanto está num estado em que as alterações podem ser aplicadas permanentemente, sendo este comportamento de bloqueio no modo de manutenção outra razão para configurar uma janela de manutenção por um período em que os utilizadores não irão iniciar sessão nestes dispositivos.  

 O Gestor de Configuração suporta a gestão dos seguintes tipos de filtros de escrita:  

- Filtro de escrita baseado em ficheiros (FBWF) - Para mais informações, consulte [filtro de escrita baseado em ficheiros](https://docs.microsoft.com/previous-versions/windows/embedded/aa940926(v=winembedded.5)).  

- FILTRO de escrita melhorado (EWF) RAM - Para mais informações, consulte Filtro de [Escrita Melhorado](https://docs.microsoft.com/previous-versions/windows/embedded/ms912906(v=winembedded.5)).  

- Filtro de escrita unificado (UWF) - Para mais informações, consulte filtro de [escrita unificado](https://docs.microsoft.com/windows-hardware/customize/enterprise/unified-write-filter).  

  O Gestor de Configuração não suporta as operações de filtragem de escrita quando o dispositivo Incorporado do Windows está no modo EWF RAM Reg.  

> [!IMPORTANT]
>  Se tiver escolha, utilize filtros de escrita baseados em ficheiros (FBWF) com O Gestor de Configuração para aumentar a eficiência e maior escalabilidade.
> 
> **Para dispositivos que utilizem apenas fbWF:** Configure as seguintes exceções para persistir no estado do cliente e os dados de inventário entre o reinício do dispositivo:  
> 
> - CCMINSTALLDIR \\ *.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Os dispositivos que executam o Windows Embedded 8.0 e posterior não suportam exclusões que contêm carateres universais. Nestes dispositivos, tem de configurar as seguintes exclusões individualmente:  
> 
> - Todos os ficheiros em CCMINSTALLDIR com a extensão .sdf, normalmente:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Para dispositivos que utilizem apenas FBWF e UWF:** Quando os clientes de um grupo de trabalho usam certificados de autenticação para pontos de gestão, deve também excluir a chave privada para garantir que o cliente continua a comunicar com o ponto de gestão. Nestes dispositivos, configure as seguintes exceções:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> Não são necessárias exceções adicionais pelo cliente do Gestor de Configuração que não sejam as documentadas na caixa **importante** acima referida. A adição de exceções adicionais do Gestor de Configuração ou do WMI (WBEM) pode levar a falhas do Gestor de Configuração, incluindo dispositivos que ficarão presos no modo de manutenção ou dispositivos que experimentam ciclos de reinicialização. Exceções desnecessárias incluem o diretório de clientes do Gestor de Configuração, o diretório CCMcache, o diretório CCMSetup, o diretório de cache da Sequência de Tarefas, o diretório WBEM e as chaves de registo relacionadas com o Gestor de Configuração.

 Para um cenário de exemplo para implementar e gerir dispositivos Windows Embedded ativados por filtro sonante no Gestor de Configuração, consulte o cenário exemplo para implementar e gerir os clientes do Gestor de [Configuração em dispositivos Incorporados](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)do Windows .  

 Para mais informações sobre como criar imagens para dispositivos Windows Embedded e configurar filtros de escrita, consulte a documentação do Windows Embedded ou contacte o OEM.  

> [!NOTE]
>  Quando seleciona as plataformas aplicáveis para implementações de software e itens de configuração, estas apresentam famílias Windows Embedded em vez de versões específicas. Utilize a lista seguinte para mapear a versão específica do Windows Embedded para as opções na caixa de listagem:  
> 
> - **Os Sistemas Operativos Incorporados baseados no Windows XP (32 bits)** incluem o seguinte:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded for Point of Service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Os sistemas operativos incorporados baseados no Windows 7 (32 bits)** incluem o seguinte:  
> 
>   -   Windows Embedded Standard 7 (32 bits)  
>   -   Windows Embedded POSReady 7 (32 bits)  
>   -   Windows ThinPC  
>   -   **Os sistemas operativos incorporados baseados no Windows 7 (64 bits)** incluem o seguinte:  
> 
>   -   Windows Embedded Standard 7 (64 bits)  
>   -   Windows Embedded POSReady 7 (64 bits)
