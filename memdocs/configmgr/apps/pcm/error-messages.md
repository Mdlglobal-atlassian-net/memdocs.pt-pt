---
title: Mensagens de erro
titleSuffix: Configuration Manager
description: Conheça as mensagens de erro do Gestor de Conversão de Pacotes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709888"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Referência técnica para mensagens de erro do Gestor de Conversão de Pacotes

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--1357861-->

Este artigo descreve as mensagens de erro que o Gestor de Conversão de Pacotes exibe. Inclui também as possíveis causas do erro e métodos para corrigir o erro. O Gestor de Conversão de Pacotes regista mensagens de erro em **PCMTrace.log**. Para obter mais informações, incluindo como controlar o nível de verbosidade, consulte [ficheiros De Registo](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>A criação de candidaturas falhou com a seguinte exceção

A exceção especificada ocorreu durante a submissão do objeto de aplicação ao servidor 'Gestor de Configuração'.

Verifique as suas permissões no 'Gestor de Configuração', valide a sua conectividade e, em seguida, volte a tentar. Se essas ações não corrigirem o problema, examine o ficheiro **PCMtrace.log** (verbosity level 4) e **O SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Erro de conversão – aplica-se a um estatuto de transformação de pacote

Durante a conversão do pacote ocorreu uma exceção geral. Procure no ficheiro **PCMtrace.log** (verbosity level 4).

Verifique as permissões do utilizador para a partilha da rede (fonte de dados do pacote), valide a sua conectividade e, em seguida, volte a tentar. Se essas ações não resolverem o problema, examine o ficheiro **PCMtrace.log** (verbosity level 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Não encontrou um pacote convertido e a sua aplicação resultante nas saídas de fluxo de trabalho
A aplicação (pacote/programa convertido) foi eliminada.

Modifique o pacote/programa dependente para garantir que o pacote/programa dependente existe.


#### <a name="objects-were-not-created-successfully"></a>Objetos não foram criados com sucesso
Há várias causas possíveis.

Verifique as suas permissões no 'Gestor de Configuração', valide a sua conectividade e, em seguida, volte a tentar. Se essas ações não corrigirem o problema, examine o ficheiro **PCMtrace.log** (verbosity level 4) e o ficheiro **SMSProv.log.**


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Por favor, feche o assistente e resolva quaisquer problemas com o pacote selecionado. Consulte PCMTrace.Log para mais detalhes
Há várias causas possíveis.

Verifique as suas permissões no 'Gestor de Configuração', valide a sua conectividade e, em seguida, volte a tentar. Se essas ações não corrigirem o problema, examine o ficheiro **PCMtrace.log** (verbosity level 4) e o ficheiro **SMSProv.log.**


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Alguns tipos de implantação estão a faltar métodos de deteção. Todos os tipos de implementação devem ter métodos de deteção
Faltam métodos de deteção do programa.

Adicione um ou mais métodos de deteção durante o processo **de Correção e Conversão.**


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Houve um erro preparando o pacote para conversão
Há várias causas possíveis.

Verifique as suas permissões no 'Gestor de Configuração', valide a sua conectividade e, em seguida, volte a tentar. Se essas ações não corrigirem o problema, examine o ficheiro **PCMtrace.log** (verbosity level 4) e o ficheiro **SMSProv.log.**


