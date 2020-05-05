---
title: Ferramenta de Monitorização da Implementação
titleSuffix: Configuration Manager
description: Utilize a Ferramenta de Monitorização de Implementação para resolver as implementações de software num cliente do Gestor de Configuração.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723377"
---
# <a name="deployment-monitoring-tool"></a>Ferramenta de Monitorização da Implementação

*Aplica-se a: Gestor de Configuração (ramo atual)*

A ferramenta de monitorização de implementação é uma das ferramentas do Gestor de [Configuração.](tools.md) É uma interface gráfica de utilizador projetada para ajudar na aplicação de resolução de problemas, atualização de software e implementações de linha de base de configuração num cliente do Gestor de Configuração. A ferramenta é apenas de leitura, uma vez que não muda nenhum estado sobre o cliente. Pode usá-lo com segurança para diagnosticar cenários comuns de implantação.


## <a name="features"></a>Funcionalidades

- Executa-o como administrador para resolver problemas com um cliente local.  

- Implantações de problemas num cliente remoto. Lance a ferramenta e ligue-se a uma máquina remota como administrador.  

- Exportar para XML todos os dados recolhidos na ferramenta. Partilhe o ficheiro XML com outros e use-o como uma plataforma comum para falar sobre implementações de resolução de problemas.  

- Importar dados previamente exportados para uma máquina diferente e usá-lo para executar a ferramenta em modo offline.   


## <a name="usage"></a>Utilização

A ferramenta de monitorização de implementação suporta apenas a interface gráfica do utilizador. Para lançar a ferramenta, execute o **DeploymentMonitoringTool.exe** como administrador. Há três pontos de vista:  

- **Propriedades**do Cliente : Uma lista de atributos úteis sobre o dispositivo e o cliente do Gestor de Configuração. Esta vista é o padrão.   

- **Implementações**: Ver todas as implementações atualmente direcionadas. Selecione uma implementação no painel de resultados para ver mais informações no painel de detalhes.  

- **Todas as Atualizações**: Veja todas as atualizações de software e o seu estado.  

Para copiar dados em qualquer vista, selecione uma célula e prima **CTRL** + **C**.


### <a name="actions-menu"></a>Menu de ações

As seguintes ações estão disponíveis no menu **Ações:**  

- **Ligue-se à máquina remota:** Selecione um computador para ligar. Quando não especifica o nome de utilizador e a palavra-passe, utiliza as credenciais atuais. Clique em **Guardar** para ligar ao computador remoto.  

- **Dados de Exportação**: Selecione o ficheiro para escrever os dados e clique em **Guardar**. Utilize o ficheiro XML exportado para resolução remota de problemas num computador diferente.  

- **Dados de Importação**: Selecione um ficheiro para importar para a ferramenta.  

- **Ver Registo**: Abre um ficheiro de registo associado, dependendo da vista:  
    - Propriedades do Cliente:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Implantações:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Todas as Atualizações:`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Consulte também

- [Implementar aplicações](../../apps/deploy-use/deploy-applications.md)
- [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md)
- [Implementar linhas de base da configuração](../../compliance/deploy-use/deploy-configuration-baselines.md)
