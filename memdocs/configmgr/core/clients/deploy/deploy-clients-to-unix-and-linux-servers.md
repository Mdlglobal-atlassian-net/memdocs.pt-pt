---
title: Implementar clientes UNIX/Linux
titleSuffix: Configuration Manager
description: Aprenda a implementar um cliente num servidor UNIX ou Linux no Gestor de Configuração.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906326"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Como implementar clientes para servidores UNIX e Linux no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

> [!Important]  
> A partir da versão 1902, o Gestor de Configuração não suporta clientes Linux ou UNIX. 
> 
> Considere a Microsoft Azure Management para gerir servidores Linux. As soluções Azure têm um suporte linux extensivo que na maioria dos casos excede a funcionalidade do Gestor de Configuração, incluindo a gestão de patch sem fim para o Linux.


Antes de poder gerir um servidor Linux ou UNIX com o Gestor de Configuração, tem de instalar o cliente do Gestor de Configuração para linux e UNIX em cada servidor Linux ou UNIX. Pode efetuar a instalação do cliente manualmente em cada computador ou utilizar um script de shell que instala o cliente remotamente. O Gestor de Configuração não suporta o uso da instalação push do cliente para servidores Linux ou UNIX. Opcionalmente, pode configurar um Runbook do System Center Orchestrator para automatizar a instalação do cliente no servidor Linux ou UNIX.  

 Independentemente do método de instalação utilizado, o processo de instalação requer a utilização de um script com o nome **install** para gerir o processo de instalação. Este script está incluído quando transferir o cliente para Linux e UNIX.  

 O script de instalação para o cliente do Gestor de Configuração para Linux e UNIX suporta propriedades da linha de comando. Algumas propriedades da linha de comando são necessárias, enquanto outras são opcionais. Por exemplo, quando instala o cliente, tem de especificar um ponto de gestão do site que é utilizado pelo servidor Linux ou UNIX para o contacto inicial com o site. Para obter a lista completa de propriedades da linha de comando, consulte [as propriedades da linha de comando para instalar o cliente nos servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

 Depois de instalar o cliente, especifice as Definições do Cliente na consola Do Gestor de Configuração para configurar o agente cliente da mesma forma que os clientes baseados no Windows. Para obter mais informações, veja  [Definições de cliente para servidores Linux e UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>Sobre os pacotes de instalação de clientes e o agente universal  
 Para instalar o cliente para Linux e UNIX numa plataforma específica, tem de utilizar o pacote de instalação de cliente aplicável ao computador onde instalar o cliente. Os pacotes de instalação de cliente aplicáveis são incluídos como parte de cada transferência de cliente a partir do [Centro de Transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Para além de pacotes de instalação de cliente, a transferência do cliente inclui o script de **instalação** que gere a instalação do cliente em cada computador.  

 Ao instalar um cliente, pode utilizar as mesmas propriedades de processo e linha de comando, independentemente do pacote de instalação do cliente que utilize.  

 Para obter informações sobre os sistemas operativos, plataformas e pacotes de instalação de clientes que são suportados por cada lançamento do cliente do Gestor de Configuração para linux e UNIX, consulte [os servidores Linux e UNIX.](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers)  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>Instale o cliente nos servidores Linux e UNIX  
 Para instalar o cliente para Linux e UNIX, tem de executar um script em cada computador Linux ou UNIX. O script é nomeado **instalar** e suporta propriedades da linha de comando que modificam o comportamento de instalação e referenciam o pacote de instalação do cliente. O script de instalação e o pacote de instalação de cliente têm de estar localizados no cliente. O pacote de instalação do cliente contém os ficheiros do cliente do Gestor de Configuração para um sistema operativo específico Linux ou UNIX e plataforma.
Cada pacote de instalação de clientes contém todos os ficheiros necessários para completar a instalação do cliente e, ao contrário dos computadores baseados no Windows, não descarrega ficheiros adicionais a partir de um ponto de gestão ou de outra localização de origem.  

 Depois de instalar o cliente do Gestor de Configuração para o Linux e uniX, não precisa de reiniciar o computador. Assim que a instalação do software estiver concluída, o cliente está operacional. Se reiniciar o computador, o cliente do Gestor de Configuração reinicia automaticamente.  

 O cliente instalado é executado com credenciais de raiz. As credenciais de raiz são necessárias para recolher o inventário de hardware e fazer implementações de software.  

 Utilize o seguinte formato de comando:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install`é o nome do ficheiro script que instala o cliente para linux e UNIX. Este ficheiro é fornecido com o software de cliente.  

-   `-mp <computer>`especifica o ponto de gestão inicial que é utilizado pelo cliente. Exemplo: `smsmp.contoso.com`  

-   `-sitecode <site code>`especifica o código do site a que o cliente é designado. Exemplo: `S01`  

-   `<property #1> <property #2>`especifica as propriedades da linha de comando para usar com o script de instalação.  

    > [!NOTE]  
    >  Para mais informações, consulte [as propriedades da linha de comando para instalar o cliente nos servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **client installation package** é o nome do pacote .tar de instalação de cliente para o sistema operativo, versão e arquitetura de CPU deste computador. O ficheiro .tar de instalação de cliente tem de ser especificado no fim. Exemplo: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>Para instalar o cliente do Gestor de Configuração nos servidores Linux e UNIX  

1.  Num computador Windows, [transfira o ficheiro de cliente adequado para o servidor Linux ou UNIX](https://www.microsoft.com/download/details.aspx?id=47719) que pretende gerir.  

2.  Execute o ficheiro .exe de extração automática no computador Windows para extrair o script de instalação e o ficheiro .tar de instalação do cliente.  

3.  Copie o script **install** e o ficheiro .tar para uma pasta no servidor que pretende gerir.  

4.  No servidor UNIX ou Linux, execute o seguinte comando para permitir que o script corra como um programa:`chmod +x install`  

    > [!IMPORTANT]  
    >  É necessário utilizar credenciais de raiz para instalar o cliente.  

5.  Em seguida, executar o seguinte comando para instalar o cliente do Gestor de Configuração:`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Ao introduzir este comando, utilize as propriedades de linha de comandos adicionais de que necessita. Para a lista de propriedades da linha de comando, consulte [as propriedades da linha de comando para instalar o cliente nos servidores Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Após a execução do script, valide a instalação revendo o ficheiro **/var/opt/microsoft/scxcm.log** . Além disso, pode confirmar que o cliente está instalado e a comunicar com o site visualizando detalhes para o cliente no nó de **Dispositivos** do espaço de trabalho **De Ativos e Compliance** na consola Do Gestor de Configuração.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>Propriedades de linha de comando para instalar o cliente em servidores Linux e UNIX  
 As seguintes propriedades estão disponíveis para modificar o comportamento do script de instalação:  

> [!NOTE]  
>  Utilize a propriedade `-h` para exibir esta lista de propriedades suportadas.  

-   `-mp <server FQDN>`  

     Necessário. Especifica por FQDN, o servidor de ponto de gestão que o cliente utiliza como ponto de contacto inicial.  

    > [!IMPORTANT]  
    >  Esta propriedade não especifica o ponto de gestão a que o cliente é atribuído após a instalação.  

    > [!NOTE]  
    >  Quando utiliza a propriedade para especificar um ponto de `-mp` gestão configurado para aceitar apenas ligações de clientes HTTPS, também deve utilizar a `-UsePKICert` propriedade.  

-   `-sitecode <sitecode>`  

     Necessário. Especifica o site principal do Gestor de Configuração para atribuir ao cliente do Gestor de Configuração. Exemplo: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Opcional. Especifica através do FQDN, o servidor de ponto de estado de contingência que o cliente utiliza para submeter mensagens de estado. Para mais informações, consulte [Determine se necessita de um ponto](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)de estado de recuo .  

-   `-dir <directory>`  

     Opcional. Especifica uma localização alternativa para instalar os ficheiros do cliente do Gestor de Configuração. Por predefinição, o cliente instala-se no seguinte local:`/opt/microsoft`  

-   `-nostart`  

     Opcional. Impede o arranque automático do serviço de cliente do Gestor de Configuração, **ccmexec.bin,** após o fim da instalação do cliente.  

     Após a instalação do cliente, tem de iniciar manualmente o serviço de cliente.  

     Por predefinição, o serviço de cliente é iniciado depois de concluída a instalação do cliente e sempre que o computador é reiniciado.  

-   `-clean`  

     Opcional. Especifica a remoção de todos os dados e ficheiros de cliente a partir de um cliente anteriormente instalado para Linux e UNIX, antes de a nova instalação ser iniciada. Esta ação remove a base de dados do cliente e a loja de certificados.  

-   `-keepdb`  

     Opcional. Especifica que a base de dados do cliente local é mantida e reutilizada quando reinstala um cliente. Por predefinição, quando reinstalar um cliente, esta base de dados é eliminada.  

-   `-UsePKICert <parameter>`  

     Opcional. Especifica o nome de ficheiro e caminho completo de um certificado PKI X.509 no formato Public Key Certificate Standard (PKCS#12). Este certificado é utilizado para autenticação de cliente. Se não for especificado um certificado durante a instalação e precisar de adicionar ou alterar um certificado, utilize o utilitário **certutil** . Para mais informações, consulte [Como gerir certificados sobre o cliente para linux e UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Quando `-UsePKICert` utilizar, deve também fornecer a palavra-passe associada ao ficheiro PKCS#12 através da utilização do `-certpw` parâmetro da linha de comando.  

     Se não utilizar esta propriedade para especificar um certificado PKI, o cliente utiliza um certificado auto-assinado e todas as comunicações para os sistemas do site estão acima de HTTP.  

     Se especificar um certificado inválido na linha de comandos de instalação do cliente, não são devolvidos erros. A validação do certificado ocorre após a instalação do cliente. Quando o cliente começa, os certificados são validados com o ponto de gestão. Se um certificado falhar na validação, a seguinte mensagem aparece em **scxcm.log**: **Falha validar o certificado para Ponto**de Gestão . A localização do ficheiro de registo predefinida é:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Deve especificar esta propriedade quando instala um cliente e utilizar a propriedade para especificar um ponto de `-mp` gestão configurado para aceitar apenas ligações de clientes HTTPS.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Opcional. Especifica a palavra-passe associada ao ficheiro PKCS#12 que especificou através da utilização da `-UsePKICert` propriedade.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Opcional. Especifica que um cliente não deve verificar a lista de revogação do certificado (CRL) quando comunica em HTTPS através de um certificado PKI. Quando esta opção não é especificada, o cliente verifica o CRL antes de estabelecer uma ligação HTTPS através da utilização de certificados PKI. Para obter mais informações sobre a verificação da CRL de cliente, veja Planear a Revogação de Certificados PKI.  

     Exemplo: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Opcional. Especifica o caminho completo e o nome do ficheiro para a chave raiz fidedigna do Gestor de Configuração. A chave de raiz fidedigna do Gestor de Configuração fornece um mecanismo que os clientes Linux e UNIX usam para verificar se estão ligados a um sistema de site que pertence à hierarquia correta.  

     Se não especificar a chave de raiz fidedigna na linha de comando, o cliente confiará no primeiro ponto de gestão com que comunica e irá automaticamente recuperar a chave raiz fidedigna desse ponto de gestão.  

     Para mais informações, consulte [Planeamento para a Chave raiz fidedigna](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exemplo: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Opcional. Especifica a porta que está configurada nos pontos de gestão que o cliente utiliza ao comunicar com pontos de gestão através de HTTP. Se a porta não for especificada, o valor padrão de 80 é utilizado.  

     Exemplo: `-httpport 80`  

-   `-httpsport <port>`  

     Opcional. Especifica a porta que está configurada nos pontos de gestão que o cliente utiliza ao comunicar com pontos de gestão através de HTTPS. Se a porta não for especificada, o valor padrão de 443 é utilizado.  

     Exemplo: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Opcional. Especifica que a instalação do cliente ignora a validação de SHA-256. Utilize esta opção ao instalar o cliente em sistemas operativos que não foram lançados com uma versão do OpenSSL que suporta o SHA-256. Para mais informações, consulte [os sistemas operativos Linux e UNIX que não suportam o SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Opcional. Especifica o caminho completo e o nome do ficheiro **.cer** do certificado auto-assinado exportado no servidor do site. Se os certificados PKI não estiverem disponíveis, o servidor do site do Gestor de Configuração gera automaticamente certificados auto-assinados.  

     Estes certificados são utilizados para confirmar se as políticas de cliente transferidas do ponto de gestão foram enviadas a partir do site pretendido. Se não for especificado um certificado autoassinado durante a instalação ou se precisar de alterar um certificado, utilize o utilitário **certutil** . Para mais informações, consulte [Como gerir certificados sobre o cliente para linux e UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Este certificado pode ser obtido através do arquivo de certificados **SMS** e tem o nome de Requerente **Servidor do Site** e o nome amigável **Certificado de Assinatura do Servidor do Site**.  

     Se esta opção não for especificada durante a instalação, os clientes Linux e UNIX confiam no primeiro ponto de gestão com que comunicam. Eles automaticamente recuperam o certificado de assinatura desse ponto de gestão.  

     Exemplo: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Opcional. Especifica certificados PKI adicionais para importar que não façam parte de uma hierarquia da autoridade de certificação de pontos de gestão (CA). Se especificar vários certificados na linha de comandos, estes devem ser delimitados por vírgulas.  

     Utilize esta opção se utilizar certificados de cliente PKI que não acorrentam a um certificado CA raiz que é confiado pelos pontos de gestão dos seus sites. Os pontos de gestão rejeitarão o cliente se o certificado de cliente não se limitar a um certificado de raiz fidedigno na lista de emitentes de certificados do site.  

     Se não utilizar esta opção, o cliente Linux e UNIX verificará a hierarquia de confiança usando apenas o certificado na `-UsePKICert` opção.  

     Exemplo: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>Desinstalar o cliente dos servidores Linux e UNIX  
 Para desinstalar o cliente do Gestor de Configuração para o Linux e o UNIX, utiliza o utilitário de **desinstalação, desinstalar.** Por predefinição, este ficheiro está localizado na pasta **/opt/microsoft/configmgr/bin/** no computador cliente. Este comando de desinstalação não suporta quaisquer parâmetros de linha de comando e removerá todos os ficheiros relacionados com o software do cliente do servidor.  

 Para desinstalar o cliente, utilize a seguinte linha de comandos: **/opt/microsoft/configmgr/bin/uninstall**  

 Não é preciso reiniciar o computador depois de desinstalar o cliente do Gestor de Configuração para o Linux e uniX.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a>Configure Portas de Pedido para o Cliente para Linux e UNIX  
 Semelhante aos clientes baseados no Windows, o cliente do Gestor de Configuração do Linux e da UNIX utiliza HTTP e HTTPS para comunicar com os sistemas de site do Gestor de Configuração. As portas que o cliente do Gestor de Configuração utiliza para comunicar são referidas como portas de pedido.  

 Quando instalar o cliente do Gestor de Configuração para o Linux e o UNIX, pode alterar as portas de pedido predefinidas dos clientes especificando as propriedades de instalação **-httpport** e **-httpsport.** Quando não especifica a propriedade de instalação e um valor personalizado, o cliente utiliza os valores predefinidos. Os valores predefinidos são **80** para tráfego HTTP e **443** para tráfego HTTPS.  

 Depois de instalar o cliente, não pode alterar a configuração da porta de pedido. Em vez disso, para alterar a configuração da porta, tem de reinstalar o cliente e especificar a nova configuração de porta. Quando reinstalar o cliente para alterar os números da porta de pedido, execute o comando de **instalação** semelhante à instalação do novo cliente, mas utilize a propriedade adicional da linha de comando de **-keepdb**. Este interruptor instrui a instalação para manter a base de dados do cliente e os ficheiros, incluindo o CLIENTE GUID e loja de certificados.  

 Para obter mais informações sobre os números da porta de comunicação do cliente, consulte [Como configurar as portas](../../../core/clients/deploy/configure-client-communication-ports.md)de comunicação do cliente .  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a>Configure o Cliente para Linux e UNIX para localizar pontos de gestão  
 Quando instalar o cliente do Gestor de Configuração para o Linux e o UNIX, deve especificar um ponto de gestão a utilizar como ponto de contacto inicial.  

 O cliente do Gestor de Configuração da Linux e da UNIX contacta este ponto de gestão no momento em que o cliente instala. Se o cliente não conseguir contactar o ponto de gestão, o software de cliente continuará a tentar até ter êxito.  

 Para obter mais informações sobre como os clientes localizam pontos de gestão, veja [Localizar Pontos de Gestão](assign-clients-to-a-site.md#locating-management-points).
