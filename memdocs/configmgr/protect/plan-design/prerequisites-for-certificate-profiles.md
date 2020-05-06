---
title: Pré-requisitos do perfil de certificado
titleSuffix: Configuration Manager
description: Conheça os perfis de certificado no Gestor de Configuração e as suas dependências e dependências externas no produto.
ms.date: 12/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 396738fb854f859b1553bae02dd3709ef96b69ff
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722152"
---
# <a name="prerequisites-for-certificate-profiles-in-configuration-manager"></a>Pré-requisitos para perfis de certificado sintetmente em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


Os perfis de certificado no Gestor de Configuração têm dependências e dependências externas no produto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependências Externas ao Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Uma empresa autoridade de certificação (AC) emissora que esteja a executar os Serviços de Certificados do Active Directory (AD CS).<br /><br /> Para revogar certificados, a conta de computador do servidor do site no topo da hierarquia requer direitos de *Emitir e Gerir Certificados* para cada modelo de certificado utilizado por um perfil de certificado no Configuration Manager. Em alternativa, conceda permissões ao Gestor de Certificados para conceder permissões em todos os modelos de certificado utilizados por essa AC<br /><br /> A aprovação do gestor para pedidos de certificado é suportada. No entanto, os modelos de certificado utilizados para emitir certificados devem ser configurados para **fornecimento no pedido** do sujeito do certificado para que o Gestor de Configuração possa fornecer automaticamente este valor.|Para mais informações sobre os Serviços de Certificados do Active Directory, consulte a documentação do Windows Server.<br /><br /> Para Windows Server 2012: [Descrição Geral dos Serviços de Certificados do Active Directory](https://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Para Windows Server 2008: [Serviços de Certificados do Active Directory no Windows Server 2008](https://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|Utilize o script PowerShell para verificar e, se necessário, instale os pré-requisitos para o serviço de inscrição do dispositivo de rede (NDES) e o ponto de registo do Certificado de Configuração. <br /><br />|O ficheiro de instrução, readme_crp.txt, está localizado em ConfigMgrInstallDir\cd.latest\SMSSETUP\POLICYMODULE\X64.<br /><br />O script PowerShell, Test-NDES-CRP-Prereqs.ps1, está no mesmo diretório que as instruções. <br /><br /> O script PowerShell deve ser executado localmente no servidor NDES.|
|O serviço de inscrição de dispositivos de rede (NDES) para serviços de certificados de diretório ativo, em execução no Windows Server 2012 R2.<br /><br /> Além disso:<br /><br /> Os números de porta diferentes de TCP 443 (para HTTPS) ou TCP 80 (para HTTP) não são suportados para a comunicação entre o cliente e o Serviço de Inscrição de Dispositivos de Rede.<br /><br /> O servidor que estiver a executar o Serviço de Inscrição de Dispositivos de Rede tem de estar num servidor diferente da AC emissora.|O Gestor de Configuração comunica com o Serviço de Inscrição de Dispositivos de Rede no Windows Server 2012 R2 para gerar e verificar pedidos de Protocolo de Inscrição de Certificadosimples Simples (SCEP).<br /><br /> Se emitir certificados para utilizadores ou dispositivos que se ligam a partir da Internet, como dispositivos móveis geridos pelo Microsoft Intune, esses dispositivos devem poder aceder ao servidor que executa o Serviço de Inscrição de Dispositivos de Rede a partir da Internet. Por exemplo, instale o servidor numa rede de perímetro (também conhecida como DMZ, zona desmilitarizada, e sub-rede filtrada).<br /><br /> Se tiver uma firewall entre o servidor que executa o Serviço de Inscrição de Dispositivos de Rede e a AC emissora, tem de configurar a firewall para permitir o tráfego de comunicação (DCOM) entre os dois servidores. Este requisito de firewall também se aplica ao servidor que executa o servidor do site do Gestor de Configuração e o CA emissor, para que o Gestor de Configuração possa revogar os certificados.<br /><br /> Se o Serviço de Inscrição de Dispositivos de Rede estiver configurado para exigir o SSL, uma boa prática de segurança é certificar-se de que os dispositivos de ligação podem aceder à lista de revogação do certificado (CRL) para validar o certificado do servidor.<br /><br /> Para mais informações sobre o Serviço de Inscrição de Dispositivos de Rede no Windows Server 2012 R2, veja [Utilizar um Módulo de Política com o Serviço de Inscrição de Dispositivos de Rede](https://go.microsoft.com/fwlink/p/?LinkId=328657).|  
|Se a AC emissora executar o Windows Server 2008 R2, este servidor requer uma correção para pedidos de renovação SCEP.|Se a correção ainda não estiver instalada no computador da AC emissora, instale a correção. Para mais informações, veja o artigo [2483564: Pedido de renovação para um pedido de certificado SCEP falha no Windows Server 2008 R2 se o certificado for gerido através de NDES](https://go.microsoft.com/fwlink/?LinkId=311945) na Base de Dados de Conhecimento Microsoft.|  
|Um certificado de autenticação de cliente PKI e o certificado da AC de raiz exportado.|Este certificado autentica o servidor que está a executar o Serviço de Inscrição de Dispositivos de Rede para o Gestor de Configuração.<br /><br /> Para mais informações, consulte [os requisitos de certificado PKI para O Gestor de Configuração](../../core/plan-design/network/pki-certificate-requirements.md).|  
|Sistemas operativos de dispositivos suportados.|Pode implementar perfis de certificados para dispositivos que executam o Windows 8.1, Windows RT 8.1 e Windows 10.|  

## <a name="configuration-manager-dependencies"></a>Dependências do Configuration Manager  

|Dependência|Mais informações|  
|----------------|----------------------|  
|Função do sistema de sites do ponto de registo de certificados|Para poder utilizar perfis de certificado, é necessário instalar a função do sistema de sites do ponto de registo de certificados. Esta função comunica com a base de dados do Gestor de Configuração, o servidor do site do Gestor de Configuração e o Módulo de Política do Gestor de Configuração.<br /><br /> Para obter mais informações sobre os requisitos do sistema para este papel do sistema do site e onde instalar o papel na hierarquia, consulte a secção **requisitos** do sistema do site nas [configurações suportadas para](../../core/plan-design/configs/supported-configurations.md) o artigo Do Gestor de Configuração.<br /><br /> O ponto de registo do certificado não deve ser instalado no mesmo servidor que executa o Serviço de Inscrição de Dispositivos de Rede.|  
|Módulo de Política de Gestor de Configuração que está instalado no servidor que está executando o serviço de função de serviço de inscrição de dispositivos de rede para serviços de certificado de direção ativa|Para implementar perfis de certificado, tem de instalar o Módulo de Política do Gestor de Configuração. Pode encontrar este módulo de política nos meios de instalação do Gestor de Configuração.|  
|Dados de deteção|Os valores para o sujeito do certificado e o nome alternativo sujeito são fornecidos pelo Gestor de Configuração e recuperados a partir de informações recolhidas a partir da descoberta:<br /><br /> Para certificados de utilizador: Deteção de Utilizadores do Active Directory<br /><br /> Para certificados de computador: Deteção de Sistemas do Active Directory e Deteção de Rede|  
|Permissões de segurança específicas para gerir perfis de certificado|É necessário possuir as seguintes permissões de segurança para gerir definições de acesso a recursos da empresa, tais como perfis de certificado, perfis Wi-Fi e perfis VPN:<br /><br /> Para ver e gerir alertas e relatórios sobre perfis de certificado: **Criar**, **Eliminar**, **Modificar**, **Modificar Relatório**, **Leitura**e **Executar Relatório** para o objeto **Alertas** .<br /><br /> Para criar e gerir perfis de certificado: **Política de Autor,** **Relatório de Modificação,** **Ler**e **Executar Relatório** para o objeto de perfil de **certificado.**<br /><br /> Para gerir implementações de perfis Wi-Fi, certificado e VPN: **Implementar Políticas de Configuração**, **Modificar Alerta de Estado de Clientes**, **Leitura**e **Ler Recurso** para o objeto **Coleção** .<br /><br /> Para gerir todas as políticas de configuração: **Criar**, **Eliminar,** **Modificar,** **Ler**e **Definir o âmbito** de segurança para o objeto de política de **configuração.**<br /><br /> Para executar consultas relacionadas com perfis de certificado: permissão de **Leitura** para o objeto **Consulta** .<br /><br /> Para visualizar informações sobre perfis de certificado na consola Do Gestor de Configuração: **Leia** a permissão para o objeto **do Site.**<br /><br /> Para ver mensagens de estado para perfis de certificado: permissão de **Leitura** para o objeto **Mensagens de Estado** .<br /><br /> Para criar e modificar o perfil de certificado DE CA fidedigno: Política de **Autor,** **Relatório de Modificação,** **Leitura**e Relatório **de Execução** para o objeto de perfil de **certificado de certificado de CA fidedigno.**<br /><br /> Para criar e gerir perfis VPN: **Política de Autor,** **Modificar Relatório,** **Ler**e **Executar Relatório** para o objeto de **perfil VPN.**<br /><br /> Para criar e gerir perfis Wi-Fi: Política de **Autor,** **Modificar relatório,** **Ler**e **Executar relatório** para o objeto de **perfil Wi-Fi.**<br /><br /> A função de segurança **do Gestor** de Acesso a Recursos da Empresa inclui estas permissões que são necessárias para gerir perfis de certificado sintetizadores no Gestor de Configuração. Para mais informações, consulte a secção de administração baseada em **funções Configurar** no artigo de [segurança configure.](../../core/plan-design/security/configure-security.md)|  