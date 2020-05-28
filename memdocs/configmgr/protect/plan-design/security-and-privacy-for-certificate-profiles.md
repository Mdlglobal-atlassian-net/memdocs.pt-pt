---
title: Segurança e privacidade de perfis de certificado
titleSuffix: Configuration Manager
description: Conheça as melhores práticas de segurança para gerir perfis de certificados para utilizadores e dispositivos no Gestor de Configuração.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3825ef9b9b1efd576a31742e0fdbe7c2bc3b1628
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906855"
---
# <a name="security-and-privacy-for-certificate-profiles-in-configuration-manager"></a>Segurança e privacidade para perfis de certificado sintetmente em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Procedimentos Recomendados de Segurança para Perfis de Certificado  
 Utilize os seguintes procedimentos recomendados de segurança ao gerir perfis de certificado para utilizadores e dispositivos.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Identifique e siga os eventuais procedimentos recomendados de segurança do Serviço de Inscrição de Dispositivos de Rede, que incluem a configuração do Web site do Serviço de Inscrição de Dispositivos de Rede nos Serviços de Informação Internet (IIS) para que exija SSL e ignore os certificados de cliente.|Para mais informações, consulte [a Orientação](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11))do Serviço de Inscrição de Dispositivos de Rede .|  
|Ao configurar os perfis de certificado SCEP, escolha as opções mais seguras suportadas pelos dispositivos e pela infraestrutura.|Identifique, implemente e siga os procedimentos de segurança eventualmente recomendados para os dispositivos e para a infraestrutura.|  
|Especifique manualmente a afinidade dispositivo/utilizador em vez de permitir que os utilizadores identifiquem o respetivo dispositivo primário. Além disso, não ative a configuração baseada na utilização.|Se clicar na opção **Permitir inscrição de certificados apenas no dispositivo primário dos utilizadores** num perfil de certificado SCEP, não considere autoritativas as informações recolhidas junto dos utilizadores ou do dispositivo. Se implementar perfis de certificado SCEP com esta configuração e um utilizador administrativo fidedigno não especificar a afinidade dispositivo/utilizador, os utilizadores não autorizados poderão obter privilégios elevados e certificados para autenticação.<br /><br /> **Nota:** Se ativar a configuração baseada na utilização, esta informação é recolhida utilizando mensagens estatais que não são protegidas pelo Gestor de Configuração. Para ajudar a atenuar esta ameaça, utilize a assinatura SMB ou IPsec entre computadores cliente e o ponto de gestão.|  
|Não adicione permissões de Leitura e Inscrição para utilizadores aos modelos de certificado ou configure o ponto de registo de certificados para ignorar a verificação do modelo de certificado.|Embora o Gestor de Configuração suporte a verificação adicional se adicionar as permissões de segurança de Read and Enroll para os utilizadores, e pode configurar o ponto de registo do certificado para não verificar se a autenticação não é possível, nenhuma configuração é uma boa prática de segurança. Para mais informações, consulte [O Planeamento para obter permissões](../../protect/plan-design/planning-for-certificate-template-permissions.md)de modelo de certificado para perfis de certificado .|  

## <a name="privacy-information-for-certificate-profiles"></a>Informações de Privacidade para Perfis de Certificado  
 Poderá utilizar perfis de certificado para implementar certificados de autoridade de certificação (AC) de raiz e de cliente, avaliando em seguida se esses dispositivos se tornam compatíveis após a aplicação dos perfis. O ponto de gestão envia informações de conformidade para o servidor do site, e o Gestor de Configuração armazena essa informação na base de dados do site. As informações de conformidade incluem propriedades de certificado, tais como o nome do requerente e o thumbprint. As informações são encriptadas quando os dispositivos as enviam para o ponto de gestão, mas não são armazenadas em formato encriptado na base de dados do site. A base de dados mantém as informações até que a tarefa de manutenção do site **Eliminar Dados de Gestão de Configuração Desatualizados** as elimine, após o intervalo predefinido de 90 dias. Pode configurar o intervalo de eliminação. As informações de conformidade não são enviadas à Microsoft.  

 Os perfis de certificado sustem informações que o Gestor de Configuração recolhe através da descoberta. Para obter mais informações sobre informações sobre privacidade para descoberta, consulte a secção **Informações** de Privacidade para Descoberta em Segurança e privacidade para O Gestor de [Configuração](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Os certificados emitidos para utilizadores ou dispositivos poderão permitir o acesso a informações confidenciais.  

 Por predefinição, os dispositivos não avaliam os perfis de certificado. Além disso, terá de configurar os perfis de certificado e implementá-los para os utilizadores ou dispositivos.  

 Antes de configurar os perfis de certificado, considere os requisitos de privacidade.  
