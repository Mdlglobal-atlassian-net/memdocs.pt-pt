---
title: Registos de eventos do servidor
titleSuffix: Configuration Manager
description: Uma referência técnica para as possíveis entradas do servidor BitLocker (MBAM) no registo de eventos do Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d49a24b6fea08f12d1fe70c1e0b7415adf98719
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074814"
---
# <a name="server-event-logs"></a>Registos de eventos do servidor

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

Utilize o Windows Event Viewer para visualizar os registos de eventos para os seguintes componentes do servidor de gestão BitLocker no Gestor de Configuração:

- Serviço de recuperação no ponto de gestão
- Portal self-service
- Site de administração e monitorização

Num servidor que acolhe um ou mais destes componentes, abra o Espectador de Eventos. Em seguida, vá a Registos de **Aplicações e Serviços,** **Microsoft,** **Windows,** e expanda **MBAM-Web**. Por padrão, existem registos de eventos [de administração](#admin) e [operacionais.](#operational)

As seguintes secções contêm mensagens e informações de resolução de problemas para iDs de eventos que podem ocorrer com os componentes do servidor de gestão BitLocker.

## <a name="admin"></a>Administrador

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Aplicação: {SiteName}{VirtualDirectory} está a faltar os seguintes Nomes Principais de Serviço (SPNs):{ListOfSpns} Registe as SPNs necessárias na conta: {ExecutionAccount}.

Para que a autenticação integrada do Windows tenha sucesso, as SPNs necessárias precisam de estar em vigor. Esta mensagem indica que o SPN necessário para a aplicação não está corretamente configurado. Os detalhes contidos neste evento devem fornecer mais informações.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Possíveis mensagens de erro:

- GetMachineUsers: Ocorreu um erro ao obter informações do utilizador a partir da base de dados.
- GetRecoveryKey: ocorreu um erro ao obter a chave de recuperação da base de dados.
- GetRecoveryKey: ocorreu um erro ao obter informações do utilizador a partir da base de dados.
- GetRecoveryKeyIds: ocorreu um erro ao obter ids chave de recuperação da base de dados.
- GetTpmHashForUser: Ocorreu um erro ao obter dados de hash TPM da base de dados de recuperação.
- GetTpmHashForUser: Ocorreu um erro ao obter dados de hash TPM da base de dados de recuperação.
- QueryDriveRecoveryData: Ocorreu um erro ao obter dados de recuperação de unidades a partir da base de dados.
- QueryRecoveryKeyIdsForUser: Ocorreu um erro ao obter ids chave de recuperação da base de dados.
- ConsultaVolumeUsers: Ocorreu um erro ao obter informações do utilizador a partir da base de dados.

Esta mensagem é registada sempre que há uma exceção enquanto comunica com a base de dados de recuperação. Leia as informações contidas no vestígio para obter detalhes específicos sobre a exceção.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Possíveis mensagens de erro:

- GetRecoveryKey: Ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.
- GetRecoveryKeyIds: Ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.
- GetTpmHashForUser: Ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.
- QueryRecoveryKeyIdsForUser: Ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.
- QueryDriveRecoveryData: Ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.

Esta mensagem é registada sempre que há uma exceção enquanto comunica com a base de dados de conformidade. Leia as informações contidas no vestígio para obter detalhes específicos sobre a exceção.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Esta mensagem indica uma exceção quando o serviço tenta comunicar com a base de dados de recuperação. Leia a mensagem contida no caso para obter informações específicas sobre a exceção.

Verifique se a conta de piscina de aplicações MBAM exigiu permissões para se ligar à base de dados de recuperação.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Possíveis mensagens de erro:

- Incapaz de detetar conta de máquina de cliente ou conta de utilizador de migração de dados.

    Sempre que é feita `PostKeyRecoveryInfo` `IsRecoveryKeyResetRequired`uma `CommitRecoveryKeyRest`chamada `GetTpmHash` para os métodos , ou web, ele recupera o contexto de chamada para obter credenciais de chamada. Se o contexto de chamada for nulo ou vazio, o serviço regista esta mensagem.

- A verificação da conta falhou na identidade do chamador.

    Esta mensagem é registada se o método web estiver à espera que o chamador seja uma conta de computador e não é. Também pode ser causado se o método web estiver esperando que o chamador seja uma conta de utilizador, e não é uma conta de utilizador ou um membro de uma conta de grupo de migração de dados.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

A cadeia de ligação à base de dados de conformidade no registo está vazia.

Esta mensagem é registada sempre que a cadeia de ligação db de conformidade é inválida. Verifique o valor na `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`chave do registo .

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Este erro indica que os websites ou serviços web não conseguiram ligar-se à base de dados de conformidade. Verifique se a conta de piscina de aplicativos IIS pode ligar-se à base de dados.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Erros conhecidos e possíveis causas:

- O pedido de URL causou um erro interno.

    Foi levantada uma exceção não tratada no pedido de administração e monitorização do site (helpdesk). Reveja as entradas de registo no registo do evento **Admin** para encontrar a exceção específica.

- Ocorreu um erro ao obter informações sobre o contexto de execução. Incapaz de verificar o registo do nome principal do serviço (SPN).

    Durante a operação inicial de carga do site de helpdesk, verifica o SPN. Para verificar o SPN, requer informações sobre contas, nome do Site IIS e AplicaçõesVirtualPath correspondentes ao site do helpdesk. Regista esta mensagem de erro quando um ou mais destes atributos são inválidos ou em falta.

- Ocorreu um erro ao verificar o registo do nome principal do serviço (SPN).

    Esta mensagem indica que uma exceção de segurança é lançada ao verificar o SPN. Consulte a exceção contida nos detalhes do evento.

### <a name="107-selfserviceportalerror"></a>107: AutoServicePortalError

Erros conhecidos e possíveis causas:

- Ocorreu um erro ao obter a chave de recuperação para um utilizador

    Indica que foi lançada uma exceção inesperada quando foi feito um pedido para recuperar uma chave de recuperação. Consulte a mensagem de exceção nos detalhes do evento. Se o rastreio estiver ativado na aplicação de helpdesk, consulte os dados de rastreio para obter mensagens de exceção detalhadas.

- Ocorreu um erro ao obter informações sobre o contexto de execução. Incapaz de verificar o registo do nome principal do serviço (SPN)

    Durante uma operação de carga inicial, o portal de auto-atendimento recupera informações de conta, nome do Site IIS e AplicaçãoVirtualPath para o site de self-service para verificar o SPN. Esta mensagem de erro é registada quando um ou mais destes atributos são inválidos.

- Ocorreu um erro ao verificar o registo do nome principal do serviço (SPN). Detalhes do evento:{Mensagem de exceção}

    Esta mensagem indica que foi lançada uma exceção de segurança durante a verificação da SPN. Consulte a exceção contida nos detalhes do evento.

### <a name="108-domaincontrollererror"></a>108: Error ControllerError de domínio

Erros conhecidos e possíveis causas:

- Ocorreu um erro durante a resolução do nome de domínio {DomainName}, ocorreu uma falha na atribuição de memória.

    Para resolver o nome `DsGetDcName` de domínio, chama a API do Windows. Esta mensagem é registada quando `ERROR_NOT_ENOUGH_MEMORY`esta API retorna , o que indica uma falha na atribuição de memória.

- Não podia invocar o método DsGetDcName

    Esta mensagem indica `DsGetDcName` que a API não está disponível no hospedeiro.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Erros conhecidos e possíveis causas:

- Ocorreu um erro ao ler a configuração da base de dados recovery. A cadeia de ligação à base de dados recovery não está configurada.

    Esta mensagem indica que a `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` informação de cadeia de ligação de base de dados de recuperação é inválida. Verifique o valor-chave do registo.

Se vir alguma das seguintes mensagens, verifique se as credenciais de pool de aplicações do servidor IIS podem fazer uma ligação à base de dados de recuperação:

- DoesUserHaveMatchingRecoveryKey: ocorreu um erro ao obter ids chave de recuperação para um utilizador.
- QueryDriveRecoveryData: ocorreu um erro ao obter dados de recuperação de unidades.
- QueryRecoveryKeyIdsForUser: ocorreu um erro ao obter ids chave de recuperação para um utilizador.
- Ocorreu um erro ao obter o hash de senha TPM da base de dados recovery.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Erros conhecidos e possíveis causas:

- Ocorreu um erro ao ler a configuração da base de dados compliance. A cadeia de ligação à base de dados compliance não está configurada.

    Esta mensagem indica que as `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` informações de cadeia de ligação de ligação à base de dados de conformidade são inválidas. Verifique o valor desta chave de registo.

Se vir alguma das seguintes mensagens, verifique se as credenciais de pool de aplicações do servidor IIS podem fazer uma ligação à base de dados de conformidade:

- GetRecoveryKeyForCurrentUser: ocorreu um erro ao registar um evento de auditoria na base de dados de Compliance.
- QueryRecoveryKeyIdsForUser: ocorreu um erro ao registar um evento de auditoria na base de dados de Compliance.
- QueryRecoveryKeyIdsForUser: ocorreu um erro ao registar um evento de auditoria na base de dados de conformidade.

### <a name="111-webappdberror"></a>111: WebAppDbError

Estes erros indicam uma das duas condições seguintes

- Os websites/webservices do MBAM não conseguiram ligar-se à base de dados de conformidade ou de recuperação
- Os websites MBAM/conta de execução de serviços web (conta de piscina de aplicações) não puderam executar o `GetVersion` procedimento armazenado na base de dados de conformidade ou recuperação

A mensagem contida no evento fornece mais detalhes sobre a exceção.

Verifique se a conta de piscina de aplicações pode ligar-se às bases de dados de conformidade ou recuperação. Confirme que tem permissões para executar o `GetVersion` procedimento armazenado.

### <a name="112-webapperror"></a>112: WebAppError

Ocorreu um erro ao verificar o registo do nome principal do serviço (SPN).

Para verificar o SPN, consulta o Ative Directory para recuperar uma lista de SPNs mapeadas conta de execução. Também questiona `ApplicationHost.config` o facto de obter as encadernações do site. Esta mensagem de erro indica que não podia comunicar com o `ApplicationHost.config` Diretório Ativo, ou não conseguia carregar o ficheiro.

Verifique se a conta de piscina de aplicativos `ApplicationHost.config` tem permissões para consultar o Ative Directory ou o ficheiro. Verifique também as entradas `ApplicationHost.config` de encadernação do site no ficheiro.

## <a name="operational"></a>Operacional

### <a name="4-performancecountererror"></a>4: Erro de contra-erro de desempenho

Ocorreu um erro ao recuperar um contador de desempenho.

A mensagem de rastreio contém a mensagem de exceção real, algumas das quais estão listadas aqui:

- ArgumentNullException: Esta exceção é lançada se a categoria, contador ou instância do contador de desempenho solicitado for inválida.
- System.InvalidOperationException: categoryName é uma corda vazia (""). contranome é uma corda vazia("").
- A definição de permissão de leitura/escrita solicitada é inválida para este contador.
- A categoria especificada não existe (se a leitura For verdadeira).
- A categoria especificada não é uma categoria de .NET Framework custom (se a leituraApenas for falsa).
- A categoria especificada é marcada como multiinstância e exige que o contador de desempenho seja criado com um nome de instância.
- caso o nome é superior a 127 caracteres.
- categoriaNome e contranome foram localizados em diferentes idiomas.
- System.ComponentModel.Win32Exception: Ocorreu um erro ao aceder a uma API do sistema.
- System.UnauthorizedAccessException: Código que está a executar sem privilégios administrativos tentou ler um contador de desempenho.

A mensagem no evento fornece mais detalhes sobre a exceção.

Para `System.UnauthorizedAccessException`a , verifique se a conta de piscina de aplicativos tem acesso a APIs de desempenho.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

A aplicação do site da administração encontrou e ligou com sucesso a uma versão suportada da base de dados de recuperação/conformidade.

Indica uma ligação bem sucedida à base de dados de recuperação ou conformidade do site do helpdesk.

### <a name="201-selfserviceportalinformation"></a>201: AutoServicePortalInformation

A aplicação do portal self-service encontrou e ligou com sucesso a uma versão suportada da base de dados de recuperação/conformidade.

Indica uma ligação bem sucedida à base de dados de recuperação ou conformidade do portal self-service.

### <a name="202-webappinformation"></a>202: WebAppInformation

A aplicação tem as suas SPNs registadas corretamente.

Indica que as SPNs necessárias para o site do helpdesk estão corretamente registadas contra a conta de execução.

## <a name="see-also"></a>Consulte também

Para obter mais informações sobre a utilização destes registos, consulte os registos do [evento BitLocker](about-event-logs.md).

Para obter mais informações sobre resolução de problemas, consulte [Troubleshoot BitLocker](troubleshoot.md).

Para obter mais informações sobre a instalação destes websites, consulte [Configurar relatórios e portais BitLocker](../../deploy-use/bitlocker/setup-websites.md).
