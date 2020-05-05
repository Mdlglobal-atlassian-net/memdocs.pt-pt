---
title: Criar e aplicar planos de energia
titleSuffix: Configuration Manager
description: Crie e aplique planos de potência no Gestor de Configuração.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076701"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Como criar e aplicar planos de energia no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A gestão de energia no Gestor de Configuração permite-lhe aplicar planos de energia fornecidos com O Gestor de Configuração a coleções de computadores na sua hierarquia ou criar os seus próprios planos de energia personalizados. Utilize o procedimento neste tópico para aplicar um esquema de energia incorporado ou personalizado a computadores.  

> [!IMPORTANT]  
>  Só é possível aplicar planos de potência do Gestor de Configuração às coleções de dispositivos.  

 Se um computador for membro de várias coleções, em que cada aplica esquemas de energia diferentes, serão executadas as seguintes ações:  

- Esquema de energia: se forem aplicados vários valores de definições de energia a um computador, será utilizado o valor menos restritivo.  

- Hora de reativação: se forem aplicadas várias horas de reativação a um computador de secretária, será utilizada a hora mais próxima da meia-noite.  

  Utilize o relatório **Computadores com Vários Esquemas de Energia** para apresentar todos os computadores com vários esquemas de energia aplicados aos mesmos. Isto pode ajudar a detetar os computadores que têm conflitos de energia. Para obter mais informações sobre relatórios de gestão de energia, consulte [como monitorizar e planear a gestão de energia.](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)  

> [!IMPORTANT]  
>  As definições de potência configuradas utilizando a Política do Grupo Windows sobrepor-se-ão às definições configuradas pela gestão de energia do Gestor de Configuração.  

 Utilize o seguinte procedimento para criar e aplicar um plano de potência do Gestor de Configuração.  

### <a name="to-create-and-apply-a-power-plan"></a>Para criar e aplicar um esquema de energia  

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3. Na lista **Coleções de Dispositivos** , clique na coleção para a qual pretende aplicar as definições de gestão de energia e, em seguida, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4. No separador **Power Management** da caixa de diálogo<<em>Collection Name\></em>**Properties,** selecione **Especificar as definições**de gestão de energia para esta recolha .  

   > [!NOTE]  
   >  Também pode clicar em **Procurar** e, em seguida, copiar as definições de gestão de energia de uma determinada coleção para a coleção selecionada.  

5. Nos campos **Início** e **Fim** , especifique a hora de início e de fim das horas de pico (ou horário comercial).  

6. Ative a **Hora de reativação (computadores de secretária)** para especificar a hora em que um computador de secretária será reativado da suspensão ou da hibernação para instalar atualizações agendadas ou instalar software.  

   > [!IMPORTANT]  
   >  A gestão de energia utiliza a funcionalidade de hora de reativação interna do Windows para reativar os computadores do modo de suspensão ou hibernação. As definições de hora de reativação não se aplicam aos computadores portáteis, de modo a evitar cenários em que poderão ser reativados quando não estão ligados à corrente. A hora de reativação é aleatória e os computadores serão reativados durante um período de uma hora a partir da hora de reativação especificada.  

7. Se pretender configurar um esquema de energia personalizada para as horas de pico (ou horário comercial), selecione **Pico Personalizado (ConfigMgr)** a partir da lista pendente **Esquema de pico** e clique em **Editar**. Se pretender configurar um esquema de energia para as horas fora de pico (ou horário não comercial), selecione **Fora de Pico Personalizado (ConfigMgr)** a partir do **Esquema fora de pico** na lista pendente e, em seguida, clique em **Editar**.  

   > [!NOTE]  
   >  Pode utilizar o relatório **Atividade do Computador** para o ajudar a decidir as agendas a utilizar para as horas de pico e fora de pico quando aplicar os esquemas de energia a coleções de computadores. Para mais informações, consulte [Como monitorizar e planear a gestão de energia.](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)  

    Também pode selecionar a partir de esquemas de energia incorporados, **Equilibrado (ConfigMgr)**, **Elevado Desempenho (ConfigMgr)** e **Poupança de Energia (ConfigMgr)**, e clicar em **Ver** para apresentar as propriedades de cada esquema de energia.  

   > [!NOTE]  
   >  Não é possível modificar os esquemas de energia incorporados.  

8. No <em>nome\>de</em><plano de alimentação**Propriedades,** configure as seguintes definições:  

   -   **Nome:** especifique um nome para este esquema de energia ou utilize o valor predefinido fornecido.  

   -   **Descrição:**  especifique uma descrição para este esquema de energia ou utilize o valor predefinido fornecido.  

   -   **Especificar as propriedades deste esquema de energia:** configure as propriedades do esquema de energia. Para desativar uma propriedade, desmarque a respetiva caixa de verificação. Para obter informações sobre as definições disponíveis, consulte [Available power management plan settings](#BKMK_Plans) neste tópico.  

       > [!IMPORTANT]  
       >  As definições ativadas são aplicadas nos computadores quando o esquema de energia é aplicado. Se desmarcar a caixa de verificação de uma definição de energia, o valor no computador cliente não é alterado quando o esquema de energia é aplicado. Desmarcar uma caixa de verificação não restaura a definição de energia para o valor anterior antes de ter sido aplicado um esquema de energia.  

9. Clique **em OK** para fechar o nome <em>\>de</em><plano de energia**Properties.**  

10. Clique **em OK** para fechar a caixa de diálogo de**definições** de nome <em>\></em>de recolha de<e para aplicar o plano de alimentação.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 A tabela seguinte lista as definições de gestão de energia disponíveis no Gestor de Configuração. Pode configurar diferentes definições para quando o computador está ligado à corrente ou em execução com energia da bateria. Dependendo da versão do Windows que estiver a utilizar, algumas definições poderão não ser configuráveis.  

> [!NOTE]  
>  As definições de energia que não configurar irão manter o respetivo valor atual nos computadores cliente.  

|Nome|Descrição|  
|----------|-----------------|  
|**Desligar o ecrã após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de o ecrã ser desativado. Especifique o valor **0** se não pretender que a gestão de energia desative o ecrã.|  
|**Suspensão após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de ser suspenso. Especifique um valor de **0** se não pretender que a gestão de energia suspenda o computador.|  
|**Pedir uma palavra-passe ao reativar**|Um valor **sim** ou **sem** valor especifica se uma palavra-passe é necessária para desbloquear o computador quando entra a acordar do sono.|  
|**Ação do botão de energia**|Especifica a ação que é tomada quando o botão de alimentação do computador é premido. Valores possíveis **Não faça nada,** **Durma,** **Hibernae**e **Desligue.**|  
|**Botão de energia do menu Iniciar**|Especifica a ação que ocorre quando carrega no botão de alimentação do menu **Iniciar** do computador. Valores possíveis **Dormir,** **Hibernar**e **Desligar.**|  
|**Ação do botão de suspensão**|Especifica a ação que ocorre quando carrega no botão **de sono** do computador. Valores possíveis **Não faça nada,** **Durma,** **Hibernae**e **Desligue.**|  
|**Ação de fechar a tampa**|Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Valores possíveis **Não faça nada,** **Durma,** **Hibernae**e **Desligue.**|  
|**Desligar o disco rígido após (minutos)**|Especifica o tempo, em minutos, de que o disco rígido do computador deve estar inativo antes de ser desligado. Especifique um valor de **0** se não quiser que a gestão de energia desligue o disco rígido do computador.|  
|**Hibernar após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de ser hibernado. Especifique um valor de **0** se não pretender que a gestão de energia hiberne o computador.|  
|**Ação de pouca bateria**|Especifica a ação que ocorre quando a bateria do computador atinge o nível de notificação de bateria baixa especificado. Valores possíveis **Não faça nada,** **Durma,** **Hibernae**e **Desligue.**|  
|**Ação de bateria crítica**|Especifica a ação que é tomada quando a bateria do computador atinge o nível de notificação crítico especificado da bateria. Quando **estiver na bateria** possíveis valores **Durma,** **hite**e **desligue.** Quando **ligado sem** valores possíveis **Não faça nada,** **Durma,** **Hitee**e **Desligue.**|  
|**Permitir suspensão híbrida**|A seleção do valor **De Ligar** ou **Off** especifica se o Windows guarda um ficheiro de hibernação ao entrar no sono, que pode ser usado para restaurar o estado do computador em caso de perda de energia enquanto este entrou no sono.<br /><br /> A suspensão híbrida foi concebida para computadores de secretária e, por predefinição, não está ativada nos computadores portáteis. Em computadores que executem o Windows 7, ativar o modo de suspensão híbrida desativa a funcionalidade de hibernação.|  
|**Permitir ação de estado de espera durante a suspensão**|A seleção do valor **De Ligar** ou **Off** permite que o computador esteja em espera, o que ainda consome alguma energia, mas permite que o computador acorde mais rapidamente. Se esta definição estiver definida como **Desativada**, o computador só pode hibernar ou ser desligado.|  
|**Inatividade necessária para suspender (%)**|Especifica a percentagem de tempo inativo no tempo de processador do computador necessária para o computador entrar no modo de suspensão. Para computadores que executam o Windows 7, este valor está sempre definido para **0**.|  
|**Ativar o temporizador de reativação do Windows para computadores de secretária**|A seleção do valor **Enable** ou **Disable** pode permitir que o temporizador do Windows incorporado seja utilizado pela gestão de energia para despertar um computador de secretária. Quando um computador de secretária é reativado com o temporizador de reativação do Windows, permanecerá ativo durante dez minutos por predefinição, para ter tempo para instalar atualizações ou receber políticas.<br /><br /> Os temporizadores de reativação não são suportados em computadores portáteis para impedir cenários em que poderão ser reativados quando não estão ligados.|  
