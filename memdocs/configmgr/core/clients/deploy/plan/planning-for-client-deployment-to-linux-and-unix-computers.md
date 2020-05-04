---
title: Planejamento da implementação de clientes para computadores Linux e UNIX
titleSuffix: Configuration Manager
description: Plano para implantação de clientes para computadores Linux e UNIX em Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dfede7594224ff48af2a1e4066e69d551c3c576e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713234"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-configuration-manager"></a>Planeamento para implementação de clientes para computadores Linux e UNIX em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.

Pode instalar o cliente Do Gestor de Configuração em computadores que executam o Linux ou o UNIX. Este cliente é projetado para servidores que operam como um computador de grupo de trabalho, e o cliente não suporta interação com utilizadores conectados. Depois de instalar o software do cliente e o cliente estabelecer comunicação com o site do Gestor de Configuração, gere o cliente utilizando a consola e os relatórios do Gestor de Configuração.  

> [!NOTE]
>  O cliente do Gestor de Configuração dos computadores Linux e UNIX não suporta as seguintes capacidades de gestão:  
> 
> - Instalação push do cliente  
>   -   Implementação do sistema operativo  
>   -   Implementação de aplicações; em vez disso, implemente software utilizando pacotes e programas.  
>   -   Inventário de software  
>   -   Atualizações de software  
>   -   Definições de compatibilidade  
>   -   Controlo remoto  
>   -   Gestão de energia  
>   -   Verificação de cliente do estado do cliente e remediação  
>   -   Gestão de clientes baseada na Internet  

 Para obter informações sobre as distribuições suportadas de Linux e UNIX e o hardware necessário para apoiar o cliente para linux e UNIX, consulte [hardware recomendado para O Gestor](../../../../core/plan-design/configs/recommended-hardware.md)de Configuração .  

 Utilize as informações deste artigo para o ajudar a planear implementar o cliente do Gestor de Configuração para o Linux e uniX.  

##  <a name="prerequisites-for-client-deployment-to-linux-and-unix-servers"></a><a name="BKMK_ClientDeployPrereqforLnU"></a>Pré-requisitos para a implantação de clientes para servidores Linux e UNIX  
 Utilize as seguintes informações para determinar os pré-requisitos que devem estar implementados para instalar o cliente para Linux e UNIX.  

###  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ClientDeployExternalforLnU"></a>Dependências Externas ao Gestor de Configuração:  
 As tabelas seguintes descrevem os sistemas operativos UNIX e Linux necessários e as dependências de pacote.  

 **Red Hat Enterprise Linux Server release 5.1 (Tikanga)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.5-12|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8b-8.3.el5|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server release 6**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.12-1.7|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|1.0.0-4|  
|PAM|Módulos de Autenticação Incorporável|1.1.1-4|  

 **Red Hat Enterprise Linux Server release 7**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliotecas Padrão C|2.17|  
|Openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|1.0.1|  
|PAM|Módulos de Autenticação Incorporável|1.1.1-4|  

 **Solaris 10 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch de sistema operativo necessário|Fuga de memória de PAM|117463-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Bibliotecas de Matemática e de Microtarefas (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Bibliotecas de Matemática e de Microtarefas (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Bibliotecas de Solaris Principais (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|OpenSSL|Bibliotecas de SUNopenssl (Usr)<br /><br /> A Sun fornece as bibliotecas OpenSSL para o Solaris 10 SPARC. Estão incluídas no sistema operativo.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Módulos de Autenticação Incorporável<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Patch de sistema operativo necessário|Fuga de memória de PAM|117464-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Bibliotecas Math e Microtasking (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Core Solaris, (Shared Libs) (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Bibliotecas de Solaris Core (Root) (i386)|11.10.0, REV=2005.01.21.16.34|  
|OpenSSL|Bibliotecas de SUNWopenssl; Bibliotecas de OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Módulos de Autenticação Incorporável<br /><br /> SUNWcsr Core Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Matemática e Microtarefas (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Solaris Principal (Root)|11.11, REV=2009.11.11|  
|Bibliotecas de SUNWopenssl|Bibliotecas de OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliotecas de Matemática e Microtarefas (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Bibliotecas de Solaris Principais (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Solaris Principal (Root)|11.11, REV=2009.11.11|  
|Bibliotecas de SUNWopenssl|Bibliotecas de OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.4-31.30|Biblioteca partilhada padrão C|2.4-31.30|  
|OpenSSL|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.90,8a-18,15|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Biblioteca partilhada padrão C|2.9-13.2|  
|PAM|Módulos de Autenticação Incorporável|pam-1.0.2-20.1|  

 **Universal Linux (pacote Debian) Debian, Ubuntu Server**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|libc6|Biblioteca partilhada padrão C|2.3.6|  
|OpenSSL|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Incorporável|0.79-3|  

 **Universal Linux (pacote RPM) CentOS, Oracle Linux**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|glibc|Biblioteca partilhada padrão C|2.5-12|  
|OpenSSL|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8 ou 1.0|  
|PAM|Módulos de Autenticação Incorporável|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operativo|AIX 6.1: qualquer nível de tecnologia e pacote de serviço|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|Versão do SO|Versão do sistema operativo|AIX 7.1: qualquer nível de tecnologia e pacote de serviço|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede||  


 **HP-UX 11i v3 IA64**  

|Pacote necessário|Descrição|Versão mínima|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|Base do Ambiente Operativo de HP-UX|B.110,310,0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliotecas de desenvolvimento do IA específicas|B.110,31|  
|SysMgmtMin|Ferramentas de Implementação de Software Mínimas|B.110,310,0709|  
|SysMgmtMin.openssl|Bibliotecas de OpenSSL; Protocolo Seguro de Comunicações de Rede|A.00.09.08d.002|  
|PAM|Módulos de Autenticação Incorporável|Em HP-UX, PAM faz parte dos componentes principais do sistema operativo. Não existem nenhumas outras dependências.|  

 **Dependências do Gestor de Configuração:** A tabela seguinte lista as funções do sistema de site que suportam os clientes Linux e UNIX. Para obter mais informações sobre estas funções do sistema do site, consulte [Determinar as funções do sistema do site para clientes do Gestor de Configuração](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Sistema de site do Gestor de Configuração|Mais informações|  
|---------------------------------------|----------------------|  
|Ponto de gestão|Embora um ponto de gestão não seja necessário para instalar um cliente de Gestor de Configuração para linux e UNIX, você deve ter um ponto de gestão para transferir informações entre computadores clientes e servidores de Gestor de Configuração. Sem um ponto de gestão, não se pode gerir computadores de clientes.|  
|Ponto de distribuição|O ponto de distribuição não é necessário para instalar um cliente de Gestor de Configuração para linux e UNIX. No entanto, a função de sistema de sites é necessária se implementar software em servidores Linux e UNIX.<br /><br /> Uma vez que o cliente do Gestor de Configuração da Linux e da UNIX não suporta comunicações que utilizem SMB, os pontos de distribuição que utiliza com o cliente devem suportar a comunicação HTTP ou HTTPS.|  
|Ponto de estado de contingência|O ponto de estado de recuo não é necessário para instalar um cliente de Gestor de Configuração para linux e UNIX. No entanto, o ponto de estado de recuo permite que os computadores no site do Gestor de Configuração enviem mensagens de Estado quando não conseguem comunicar com um ponto de gestão. O cliente também pode enviar o respetivo estado de instalação para o ponto de estado de contingência.|  

 **Requisitos de firewall**: Certifique-se de que as firewalls não bloqueiam as comunicações através das portas que especifica como portas de pedido do cliente. O cliente para Linux e UNIX comunica diretamente com pontos de gestão, pontos de distribuição e pontos de estado de contingência.  

 Para obter informações sobre a as portas de pedido e a comunicação do cliente, veja [Configurar o Cliente para Linux e UNIX para Localizar Pontos de Gestão](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="planning-for-communication-across-forest-trusts-for-linux-and-unix-servers"></a><a name="BKMK_PlanningforCommunicationsforLnU"></a>Planeamento de Comunicação através de Fundos Florestais para Linux e SERVIDORES UNIX  
 Os servidores Linux e UNIX que gere com o Gestor de Configuração operam como clientes de grupo de trabalho e requerem configurações semelhantes às dos clientes baseados no Windows que estão num grupo de trabalho. Para obter informações sobre comunicações de computadores que se encontram em grupos de trabalho, consulte comunicações através de [florestas de Diretório Ativo](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).  

###  <a name="service-location-by-the-client-for-linux-and-unix"></a><a name="BKMK_ServiceLocationforLnU"></a>Localização do serviço pelo cliente para Linux e UNIX  
 A tarefa de localizar um servidor de sistema de sites que forneça serviços aos clientes é referida como localização de serviço. Ao contrário de um cliente baseado no Windows, o cliente da Linux e da UNIX não utiliza o Ative Directory para a localização do serviço. Além disso, o cliente do Gestor de Configuração da Linux e da UNIX não suporta uma propriedade de cliente que especifique o sufixo de domínio de um ponto de gestão. Em vez disso, o cliente toma conhecimento dos servidores de sistema de sites adicionais que fornecem serviços aos clientes a partir de um ponto de gestão conhecido, que é atribuído quando instala o software de cliente.  

 Para mais informações, consulte a Localização do [Serviço e como os clientes determinam o seu ponto de gestão atribuído](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

##  <a name="planning-for-security-and-certificates-for-linux-and-unix-servers"></a><a name="BKMK_SecurityforLnU"></a>Planeamento de Segurança e Certificados para Servidores Linux e UNIX  
 Para comunicações seguras e autenticadas com sites do Gestor de Configuração, o cliente do Gestor de Configuração do Linux e da UNIX utiliza o mesmo modelo para comunicação que o cliente do Gestor de Configuração para windows.  

 Quando instalar o cliente Linux e UNIX, pode atribuir ao cliente um certificado PKI que lhe permite utilizar HTTPS para comunicar com sites do Gestor de Configuração. Se não atribuir um certificado PKI, o cliente cria um certificado auto-assinado e comunica apenas pela HTTP.  

 Os clientes aos quais é fornecido um certificado PKI, quando são instalados, utilizam HTTPS para comunicar com pontos de gestão. Quando um cliente não consegue localizar um ponto de gestão que suporte HTTPS, irá reverter para a utilização de HTTP com o certificado PKI fornecido.  

 Quando um cliente Linux ou UNIX usa um certificado PKI, não tem de os aprovar. Quando um cliente usa um certificado auto-assinado, reveja as definições de hierarquia para aprovação do cliente na consola Do Gestor de Configuração. Se o método de aprovação do cliente não for **Aprovar automaticamente todos os computadores (não recomendado)**, terá de aprovar manualmente o cliente.  

 Para obter mais informações sobre como aprovar manualmente o cliente, consulte [Gerir os clientes a partir do nó dos dispositivos](../../manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 Para obter informações sobre como utilizar certificados no Gestor de Configuração, consulte [os requisitos do certificado PKI](../../../plan-design/network/pki-certificate-requirements.md).  

###  <a name="about-certificates-for-use-by-linux-and-unix-servers"></a><a name="BKMK_AboutCertsforLnU"></a>Sobre Certificados para utilização por Linux e SERVIDORUNIX  
 O cliente do Gestor de Configuração do Linux e da UNIX utiliza um certificado auto-assinado ou um certificado PKI X.509 tal como os clientes baseados no Windows. Não existem alterações nos requisitos do PKI para sistemas de site do Gestor de Configuração quando gere os clientes Linux e UNIX.  

 Os certificados que utiliza para clientes Linux e UNIX que comunicam aos sistemas de site do Gestor de Configuração devem estar num formato De Certificado de Chave Pública (PKCS#12) e a palavra-passe deve ser conhecida para que possa especificá-la ao cliente quando especificar o certificado PKI.  

 O cliente do Gestor de Configuração da Linux e da UNIX suporta um único certificado PKI e não suporta vários certificados. Portanto, os critérios de seleção de certificados que configura para um site do Gestor de Configuração não se aplicam.  

###  <a name="configuring-certificates-for-linux-and-unix-servers"></a><a name="BKMK_ConfigCertsforLnU"></a>Configuração de Certificados para Servidores Linux e UNIX  
 Para configurar um cliente de Gestor de Configuração para servidores Linux e UNIX para utilizar comunicações HTTPS, tem de configurar o cliente para utilizar um certificado PKI no momento em que instala o cliente. Não pode fornecer um certificado antes da instalação do software do cliente.  

 Quando instala um cliente que utiliza um certificado PKI, `-UsePKICert` utiliza o parâmetro da linha de comando para especificar a localização e o nome de um ficheiro PKCS#12 que contém o certificado PKI. Além disso, deve utilizar o `-certpw` parâmetro da linha de comando para especificar a palavra-passe para o certificado.  

 Se não especificar, `-UsePKICert`o cliente gera um certificado auto-assinado e tenta comunicar aos servidores do sistema do site usando apenas HTTP.  

##  <a name="versions-that-dont-support-sha-256"></a><a name="BKMK_NoSHA-256"></a>Versões que não suportam SHA-256  
 Os seguintes sistemas operativos Linux e UNIX que são suportados como clientes para O Gestor de Configuração foram lançados com versões do OpenSSL que não suportam SHA-256:  

-   Versão Solaris 10 (SPARC/x86)  


 Para gerir estes sistemas operativos com o Gestor de Configuração, tem de instalar o cliente do Gestor de Configuração para o Linux e o UNIX com um interruptor de linha de comando que direciona o cliente para a validação de SHA-256. Os clientes do Gestor de Configuração que executam estas versões do sistema operativo operam num modo menos seguro do que os clientes que suportam o SHA-256. Este modo menos seguro de funcionamento tem o seguinte comportamento:  

-   Os clientes não validam a assinatura do servidor do site associada à política que solicitam a partir de um ponto de gestão.  

-   Os clientes não validam o hash para pacotes que descarregam a partir de um ponto de distribuição.  

> [!IMPORTANT]  
>  A `ignoreSHA256validation` opção permite-lhe executar o cliente para computadores Linux e UNIX num modo menos seguro. Destina-se à utilização em plataformas mais antigas que não incluíam suporte para SHA-256. Trata-se uma substituição de segurança e não é recomendada pela Microsoft, mas é suportada para utilização num ambiente de centro de dados seguro e fidedigno.  

 Quando o cliente do Gestor de Configuração do Linux e uniX instala, o script de instalação verifica a versão do sistema operativo. Por predefinição, se a versão do sistema operativo for identificada como tendo sido lançada sem uma versão do OpenSSL que suporta o SHA-256, a instalação do cliente Do Gestor de Configuração falha.  

 Para instalar o cliente do Gestor de Configuração nos sistemas operativos Linux e UNIX que não foram lançados com uma `ignoreSHA256validation`versão do OpenSSL que suporta o SHA-256, tem de utilizar o interruptor de linha de comando de instalação . Quando utilizar esta opção de linha de comando num sistema operativo Linux ou UNIX aplicável, o cliente do Gestor de Configuração ignorará a validação SHA-256 e após a instalação, o cliente não utilizará o SHA-256 para assinar os dados que submete aos sistemas do site utilizando http. Para obter informações sobre a configuração dos clientes Linux e UNIX para utilizar certificados, consulte [Planeamento de Segurança e Certificados para Servidores Linux e UNIX](#BKMK_SecurityforLnU). Para obter mais informações sobre a necessidade de SHA-256, consulte a [assinatura e encriptação do Configure](../../../plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption).  

> [!NOTE]  
>  A opção `ignoreSHA256validation` de linha de comando é ignorada em computadores que executam uma versão do Linux e da UNIX que foi lançada com versões do OpenSSL que suportam o SHA-256.  
