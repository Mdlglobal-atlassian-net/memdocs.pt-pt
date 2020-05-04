---
title: Tarefas de manutenção
titleSuffix: Configuration Manager
description: Compreenda quais as tarefas de manutenção a executar para sites e hierarquias do Gestor de Configuração e quando executá-las.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713731"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Tarefas de manutenção para Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os sites e hierarquias do Gestor de Configuração requerem manutenção e monitorização regulares para fornecer serviços de forma eficaz e contínua. A manutenção regular garante que a base de dados do Hardware, software e Gestor de Configuração continua a funcionar correta e eficientemente. O desempenho ideal reduz consideravelmente o risco de falha.  

 Para configurar alertas e utilizar o Sistema de Estado para monitorizar a saúde do Gestor de Configuração, consulte [os alertas de utilização e o sistema de estado para o Gestor](../../../core/servers/manage/use-alerts-and-the-status-system.md)de Configuração .  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a>Tarefas de manutenção

 A manutenção regular é importante para garantir as operações corretas no local. Mantenha um registo de manutenção para documentar as datas de manutenção, quem fez manutenção, e quaisquer comentários relacionados com a manutenção sobre as tarefas. Para manter o seu site, considere a manutenção diária ou semanal. Algumas tarefas podem requerer um horário diferente. A manutenção comum pode incluir tanto as tarefas de manutenção incorporadas como outras tarefas, como a manutenção de contas, para manter o cumprimento das políticas da sua empresa.  

 Utilize as seguintes informações como guia para o ajudar a planear quando fazer diferentes tarefas de manutenção. Utilize estas listas como ponto de partida e adicione tarefas que possa necessitar.  

### <a name="daily-tasks"></a>Tarefas Diárias
Seguem-se tarefas de manutenção que poderá considerar num horário diário:  

- Verifique se as tarefas de manutenção pré-definidas que estão programadas para serem executadas diariamente estão a funcionar com sucesso.  

- Verifique o estado da base de dados do Gestor de Configuração.  

- Verifique o estado do servidor do site.  

- Verifique as caixas de entrada do sistema de configuração do site para obter atrasos de ficheiros.  

- Verifique o estado dos sistemas do site.  

- Verifique os registos de eventos do sistema operativo dos sistemas do site.  

- Verifique o registo de erros do Servidor SQL a partir do computador de base de dados do site.  

- Verifique o desempenho do sistema.  

- Verifique os alertas do Gestor de Configuração.  

### <a name="weekly-tasks"></a>Tarefas Semanais

Seguem-se tarefas de manutenção que poderá considerar para um horário semanal:  

- Verifique se as tarefas de manutenção pré-definidas que estão programadas para serem executadas semanalmente estão a funcionar com sucesso.  

- Eliminar ficheiros desnecessários dos sistemas do site.  

- Produzir e distribuir relatórios de utilizador final, se necessário.  

- Back up application, security, and system event logs and clear them.  

- Verifique o tamanho da base de dados do site e verifique se há espaço suficiente para o disco disponível no servidor de base de dados do site para que a base de dados do site possa crescer.  

- Faça a manutenção da base de dados do SQL Server na base de dados do site de acordo com o seu plano de manutenção do Servidor SQL.  

- Verifique o espaço disponível em disco em todos os sistemas do site.  

- Executar ferramentas de desfragmentação do disco em todos os sistemas do site.  

### <a name="periodic-tasks"></a>Tarefas Periódicas

Algumas tarefas que não requerem manutenção diária ou semanal são importantes para garantir a saúde geral do local. Estas tarefas também asseguram que os planos de segurança e de recuperação de catástrofes estão atualizados. Seguem-se tarefas de manutenção que poderá considerar para um horário mais periódico do que as tarefas diárias ou semanais:  

- Mude as contas e as palavras-passe, se for necessário, de acordo com o seu plano de segurança.  

- Reveja o plano de manutenção para verificar se as tarefas de manutenção programadas estão programadas correta mente e eficazmente, dependendo das configurações configuradas do site.  

- Reveja o design da hierarquia do Gestor de Configuração para quaisquer alterações necessárias.  

- Verifique o desempenho da rede para garantir que não foram feitas alterações que afetem as operações do local.  

- Verifique se as definições de Diretório Ativo que afetam as operações do local não mudaram. Por exemplo, verifique se as subredes que são atribuídas a sites de Diretório Ativo e que são usadas como limites para o site do Gestor de Configuração não mudaram.  

- Reveja o seu plano de recuperação de desastres para quaisquer alterações necessárias.  

- Faça uma recuperação do site de acordo com o plano de recuperação de desastres num laboratório de teste usando uma cópia de cópia de reserva da cópia de segurança mais recente que a tarefa de manutenção do Servidor do Site de Backup criou.

- Verifique se há erros ou atualizações de hardware disponíveis.  

- Verifique a saúde geral do site.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>Mantenha a saúde operacional da sua base de dados do site

 Enquanto o site e a hierarquia do Gestor de Configuração fazem as tarefas que programa e configura, os componentes do site adicionam continuamente dados à base de dados do Gestor de Configuração. À medida que a quantidade de dados aumenta, o desempenho da base de dados e o espaço de armazenamento gratuito na base de dados diminuem. Pode configurar tarefas de manutenção do site para remover dados envelhecidos que já não necessita.  

 O Gestor de Configuração fornece tarefas de manutenção pré-definidas que pode utilizar para manter a saúde da base de dados do Gestor de Configuração. Nem todas as tarefas de manutenção estão disponíveis em cada site, por padrão. Várias tarefas são ativadas enquanto algumas não estão, e todos suportam um horário que você pode configurar.  

 A maioria das tarefas de manutenção remove periodicamente dados desatualizados da base de dados do Gestor de Configuração. A redução do tamanho da base de dados através da remoção de dados desnecessários melhora o desempenho e a integridade da base de dados, o que aumenta a eficiência do site e da hierarquia. Outras tarefas, como **os Índices de Reconstrução,** ajudam a manter a eficiência da base de dados. Outras tarefas, como a tarefa do Servidor do **Site de Backup,** ajudam-no a preparar-se para a recuperação de desastres.  

> [!IMPORTANT]
> Quando planeia o calendário de qualquer tarefa que apague os dados, considere a utilização desses dados em toda a hierarquia. Quando uma tarefa que elimina os dados corre num site, a informação é removida da base de dados do Gestor de Configuração, e esta alteração replica-se a todos os sites da hierarquia. Esta eliminação pode afetar outras tarefas que dependem desses dados. Por exemplo, no site da administração central, você pode configurar discovery para executar uma vez por mês para identificar computadores não clientes. Planeia instalar o cliente do Gestor de Configuração nestes computadores dentro de duas semanas após a sua descoberta. No entanto, num dos locais da hierarquia, um administrador configura a tarefa eliminar dados de descobertas envelhecidas para executar de sete em sete dias. O resultado é que sete dias após a descoberta de computadores não clientes, são eliminados da base de dados do Gestor de Configuração. De volta ao site da administração central, prepara-se para pressionar a instalação do cliente do Gestor de Configuração a estes novos computadores no dia 10. No entanto, como a tarefa eliminar dados de descobertas envelhecidas foi recentemente executada e eliminada de dados que são sete dias ou mais, os computadores recentemente descobertos já não estão disponíveis na base de dados.

Depois de instalar um site do Gestor de Configuração, reveja as tarefas de manutenção disponíveis e ative as tarefas que as suas operações necessitam. Reveja o calendário padrão de cada tarefa e, quando necessário, estabeleça o calendário para afinar a tarefa de manutenção para se adaptar à sua hierarquia e ambiente. Embora o calendário padrão de cada tarefa deva servir a maioria dos ambientes, monitorize o desempenho dos seus sites e base de dados e espere afinar tarefas para aumentar a eficiência da sua implementação. Planeie rever periodicamente o desempenho do site e da base de dados e reconfigurar as tarefas de manutenção e os seus horários para manter essa eficiência.  

## <a name="set-up-maintenance-tasks"></a>Configurar tarefas de manutenção

 Cada site do Gestor de Configuração suporta tarefas de manutenção que ajudam a manter a eficiência operacional da base de dados do site. Por padrão, várias tarefas de manutenção estão ativadas em cada site, e todas as tarefas suportam horários independentes. As tarefas de manutenção são configuradas individualmente para cada site e aplicam-se à base de dados desse site. No entanto, algumas tarefas, como eliminar dados de **descobertas envelhecidas,** afetam a informação que está disponível em todos os sites numa hierarquia.  

 Apenas as tarefas de manutenção que pode configurar num site são apresentadas na consola 'Gestor de Configuração'. Para obter uma lista completa de tarefas de manutenção por tipo de site, consulte [referência para tarefas](../../../core/servers/manage/reference-for-maintenance-tasks.md)de manutenção para Gestor de Configuração .  

 Utilize o seguinte procedimento para o ajudar a configurar as definições comuns das tarefas de manutenção.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Para configurar tarefas de manutenção para a versão 1906 do Gestor de Configuração
<!--3555894-->
A partir da versão 1906, as tarefas de manutenção do servidor do site podem agora ser visualizadas, editadas e monitorizadas a partir do seu próprio separador na visão de detalhes de um servidor de site. Ainda pode editar tarefas de manutenção escolhendo a Manutenção do **Site** no grupo **Definições,** como fez nas versões anteriores do Gestor de Configuração.

1. Na consola do Gestor de Configuração, vá aos**Sites**de**Configuração** >do Site **da Administração.** > 
1. Selecione um site da sua lista e, em seguida, clique no separador **Tarefas de Manutenção** no painel de detalhes.
1. Apenas são apresentadas as tarefas disponíveis no site selecionado. Clique na direita numa das tarefas de manutenção e escolha uma das seguintes opções:
   - **Ativar** - Ligue a tarefa.
   - **Desativar** - Desligue a tarefa.
   - **Editar** - Editar o calendário de tarefas ou as suas propriedades.

![Aba para tarefas de manutenção na visão detalhada de um servidor de site](./media/3555894-maintenance-tasks.png)

O separador **Tarefas de Manutenção** dá-lhe informações como:

- Se a tarefa estiver ativada
- O calendário de tarefas
- Última hora de início
- Última hora de conclusão
- Se a tarefa concluída com sucesso
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Para configurar tarefas de manutenção para a versão 1902 e anterior do Gestor de Configuração

1. Na consola do Gestor de Configuração, vá aos**Sites**de**Configuração** >do Site **da Administração.** > 
2. Escolha o site que tem a tarefa de manutenção que pretende configurar.  
3. No separador **Casa,** no grupo **Definições,** escolha a Manutenção do **Site**e, em seguida, escolha a tarefa de manutenção que pretende configurar. Apenas são apresentadas as tarefas disponíveis no site selecionado.

4. Para configurar a tarefa, escolha **Editar**. Certifique-se de que esta caixa de verificação de **tarefas é** verificada e configura um horário para quando a tarefa estiver em funcionação. Se a tarefa também eliminar os dados envelhecidos, configurar a idade dos dados que serão eliminados da base de dados quando a tarefa for executado. Escolha **OK** para fechar a tarefa **Propriedades**.

   > [!NOTE]  
   > Para **eliminar mensagens**de estado envelhecidos, configura a idade dos dados para eliminar quando configurar as regras do filtro de estado.  

5. Para ativar ou desativar a tarefa sem editar as propriedades da tarefa, escolha o botão **Ativar** ou **Desativar.** A etiqueta do botão muda dependendo da configuração atual da tarefa.  
6. Quando terminar de configurar as tarefas de manutenção, escolha **OK** para terminar o procedimento.

## <a name="next-steps"></a>Passos seguintes

[Referência para tarefas de manutenção](reference-for-maintenance-tasks.md)
