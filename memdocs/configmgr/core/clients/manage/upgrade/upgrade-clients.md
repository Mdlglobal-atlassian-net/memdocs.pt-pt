---
title: Atualizar clientes
titleSuffix: Configuration Manager
description: Obtenha informações sobre como atualizar os clientes no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076684"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Atualizar clientes no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Pode utilizar diferentes métodos para atualizar o software cliente do Gestor de Configuração em computadores Windows, servidores UNIX e Linux e computadores Mac. Aqui estão as vantagens e desvantagens de cada método.  

> [!TIP]  
>  Se estiver a atualizar a infraestrutura do servidor a partir de uma versão anterior do \(como o Configuration Manager 2007 ou o System Center 2012 Configuration Manager\), recomendamos que conclua a atualização do servidor incluindo a instalação de todas as atualizações do current branch, antes de atualizar os clientes do Configuration Manager. Desta forma, terá também a versão mais recente do software do cliente.  

## <a name="group-policy-installation"></a>Instalação de Política de Grupo  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

- Pode ser utilizada para novas instalações de cliente ou para atualizações.  

- Os computadores podem ler as propriedades de instalação de cliente que tiverem sido publicadas nos Serviços de Domínio do Active Directory Domain Services.  

- Não necessita que seja configurada e mantida uma conta de instalação para o computador cliente pretendido.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se estiver a atualizar muitos clientes.  

- Se o esquema de Diretório Ativo não for estendido para O Gestor de Configuração, deve utilizar [as definições](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) de Política de Grupo para adicionar propriedades de instalação de clientes a computadores no seu site.  


## <a name="logon-script-installation"></a>Instalação do script de início de sessão  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de instalar o cliente.  

- Pode ser utilizada para novas instalações de cliente ou para atualizações.  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se estiver a atualizar muitos clientes em pouco tempo.  

- Pode demorar muito tempo a atualizar todos os computadores clientes se os utilizadores não iniciarem frequentemente sessão na rede.  

  Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando Scripts de Início de Sessão](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Instalação manual  
 **Plataforma de cliente suportada:** Windows, UNIX/Linux e Mac OS X  

#### <a name="advantages"></a>Vantagens  

- Não necessita que os computadores sejam detetados antes de atualizar o cliente.  

- Pode ser útil para fins de teste.  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Sem automatização, portanto demorada.  

  Para obter mais informações, consulte os seguintes tópicos:  

- [Como Instalar Manualmente Clientes do Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Como atualizar clientes para servidores Linux e UNIX](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Como atualizar clientes em computadores Mac](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Instalação de atualização (gestão de aplicações)  
 **Plataforma de cliente suportada:** Windows  

> [!NOTE]  
>  Não é possível atualizar os clientes do Gestor de Configuração 2007 com este método. Neste cenário, pode implementar o cliente do Gestor de Configuração como um pacote do site Do Gestor de Configuração de 2007, ou pode utilizar a atualização automática do cliente que cria e implementa automaticamente um pacote que contém a versão mais recente do cliente.  

#### <a name="advantages"></a>Vantagens  

- Suporta a utilização de propriedades da linha de comandos para CCMSetup.  

#### <a name="disadvantages"></a>Desvantagens  

- Pode causar tráfego de rede elevado se distribuir o cliente por grandes coleções.  

- Só pode ser utilizado para atualizar o software de cliente em computadores que tenham sido detetados e atribuídos ao site.  

  Para mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando um Pacote e Programa](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Atualização automática de cliente  

> [!NOTE]  
> Pode ser usado para atualizar os clientes do Gestor de Configuração 2007 para clientes de sucursais atuais do Gestor de Configuração. Um cliente do Gestor de Configuração 2007 pode atribuir a um site do Gestor de Configuração, mas não pode realizar quaisquer ações além da atualização automática do cliente.  

 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Devido à aleatoriedade durante o período especificado, apenas a atualização automática é adequada para upgrades de clientes em larga escala. Outros métodos são muito lentos em larga escala, ou não têm aleatoriedade. 

    > [!Note]
    > A pilotagem de clientes não é boa para grande escala, já que não aleatoriamente.  
- Pode ser utilizado para manter automaticamente os clientes no site na versão mais recente.  

- Requer uma administração mínima.  

#### <a name="disadvantages"></a>Desvantagens  

- Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

- Aplica-se a todos os clientes na hierarquia que estão atribuídos a um site. Não pode ser limitado por coleção.  

- Opções de agendamento limitadas.  

  Para mais informações, consulte [Como atualizar os clientes para computadores Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Teste de clientes  
 **Plataforma de cliente suportada:** Windows  

#### <a name="advantages"></a>Vantagens  

- Pode ser usado para testar novas versões de clientes numa coleção de pré-produção mais pequena.  

- Quando os testes estão completos, os clientes em pré-produção são promovidos à produção e automaticamente atualizados através do site do Gestor de Configuração.  

#### <a name="disadvantages"></a>Desvantagens  

- Só pode ser utilizado para atualizar o software de cliente e não pode ser utilizado para instalar um novo cliente.  

  [Como testar as atualizações dos clientes numa coleção de pré-produção](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
