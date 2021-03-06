---
title: Dados de diagnóstico e utilização para 1802
titleSuffix: Configuration Manager
description: Conheça os níveis de diagnóstico e dados de utilização recolhidos na versão 1802.
ms.date: 05/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 29dd51b8-6576-4010-81ba-3129ed2c3421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c2edff394e915273fb34f4627e3636ea6e20237c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710875"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1802-of-configuration-manager"></a>Níveis de recolha de dados de utilização de diagnóstico para a versão 1802 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A versão 1802 do Gestor de Configuração recolhe três níveis de diagnóstico e dados de utilização: **Básico,** **Melhorado**e **Completo**. Por predefinição, esta funcionalidade está definida no nível Avançado. As seguintes secções fornecem detalhes adicionais sobre os dados recolhidos em cada nível.

As alterações das versões anteriores são notadas com ***[New]***, ***[Removido],*** ou ***[Move]***. ***[Removed]***


> [!IMPORTANT]
>  O Gestor de Configuração não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis Básico ou Melhorado. Qualquer recolha desta informação a nível completo não é propositada. Está potencialmente incluído em informações avançadas de diagnóstico, como ficheiros de registo ou instantâneos de memória. A Microsoft não utiliza estas informações para o identificar, contactar ou desenvolver publicidade.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito administrativo baseado em funções que inclua **modificar** permissões na classe de objetos **do Site** podem alterar o nível de dados recolhidos nas definições de Dados de Diagnóstico e Utilização na consola do Gestor de Configuração.

Altera o nível de recolha de dados a partir da consola navegando para**sites**de**configuração** > de site de**visão geral** > da **administração** > . Abra **as Definições da Hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nível 1 - Básico
O nível Básico inclui dados sobre a sua hierarquia, dados que são necessários para ajudar a melhorar a sua experiência de instalação ou upgrade, e dados que ajudam a determinar as atualizações do Gestor de Configuração aplicáveis à sua hierarquia.

Para a versão 1802 do Gestor de Configuração, este nível inclui os seguintes dados:

- Estatísticas sobre ligações de consola do Gestor de Configuração: versão OS, idioma, SKU e arquitetura, memória do sistema, contagem lógica de processadores, id do site de ligação, versões instaladas .NET e pacotes de idiomas de consola

- Contagens básicas de aplicações e implementação: aplicações totais, aplicações totais com vários tipos de implementação, aplicações totais com dependências, aplicações supersed totais e contagem de tecnologias de implementação em uso

- Dados da hierarquia do site do Gestor de Configuração Básico: lista de site, tipo, versão, estado, contagem de clientes e fuso horário

- Configuração básica da base de dados: processadores, configuração de cluster e configuração de vistas distribuídas

- Estatísticas básicas de descoberta: contagem de descobertas, tamanhos mínimo/máximo/médio do grupo, e quando o site está funcionando inteiramente com Serviços de Diretório Ativo Azure

- Informações básicas sobre as versões de clientes antimalware

- Contagem básica de implementação de oso de imagens

- Informações básicas do servidor do sistema do site: funções do sistema do site utilizadas, estado da Internet e SSL, OS, processadores, máquina física ou virtual, e utilização da elevada disponibilidade do servidor do site

- Esquema de base de dados do Gestor de Configuração (hash de todas as definições de objeto)

- Nível de telemetria configurado, modo on-line ou offline, e configuração de atualização rápida

- Conde de línguas e locais de cliente

- Contagem de versões de clientes do Gestor de Configuração, versões DE Os e Versões do Office

- Contagem dos sistemas operativos para dispositivos e políticas geridos definidos pelo Conector de Intercâmbio

- Contagem de dispositivos Windows 10 por ramo e compilação

- ***[Movido]*** Contagem de clientes do Windows 10 que usam a Atualização do Windows para Negócios  

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

- Estatísticas da telemetria: quando executado, tempo de execução, erros

- Se a descoberta da rede está ativada ou desativada

- ***[Movido]*** Contagem de clientes juntou-se ao Diretório Ativo azure

- ***[Novo]*** Contagem de implementações faseadas criadas por tipo

- ***[Novo]*** Contagem de clientes de interoperabilidade alargada

- ***[Novo]*** Lista hashed de propriedades de inventário de hardware mais de 255 caracteres



##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nível 2 - Avançado
O nível melhorado é o padrão após os acabamentos de configuração. Este nível inclui dados recolhidos no nível Básico e dados específicos de funcionalidades (frequência e duração da utilização), configurações do cliente do Gestor de Configuração (nome do componente, estado e certas configurações, como intervalos de votação), e informações básicas sobre atualizações de software.

Este nível é recomendado porque fornece à Microsoft os dados mínimos necessários para fazer melhorias úteis em futuras versões de produtos e serviços. Este nível não recolhe nomes de objetos (sites, utilizadores, computador escusadoes ou objetos), detalhes de objetos relacionados com a segurança ou vulnerabilidades como contagens de sistemas que requerem atualizações de software.

Para a versão 1802 do Gestor de Configuração, este nível inclui os seguintes dados:

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

- Contagem de aplicações referenciadas por uma sequência de tarefas

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

- ***[Novo]*** Estatísticas agregadas da afinidade do dispositivo de utilizador 

- ***[Novo]*** Utilizadores primários max e médios por dispositivo


### <a name="client"></a>Cliente  

- Versão cliente de Tecnologia de Gestão Ativa (AMT)

- IDADE BIOS em anos

- Contagem de dispositivos com bota segura ativada

- Contagem de dispositivos por estado tpm

- Atualização automática do cliente: configuração de implementação incluindo a pilotagem do cliente e o uso de exclusão (cliente de interoperabilidade alargada)

- Configuração do tamanho do cache do cliente

- Erros de descarregamento de implementação de clientes

- Estatísticas de saúde dos clientes e resumo de questões de topo

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

- ***[Novo]*** Contagem de dispositivos por navegador padrão


### <a name="cloud-services"></a>Serviços Cloud  

- Estatísticas de descoberta de diretórios ativos azure

- Estatísticas de configuração e utilização do Gateway de Gestão de Nuvem: contagens de regiões e ambientes, e estatísticas de autenticação/autorização

- Contagem de aplicações e serviços de Diretório Ativo Azure ligados ao Gestor de Configuração

- Contagem de coleções sincronizadas com Azure Log Analytics

- Contagem de Conectores de Atualização Analytics

- Se o conector de nuvem Azure Log Analytics está ativado


### <a name="co-management"></a>Cogestão  
- Estatísticas de utilização agregadas de cogestão: número de clientes inscritos, clientes que recebem política, estados de carga de trabalho, tamanhos de recolha piloto/exclusão e erros de inscrição  

- Contagem de clientes por método de inscrição de cogestão  

- Estatísticas de erro para inscrição em cogestão  

- Horário de matrículas e estatísticas históricas  

- Contagem de clientes elegíveis para cogestão  

- Inquilino Associado da Microsoft Intune


### <a name="collections"></a>Coleções  

- Utilização de ID de recolha (não ficando sem iDs)

- Estatísticas de avaliação de cobrança: tempo de consulta, atribuído versus contagens não atribuídas, conta por tipo, capotamento de ID e utilização de regras

- Coleções sem implantação


### <a name="compliance-settings"></a>Definições de compatibilidade  

- Informação de base de configuração básica: contagem, número de implementações e número de referências

- Estatísticas de erro de política de conformidade

- Contagem de itens de configuração por tipo  

- Contagem de implementações que referenciam configurações incorporadas, incluindo a definição de remediação  

- Contagem de regras e implementações criadas para configurações personalizadas, incluindo a definição de remediação  

- Contagem dos modelos de inscrição de certificados simples (SCEP), VPN, Wi-Fi, certificado (.pfx) e modelos de política de conformidade

- Contagem de certificados SCEP, VPN, Wi-Fi, certificado (.pfx) e implementações de política de conformidade por plataforma

- Política do Windows Hello for Business (criada, implementada)


### <a name="content"></a>Conteúdo  

- ***[Atualizado]*** Estatísticas do grupo de fronteira: quantos rápidos, quantos lentos, contagem por grupo, e relações de recuo

- Informações do grupo de fronteira: contagem de fronteiras e sistemas de site que são atribuídos a cada grupo de fronteiras  

- Relações de grupo de fronteiras e configuração de recuo

- Estatísticas de descarregamento de conteúdo de clientes

- Contagem de limites por tipo  

- Contagem de clientes de cache de pares, estatísticas de uso e estatísticas parciais de descarregamento

- Informação de configuração do Gestor de Distribuição: threads, retry delay, número de repetições e definições de ponto de distribuição de puxar  

- Informação de configuração de pontos de distribuição: utilização do cache do ramo e monitorização do ponto de distribuição

- Informação do grupo de pontos de distribuição: contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Políticas de Proteção avançada de ameaças (ATP) do Microsoft Defender (anteriormente conhecida como Windows Defender ATP): contagem de políticas e se as políticas são implementadas.

- Contagem de alertas configurados para a função de Proteção de Pontofinal  

- Contagem de coleções que são selecionadas para aparecer no painel de proteção de Ponto Final  

- Contagem de políticas, implementações e clientes direcionados do Windows Defender Exploit Guard

- Erros de implementação de proteção de pontos finais, contagem de códigos de erro da política de proteção do ponto final  

- Utilização da política de proteção de pontos finais e de firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Estes dados não incluem qualquer informação sobre as definições incluídas na política.  


### <a name="migration"></a>Migração  

- Contagem de objetos migrados (utilização de assistente de migração)


### <a name="mobile-device-management-mdm"></a>Mobile device management (MDM) (Gestão de dispositivos móveis [MDM])  

- Contagem de ações de dispositivos móveis emitidas: bloqueio, apoio de pinos, limpeza, aposentadoria e sincronização agora comandos

- Contagem de políticas de dispositivos móveis  

- Contagem de dispositivos móveis geridos pelo Gestor de Configuração e Microsoft Intune e como foram matriculados (a granel, baseados no utilizador)  

- Contagem de utilizadores que tenham vários dispositivos móveis matriculados  

- Horário de sondagens para dispositivos móveis e estatísticas para a duração do check-in do dispositivo móvel  


### <a name="microsoft-intune-troubleshooting"></a>Microsoft Intune resolução de problemas  

- Contagem e tamanho das ações do dispositivo (limpeza, aposentadoria, bloqueio), telemetria e mensagens de dados que são replicadas para Microsoft Intune

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


### <a name="site-updates"></a>Atualizações do site  

- Versões de hotfixos instalados do Gestor de Configuração


### <a name="software-updates"></a>Atualizações de Software  

- Deltas disponíveis e prazos que são usados em regras de implementação automática  

- Número médio e máximo de atribuições por atualização  

- Avaliação de atualização de cliente e agendas de análise  

- Classificações sincronizadas por ponto de atualização de software

- Estatísticas de aplicação de patches de cluster  

- Configuração de atualizações expressas do Windows 10

- Configurações que são usadas para planos de manutenção ativos do Windows 10  

- Contagem de atualizações do Office 365 implementadas  

- Contagem de controladores Microsoft Surface sincronizados

- Contagem de grupos de atualização e atribuições  

- Contagem dos pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são direcionados com pacotes  

- Contagem de atualizações que são criadas e implementadas com system center update Publisher  

- Contagem de Atualizações do Windows para políticas empresariais criadas e implementadas

- ***[Novo]*** Estatísticas agregadas do Windows Update para configurações de Negócios

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


### <a name="sqlperformance-data"></a>Dados SQL/desempenho  

- Configuração e duração da resumição do site

- Contagem das maiores tabelas de bases de dados  

- Estatísticas operacionais de descoberta (contagem de objetos encontrados)

- Tipos de descoberta, habilitados e programadores (completos, incrementais)

- SQL AlwaysOn replica informação, uso e estado de saúde

- SQL alterar problemas de desempenho de rastreio, período de retenção e estado de limpeza automática

- Período de retenção de rastreio de alterações SQL

- Estatísticas de desempenho da mensagem de estado e de estado, incluindo os tipos de mensagens mais comuns e mais caros


### <a name="miscellaneous"></a>Diversos  

- Configuração do ponto de serviço de armazém de dados, incluindo o horário de sincronização e o tempo médio

- Contagem de scripts e estatísticas de execução

- Contagem de sites com Wake On LAN (WOL)

- Relatóriode estatísticas de utilização e desempenho

- ***[Novo]*** Estatísticas de utilização faseadas



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis Básico e Melhorado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software. Este nível também pode incluir informações avançadas de diagnóstico, como ficheiros do sistema e instantâneos de memória, que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Para a versão 1802 do Gestor de Configuração, este nível inclui os seguintes dados:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo da Saúde ATP

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

- ***[Atualizado]*** Estatísticas de implantação do código de produtos MSI 

- Compatibilidade geral das implementações de atualizações de software

- Contagem de grupos que expiraram atualizações de software

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualização de software: percentagem de implementações que são direcionadas com o tempo cliente versus UTC, necessárias versus opcionais versus silenciosas, e reinicializar a supressão

- Produtos de atualização de software sincronizados por ponto de atualização de software

- Percentagens de êxito de análise de atualização de software

- Top 50 CPUs no ambiente

- Tipo de Políticas de acesso condicional Exchange Ative Sync (EAS) para dispositivos que a Microsoft Intune gere

- Microsoft Store for Business application details: lista não agregada de aplicações sincronizadas, incluindo AppID, estado online ou estado offline, e contagens totais de licenças adquiridas
