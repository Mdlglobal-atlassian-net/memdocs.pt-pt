---
title: Dados de diagnóstico e utilização para 1910
titleSuffix: Configuration Manager
description: Conheça os dados específicos que o Gestor de Configuração recolhe em cada nível na versão 1910.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3ce6b9a-7d54-4374-9b7a-f017f872bd6f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95fb434f94ece47a0e896e5cf1913f3f67cac7d0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720346"
---
# <a name="diagnostic-and-usage-data-for-version-1910"></a>Dados de diagnóstico e utilização para a versão 1910

*Aplica-se a: Gestor de Configuração (ramo atual)*

As seguintes secções fornecem detalhes adicionais sobre os dados recolhidos em cada nível. Para obter mais informações sobre os níveis e como alterá-los, consulte [Níveis de dados de utilização de diagnóstico](levels-overview.md).

As alterações das versões anteriores são notadas com ***[New]***, ***[Removido],*** ou ***[Move]***. ***[Removed]***

> [!IMPORTANT]
> O Gestor de Configuração não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis Básico ou Melhorado. Qualquer recolha desta informação a nível completo não é propositada. Está potencialmente incluído em informações avançadas de diagnóstico, como ficheiros de registo ou instantâneos de memória. A Microsoft não utiliza estas informações para o identificar, contactar ou desenvolver publicidade.

## <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nível 1 - Básico

Para a versão 1910 do Gestor de Configuração, este nível inclui os seguintes dados:

- Estatísticas sobre ligações de consola do Gestor de Configuração: versão OS, idioma, SKU e arquitetura, memória do sistema, contagem lógica de processadores, id do site de ligação, versões instaladas .NET, pacotes de idiomas de consola e nível de autenticação capaz

- Contagens básicas de aplicações e implementação: aplicações totais, aplicações totais com vários tipos de implementação, aplicações totais com dependências, aplicações supersed totais e contagem de tecnologias de implementação em uso

- Dados da hierarquia do site do Gestor de Configuração Básico: lista de site, tipo, versão, estado, contagem de clientes e fuso horário

- Configuração básica da base de dados: processadores, tamanho de memória, definições de memória, configuração da base de dados do Gestor de Configuração, tamanho da base de dados do Gestor de Configuração, configuração do cluster, configuração de vistas distribuídas e versão de rastreio de alterações  

- Estatísticas básicas de descoberta: contagem de descobertas, tamanhos mínimo/máximo/médio do grupo, e quando o site está funcionando inteiramente com Serviços de Diretório Ativo Azure

- Informações básicas sobre as versões de clientes antimalware

- Contagem básica de implementação de oso de imagens

- Informações básicas do servidor do sistema do site: funções do sistema do site utilizadas, estado da Internet e SSL, OS, processadores, máquina física ou virtual, e utilização da elevada disponibilidade do servidor do site

- Esquema de base de dados do Gestor de Configuração (hash de todas as definições de objeto)

- Nível configurado para diagnósticos e dados de utilização, modo on-line ou offline, e configuração de atualização rápida

- Conde de línguas e locais de cliente

- Contagem de versões de clientes do Gestor de Configuração, versões DE Os e Versões do Office

- Contagem dos sistemas operativos para dispositivos e políticas geridos definidos pelo Conector de Intercâmbio

- Contagem de dispositivos Windows 10 por ramo, construção e floresta única de Diretório Ativo  

- Contagem de clientes do Windows 10 que usam a Atualização do Windows para Negócios  

- Métricas de desempenho da base de dados: informações de processamento de replicação, procedimentos armazenados por processador e utilização do disco

- Tipos de pontos de distribuição e pontos de gestão e informações básicas de configuração: protegidos, pré-encenados, PXE, multicast, estado SSL, pontos de distribuição pull/peer, ativados por MDM e ssl-habilitados

- Lista hashed de extensões para administrar páginas de propriedade de consola e assistentes

- Informações de configuração:  

  - Construir, instalar tipo, pacotes de idiomas, funcionalidades que permitiu

  - Utilização pré-libertação, tipo de meio de configuração, tipo de ramo  

  - Data de validade da garantia de software  

  - Atualizar o estado e os erros de implementação do pack, transferir progressos e erros pré-requisitos

  - Utilização do anel rápido de atualização  

  - Versão do script pós-upgrade  

- Versão SQL, nível de pacote de serviço, edição, ID de colagem e conjunto de caracteres  

- Diagnósticos e estatísticas de dados de utilização: quando executado, tempo de execução, erros  

- Se a descoberta da rede está ativada ou desativada  

- Contagem de clientes juntou-se ao Diretório Ativo azure  

- Contagem de implementações faseadas criadas por tipo  

- Contagem de clientes de interoperabilidade alargada  

- Lista hashed de propriedades de inventário de hardware mais de 255 caracteres  

- Contagem de clientes por método de inscrição de cogestão  

- Estatísticas de erro para inscrição em cogestão  

- Contagem de clientes por idade do Windows OS, ao intervalo de três meses mais próximo  

- 10 nomes de processadores usados em clientes e servidores  

- Contagem e taxas de processamento dos objetos chave Do Gestor de Configuração: registos de descoberta de dados (DDR), mensagens de estado, mensagens de estado, inventário de hardware, inventário de software e contagem geral de ficheiros em caixas de entrada  

- Informações sobre o desempenho do servidor do site e do processador  

- Informações de utilização de tempo e memória para os processos do servidor do Site do Gestor de Configuração  

- Contagem de falhas para processos de servidor de site do Gestor de Configuração e ID de assinatura Watson, se disponível  

- Lista hashed das principais consultas SQL por uso de memória e contagem de bloqueio  

- Estatísticas de utilização agregadas de cogestão: número de clientes já inscritos, número de clientes inscritos, número de clientes pendentes de inscrição, clientes que recebem política, estados de carga de trabalho, tamanhos de recolha piloto/exclusão e erros de inscrição  

- Existência de extensões do lado do servidor microsoft BitLocker Administration e Monitoring (MBAM)  

- Contagem de aplicações categorizadas e não categorizadas para inteligência de ativos

- Estado e saúde do serviço administrativo

- Hash de principais atributos do site (ID do site, ID do corretor SQL e chave de troca de site)

- ***[Novo]*** Contagem de instalações do Microsoft Edge

## <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nível 2 - Avançado

Para a versão 1910 do Gestor de Configuração, este nível inclui os seguintes dados:

### <a name="application-management"></a>Gestão de aplicações  

- Requisitos da aplicação: contagem de condições incorporadas referenciadas pela tecnologia de implantação  

- Supersedência da aplicação, profundidade máxima da cadeia  

- Estatísticas de aprovação de aplicações e frequência de utilização  

- Estatísticas do tamanho do conteúdo da aplicação  

- Informações de implementação da aplicação: utilização da instalação versus desinstalação, requer aprovação, interação do utilizador ativada/desativada, dependência, supersedência e contagem de utilização da funcionalidade de comportamento de instalação  

- Tamanho da política de aplicação e estatísticas de complexidade  

- Estatísticas de pedidos de aplicação disponíveis  

- Informações básicas de configuração para pacotes e programas: opções de implementação e bandeiras de programas  

- Informações básicas de utilização/segmentação para tipos de implementação: utilizador versus dispositivo direcionado, necessário versus disponível, e aplicações universais  

- Contagem de ambientes de App-V e propriedades de implementação  

- Contagem da aplicabilidade da aplicação por OS  

- Contagem de aplicações referenciadas numa sequência de tarefas  

- Contagem de marcas distintas para catálogo de aplicações  

- Contagem de 365 aplicações criadas com recurso a painel de instrumentos  

- Contagem de pacotes por tipo  

- Contagem de implementações de pacote/programa  

- Contagem de licenças de aplicação licenciadas para Windows 10  

- Contagem dos tipos de implementação do Instalador do Windows desinstalando as definições de conteúdo  

- Contagem da Microsoft Store para aplicações empresariais e estatísticas de sincronização: tipos resumidos de apps, estatuto de aplicação licenciada e número de aplicações licenciadas online e offline  

- Tipo e duração da janela de manutenção  

- Número mínimo/máximo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo  

- Códigos de erro de instalação de aplicação mais comuns através da tecnologia de implementação  

- Opções de configuração MSI e conta  

- Estatísticas sobre a interação do utilizador final com a notificação para implementações de software necessárias  

- Uso universal de acesso a dados, como criado  

- Estatísticas de afinidade de dispositivos de utilizador agregados  

- Utilizadores primários max e médios por dispositivo  

- Aplicação uso de condição global por tipo  

- Configuração de personalização do Centro de Software  

- Prontidão e contagens do Gestor de Conversão de Pacotes  

- Contagem dos métodos de deteção de aplicações por tipo  

- Contagem de erros de execução da aplicação  

- Propriedades do instalador MSI  

- Estatísticas dos pedidos de instalação de utilizadores  

- Estatísticas agregadas sobre a utilização da funcionalidade de aprovação de e-mail  

- Contagem de ficheiros, tamanho de conteúdo, contagem de serviços e contagem de ação personalizada de MSIs no catálogo de aplicações  

- Contagem de dispositivos pelo Estado de prontidão do Office ProPlus

- Estatísticas agregadas sobre a utilização de grupos de aplicação

- Estatísticas agregadas de add-ins do Office, utilização do Kit de Ferramentas de Prontidão do Escritório e contagens de clientes com o Office 365 ProPlus

- ***[Novo]*** Estatísticas agregadas sobre a saúde add-in do Office

- ***[Novo]*** Contagem e tamanho das coleções piloto do Office Pro Plus

### <a name="client"></a>Cliente  

- Versão cliente de Tecnologia de Gestão Ativa (AMT)  

- IDADE BIOS em anos  

- Contagem de dispositivos com bota segura ativada  

- Contagem de dispositivos por estado tpm  

- Atualização automática do cliente: configuração de implementação incluindo a pilotagem do cliente e o uso de exclusão (cliente de interoperabilidade alargada)  

- Configuração do tamanho do cache do cliente  

- Erros de descarregamento de implementação de clientes  

- Estatísticas de saúde do cliente e resumo de emissão de topo por versão cliente, componente, SO e carga de trabalho  

- Estado de ação de operação de notificação de clientes: quantas vezes cada um é executado, número máximo de clientes direcionados e taxa média de sucesso  

- Contagem de instalações de cliente a partir de cada tipo de localização de origem  

- Contagem de falhas de instalação de cliente  

- Contagem de dispositivos virtualizados por Hyper-V ou Azure  

- Contagem de ações do Centro de Software  

- Contagem de dispositivos ativados pela UEFI  

- Métodos de implantação utilizados para cliente e contagem de clientes por método de implementação  

- Lista/contagem de agentes de cliente ativados  

- Idade do OS em meses  

- Número de classes de inventário de hardware, regras de inventário de software e regras de recolha de ficheiros  

- Estatísticas para atestado de saúde de dispositivos: códigos de erro mais comuns, número de servidores no local e contagens de dispositivos em vários estados  

- Contagem de dispositivos por navegador padrão  

- Contagem de certificados de autenticação de servidor gerados pelo Gestor de Configuração  

- Contagem de dispositivos Microsoft Surface por modelo  

- Contagem de falhas de verificação de saúde do cliente por tipo de emissão

### <a name="cloud-services"></a>Serviços Cloud  

- Estatísticas de descoberta de diretórios ativos azure  

- Estatísticas de configuração e utilização do Gateway de Gestão de Nuvem: contagens de regiões e ambientes, e estatísticas de autenticação/autorização  

- Contagem de aplicações e serviços de Diretório Ativo Azure ligados ao Gestor de Configuração  

- Contagem de coleções sincronizadas com Azure Log Analytics  

- Contagem de Conectores de Atualização Analytics  

- Se o conector de nuvem Azure Log Analytics está ativado  

- Contagem de pontos de distribuição de puxar com um ponto de distribuição em nuvem como uma localização de origem  

### <a name="cmpivot"></a>CMPivot

- Estatísticas de utilização da CMPivot  

- Contagem de consultas salvas da CMPivot  

- Contagem de consultas por tipo de entidade  

### <a name="co-management"></a>Cogestão  

- Horário de matrículas e estatísticas históricas  

- Contagem de clientes elegíveis para cogestão  

- Inquilino Associado da Microsoft Intune  

### <a name="collections"></a>Coleções  

- Utilização de ID de recolha (não ficando sem iDs)  

- Estatísticas de avaliação de cobrança: tempo de consulta, atribuído versus contagens não atribuídas, conta por tipo, capotamento de ID e utilização de regras  

- Coleções sem implantação  

- Contagem de coleções sincronizadas com Diretório Ativo Azure

### <a name="compliance-settings"></a>Definições de compatibilidade  

- Informação de base de configuração básica: contagem, número de implementações e número de referências  

- Estatísticas de erro de política de conformidade  

- Contagem de itens de configuração por tipo  

- Contagem de implementações que referenciam configurações incorporadas, incluindo a definição de remediação  

- Contagem de regras e implementações criadas para configurações personalizadas, incluindo a definição de remediação  

- Contagem dos modelos de inscrição de certificados simples (SCEP), VPN, Wi-Fi, certificado (.pfx) e modelos de política de conformidade  

- Contagem de certificadoS SCEP, VPN, Wi-Fi, certificado (.pfx) e implementações de política de conformidade por plataforma  

- Política do Windows Hello for Business (criada, implementada)  

- Contagem das políticas de navegador do Microsoft Edge implementadas  

- Contagem das políticas OneDrive (criadas, implementadas)

### <a name="content"></a>Conteúdo  

- Estatísticas do grupo de fronteira: quantos rápidos, quantos lentos, contagem por grupo, e relações de recuo  

- Informações do grupo de fronteira: contagem de fronteiras e sistemas de site que são atribuídos a cada grupo de fronteiras  

- Relações de grupo de fronteiras e configuração de recuo  

- Estatísticas de descarregamento de conteúdo de clientes  

- Contagem de limites por tipo  

- Contagem de clientes de cache de pares, estatísticas de uso e estatísticas parciais de descarregamento  

- Informação de configuração do Gestor de Distribuição: threads, retry delay, número de repetições e definições de ponto de distribuição de puxar  

- Informação de configuração de pontos de distribuição: utilização do cache do ramo e monitorização do ponto de distribuição  

- Informação do grupo de pontos de distribuição: contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição  

- Tipo de biblioteca de conteúdos, local ou remoto  

- Contagem de grupos de fronteira por configuração  

### <a name="endpoint-protection"></a>Endpoint Protection  

- Políticas de Proteção avançada de ameaças (ATP) do Microsoft Defender (anteriormente conhecida como Windows Defender ATP): contagem de políticas e se as políticas são implementadas.

- Contagem de alertas configurados para a função de Proteção de Pontofinal  

- Contagem de coleções que são selecionadas para aparecer no painel de proteção de Ponto Final  

- Contagem de políticas, implementações e clientes direcionados do Windows Defender Exploit Guard  

- Erros de implementação de proteção de pontos finais, contagem de códigos de erro da política de proteção do ponto final  

- Utilização da política de proteção de pontos finais e de firewall do Windows (número de políticas únicas atribuídas ao grupo). Estes dados não incluem qualquer informação sobre as definições incluídas na política.  

### <a name="migration"></a>Migração  

- Contagem de objetos migrados (utilização de assistente de migração)  

### <a name="mobile-device-management-mdm"></a>Mobile device management (MDM) (Gestão de dispositivos móveis [MDM])  

- Contagem de ações de dispositivos móveis emitidas: bloqueio, apoio de pinos, limpeza, aposentadoria e sincronização agora comandos  

- Contagem de políticas de dispositivos móveis  

- Contagem de dispositivos móveis O Gestor de Configuração gere e como os matriculou (a granel, baseado no utilizador)  

- Contagem de utilizadores que tenham vários dispositivos móveis matriculados  

- Horário de sondagens para dispositivos móveis e estatísticas para a duração do check-in do dispositivo móvel  

### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune resolução de problemas  

- Contagem e tamanho das ações do dispositivo (limpar, retirar, bloquear), dados de utilização e mensagens de dados que são replicadas para microsoft Intune  

- Contagem e dimensão do estado, estado, inventário, RDR, DDR, UDX, Estado inquilino, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM e mensagens de conformidade que são descarregadas a partir do Microsoft Intune  

- Estatísticas completas e delta de sincronização dos utilizadores para o Microsoft Intune  

### <a name="on-premises-mobile-device-management-mdm"></a>Gestão de dispositivos móveis (MDM) no local  

- Contagem de pacotes e perfis de inscrição em massa do Windows 10  

- Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  

### <a name="os-deployment"></a>Implementação de SO  

- Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

- Contagem de imagens de arranque por versão cliente do Gestor de Configuração  

- Contagem de imagens de arranque por versão do Windows PE  

- Contagem de políticas de upgrade de edição  

- Contagem de identificadores de hardware excluídos do PXE  

- Contagem da implantação do OS por versão OS  

- Contagem de atualizações de SO ao longo do tempo  

- Contagem de implementações de sequências de tarefas utilizando a opção de pré-descarregamento de conteúdos  

- Contagem de utilização da sequência de tarefas  

- Versão do Windows ADK instalada  

- Contagem de tarefas de manutenção de imagem  

- Contagem de máquinas importadas  

- Contagem de identificadores de hardware duplicados (endereço MAC e SMBIOS GUID) excluídos do PXE e registo de clientes

- Contagem de sequências de tarefas por tipo (implantação de OS ou sequência de tarefas genérica)

- Contagem de pacotes com definições de conteúdo pré-cache

### <a name="site-updates"></a>Atualizações do site  

- Versões de hotfixos instalados do Gestor de Configuração  

### <a name="software-updates"></a>Atualizações de Software  

- Deltas disponíveis e prazos que são usados em regras de implementação automática  

- Número médio e máximo de atribuições por atualização  

- Avaliação de atualização de cliente e agendas de análise  

- Classificações sincronizadas pelo ponto de atualização do software  

- Estatísticas de aplicação de patches de cluster  

- Configuração de atualizações expressas do Windows 10  

- Configurações que são usadas para planos de manutenção ativos do Windows 10  

- Contagem de atualizações do Office 365 implementadas  

- Contagem de controladores Microsoft Surface sincronizados  

- Contagem de grupos de atualização e atribuições  

- Contagem dos pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são direcionados com pacotes  

- Contagem de atualizações que são criadas e implementadas com system center update Publisher  

- Contagem de Atualizações do Windows para políticas empresariais criadas e implementadas  

- Estatísticas agregadas do Windows Update para configurações de Negócios  

- Número de regras de implantação automática ligadas à sincronização  

- Número de regras de implementação automática que criam atualizações novas ou acrescentam atualizações a um grupo existente  

- Número de regras de implementação automática que têm múltiplas implementações  

- Número de grupos de atualização e número máximo/mínimo/médio de atualizações por grupo  

- Número de atualizações e percentagem de atualizações que são implementadas, expiradas, sobrecarregadas, descarregadas e contêm EULAs  

- Estatísticas de equilíbrio de pontos de atualização de software  

- Agenda de sincronização de ponto de atualização de software  

- Número total/médio de coleções que têm implementações de atualizações de software e o número máximo/médio de atualizações implementadas  

- Atualizar códigos de erro de análise e contagem de máquinas  

- Versões de conteúdo de dashboard do Windows 10  

- Contagem de subscrições de catálogo de atualizações de software de terceiros e utilização  

- Contagem de atualizações de software implementadas com e sem conteúdo  

- Estatísticas agregadas sobre o número de atualizações da UUP que são necessárias, implantadas, expiradas, supersedee e descarregadas  

- Utilização de categorias de produtos UUP  

- Contagem de clientes que implementaram pelo menos uma atualização de qualidade uUP ou atualização de funcionalidadeu UUP  

- Códigos de erro da UUP superiores e contagem de dispositivos afetados  

- Lista de subscrições de catálogos de atualizações de software de terceiros

- Utilização de definições de manutenção wSUS

### <a name="sqlperformance-data"></a>Dados SQL/desempenho  

- Configuração e duração da resumição do site  

- Contagem das maiores tabelas de bases de dados  

- Estatísticas operacionais de descoberta (contagem de objetos encontrados)  

- Tipos de descoberta, habilitados e programadores (completos, incrementais)  

- SQL AlwaysOn replica informação, uso e estado de saúde  

- SQL alterar problemas de desempenho de rastreio, período de retenção e estado de auto-limpeza  

- Período de retenção de rastreio de alterações SQL  

- Estatísticas de desempenho da mensagem de estado e de estado, incluindo os tipos de mensagens mais comuns e mais caros  

- Estatísticas de tráfego de pontos de gestão (bytes totais enviados e recebidos por ponto final)  

- Medições de contador de desempenho de pontode gestão  

- Estatísticas de desempenho agregadas de chamadas feitas para pontos finais do Centro de Software no ponto de gestão

### <a name="miscellaneous"></a>Diversos  

- Configuração do ponto de serviço de armazém de dados, incluindo horário de sincronização, tempo médio e utilização de tabelas personalizadas  

- Contagem de scripts e estatísticas de execução/edição  

- Contagem de sites com Wake On LAN (WOL)  

- Relatóriode estatísticas de utilização e desempenho  

- Estatísticas de utilização faseadas  

- O item de insights de gestão conta e o progresso  

- Contagem de falhas para processos exclusivos do Gestor de Não-Configuração no servidor do site, e ID de assinatura Watson, se disponível  

- Estatísticas agregadas sobre erros de inscrição e utilização de Desktop Analytics

- Contagem de notificações não críticas das consolas

- Estatísticas agregadas do tempo de arranque do sistema por OS, fator de forma e tipo de unidade

- Estatísticas agregadas sobre a utilização do Desktop Analytics

- Configuração e estado de tarefa de manutenção SQL

- ***[Novo]*** Contagem de pastas

- ***[Novo]*** Utilização da ferramenta de migração Azure

## <a name="level-3---full"></a><a name="bkmk_level3"></a> Nível 3 - Completo

Para a versão 1910 do Gestor de Configuração, este nível inclui os seguintes dados:

- Informações de agenda de avaliação de regras de implementações automáticas  

- Resumo da saúde ATP  

- Estatísticas de avaliação e de atualização de coleções  

- Estatísticas da política de conformidade sobre conformidade e erros  

- Definições de conformidade: SCEP, VPN, Wi-Fi e detalhes de configuração de modelo de política de conformidade  

- Pacote config DCM para utilização do Gestor de Configuração  

- Erros detalhados de instalação de desenvolvimento do cliente  

- Resumo da saúde da proteção do ponto final: incluindo a contagem de clientes protegidos, em risco, desconhecidos e não apoiados  

- Configuração da política do Endpoint Protection  

- Lista de processos configurados com comportamento de instalação para aplicações  

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software  

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software  

- Número máximo/mínimo/médio de atualizações de software por pacote  

- Estatísticas de implantação do código de produtos MSI  

- Compatibilidade geral das implementações de atualizações de software  

- Contagem de grupos que expiraram atualizações de software  

- Contagens e códigos de erro de implementação de atualizações de software  

- Informações de implementação de atualização de software: percentagem de implementações que são direcionadas com o tempo cliente versus UTC, necessárias versus opcionais versus silenciosas, e reinicializar a supressão  

- Produtos de atualização de software sincronizados por ponto de atualização de software  

- Percentagens de êxito de análise de atualização de software  

- Top 50 CPUs no ambiente  

- Tipo de Políticas de acesso condicional Exchange Ative Sync (EAS) para dispositivos que a Microsoft Intune gere  

- Microsoft Store for Business application details: lista não agregada de aplicações sincronizadas, incluindo AppID, estado online ou estado offline, e contagens totais de licenças adquiridas  

- Contagem de clientes pressionados com opção de não permitir o recuo para a NTLM  

- Lista de extensões de consola do Gestor de Configuração
