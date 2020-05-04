---
title: Dados de diagnóstico para 1710 / Gestor de Configuração
titleSuffix: Configuration Manager
description: Conheça os níveis de diagnóstico e dados de utilização que a versão 1710 do Gestor de Configuração recolhe.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8fce5391-8e75-4f99-813a-76f8842be5bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fcc3d2e34c9387e158b3b35cd104c9fc43136ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715551"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1710-of-configuration-manager"></a>Níveis de recolha de dados de utilização de diagnóstico para a versão 1710 do Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A versão 1710 do Gestor de Configuração recolhe três níveis de diagnóstico e dados de utilização: **Básico,** **Melhorado**e **Completo**. Por predefinição, esta funcionalidade está definida no nível Avançado. As seguintes secções fornecem detalhes adicionais sobre os dados que cada nível recolhe.

As alterações das versões anteriores são notadas com ***[New]***, ***[Removido],*** ou ***[Move]***. ***[Removed]***


> [!IMPORTANT]
>  O Gestor de Configuração não recolhe códigos de site, nomes de sites, endereços IP, nomes de utilizador, nomes de computador, endereços físicos ou endereços de e-mail nos níveis Básico ou Melhorado. Qualquer recolha desta informação no nível Completo não é propositada, isto é, potencialmente incluída em informações avançadas de diagnóstico, como ficheiros de registo ou instantâneos de memória. A Microsoft não utilizará estas informações para identificá-lo, contactá-lo ou desenvolver publicidade.



##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Como alterar o nível
 Os administradores que tenham um âmbito administrativo baseado em funções que inclua **modificar** permissões na classe de objetos **do Site** podem alterar o nível de dados recolhidos nas definições de Dados de Diagnóstico e Utilização na consola do Gestor de Configuração.

Altera o nível de recolha de dados a partir da consola navegando para**sites**de**configuração** > de site de**visão geral** > da **administração** > . Abra **as Definições da Hierarquia**e, em seguida, selecione o nível de dados que pretende utilizar.  



##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Nível 1 - Básico
O nível Básico inclui dados sobre a sua hierarquia, dados que são necessários para ajudar a melhorar a sua experiência de instalação ou upgrade, e dados que ajudam a determinar as atualizações do Gestor de Configuração aplicáveis à sua hierarquia.

Para a versão 1710 do Gestor de Configuração, este nível inclui o seguinte:

- Consola de administrador:
   - Estatísticas sobre ligações de consolas (versão do sistema operativo, idioma, SKU e arquitetura, memória do sistema, contagem lógica de processadores, id do site de ligação, versões instaladas .NET e pacotes de idiomas de consola)

- Contagens básicas de aplicações e implementação (aplicações totais, aplicações totais com vários tipos de implementação, aplicações totais com dependências, aplicações supersed totais e contagem de tecnologias de implementação em uso)

- Dados da hierarquia do site do Gestor de Configuração Básica (lista de site, tipo, versão, estado, contagem de clientes e fuso horário)

- Configuração básica da base de dados (processadores, configuração de cluster e configuração de vistas distribuídas)

- Estatísticas básicas de descoberta (contagem de descobertas e tamanhos mínimo/máximo/médio de grupo) incluindo quando o site está funcionando inteiramente com os Serviços de Diretório Ativo Azure.

- Informações básicas de proteção do ponto final (versões de cliente antimalware)

- Contagens básicas de implantação do sistema operativo (OSD) (imagens)

- Informação básica do servidor do sistema do site (funções do sistema do site utilizadas, estado da Internet e SSL, sistema operativo, processadores, máquina física ou virtual e utilização da elevada disponibilidade do servidor do site)

- Esquema de base de dados do Gestor de Configuração (hash de todas as definições de objeto)

- Nível de telemetria configurado, modo (on-line ou offline) e configuração de atualização rápida

- Conde de línguas e locais de cliente

- ***[Atualizado]*** Contagem de versões de clientes do Gestor de Configuração, versões do sistema operativo e versões do Office

- Contagem dos sistemas operativos para dispositivos e políticas geridos definidos pelo Conector de Intercâmbio

- Contagem de dispositivos Windows 10 por ramo e compilação

- Métricas de desempenho de bases de dados (informações de processamento de replicação, principais procedimentos armazenados do SQL Server por processador e utilização de disco)

- Tipos de pontos de distribuição e pontos de gestão e informações básicas de configuração (protegidas, pré-encenadas, PXE, multicast, estado SSL, pontos de distribuição pull/peer, ativados por MDM, ativados por SSL, etc.)

- Lista hashed de extensões para administrar páginas de propriedade de consola e assistentes

- Informações de configuração:
     - Construir, instalar tipo, pacotes de idiomas, funcionalidades que permitiu   

     - Utilização pré-libertação, tipo de meio de configuração, tipo de ramo

     - Data de validade da garantia de software      

     - Atualizar o estado e os erros de implementação do pack, transferir progressos e erros pré-requisitos 

     - Utilização do anel rápido de atualização

     - Versão do script pós-upgrade

- Versão SQL, nível de pacote de serviço, edição, ID de colagem e conjunto de caracteres     
- Estatísticas de telemetria (momento da execução, tempo de execução, erros)

- Utilização da Descoberta da Rede (ativada ou desativada)




##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Nível 2 - Avançado
O nível melhorado é o padrão após os acabamentos de configuração. Este nível inclui dados recolhidos no nível Básico e dados específicos de funcionalidades (frequência e duração da utilização), configurações do cliente do Gestor de Configuração (nome do componente, estado e certas configurações, como intervalos de votação), e informações básicas sobre atualizações de software.

Este nível é recomendado porque fornece à Microsoft os dados mínimos necessários para fazer melhorias úteis em futuras versões de produtos e serviços. Este nível não recolhe nomes de objetos (sites, utilizadores, computador escusadoes ou objetos), detalhes de objetos relacionados com a segurança ou vulnerabilidades como contagens de sistemas que requerem atualizações de software.

Para a versão 1710 do Gestor de Configuração, este nível inclui o seguinte:

- **Gestão de aplicações:**  

   - Requisitos de aplicações (contagem de condições incorporadas é referenciado pela tecnologia de implementação)

   - Supersedência da aplicação, profundidade máxima da cadeia

   - Estatísticas de aprovação de aplicações e frequência de utilização

   - Estatísticas do tamanho do conteúdo da aplicação

   - Informações de implementação de aplicações (utilização de instalação versus desinstalação, requer aprovação, interação do utilizador ativada/desativada, dependência, supersedência e contagem de utilização da funcionalidade de comportamento de instalação)  

   - Tamanho da política de aplicação e estatísticas de complexidade

   - Estatísticas de pedidos de aplicação disponíveis

   - Informações básicas de configuração para pacotes e programas (opções de implantação e bandeiras de programas)

   - Informações básicas de utilização/segmentação para tipos de implementação que são utilizados dentro da organização (user versus dispositivo direcionado, necessário versus disponível e aplicações universais)

   - Estatísticas de grupos de fronteira (quantos rápidos, quantos lentos, e contagem por grupo)

   - Contagem de ambientes de App-V e propriedades de implementação

   - Contagem de aplicabilidade de aplicações por sistema operativo  

   - Contagem de aplicações referenciadas por uma sequência de tarefas

   - Contagem de marcas distintas para catálogo de aplicações

   - Contagem de 365 aplicações criadas com recurso a painel de instrumentos

   - Contagem de pacotes por tipo  

   - Contagem de implementações de pacote/programa  

   - Contagem de licenças de aplicação licenciadas para Windows 10  

   - Contagem dos tipos de implementação do Instalador do Windows desinstalando as definições de conteúdo

   - Contagem da Microsoft Store para aplicações empresariais e estatísticas de sincronização (incluindo tipos resumidos de apps, estatuto de aplicação licenciada e número de aplicações licenciadas online e offline)  

   - Tipo e duração da janela de manutenção  

   - Número mínimo/máximo/médio de implementações de aplicações por utilizador/dispositivo por período de tempo

   - Códigos de erro de instalação de aplicação mais comuns através da tecnologia de implementação

   - Opções de configuração MSI e conta

   - Estatísticas sobre a interação do utilizador final com a notificação para implementações de software necessárias   

   - Uso universal de acesso a dados (UDA), como criado




- **Cliente:**  

   - Versão cliente de Tecnologia de Gestão Ativa (AMT)

   - IDADE BIOS em anos

   - Contagem de dispositivos com bota segura ativada

   - Contagem de dispositivos por estado tpm

   - Atualização automática do cliente: configuração de implementação incluindo a pilotagem do cliente e o uso de exclusão (cliente de interoperabilidade alargada)

   - Configuração do tamanho do cache do cliente

   - Erros de descarregamento de implementação de clientes

   - Estatísticas de saúde dos clientes e resumo de questões de topo

   - Estado de ação de operação de notificação de clientes (quantas vezes cada um é executado, número máximo de clientes direcionados e taxa média de sucesso)
   - Contagem de instalações de cliente a partir de cada tipo de localização de origem  

   - Contagem de falhas de instalação de cliente  

   - Contagem de dispositivos virtualizados por Hyper-V ou Azure  

   - Contagem de ações do Centro de Software   

   - Contagem de dispositivos ativados pela UEFI

   - Métodos de implantação utilizados para cliente e contagem de clientes por método de implementação

   - Lista/contagem de agentes de cliente ativados  

   - Idade do sistema operativo em meses

   - Número de classes de inventário de hardware, regras de inventário de software e regras de recolha de ficheiros

   - Estatísticas para atestado de saúde de dispositivos, incluindo os códigos de erro mais comuns, número de servidores no local e contagens de dispositivos em vários estados.



- **Serviços de Nuvem:**

  - Estatísticas de descoberta de diretórios ativos azure

  - Estatísticas de configuração e utilização do Gateway de Gestão de Nuvem, incluindo contagens de regiões e ambientes, e estatísticas de autenticação/autorização

  - Contagem de aplicações e serviços de Diretório Ativo Azure ligados ao Gestor de Configuração

  - Contagem de clientes juntou-se aos Serviços de Diretório Ativo da Azure

  - Contagem de coleções sincronizadas com Azure Log Analytics

  - Contagem de Conectores de Atualização Analytics

  - Se o conector de nuvem Azure Log Analytics está ativado


- ***[Novo]*** Cogestão
  - ***[Novo]*** Estatísticas de utilização agregadas de cogestão, incluindo o número de clientes inscritos, clientes que recebem política, estados de carga de trabalho, tamanhos de recolha piloto/exclusão, erros de inscrição
  - ***[Novo]*** Contagem de clientes por método de inscrição de cogestão
  - ***[Novo]*** Estatísticas de erro para inscrição em cogestão
  - ***[Novo]*** Horário de matrículas e estatísticas históricas
  - ***[Novo]*** Contagem de clientes elegíveis para cogestão
  - ***[Novo]*** Inquilino Intune Associado


- **Coleções:**

    - Utilização de ID de recolha (não ficando sem iDs)

    - Estatísticas de avaliação de cobrança (tempo de consulta, atribuído sem contagens não atribuídas, contapor tipo, capotamento de ID e utilização de regras)

    - Coleções sem implantação




- **Definições de conformidade:**  

    - Informações básicas de linha de base de configuração (contagem, número de implementações e número de referências)

    - Estatísticas de erro de política de conformidade

    - Contagem de itens de configuração por tipo  

    - Contagem de implementações que referenciam definições incorporadas (capturando agora a definição de remediação)  

    - Contagem de regras e implementações criadas para configurações personalizadas (capturando agora a definição de remediação)  

    - Contagem dos modelos de inscrição de certificados simples (SCEP), VPN, Wi-Fi, certificado (.pfx) e modelos de Política de Conformidade

    - Contagem de certificações SCEP, VPN, Wi-Fi, certificado (.pfx) e implementações de Política de Conformidade por plataforma

    - Política de Passaporte para o Trabalho (criada, implantada)



- **Conteúdo:**  

    - Informações de grupo de fronteiras (contagem de fronteiras e sistemas de sites que são atribuídos a cada grupo de fronteiras)  

    - Relações de grupo de fronteiras e configuração de recuo

    - Estatísticas de descarregamento de conteúdo de clientes

    - Contagem de limites por tipo  

    - Contagem de clientes de cache de pares, estatísticas de uso e estatísticas parciais de descarregamento

    - Informação de configuração do Gestor de Distribuição (linhas, atraso de retry, número de repetições e definições de ponto de distribuição)  

    - Informação de configuração de pontos de distribuição (utilização de cache de ramo e monitorização de pontos de distribuição)

    - Informações do grupo de pontos de distribuição (contagem de pacotes e pontos de distribuição atribuídos a cada grupo de pontos de distribuição)  



- **Proteção do ponto final:**  

   - Políticas avançadas de proteção contra ameaças (ATP) (contagem de políticas e se as políticas são implementadas)

   - Contagem de alertas configurados para a função de Proteção de Pontofinal  

   - Contagem de coleções que são selecionadas para aparecer no painel de proteção de Ponto Final  

   - ***[Novo]*** Contagem de políticas, implementações e clientes direcionados do Windows Defender Exploit Guard

   - Erros de implementação de proteção de pontos finais (contagem dos códigos de erro de implementação da política de proteção do ponto final)  

   - Utilização da política de proteção de pontos finais e de firewall do Windows (número de políticas únicas atribuídas ao grupo)<br /><br /> Isto não inclui qualquer informação sobre as definições incluídas na política.  



- **Migração:**

  - Contagem de objetos migrados (utilização de assistente de migração)



- **Gestão de dispositivos móveis (MDM):**  

    - Contagem de ações emitidas de dispositivos móveis: bloqueio, apoio de pinos, limpeza, aposentado e Sincronizaagora comanda

    - Contagem de políticas de dispositivos móveis  

    - Contagem de dispositivos móveis geridos pelo Gestor de Configuração e Microsoft Intune e como foram matriculados (a granel, baseados no utilizador)  

    - Contagem de utilizadores que tenham vários dispositivos móveis matriculados  

    - Horário de sondagens para dispositivos móveis e estatísticas para a duração do check-in do dispositivo móvel  




- **Microsoft Intune resolução de problemas:**

    - Contagem e tamanho das ações do dispositivo (limpeza, aposentadoria, bloqueio), telemetria e mensagens de dados que são replicadas para Microsoft Intune

    - Contagem e dimensão do estado, estado, inventário, RDR, DDR, UDX, Estado inquilino, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM e mensagens de conformidade que são descarregadas a partir do Microsoft Intune

    - Estatísticas completas e delta de sincronização dos utilizadores para o Microsoft Intune



- **Gestão de dispositivos móveis (MDM) no local:**  

    - Contagem de pacotes e perfis de inscrição em massa do Windows 10  

    - Estatísticas de êxito/falha de implementação para implementações de aplicações MDM no local  




- **Implantação do sistema operativo:**  

    - Contagem de imagens de arranque, controladores, pacotes de controladores, pontos de distribuição preparados com multicast ativado, pontos de distribuição com PXE ativado e sequências de tarefas  

    - Contagem de imagens de arranque por versão cliente do Gestor de Configuração

    - Contagem de imagens de arranque por versão do Windows PE

    - Contagem de políticas de upgrade de edição

    - Contagem de identificadores de hardware excluídos do PXE

    - ***[Novo]*** Contagem da implantação do OS por versão OS

    - ***[Novo]*** Contagem de atualizações de SO ao longo do tempo

    - Contagem de implementações de sequências de tarefas utilizando a opção de pré-descarregamento de conteúdos

    - Contagem de utilização da sequência de tarefas

    - Versão do Windows ADK instalada


- **Atualizações do site:**

    - Versões de hotfixos instalados do Gestor de Configuração



- **Atualizações de software:**  

    - Deltas disponíveis e prazos que são usados em regras de implementação automática  

    - Número médio e máximo de atribuições por atualização  

    - Avaliação de atualização de cliente e agendas de análise  

    - Classificações sincronizadas por Software Update Point

    - Estatísticas de aplicação de patches de cluster  

    - Configuração de atualizações expressas do Windows 10

    - Configurações que são usadas para planos de manutenção ativos do Windows 10  

    - Contagem de atualizações do Office 365 implementadas  

    - Contagem de controladores Microsoft Surface sincronizados

    - Contagem de grupos de atualização e atribuições  

    - Contagem dos pacotes de atualização e o número máximo/mínimo/médio de pontos de distribuição que são direcionados com pacotes  

    - Contagem de atualizações que são criadas e implementadas com system center update Publisher  

    - Contagem de clientes do Windows 10 que usam a Atualização do Windows para Negócios  

    - Contagem de Atualizações do Windows para políticas empresariais criadas e implementadas

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



- **Dados de desempenho/SQL:**  

    - Configuração e duração da resumição do site

    - Contagem das maiores tabelas de bases de dados  

    - Estatísticas operacionais de descoberta (contagem de objetos encontrados)

    - Tipos de descoberta, habilitados e programados (completos, incrementais)

    - SQL AlwaysOn replica informação, uso e estado de saúde

    - SQL alterar problemas de desempenho de rastreio, período de retenção e estado de limpeza automática

    - Período de retenção de rastreio de alterações SQL

    - Estatísticas de desempenho da mensagem de estado e de estado, incluindo os tipos de mensagens mais comuns e mais caros



- **Diversos**

    - Configuração do Data Warehouse Service Point, incluindo o calendário de sincronização e o tempo médio

    - Contagem de Scripts e estatísticas de execução

    - Contagem de sites com Wake On Lan (WOL)

    - Relatóriode estatísticas de utilização e desempenho  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Nível 3 - Completo
O nível completo inclui todos os dados nos níveis Básico e Melhorado. Também inclui informações adicionais sobre o Endpoint Protection, percentagens de compatibilidade de atualização e informações de atualização de software.  Este nível também pode incluir informações avançadas de diagnóstico, como ficheiros do sistema e instantâneos de memória que podem incluir informações pessoais que existiam na memória ou ficheiros de registo no momento da captura.

Para a versão 1710 do Gestor de Configuração, este nível inclui o seguinte:

- Informações de agenda de avaliação de regras de implementações automáticas

- Resumo da Saúde ATP

- Estatísticas de avaliação e de atualização de coleções

- Estatísticas da política de conformidade sobre conformidade e erros

- Definições de conformidade: SCEP, VPN, Wi-Fi e compliance Policy detalhes de configuração Contagem de grupos que tenham expirado atualizações de software

- Pacote config DCM para utilização do Gestor de Configuração

- Erros detalhados de instalação de desenvolvimento do cliente

- Resumo do estado de funcionamento do Endpoint Protection (incluindo contagem de clientes protegidos, em risco, desconhecidos e não suportados)

- Configuração da política do Endpoint Protection

- Lista de processos configurados com comportamento de instalação para aplicações

- Número máximo/mínimo/médio de horas desde a última análise de atualização de software

- Número máximo/mínimo/médio de clientes inativos em coleções de implementações de atualização de software

- Número máximo/mínimo/médio de atualizações de software por pacote

- Código de produto MSI (aplicações comuns que os clientes implementam)

- Compatibilidade geral das implementações de atualizações de software

- Contagens e códigos de erro de implementação de atualizações de software

- Informações de implementação de atualizações de software (percentagem de implementações que são direcionadas com o tempo cliente versus UTC, necessárias versus opcionais versus silenciosas, e reinicialização da supressão)

- Produtos de atualização de software sincronizados por Software Update Point

- Percentagens de êxito de análise de atualização de software

- Top 50 CPUs no ambiente

- Tipo de políticas de acesso condicional DaEAs (bloco ou quarentena) para dispositivos que intune gere

- Microsoft Store for Business application details (lista não agregada de aplicações sincronizadas, incluindo AppID, estado online ou estado offline, e contagem total de licenças adquiridas)
