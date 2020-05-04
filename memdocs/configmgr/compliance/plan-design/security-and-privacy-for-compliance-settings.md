---
title: Segurança e privacidade para as definições de conformidade
titleSuffix: Configuration Manager
description: Conheça as melhores práticas de segurança para as definições de conformidade no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: eae705b97add7515403549eb668e68f1489d6756
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712149"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Segurança e privacidade para configurações de conformidade no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


## <a name="security-best-practices-for-compliance-settings"></a>Procedimentos recomendados de segurança para definições de compatibilidade  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Não monitorize dados confidenciais.|Para ajudar a evitar a divulgação de informações, não configure os itens de configuração para monitorizar informações potencialmente confidenciais.|  
|Não configure regras de conformidade que utilizem dados passíveis de serem modificados por utilizadores finais.|Se criar uma regra de compatibilidade com base em dados que os utilizadores podem modificar, como definições de registo para opções de configuração, os resultados de compatibilidade não serão fiáveis.|  
|Importe pacotes de configuração do Microsoft System Center e outros dados de configuração de origens externas apenas se tiverem uma assinatura digital válida de um fabricante fidedigno.|Os dados de configuração publicados podem ser assinados digitalmente para que possa verificar a origem da publicação e certificar-se de que os dados não foram adulterados. Se a verificação da assinatura digital falhar, é apresentado um aviso e é-lhe perguntado se pretende continuar com a importação. Não importe dados não assinados se não conseguir verificar a origem e a integridade dos dados.|  
|Implemente controlos de acesso para proteger computadores de referência.|Certifique-se de que quando um utilizador administrativo configura uma definição de registo ou de sistema de ficheiros navegando para um computador de referência, o computador de referência não tinha sido comprometido.|  
|Proteja o canal de comunicação ao navegar para um computador de referência.|Para evitar a adulteração dos dados quando estes são transferidos através da rede, utilize a segurança do Protocolo de Internet (IPsec) ou o bloco de mensagens do servidor (SMB) entre o computador que executa a consola do Gestor de Configuração e o computador de referência.|  
|Restrinja e monitorize os utilizadores administrativos a quem é concedida a função de segurança baseada em funções Gestor de Definições de Compatibilidade|Os utilizadores administrativos a quem é concedida a função **Gestor de Definições de Compatibilidade** podem implementar itens de configuração em todos os dispositivos e em todos os utilizadores na hierarquia. Os itens de configuração podem ser muito eficientes e podem incluir, por exemplo, scripts e reconfiguração do registo.|  

## <a name="privacy-information-for-compliance-settings"></a>Informações de privacidade para definições de compatibilidade  
 Pode utilizar definições de compatibilidade para avaliar se os dispositivos cliente são compatíveis com os itens de configuração que implementar em linhas de base de configuração. Algumas definições podem ser remediadas automaticamente se não forem compatíveis. As informações de conformidade são enviadas para o servidor do site pelo ponto de gestão e armazenadas na base de dados do site. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. As informações são retidas na base de dados até que a tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** as elimine todos os 90 dias. Pode configurar o intervalo de eliminação. As informações de conformidade não são enviadas à Microsoft.  

 Por predefinição, os dispositivos não avaliam as definições de compatibilidade. Além disso, tem de configurar os itens de configuração e as linhas de base de configuração e, em seguida, implementá-los nos dispositivos.  
