---
title: Privacidade de segurança de inventário de software
titleSuffix: Configuration Manager
description: Obtenha informações de segurança e privacidade para inventário de software no Gestor de Configuração.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710672"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Segurança e privacidade para inventário de software em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este tópico contém informações de segurança e privacidade para inventário de software no Gestor de Configuração.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Procedimentos recomendados de segurança para inventário de software  
 Utilize as seguintes melhores práticas de segurança para quando recolher os dados de inventário de software a partir de clientes:  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Assinar e encriptar dados de inventário|Quando os clientes comunicam com pontos de gestão através de HTTPS, todos os dados enviados são encriptados com SSL. No entanto, quando os computadores cliente utilizam HTTP para comunicar com pontos de gestão na intranet, os dados de inventário de cliente e os ficheiros recolhidos podem ser enviados não estando assinados nem encriptados. Certifique-se de que o site está configurado para exigir assinatura e utilizar encriptação. Além disso, se os clientes suportarem o algoritmo SHA-256, selecione a opção para exigir SHA-256.|  
|Não utilize a recolha de ficheiros para recolher ficheiros críticos ou informações confidenciais|O inventário de software do Gestor de Configuração utiliza todos os direitos da conta LocalSystem, que tem a capacidade de recolher cópias de ficheiros críticos do sistema, como a base de dados de contas de registo ou de segurança. Quando estes ficheiros estão disponíveis no servidor do site, uma pessoa que tenha os direitos de Ler Recurso ou os direitos NTFS para a localização do ficheiro armazenado pode analisar os respetivos conteúdos e, possivelmente, discernir detalhes importantes sobre o cliente, para que seja possível comprometer a segurança.|  
|Restrinja os direitos administrativos locais no computador cliente|Um utilizador com direitos administrativos locais pode enviar dados inválidos como informações de inventário.|  

### <a name="security-issues-for-software-inventory"></a>Problemas de segurança para inventário de software  
 Recolher o inventário expõe potenciais vulnerabilidades. Os atacantes podem efetuar as seguintes tarefas:  

- Enviar dados inválidos, que serão aceites pelo ponto de gestão mesmo quando a definição de cliente de inventário de software está desativada e a recolha de ficheiros não está ativada.  

- Enviar excessivamente grandes quantidades de dados num único ficheiro e em muitos ficheiros, o que poderá provocar denial of service.  

- Aceda à informação de inventário de acesso à medida que é transferida para o Gestor de Configuração.  

  Se os utilizadores souberem que é possível criar um ficheiro oculto denominado **Skpswi.dat** e colocá-lo na raiz de uma unidade de disco rígido do cliente para excluí-lo do inventário de software, não será possível recolher dados de inventário de software a partir desse computador.  

  Dado que um utilizador com privilégios administrativos locais pode enviar qualquer informação como dados de inventário, não considere os dados de inventário que são recolhidos pelo Gestor de Configuração como autoritários.  

  O inventário de software está ativado por predefinição como uma definição de cliente.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informações de privacidade para inventário de software  
 O inventário de hardware permite-lhe recuperar qualquer informação que esteja armazenada no registo e no WMI nos clientes do Gestor de Configuração. O inventário de software permite-lhe detetar todos os ficheiros de um tipo especificado ou recolher todos os ficheiros especificados a partir dos clientes. O Asset Intelligence melhora as capacidades de inventário ao expandir o inventário de hardware e software e ao adicionar novas funcionalidades de gestão de licenças.  

 O inventário de hardware está ativado por predefinição como uma definição de cliente e as informações da WMI recolhidas são determinadas pelas opções que selecionar. O inventário de software está ativado por predefinição, mas os ficheiros não são recolhidos por predefinição. A recolha de dados do Asset Intelligence é ativada automaticamente, embora possa selecionar as classes de relatório de inventário de hardware a ativar.  

 As informações de inventário não são enviadas à Microsoft. As informações de inventário são armazenadas na base de dados do Gestor de Configuração. Quando os clientes utilizam HTTPS para ligar a pontos de gestão, os dados de inventário enviados para o site são encriptados durante a transferência. Se os clientes utilizarem HTTP para ligar a pontos de gestão, terá a opção para ativar a encriptação de inventário. Os dados de inventário não são armazenados em formato encriptado na base de dados. As informações são retidas na base de dados até serem eliminadas pelas tarefas de manutenção do site **Eliminar Histórico de Inventário Desatualizado** ou **Eliminar Ficheiros Recolhidos Desatualizados** todos os 90 dias. Pode configurar o intervalo de eliminação.  

 Antes de configurar o inventário de hardware, o inventário de software, a recolha de ficheiros ou a recolha de dados do Asset Intelligence, considere os requisitos de privacidade.  
