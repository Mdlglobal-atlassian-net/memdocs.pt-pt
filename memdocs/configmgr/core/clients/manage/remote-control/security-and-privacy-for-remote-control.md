---
title: Privacidade de segurança de controlo remoto
titleSuffix: Configuration Manager
description: Obtenha informações de segurança e privacidade para controlo remoto no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715103"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Segurança e privacidade para controlo remoto em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém informações de segurança e privacidade para controlo remoto no Gestor de Configuração.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Melhores práticas de segurança para controlo remoto  
 Utilize as melhores práticas de segurança seguintes quando gerir computadores cliente utilizando o controlo remoto.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando ligar a um computador remoto, não continue se for utilizada a autenticação NTLM em vez de Kerberos.|Quando o Gestor de Configuração detetar que a sessão de controlo remoto é autenticada utilizando o NTLM em vez de Kerberos, vê uma solicitação que o avisa de que a identidade do computador remoto não pode ser verificada. Não continue a sessão de controlo remoto. A autenticação NTLM é um protocolo de autenticação mais fraco que Kerberos e é vulnerável a repetição e representação.|  
|Não ative a partilha da Área de Transferência no visualizador de controlo remoto.|A Área de Transferência suporta objetos, como ficheiros executáveis e texto, e pode ser utilizada pelo utilizador no computador anfitrião durante a sessão de controlo remoto para executar um programa no computador de origem.|  
|Não introduza palavras-passe para contas com privilégios quando administrar remotamente um computador.|É possível que software que observe a introdução por teclado capture a palavra-passe. Em alternativa, se o programa que está a ser executado no computador cliente não for o programa que o utilizador do controlo remoto assume, o programa pode estar a capturar a palavra-passe. Quando forem necessárias contas e palavras-passe, o utilizador final deve introduzi-las.|  
|Bloqueie o teclado e o rato durante uma sessão de controlo remoto.|Se o Gestor de Configuração detetar que a ligação de controlo remoto está terminada, o Gestor de Configuração bloqueia automaticamente o teclado e o rato de modo a que um utilizador não possa assumir o controlo da sessão de controlo remoto aberto. No entanto, esta deteção pode não ocorrer imediatamente e não ocorre se o serviço de controlo remoto for terminado.<br /><br /> Selecione a ação **Bloquear Teclado e Rato Remotos** na janela **Controlo Remoto do ConfigMgr** .|  
|Não permita aos utilizadores configurar as definições de controlo remoto no Centro de Software.|Não ative a definição de cliente **Os utilizadores podem alterar as definições de notificação ou da política no Centro de Software** para ajudar a impedir que os utilizadores sejam espiados. Se um utilizador o alterar, pode permitir que um utilizador diferente na mesma máquina seja visto remotamente. <br /><br />**Esta definição é para o computador, não para o utilizador ligado.**|  
|Ative o perfil da Firewall do Windows **Domínio** .|Ative a definição de cliente **Ativar controlo remoto nos perfis de exceção de Firewall de clientes** e, em seguida, selecione a Firewall do Windows **Domínio** para computadores de intranet.|  
|Se terminar a sessão durante uma sessão de controlo remoto e iniciar sessão como um utilizador diferente, certifique-se de que termina a sessão antes de desligar a sessão de controlo remoto.|Se não terminar a sessão neste cenário, a sessão permanece aberta.|  
|Não conceda direitos de administrador local aos utilizadores.|Quando conceder direitos de administrador local aos utilizadores, estes poderão assumir o controlo da sua sessão de controlo remoto ou comprometer as suas credenciais.|  
|Utilize a Política de Grupo ou o Gestor de Configuração para configurar as definições de Assistência Remota, mas não ambas.|Pode utilizar o Gestor de Configuração e a Política de Grupo para efazer alterações de configuração nas definições de Assistência Remota. Quando a Política de Grupo é atualizada no cliente, por predefinição, otimiza o processo ao alterar apenas as políticas que foram alteradas no servidor. O Gestor de Configuração altera as definições na política de segurança local, que pode não ser substituída a menos que a atualização da Política do Grupo seja forçada.<br /><br /> A definição da política em ambos os locais pode originar resultados inconsistentes. Escolha um dos seguintes métodos para configurar as definições de Assistência Remota.|  
|Ative a definição de cliente **Solicitar ao utilizador permissão do Controlo Remoto**.|Embora existam formas desta definição de cliente solicitar a um utilizador para confirmar uma sessão de controlo remoto, ative esta definição para reduzir a probabilidade de os utilizadores serem espiados enquanto estão a trabalhar em tarefas confidenciais.<br /><br /> Além disso, informe os utilizadores para verificarem o nome da conta apresentado durante a sessão de controlo remoto e desligarem a sessão se suspeitarem que a conta não está autorizada.|  
|Limite a lista de Visualizadores Permitidos.|Não são necessários direitos de administrador local para um utilizador poder utilizar o controlo remoto.|  

### <a name="security-issues-for-remote-control"></a>Problemas de segurança do controlo remoto  
 A gestão de computadores cliente utilizando o controlo remoto tem os seguintes problemas de segurança:  

-   Não considere as mensagens de auditoria do controlo remoto fiáveis.  

     Se iniciar uma sessão de controlo remoto e, em seguida, iniciar sessão utilizando credenciais alternativas, a conta original envia as mensagens de auditoria e não a conta que utilizou as credenciais alternativas.  

     As mensagens de auditoria não são enviadas se copiar os ficheiros binários para controlo remoto em vez de instalar a consola Do Gestor de Configuração e, em seguida, executar o controlo remoto no pedido de comando.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade do controlo remoto  
 O controlo remoto permite-lhe visualizar sessões ativas nos computadores clientes do Gestor de Configuração e potencialmente visualizar qualquer informação armazenada nesses computadores. Por predefinição, o controlo remoto não está ativado.  

 Embora possa configurar o controlo remoto para fornecer avisos evidentes e obter consentimento de um utilizador antes do início da sessão de controlo remoto, também pode monitorizar os utilizadores sem a sua permissão ou conhecimento. Pode configurar o nível de acesso Ver Apenas para que nada possa ser alterado no controlo remoto, ou Controlo Total. A conta do administrador de ligação é apresentada na sessão de controlo remoto, para ajudar os utilizadores a identificar quem está a ligar ao respetivo computador.  

 Por predefinição, o Gestor de Configuração concede às permissões de Controlo Remoto do grupo de Administradores locais.  

 Antes de configurar o controlo remoto, considere os requisitos de privacidade.  
