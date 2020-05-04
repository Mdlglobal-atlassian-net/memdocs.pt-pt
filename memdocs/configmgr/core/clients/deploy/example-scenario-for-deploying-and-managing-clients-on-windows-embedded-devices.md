---
title: Cenário de exemplo - implementar clientes Incorporados do Windows
titleSuffix: Configuration Manager
description: Consulte um cenário de exemplo para a implementação e gestão de clientes do Gestor de Configuração em dispositivos Incorporados do Windows.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713332"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Cenário de exemplo para implementar e gerir clientes do Gestor de Configuração em dispositivos Incorporados do Windows

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este cenário demonstra como pode gerir dispositivos Windows Embedded ativados por filtro sonante com O Gestor de Configuração.Se os seus dispositivos incorporados não suportarem filtros de escrita, comportam-se como clientes padrão do Gestor de Configuração e estes procedimentos não se aplicam.  

A Vinhedo de Coho & A Adega está a abrir um centro de visitantes e precisa de quiosques que executem o Windows Embedded para executar apresentações interativas. O edifício para o novo centro de visitantes não é próximo do departamento de TI, pelo que os quiosques devem ser geridos remotamente. Além do software que executa as apresentações, estes dispositivos devem executar software de proteção antimalware atualizado para cumprir as políticas de segurança da empresa. Os quiosques devem funcionar 7 dias por semana, sem tempo de descanso enquanto o centro de visitantes está aberto.  

 Coho já executa o Gestor de Configuração para gerir dispositivos na sua rede. O Gestor de Configuração está configurado para executar a Proteção de Pontofinal e instalar atualizações e aplicações de software. No entanto, uma vez que a equipa de TI nunca geriu dispositivos Windows Embedded antes, o administrador do Gestor de Configuração executa um piloto para gerir dois quiosques no lobby de receção.   

 Para gerir estes dispositivos Incorporados do Windows que estão ativados por filtros de escrita, o administrador do Gestor de Configuração executa as seguintes etapas para instalar o cliente do Gestor de Configuração, proteger o cliente utilizando a Proteção endpoint e instalar o software de apresentação interativa.  

1. O administrador do Gestor de Configuração (o Administrador) lê como os dispositivos Incorporados do Windows usam filtros de escrita e como o Gestor de Configuração pode facilitar isso desativando automaticamente e, em seguida, reativando os filtros do escritor para persistir uma instalação de software.  

    Para mais informações, consulte [Planplanning para implementação de clientes em dispositivos Incorporados](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)windows .  

2. Antes de o Administrador instalar o cliente do Gestor de Configuração, o Administrador cria uma nova coleção de dispositivos baseado em consultas para os dispositivos Incorporados do Windows. Uma vez que a empresa utiliza formatos de nomeação padrão para identificar os seus computadores, o Administrador pode identificar exclusivamente os dispositivos Windows Embedded pelas primeiras seis letras do nome do computador: **WEMDVC**. O Administrador usa a seguinte consulta WQL para criar esta coleção: **selecione SMS_R_System.NetbiosName a partir de SMS_R_System onde SMS_R_System.NetbiosName como "WEMDVC%".**  

    Esta coleção permite ao Administrador gerir os dispositivos Incorporados do Windows com diferentes opções de configuração dos outros dispositivos. O Administrador utilizará esta coleção para controlar os reinícios, implementar a Proteção endpoint com as definições do cliente e implementar a aplicação de apresentação interativa.  

    Ver [Como criar coleções.](../../../core/clients/manage/collections/create-collections.md)  

3. O Administrador convê a coleção para uma janela de manutenção para garantir que reinicia o que pode ser necessário para a instalação da aplicação de apresentação e que quaisquer atualizações não ocorrem durante o horário de funcionamento para o centro de visitantes. As horas de abertura serão das 9:00 às 18:00, de segunda a domingo. O Administrador configura a janela de manutenção para todos os dias, das 18:30 às 06:00.  

4. Para mais informações, consulte [Como utilizar as janelas de manutenção](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. Em seguida, o Administrador configura uma definição personalizada do cliente do dispositivo para instalar o cliente Endpoint Protection selecionando **Sim** para as seguintes definições, e depois implementa esta definição personalizada do cliente para a coleção de dispositivos Incorporados do Windows:  

   - **Instalar o cliente do Endpoint Protection nos computadores cliente**  

   - **Para dispositivos Windows Embedded com filtros de escrita, consolidar a instalação de cliente do Endpoint Protection (necessita de reinicialização)**  

   - **Permitir a instalação de cliente Endpoint Protection e reiniciar fora das janelas de manutenção**  

     Quando o cliente do Gestor de Configuração está instalado, estas definições instalam o cliente Endpoint Protection e asseguram-se de que é perinenciado no sistema operativo como parte da instalação, em vez de estar escrita apenas para a sobreposição. As políticas de segurança da empresa exigem que o software antimalware esteja sempre instalado e o Administrador não quer correr o risco de os quiosques ficarem desprotegidos por um curto período de tempo se reiniciarem.  

   > [!NOTE]  
   >  Os reinícios necessários para instalar o cliente do Endpoint Protection ocorrem apenas uma vez, durante o período de configuração dos dispositivos e antes de o centro de visitantes estar operacional. Ao contrário da implementação periódica de aplicações ou atualizações de definição de software, da próxima vez que o cliente endpoint Protection for instalado no mesmo dispositivo será provavelmente quando a empresa atualizar para a próxima versão do Gestor de Configuração.  

    Para mais informações, consulte [configurar a Proteção](../../../protect/deploy-use/endpoint-protection-configure.md)do Ponto Final .  

6. Com as configurações de configuração para o cliente agora em vigor, o Administrador prepara-se para instalar os clientes do Gestor de Configuração. Antes de o Administrador poder instalar os clientes, estes devem desativar manualmente o filtro de escrita nos dispositivos Incorporados do Windows. O Administrador lê a documentação do OEM que acompanha os quiosques e segue as suas instruções para desativar os filtros de escrita.  

    O Administrador renomea o dispositivo para que utilize o formato de nomeação padrão da empresa e, em seguida, instala o cliente manualmente executando CCMSetup com o seguinte comando de uma unidade mapeada que detém os ficheiros de origem do cliente: **CCMSetup.exe/MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    Este comando instala o cliente, atribui o cliente ao ponto de gestão que tem o FQDN da Intranet de **mpserver.cohovineyardandwinery.com**e atribui o cliente ao site primário denominado **CO1**.  

    O Administrador sabe que demora sempre algum tempo para os clientes instalarem e enviarem de volta o seu estado para o site. Assim, o Administrador aguarda antes de confirmar que os clientes instalam com sucesso, atribuem ao site e aparecem como clientes na coleção que criaram para dispositivos Windows Embedded.  

    Como confirmação adicional, o Administrador verifica as propriedades do Gestor de Configuração no Painel de Controlo dos dispositivos e compara-os com computadores Windows padrão que são geridos pelo site. Por exemplo, no separador **Componentes** , **Agente de Inventário de Hardware** apresenta **Ativado**e, no separador **Ações** , existem 11 ações disponíveis, que incluem **Ciclo de Avaliação da Aplicação de Implementação** e **Ciclo de coleção de dados de deteção**.  

    Confiante de que os clientes são instalados, atribuídos e recebendo com sucesso a política do cliente a partir do ponto de gestão, o Administrador permite manualmente os filtros de escrita seguindo as instruções do OEM.  

    Para obter mais informações, consulte:  

   -   [Como implementar clientes em computadores Windows](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Como atribuir clientes a um site](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Agora que o cliente do Gestor de Configuração está instalado nos dispositivos Incorporados do Windows, o Administrador confirma que pode geri-los da mesma forma que gere os clientes padrão do Windows. Por exemplo, a partir da consola Do Gestor de Configuração, o Administrador pode geri-los remotamente utilizando controlo remoto, iniciar a política do cliente para eles e ver propriedades do cliente e inventário de hardware.  

    Uma vez que estes dispositivos se juntam a um domínio de Diretório Ativo, o Administrador não tem de os aprovar manualmente como clientes de confiança e confirma da consola do Gestor de Configuração que são aprovados.  

    Para mais informações, consulte [Como gerir os clientes.](../../../core/clients/manage/manage-clients.md)  

8. Para instalar o software de apresentação interativa, o Administrador executa o **Assistente de Software de Implementação** e configura uma aplicação necessária. Na página **experiência** do utilizador do assistente, no manuseamento do filtro Write para a secção **de dispositivos Incorporados** pelo Windows, eles aceitam a opção predefinida que seleciona Alterações de compromisso no prazo ou durante uma janela de **manutenção (requer reinícios)**.  

    O Administrador mantém esta opção predefinida para os filtros de escrita para garantir que a aplicação persiste após um reinício, de modo a que esteja sempre disponível para os visitantes que usam os quiosques. A janela de manutenção diária fornece um período seguro durante o qual podem ocorrer os reinícios para instalação e atualizações.  

    O Administrador implementa a aplicação para a coleção de dispositivos Windows Embedded.  

    Para mais informações, consulte [como implementar aplicações com o Gestor de Configuração](../../../apps/deploy-use/deploy-applications.md).  

9. Para configurar atualizações de definição para proteção de pontos finais, o Administrador utiliza atualizações de software e executa o Assistente de Regra de Implementação Automática Create. Selecionam o modelo de Atualizações de **Definição** para pré-povoar o assistente com definições adequadas para a Proteção do Ponto Final.  

     Estas definições incluem as seguintes na página **Experiência do Utilizador** do assistente:  

   - **Comportamento do prazo**: a caixa de verificação **Instalação do Software** não está selecionada.  

   - **Processamento do filtro de escrita para dispositivos Windows Embedded**: a caixa de verificação **Confirmar alterações dentro do prazo ou durante a janela de manutenção (requer reinicialização)** não está selecionada.  

     O Administrador mantém estas definições predefinidas. Em conjunto, estas duas opções com esta configuração permitem a instalação de quaisquer definições de atualização de software para o Endpoint Protection na sobreposição durante o dia, sem aguardar para serem instaladas e consolidadas durante a janela de manutenção. Esta configuração cumpre melhor a política de segurança da empresa relativa à execução de proteção antimalware atualizada nos computadores.  

     > [!NOTE]  
     >  Ao contrário das instalações de software para aplicações, as definições de atualização de software para o Endpoint Protection podem ocorrer com muita frequência, inclusivamente várias vezes por dia. São frequentemente ficheiros pequenos. Para estes tipos de implementações relacionadas com segurança, geralmente é vantajoso instalar sempre na sobreposição em vez de aguardar até à janela de manutenção. O cliente do Gestor de Configuração reinstalará rapidamente as atualizações de definição de software se o dispositivo recomeçar porque esta ação inicia uma verificação de avaliação e não aguarda até à próxima avaliação agendada.  

     O Administrador seleciona a coleção de dispositivos Incorporados do Windows para a regra de implementação automática.  

     Para obter mais informações, veja  
               Passo 3: Configure configurar atualizações de software do gestor de configuração para entregar atualizações de definição aos computadores clientes na configuração da [proteção de ponto final](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. O Administrador decide configurar uma tarefa de manutenção que periodicamente comete todas as alterações na sobreposição. Esta tarefa destina-se a suportar a implementação de definições de atualização de software, para reduzir o número de atualizações que se acumulam e têm de ser instaladas novamente sempre que o dispositivo reinicia. Na experiência do Administrador, isto ajuda os programas antimalware a funcionar de forma mais eficiente.  

    > [!NOTE]  
    >  Estas definições de atualização de software seriam consolidadas automaticamente na imagem se os dispositivos Embedded executassem outra tarefa de gestão que suportasse a consolidação de alterações. Por exemplo, a instalação de uma nova versão do software de apresentação interativa também consolidaria as alterações das definições de atualização de software. Em alternativa, a instalação de atualizações de software padrão todos os meses durante a janela de manutenção também poderia consolidar as alterações das definições de atualização de software. No entanto, neste cenário, em que as atualizações de software padrão não são executadas e o software de apresentação interativa não é atualizado com muita frequência, poderão decorrer meses até as atualizações de definições de software serem automaticamente consolidadas na imagem.  

     O Administrador cria primeiro uma sequência de tarefas personalizada que não tem outras definições que não o nome. Executam o Assistente de Sequência de Tarefas Create:  

    1. Na página **Criar uma Nova Sequência** de Tarefas, o Administrador seleciona Criar uma nova sequência de **tarefas personalizadas,** e depois clica em **Seguinte**.  

    2. Na página **informação** da sequência de tarefas, o Administrador introduz a tarefa de **manutenção para cometer alterações em dispositivos incorporados** para o nome da sequência de tarefas e, em seguida, clica **em Seguinte**.  

    3. Na página **Resumo,** o Administrador seleciona **Seguinte**, e completa o assistente.  

       O Administrador implementa então esta sequência de tarefas personalizada para a coleção de dispositivos Incorporados do Windows, e configura o calendário a ser executado todos os meses. Como parte das definições de implementação, selecionam as **alterações de Compromisso no prazo ou durante uma janela de manutenção (requer reinício)** caixa de verificação para persistir as alterações após o reinício. Para configurar esta implementação, o Administrador seleciona a sequência de tarefas personalizada que acabaram de criar e, em seguida, no separador **Home,** no grupo **Deimplantação,** clicam em **Implementar** para iniciar o Assistente de Software de Implementação:  

    4. Na página **Geral,** o Administrador seleciona a coleção de dispositivos Incorporados do Windows e, em seguida, clica **em Seguinte**.  

    5. Na página definições de **implementação,** o Administrador seleciona o **Propósito** de **Necessário**, e depois clica **em Seguinte**.  

    6. Na página **de Agendamento,** o Administrador clica **em Novo** para especificar um horário semanal durante a janela de manutenção e, em seguida, clica **em Seguinte**.  

    7. O Administrador completa o assistente sem mais alterações.  

       Para obter mais informações, veja  
                 [Gerir sequências de tarefas para automatizar tarefas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Para que os quiosques funcionam automaticamente, o Administrador escreve um script para configurar os dispositivos para as seguintes definições:  

    - Iniciar sessão automaticamente utilizando uma conta de convidado sem palavra-passe.  

    - Executar automaticamente o software de apresentação interativa ao iniciar.  

      O Administrador utiliza pacotes e programas para implementar este script na coleção de dispositivos Windows Embedded. Quando o Administrador executa o Assistente de Software de Implantação, selecionam novamente as **alterações de Compromisso no prazo ou durante uma janela de manutenção (requer reinício)** caixa de verificação para persistir as alterações após o reinício.  

      Para mais informações, consulte [Pacotes e programas.](../../../apps/deploy-use/packages-and-programs.md)  

12. Na manhã seguinte, o Administrador verifica os dispositivos Windows Embedded. Confirmam o seguinte:  

    - A sessão do quiosque foi automaticamente iniciada com a conta de convidado.  

    - O software de apresentação interativa está em execução.  

    - O cliente do Endpoint Protection está instalado e tem as definições de atualização de software mais recentes.  

    - O dispositivo foi reiniciado durante a janela de manutenção.  

      Para obter mais informações, consulte:  

    - [Como monitorizar o Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Monitorizar aplicações com Gestor de Configuração](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. O Administrador monitoriza os quiosques e reporta a gestão bem sucedida dos mesmos ao seu gerente. Dado o êxito, são encomendados 20 quiosques para o centro de visitantes.  

     Para evitar a instalação manual do cliente do Gestor de Configuração, que requer desativação manual e, em seguida, habilitação para os filtros de escrita, o Administrador garante que a encomenda inclui uma imagem personalizada que já inclui a instalação e atribuição do site do cliente Do Gestor de Configuração. Além disso, o nome dos dispositivos é atribuído de acordo com o formato de nomenclatura da empresa.  

     Os quiosques são entregues para o centro de visitantes uma semana antes da respetiva abertura. Durante este período, os quiosques são ligados à rede, toda a gestão de dispositivos é automática e não é necessário um administrador local. O Administrador confirma que os quiosques estão a funcionar conforme necessário:  

    -   Os clientes dos quiosques concluem a atribuição de sites e transferem a chave de raiz fidedigna a partir dos Serviços de Domínio do Active Directory.  

    -   Os clientes dos quiosques são automaticamente adicionados à coleção de dispositivos Windows Embedded e configurados com a janela de manutenção.  

    -   O cliente do Endpoint Protection está instalado e tem as definições de atualização de software mais recentes da proteção antimalware.  

    -   O software de apresentação interativa está instalado e é executado automaticamente (está preparado para os visitantes).  

14. Após esta configuração inicial, quaisquer reinícios que possam ser necessários para atualizações só ocorrerão quando o centro de visitantes estiver fechado.  
