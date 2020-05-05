---
title: 'Instale um site utilizando os 1606 meios de base '
titleSuffix: Configuration Manager
description: Instale ou atualize para o LTSB para o System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722803"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Instalar e atualizar com os meios de base da versão 1606

*Aplica-se a: System Center Configuration Manager (ramo de manutenção a longo prazo)*

Quando executar a configuração a partir do meio de linha de base da versão 1606 para O Gestor de Configuração, pode instalar um site de sucursal de manutenção a longo prazo do System Center Configuration Manager.

Os meios de base estão disponíveis em DVD como parte do Microsoft System Center 2016, ou da versão de longo prazo do System Center Configuration Manager 1606. Para saber mais sobre os meios de base, consulte as [versões Baseline e update](../servers/manage/updates.md#bkmk_Baselines).


Quando utiliza os meios de base da versão 1606, o site para o que instala ou atualiza é:
- Um *site da Filial Atual* que é equivalente a um site que foi instalado pela primeira vez usando os 1511 meios de base, e depois atualizado para a versão 1606 mais o rollup hotfix de 1606 - KB3186654.
- Um *site LTSB* equivalente ao site da Filial Atual que executa a versão 1606 mais o rollup de 1606 - KB3186654. Os meios de base já incluem o rollup hotfix.  Mas, o LTSB não suporta todas as funcionalidades ou capacidades disponíveis com o Ramo Atual, conforme detalhado na [Introdução ao Ramo de Manutenção a Longo Prazo do Gestor de Configuração do Centro de Sistemas.](introduction-to-the-ltsb.md)

Se não estiver familiarizado com os diferentes ramos do Gestor de Configuração, consulte [qual o ramo do Gestor de Configuração que devo utilizar.](which-branch-should-i-use.md)




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Alterações à Configuração com os 1606 meios de base
Os meios de base de 1606 introduzem as seguintes alterações à Configuração para O Gestor de Configuração.

### <a name="branch-and-edition"></a>Ramo e edição
Ao executar a Configuração, é agora apresentada uma página de Licenciamento onde pode selecionar o ramo de Gestor de Configuração que pretende instalar. Pode escolher o Ramo Atual ou o LTSB como uma instalação licenciada, ou pode escolher uma edição de Avaliação da Sucursal Atual como uma instalação não licenciada.

Para mais informações, consulte [Licenciamento e balcões para Gestor de Configuração](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiração da Garantia de Software
Durante a Configuração, tem a opção de introduzir o valor da data de validade da Garantia de **Software.** Este é um valor opcional que pode especificar como um lembrete conveniente.

> [!NOTE]
> A Microsoft não valida a data de validade que introduz e não utilizará esta data para validação da licença.  Em vez disso, pode usá-lo como um lembrete da sua data de validade. Isto é útil porque o Gestor de Configuração verifica periodicamente novas atualizações de software oferecidas online, e o seu estado de licença de garantia de software deve ser atual para ser elegível para usar estas atualizações adicionais.    

- Pode especificar o valor da data na página chave do **produto** do Assistente de Configuração quando executar a Configuração a partir do meio de base do Gestor de Configuração 1606.
- Também pode especificar esta data selecionando as **definições de hierarquia Properties** > **Licensing** na consola 'Gestor de Configuração'.

Para mais informações, consulte "Acordos de Garantia de Software" em [Licenciamento e balcões para Gestor](learn-more-editions.md)de Configuração .


### <a name="additional-pre-upgrade-configurations"></a>Configurações adicionais de pré-actualização
Antes de iniciar uma atualização do System Center 2012 Configuration Manager para o LTSB, deve tomar os seguintes passos adicionais como parte da lista de verificação pré-actualização.  
Desinstale as funções do sistema do site que o LTSB não suporta:
- Ponto de sincronização do Asset Intelligence
- Conector do Microsoft Intune
- Pontos de distribuição baseados na nuvem

Para mais informações, consulte Upgrade para 'Gestor de [Configuração'.](../servers/deploy/install/upgrade-to-configuration-manager.md)


### <a name="new-scripted-installation-options"></a>Novas opções de instalação scriptd
O suporte de linha base da versão 1606 suporta uma nova chave de ficheiros de script sem supervisão para instalações escritas de um novo site de alto nível. Isto aplica-se à instalação de um novo local primário autónomo ou à adição de um site de administração central como parte de um cenário de expansão do site.

Ao utilizar um script não acompanhado para instalar uma sucursal licenciada, deve adicionar a seguinte secção, nomes-chave e valores à secção Opções do seu script. Não é necessário utilizar estes valores para escrever a instalação de uma edição de Avaliação do Ramo Atual:  

 **SabranchOptions**
- **Nome-chave: SAActive**
  - Valores: 0 ou 1.  
  - Detalhes: 0 instala uma edição de Avaliação não licenciada da Current Branch, e 1 instala uma edição licenciada.   

- **Ramo atual**
  - Valores: 0 ou 1.  
  - Detalhes: 0 instala o Ramo de Manutenção a Longo Prazo e 1 instala o Ramo Atual.  

Por exemplo, para instalar uma edição licenciada da Filial Atual que utilizaria:

**Nome-chave: SabranchOptions**
- **SAActive = 1**
- **Ramo atual = 1**


> [!IMPORTANT]  
> **A SABranchOptions** só funciona com a Configuração a partir dos meios de base. Não se aplica quando executa a configuração do CD. Última pasta de um site que instalou anteriormente utilizando os meios de base da versão 1606.
>
> **O SABranchOptions** não se aplica a atualizações escritas do System Center 2012 Configuration Manager e resulta sempre no Ramo Atual.

Para mais informações, consulte Utilize uma linha de comando para instalar sites do Gestor de [Configuração](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Instalar um novo site
Quando utilizar os 1606 meios de base para instalar um novo local de cada ramo, utilize os procedimentos de planeamento, preparação e instalação do site documentados no tópico de sites do Gestor de Configuração de [Instalação](../servers/deploy/install/installing-sites.md) com a adição das seguintes considerações para a Configuração:

- Durante a Configuração deve escolher o ramo do Gestor de Configuração que pretende instalar e pode especificar detalhes para o seu acordo de Garantia de Software.
- Todos os sítios da mesma hierarquia devem gerir o mesmo ramo. Não é suportado ter uma hierarquia com uma mistura de LTSB e Filial Atual em diferentes sites.
- Nova instalação escrita. Para mais informações, consulte "Novas opções de instalação escritas" no início deste artigo.

## <a name="expand-a-stand-alone-primary-site"></a>Expandir um local primário autónomo
Pode expandir um local primário autónomo que gere o LTSB.  O processo não é diferente do utilizado para um sítio do Ramo Atual com uma ressalva:

- Ao instalar o novo site da administração central, deve utilizar a Configuração a partir dos meios de origem originais utilizados para instalar o site LTSB. A executar a configuração do CD. A última pasta para este cenário não é suportada.

Para obter mais informações sobre a expansão de um site, consulte "Expandir um local primário autónomo" na [Instalação de um site utilizando o Assistente de Configuração](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Upgrade do System Center 2012 Diretor de Configuração
Quando atualizar a partir do System Center 2012 Configuration Manager, utilize o planeamento, preparação e procedimentos do site conforme documentado no tópico de Upgrade para 'Gestor de [Configuração',](../servers/deploy/install/upgrade-to-configuration-manager.md) mas com as seguintes alterações:

**Upgrade para o Ramo Atual:**
- Durante a Configuração, deve escolher a Sucursal Atual e pode especificar detalhes para o seu acordo de Garantia de Software.
- Nova instalação escrita. Para mais informações, consulte "Novas opções de instalação escritas" no início deste artigo.

**Upgrade para o LTSB:**  
- Passos adicionais a seguir na lista de verificação pré-actualização.
- Durante a Configuração tem de escolher o LTSB e pode especificar detalhes para o seu acordo de Garantia de Software.
- Só é possível atualizar um site que gere o System Center 2012 Configuration Manager com o Service Pack 1, System Center 2012 Configuration Manager com Service Pack 2, System Center 2012 R2 Configuration Manager com Service Pack 1, ou System Center 2012 R2 Configuration Manager sem pacote de serviço.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Caminhos de upgrade no local para os meios de base de 1606
Pode utilizar os 1606 meios de base para atualizar o seguinte para uma edição licenciada do Gestor de Configuração:
- System Center 2012 R2 Configuration Manager com Pacote de Serviço 1
- System Center 2012 R2 Configuration Manager sem pacote de serviço (isto requer a utilização dos meios de base para a versão 1606 que foi relançado no dia 15 de dezembro de 2016.)
- System Center 2012 Gestor de Configuração com Pacote de Serviço 2
- System Center 2012 Configuration Manager com Service Pack 1 (isto requer a utilização dos meios de base para a versão 1606 que foi relançado no dia 15 de dezembro de 2016.)


Também pode utilizar este meio de comunicação para atualizar uma edição de Avaliação não licenciada da Current Branch para uma versão totalmente licenciada da Filial Atual.

Estes meios de comunicação não suportam a atualização de:
- Outras versões do System Center 2012 Configuration Manager.
- Gestor de Configuração 2007 ou mais cedo.
- Uma instalação de candidato de lançamento do Gestor de Configuração.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre o CD. Última pasta e o LTSB
Seguem-se as limitações na utilização dos meios de comunicação que o Gestor de Configuração cria no CD. Última pasta no servidor do site. Estes limites aplicam-se aos sites que executam o LTSB:

Media no CD. A última pasta é suportada para:
- Recuperação do local.
- Manutenção do local.
- Instalação de locais primários para crianças adicionais.

Media no CD. A pasta mais recente não é suportada para:  
- Instalar um site de administração central como parte de um cenário de expansão do site.

Para mais informações, consulte [o CD. Última pasta.](../servers/manage/the-cd.latest-folder.md)

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Backup, recuperação e manutenção do site para o LTSB
Para fazer backup, recuperar ou executar a manutenção do site num site que gere o LTSB, utilize as orientações e procedimentos de [Backup e recuperação para O Gestor](../servers/manage/backup-and-recovery.md)de Configuração .  

Utilize a configuração do Gestor de Configuração a partir do CD. Última pasta da cópia de segurança do seu site LTSB.
