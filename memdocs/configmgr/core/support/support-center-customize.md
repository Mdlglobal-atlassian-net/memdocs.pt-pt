---
title: Personalizar centro de suporte
titleSuffix: Configuration Manager
description: Personalize o ficheiro de configuração do Suporte Center.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078520"
---
# <a name="customize-support-center"></a>Personalizar centro de suporte

*Aplica-se a: Gestor de Configuração (ramo atual)*

A ferramenta [Do Centro](support-center.md) de Suporte inclui um ficheiro de configuração que pode personalizar. Por predefinição, quando instala o Centro de `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`Suporte, este ficheiro encontra-se no seguinte caminho: . O ficheiro de configuração altera o comportamento do programa:

- [Personalizar a recolha](#bkmk_datacoll)de dados : Editar os conjuntos de chaves de registo e espaços de nome WMI que inclui durante a recolha de dados  

- [Personalizar grupos](#bkmk_loggroups)de registo : Defina novos grupos de ficheiros de registo utilizando expressões regulares. Adicione também outros ficheiros de registo aos grupos de registo.  

- [Recolher ficheiros de registo adicionais usando wildcards:](#bkmk_wildcards)Utilize pesquisas de wildcard para recolher ficheiros de registo adicionais  

Para efazer estas alterações, precisa de permissões administrativas locais no cliente onde instalou o Centro de Suporte. Faça estas personalizações utilizando um texto ou editor XML, como notepad ou Visual Studio.

> [!Important]  
> O ficheiro de configuração do Centro de Suporte é um ficheiro formado xML. É essencial para o funcionamento do Centro de Apoio. Modificar este ficheiro só é recomendado para utilizadores que estejam familiarizados com xML e expressões regulares.  

Antes de personalizar o ficheiro de configuração do Suporte Center, guarde uma cópia de segurança do original. Esta cópia de segurança permite-lhe recuperar a funcionalidade original do Support Center se cometer erros durante a edição do ficheiro. Se não criar uma cópia de segurança e o Centro de Suporte não funcionar corretamente depois de modificar o ficheiro de configuração, reinstale o Centro de Suporte. Também pode copiar um ficheiro de configuração de outra instalação do Centro de Suporte.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a>Personalizar a recolha de dados

Para personalizar a recolha de dados sobre o cliente, modifique o ficheiro `<dataCollectorSettings>` de configuração do Support Center utilizando elementos XML contidos no elemento.


### <a name="wmi-data-collection"></a>Recolha de dados do WMI

O `<CcmWmiDataCollector>` elemento `<collectionScopes>` contém um elemento. Utilize este elemento para alterar os espaços de nome WMI a partir dos quais o Centro de Suporte recolhe dados. Também inclui `<ignoreScopes>` um elemento. Utilize este elemento para filtrar a recolha de dados a `<collectionScopes>` partir de partes dos espaços de nome definidos no elemento.  
    
#### <a name="example"></a>Exemplo
O ficheiro de configuração `root\ccm` predefinido recolhe dados do espaço de nome. Inclui este caminho `<add/>` num `<collectionScopes>`elemento em . 

Também ignora tudo `\cimodels`sob `\invagt` `\events`o `\policy` espaço de nome. Inclui estes caminhos `<add/>` em elementos `<ignoreScopes>`contidos no interior .

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Recolha de dados do registo

O `<RegistryDataCollector>` elemento `<registryKeys>` contém um elemento. Utilize este elemento para alterar as teclas de registo `HKEY_LOCAL_MACHINE` e as subteclas que o Centro de Suporte recolhe no caminho. O Centro de Suporte não suporta a recolha de dados de registo de outras vias de registo de raiz.

#### <a name="example"></a>Exemplo
Para recolher as chaves de registo dos programas clássicos `<add/>` instalados `<registryKeys>` no dispositivo, adicione o seguinte elemento no elemento:`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a>Personalizar grupos de ficheiros de registo

Para personalizar quais os ficheiros de registo do Support Center e como os `<logGroups>` apresenta na lista de **grupos de Registo,** utilize elementos no elemento. Quando inicia o Centro de Suporte, digitaliza esta secção do ficheiro de configuração. Cria então um grupo na lista de **grupos de** `<add/>` Registo para cada `<logGroups>` valor de atributo chave único encontrado nos elementos contidos no elemento.

- **Grupo de**registo `<componentLogGroup>` de componentes: O elemento utiliza um atributo chave para definir o nome do grupo de registo que aparece na lista. Também usa um atributo de valor que contém uma expressão regular (regex). Utiliza este regex para recolher um conjunto de ficheiros de registo relacionados.  

- **Grupo de registo estático:** O `<staticLogGroup>` elemento utiliza um atributo chave para definir o nome do grupo de registo que aparece na lista. Também usa um atributo de valor que define um nome de ficheiro de registo.  

Se o mesmo valor de atributo chave for utilizado num `<add/>` elemento dentro do `<componentLogGroup>` elemento e do elemento, o `<staticLogGroup>` Centro de Suporte cria um único grupo. Este grupo inclui os ficheiros de registo definidos por ambos os elementos que utilizam a mesma tecla.

#### <a name="example"></a>Exemplo
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a>Recolha de ficheiros de registo adicionais usando wildcards

Para recolher ficheiros de registo adicionais, utilize wildcards no caminho do ficheiro ou nome de ficheiro. Estes wildcards incluem variáveis ambientais em todo o sistema, tais como, `%WINDIR%`mas excluem variáveis ambientais de âmbito de utilizador, tais como `%USERPROFILE%`. Para recolher ficheiros de registo adicionais utilizando esta pesquisa `<add/>` de ficheiros de registo não recursivo, utilize um elemento dentro do `<additionalLogFiles>` elemento. 

Estes exemplos mostram como o Support Center utiliza esta funcionalidade no ficheiro de configuração predefinido.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Exemplo 1: Recolher todos os ficheiros de registo do Windows Update no diretório do Windows
O seguinte elemento recolhe `WindowsUpdate.log` qualquer ficheiro nomeado no diretório do Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Exemplo 2: Recolher todos os ficheiros de registo no diretório de Registos do Windows
O seguinte elemento recolhe qualquer ficheiro `.log` que termine no diretório de registos do Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Exemplo completo XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
