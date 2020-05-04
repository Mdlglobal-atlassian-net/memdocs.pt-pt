---
title: Planear o Fornecedor de SMS
titleSuffix: Configuration Manager
description: Conheça a função do sistema de site do Fornecedor SMS no Gestor de Configuração.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01ea9b089da3cfcfc3e8d23e7ad25d27ab2fec7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712555"
---
# <a name="plan-for-the-sms-provider"></a>Planear o Fornecedor de SMS

*Aplica-se a: Gestor de Configuração (ramo atual)*

Para gerir o Gestor de Configuração, utilize uma consola de Configuração Manager que se conecta a uma instância do **Fornecedor SMS**. Por predefinição, um Fornecedor SMS instala-se no servidor do site quando instala um site de administração central ou um site primário.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Acerca do Fornecedor de SMS  

O Provedor de SMS é um fornecedor de Instrumentação **write** de Gestão do Windows (WMI) que atribui acesso à **base** de dados do Gestor de Configuração num site.  

- Cada site de administração central e site primário precisa de, pelo menos, um Fornecedor de SMS. Se necessário, pode instalar fornecedores adicionais.  

- O grupo de segurança **SMS Admins** fornece acesso ao Fornecedor SMS. O Gestor de Configuração cria automaticamente este grupo no servidor do site e em cada computador onde instala uma instância do Fornecedor SMS. Para mais informações, consulte [sMS Admins](accounts.md#sms-admins).  

- Os sites secundários não suportam o papel de Fornecedor de SMS.  

Os utilizadores administrativos do Gestor de Configuração utilizam um Fornecedor De SMS para aceder à informação armazenada na base de dados. Para isso, os administradores podem usar a consola do Gestor de Configuração, o Explorador de Recursos, ferramentas e scripts personalizados. O Fornecedor SMS não interage com os clientes do Gestor de Configuração. Quando uma consola do Gestor de Configuração se conecta a um site, consulta o WMI no servidor do site para localizar uma instância do Fornecedor SMS a utilizar.  

O Fornecedor SMS ajuda a impor a segurança do Gestor de Configuração. Devolve apenas a informação que o utilizador da consola está autorizado a visualizar.  

O Provedor SMS também fornece acesso de interoperabilidade da API através do HTTPS, chamado serviço de **administração.** Esta API REST pode ser usada no lugar de um serviço web personalizado para aceder a informações a partir do site. Para mais informações, veja [qual é o serviço de administração?](../../../develop/adminservice/overview.md)

> [!IMPORTANT]  
> Quando cada instância do Fornecedor SMS para um site está offline, as consolas do Gestor de Configuração não podem ligar-se ao site.  

Para obter mais informações sobre como gerir o Fornecedor de SMS, consulte [Gerir o Fornecedor de SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Pré-requisitos de instalação  

Para suportar o Fornecedor SMS, o servidor-alvo deve satisfazer os seguintes pré-requisitos:  

- No mesmo domínio que o servidor do site e os sistemas de site de base de dados do site  

- Não pode ter um papel no sistema de site de um site diferente  

- Não pode já ter um Provedor de SMS de qualquer site  

- Executar uma versão oS suportada  

- Pelo menos 650 MB de espaço de disco gratuito para suportar os componentes ADK do Windows. Para obter mais informações sobre o Windows ADK e o Fornecedor SMS, consulte os requisitos de [implementação do OS](#BKMK_WAIKforSMSProv).  

- Para o [serviço de administração](../../../develop/adminservice/overview.md) REST API:

  - .NET 4.5 ou mais tarde

  - Ativar o servidor web do servidor do Windows **(IIS)**

    > [!Note]  
    > Todos os Fornecedores de SMS tentam instalar o serviço de administração, que requer um certificado. Este serviço tem uma dependência do IIS para ligar esse certificado à porta HTTPS 443. Se ativar o [HTTP melhorado,](enhanced-http.md)o site liga esse certificado utilizando APIs IIS. Se o seu site utilizar o PKI, tem de ligar manualmente um certificado PKI no IIS no Fornecedor SMS. A partir da versão 2002, o site utiliza automaticamente o certificado auto-assinado do site.

## <a name="locations"></a><a name="bkmk_location"></a>Localizações  

Quando instala um site, instala automaticamente o primeiro Fornecedor De SMS para o site. Pode especificar qualquer uma das seguintes localizações suportadas para o Fornecedor de SMS:  

- O servidor do site  

- O servidor de base de dados do site  

- Outro servidor, que cumpre os [pré-requisitos](#installation-prerequisites) de instalação  

Para ver as localizações de cada Fornecedor de SMS para um site:

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho da **Administração,** expanda a **Configuração do Site**e, em seguida, selecione o nó **de Sites.**  

2. Selecione o site desejado na lista e, em seguida, escolha **Propriedades** na fita.  

3. No separador **Geral** do site **Propriedades,** consulte o campo de localização do **Fornecedor SMS.**  

Cada Fornecedor de SMS suporta ligações simultâneas a partir de múltiplos pedidos. As únicas limitações nestas ligações são o número de ligações do servidor que estão disponíveis para o Windows, e os recursos disponíveis no servidor para atender os pedidos de ligação.  

Depois de instalar um site, pode executar novamente a configuração do 'Gestor de Configuração' no servidor do site. Utilize a configuração para alterar a localização de um Fornecedor de SMS existente, ou para instalar fornecedores de SMS adicionais nesse site. Instale apenas um Fornecedor de SMS num computador. Um computador não pode hospedar um Provedor de SMS de mais de um site.  

### <a name="choosing-a-location"></a>Selecionar uma localização

As seguintes secções descrevem as vantagens e desvantagens da instalação de um Fornecedor de SMS em cada local suportado:  

#### <a name="configuration-manager-site-server"></a>Servidor de site do Gestor de Configuração

- **Vantagens:**  

  - O Provedor de SMS não utiliza os recursos do sistema do computador de base de dados do site.  

  - Esta localização pode proporcionar melhor desempenho do que um Fornecedor de SMS localizado num computador que não o servidor do site ou o computador da base de dados do site.  

- **Desvantagens:**  

  - O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações do servidor do site.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server que acolhe a base de dados do site

- **Vantagens:**  

  - O Fornecedor SMS não utiliza recursos do sistema no servidor do site.  

  - Esta localização pode proporcionar o melhor desempenho das três localizações, desde que estejam disponíveis recursos suficientes no servidor.  

- **Desvantagens:**  

  - O Fornecedor de SMS utiliza recursos de sistema e de rede que poderiam ser dedicados às operações de base de dados do site.  

  - Quando a base de dados do site está alojada numa instância agrupada do SQL Server, não pode utilizar esta localização.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Computador que não seja o servidor do site ou servidor de base de dados do site

- **Vantagens:**  

  - O Fornecedor SMS não utiliza recursos do servidor do site ou do sistema de base de dados do site.  

  - Este tipo de localização permite-lhe implementar Fornecedores de SMS adicionais para proporcionar uma elevada disponibilidade das ligações.  

- **Desvantagens:**  

  - O desempenho do Fornecedor SMS pode ser reduzido. Este comportamento deve-se à atividade adicional de rede que necessita para coordenar com o servidor do site e o computador de base de dados do site.  

  - Este servidor deve estar sempre acessível ao servidor de base de dados do site e a todos os computadores com a consola 'Gestor de Configuração' instalada.  

  - Esta localização pode utilizar recursos de sistema que, em condições normais, estariam dedicados a outros serviços.  

## <a name="authentication"></a><a name="bkmk_auth"></a>Autenticação

<!--1357013-->
A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores acederem aos sites do Gestor de Configuração. Esta funcionalidade impõe aos administradores que assinem no Windows com o nível exigido. Aplica-se a todos os componentes que acedem ao Fornecedor de SMS. Por exemplo, a consola do Gestor de Configuração, os métodos SDK e os cmdlets do Windows PowerShell.

### <a name="configure-authentication"></a>Configurar a autenticação

Para configurar esta definição, insera-se primeiro no Windows com o nível de autenticação pretendido.

> [!Important]  
> Esta configuração é um cenário de hierarquia. Antes de alterar esta definição, certifique-se de que todos os administradores do 'Gestor de Configuração' podem iniciar sessão no Windows com o nível de autenticação exigido.

Para configurar esta definição, utilize os seguintes passos:

1. Na consola Do Gestor de Configuração, vá ao espaço de trabalho **da Administração,** expanda a **Configuração do Site**e selecione o nó de **Sites.**  

2. **Selecione Definições de hierarquia** na fita.  

3. Mude para o separador **Autenticação.** Selecione o nível de [autenticação](#authentication-levels)desejado e, em seguida, selecione **OK**.  

    - Só quando necessário, selecione **Adicionar** para excluir utilizadores ou grupos específicos. Para mais informações, consulte [Exclusões](#exclusions).  

### <a name="authentication-levels"></a>Níveis de autenticação

Estão disponíveis os seguintes níveis:

- **Autenticação do Windows**: Exigir autenticação com credenciais de domínio de Diretório Ativo. Esta definição é o comportamento anterior e a definição padrão atual. Quando atualiza o site, não há alteração ao nível de autenticação.  

- **Autenticação do certificado**: Exigir autenticação com um certificado válido emitido por uma autoridade de certificados PKI fidedigna. Não configura este certificado no Diretor de Configuração. O Gestor de Configuração requer que o administrador seja assinado no Windows utilizando o PKI.  

- **Windows Hello for Business authentication**: Requerer a autenticação com autenticação forte de dois fatores que esteja ligada a um dispositivo e utilize biometria ou PIN. Para mais informações, consulte [o Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Exclusões

A partir do separador **autenticação** das Definições da Hierarquia, também pode excluir certos utilizadores ou grupos. Utilize esta opção com moderação. Por exemplo, quando utilizadores específicos necessitam de acesso à consola Do Gestor de Configuração, mas não conseguem autenticar o Windows ao nível exigido. Pode também ser necessário para automação ou serviços que sejam executados no contexto de uma conta de sistema.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a>Sobre os idiomas do Fornecedor sMS  

O Fornecedor SMS opera independentemente do idioma de exibição do servidor onde o instala.  

Quando um utilizador administrativo ou o processo de Configuração solicita dados utilizando o Fornecedor SMS, tenta devolver esses dados num formato que corresponda ao idioma OS do computador solicitado.

A forma como tenta combinar com a linguagem é indireta. O Provedor de SMS não traduz informação de um idioma para outro. Quando devolve os dados para visualização na consola Do Gestor de Configuração, o idioma de visualização dos dados depende da origem do objeto e do tipo de armazenamento.  

Quando o Gestor de Configuração armazena dados para um objeto na base de dados, as línguas disponíveis dependem dos seguintes fatores:  

- O Gestor de Configuração armazena objetos que cria utilizando suporte para vários idiomas. Armazena o objeto na base de dados do site utilizando os idiomas que configura para o site quando executa a configuração. A consola 'Gestor de Configuração' apresenta estes objetos no idioma de exibição do computador solicitado, quando esse idioma está disponível para o objeto. Se a consola não conseguir visualizar o objeto no idioma de visualização do computador solicitado, exibe o objeto no idioma predefinido, que é inglês.  

- O Gestor de Configuração armazena objetos que um utilizador administrativo cria utilizando o idioma que foi usado para criar o objeto. Estes objetos exibem na consola 'Gestor de Configuração' neste mesmo idioma. O Provedor de SMS não pode traduzi-los, e eles não têm várias opções linguísticas.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a>Utilize vários Fornecedores de SMS  

Após um site concluir a instalação, poderá instalar Fornecedores de SMS adicionais para o site. Para instalar fornecedores de SMS adicionais, executar configuração do Gestor de Configuração no servidor do site.

Considere instalar fornecedores de SMS adicionais quando qualquer um dos seguintes fornecedores for verdadeiro:  

- Muitos utilizadores administrativos precisam de utilizar a consola Do Gestor de Configuração e ligar-se a um site ao mesmo tempo.  

- Utiliza o SDK do Gestor de Configuração, ou outros produtos, que podem introduzir chamadas frequentes para o Fornecedor sms.  

- Tem um requisito de negócio para uma elevada disponibilidade do Provedor de SMS.  

Quando instala vários Fornecedores de SMS num site, e é feito um pedido de ligação, o site atribui aleatoriamente cada novo pedido de ligação para utilizar um Fornecedor SMS instalado. Não é possível especificar o Fornecedor SMS a utilizar com uma sessão de ligação específica.  

> [!NOTE]  
> Considere as vantagens e desvantagens de cada localização do Fornecedor SMS. Para mais informações, consulte [Localizações](#bkmk_location). Equilibre estas considerações com a informação que não pode controlar qual o Fornecedor SMS utilizado para cada nova ligação.  

Quando liga si pela primeira vez uma consola de Configuração a um site, a ligação consulta o WMI no servidor do site. Esta consulta identifica uma instância do Fornecedor SMS que a consola utiliza. Esta instância específica do Fornecedor SMS permanece em uso pela consola até ao final da sessão. Se a sessão terminar porque o servidor SMS Provider não está disponível na rede, quando reconecta a consola ao site, repete a consulta inicial. É possível que o site atribua a mesma instância de Fornecedor SMS que não está disponível. Se este comportamento ocorrer, tente reconectar a consola até que o site desemque um Fornecedor SMS disponível.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a>Sobre o espaço de nome do Fornecedor SMS  

O esquema Do Gestor de Configuração WMI define a estrutura do Provedor de SMS. Os espaços de nome schema descrevem a localização dos dados do Gestor de Configuração dentro do esquema do Fornecedor SMS. A tabela que se segue contém alguns dos espaços de nome comuns que o Fornecedor SMS utiliza:  

|Espaço de nomes|Descrição|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|O Provedor SMS, que é extensivamente utilizado pela consola do Gestor de Configuração, pelo Explorador de Recursos, ferramentas de Gestor de Configuração e scripts.|  
|`Root\SMS\SMS_ProviderLocation`|A localização dos computadores SMS Provider para um site.|  
|`Root\CIMv2`|A localização inventariada para informações de espaço de nome WMI durante o inventário de hardware e software.|  
|`Root\CCM`|Política de configuração do gestor de clientes e dados do cliente.|  
|`Root\CIMv2\SMS`|A localização das aulas de relatórios de inventário que o agente cliente de inventário recolhe. Os clientes compilam estas definições durante a avaliação da política informática. Estas definições baseiam-se na configuração do cliente para o computador.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a>Requisitos de implementação do OS

O computador onde instala uma instância do Fornecedor SMS requer uma versão suportada do Windows ADK.  

Para obter mais informações sobre este requisito, consulte [os requisitos de infraestrutura para a implementação](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) do OS e [suporte para o Windows 10](../configs/support-for-windows-10.md).  

Ao gerir as implementações do OS, o Windows ADK permite ao Fornecedor SMS completar várias tarefas, tais como:  

- Ver detalhes do ficheiro WIM  

- Adicionar ficheiros de controladores a imagens de arranque existentes  

- Criar ficheiros ISO de arranque  

A instalação do Windows ADK pode precisar de até 650 MB de espaço livre em disco em cada computador que instala o Fornecedor de SMS. Este requisito de espaço de disco elevado é necessário para o Gestor de Configuração instalar as imagens de boot do Windows PE.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a>Serviço de administração

<!--3607711, fka 1321523-->

O Provedor SMS proporciona acesso de interoperabilidade da API através de uma ligação HTTPS OData, chamada serviço de **administração.** Esta API REST pode ser usada no lugar de um serviço web personalizado para aceder a informações a partir do site.

Para mais informações, consulte [o que é o serviço de administração?](../../../develop/adminservice/overview.md)
