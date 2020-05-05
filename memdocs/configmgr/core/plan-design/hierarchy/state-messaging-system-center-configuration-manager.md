---
title: Mensagens de estado
titleSuffix: Configuration Manager
description: Descrições de mensagens de Estado nas versões suportadas do Gestor de Configuração.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720934"
---
# <a name="state-messages-in-configuration-manager"></a>Mensagens de Estado no Gestor de Configuração 

*Aplica-se a: Gestor de Configuração (ramo atual)*

As mensagens estatais contêm informações concisas sobre as condições do cliente do Gestor de Configuração. O sistema de mensagens estatais é utilizado por componentes específicos do Gestor de Configuração, tais como atualizações de software e configurações de configuração.

Os clientes do Gestor de Configuração enviam mensagens do Estado para o ponto de recuo ou sistemas de site de ponto de gestão para reportar o estado atual das operações. Pode criar relatórios para visualizar mensagens de Estado enviadas pelos clientes do Gestor de Configuração.

Cada funcionalidade do Gestor de Configuração que utiliza mensagens de estado é identificada pelo tipo tópico da mensagem de estado. Os tipos de tópicos de mensagem de estado listados neste artigo podem ser usados para definir a funcionalidade 'Gestor de Configuração' a que uma mensagem de Estado se relaciona.

> [!NOTE]  
> Um valor de id de mensagem de estado de zero (0) tipicamente indica que o tipo de tópico está em um estado desconhecido.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 | Estado de conformidade desconhecido|
| 1 | Compatível | 
| 2 | Incompatível | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0  | Estado de execução desconhecido |
| 1  | Instalação de atualizações        | 
| 2  | À espera do recomeço          | 
| 3  | Esperando que outra instalação esteja concluída         | 
| 4  | Atualização instalada com sucesso(2)          | 
| 5  | Reinício de sistema pendente         | 
| 6  | Não instalou a(s) atualização(s)         | 
| 7  | Descarregamento das atualizações   | 
| 8  | Atualização descarregada(s)    | 
| 9  | Falha no download de atualizações     | 
| 10 | Esperar pela janela de manutenção antes de instalar         | 
| 11 | À espera de orquestração         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|      
| 0 | Estado de avaliação desconhecido|                 
| 1 |Avaliação ativada      |
| 2 |Avaliação conseguida      |
| 3 |Avaliação falhada      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 | Estado de deteção desconhecido|
| 1 | Não é necessária   |
| 2 | Não detetado    |
| 3 | Detetada   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 | Estado de conformidade desconhecido|
| 1 |Compatível     |
| 2 |Incompatível     |
| 3 |Conflito detetado    |
| 4 |Erro      |
| 5 |Desconhecido     |
| 6 |Conformidade parcial   |
| 7 |Conformidade não configurada    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0  | Estado de execução desconhecido|
| 1  |A aplicação começou          |
| 2  |Execução à espera de conteúdo         |
| 3  | Esperando que outra instalação esteja concluída        |
| 4  |Esperar pela janela de manutenção antes de instalar         |
| 5  |Reiniciar necessário antes de instalar         |
| 6  |Falha geral        |
| 7  |Instalação pendente         |
| 8  |Instalação de atualização          |
| 9  |Reinício de sistema pendente        |
| 10 |Atualização instalada com sucesso         |
| 11 |Falhou na instalação da atualização        |
| 12 |Atualização de download        |
| 13 | Atualização descarregada        |
| 14 |Falhou em descarregar a atualização        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
|0 |Estado de deteção desconhecido|
| 1 | Atualização não é necessária  |
| 2 | É necessária a atualização   |
| 3 | Atualização está instalada  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 |Estado de digitalização desconhecido|
| 1 | A varredura está à espera de conteúdo   |
| 2 | A tomografia está a correr.    |
| 3 | Digitalização completa    |
| 4 | A tomografia está pendente de novo.   |
| 5 | A varredura falhou   |
| 6 | Digitalização concluída com erros |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Sem identificação do Estado.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Sem identificação do Estado.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Sem identificação do Estado.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 100 |Implantação de clientes iniciada      |       
| 101 |Esperando o download       |       
| 102 |Programado de Implantação       |       
| 103 | Esperando a janela antes de ser implantado |
| 104 |Implantação ignorada       |       
| 301 |Falha de implantação de clientes desconhecida |       
| 302 |Falhou na criação do serviço ccmsetup  |       
| 303 |Falha na eliminação do serviço ccmsetup |       
| 304 |Não é possível instalar sobre o sistema operativo incorporado com filtro de escrita baseado em ficheiros (FBWF) ativado na unidade do sistema |       
| 305 |O modo de segurança nativa não é válido no Windows 2000  |       
| 306 |Falha no início do processo de descarregamento do ccmsetup  |       
| 307 |Linha de comando ccmsetup não válida |       
| 308 |Falhou em descarregar o ficheiro sobre winhttp no endereço |       
| 309 |Falhou em descarregar os ficheiros através do BITS no endereço |       
| 310 |Falha na instalação da versão BITS |       
| 311 |Não posso verificar que o ficheiro pré-requisito é MS assinado  |       
| 312 |Falhou em copiar o ficheiro porque o disco está cheio |       
| 313 |Instalação Client.msi falhou com erro da MSI |       
| 314 |Falha na carga do ficheiro manifesto ccmsetup.xml |       
| 315 |Não obteve um certificado de cliente  |       
| 316 |Arquivo pré-requisito não é MS assinado |       
| 317 |Reiniciar necessário para continuar a instalação  |       
| 318 |Não é possível instalar o cliente no MP porque as versões MP e cliente não correspondem |       
| 319 |Sistema operativo ou pacote de serviço não suportado  |       
| 320 |Implantação não suportada       |       
| 321 |Pedaços faltando        |       
| 322 |A pasta fonte não está disponível       |       
| 323 |Appv não suportado              |       
| 324 |Versão incorreta do site              |       
| 325 |Incompatibilidade preventiva do hash       |       
| 326 |Desregisto do MDM Falhado      |       
| 327 |Registo do MDM detetado      |       
| 328 |Intune Detetado       |       
| 329 |Rede Medido sem permitido      |       
| 400 |A implementação do cliente foi bem sucedida |  
| 401 |Implementação conseguida reiniciar necessária     |       
| 402 |Implantação conseguiu reiniciar     |
| 500 |Atribuição de clientes iniciada|
| 601 |Falha de atribuição de clientes desconhecida|
| 602 |O código do site que se segue é inválido|
| 603 |Não atribuiu a MP|
| 604 |Falhou em descobrir o ponto de gestão padrão|
| 605 |Falha no descarregamento do certificado de assinatura do site|
| 606 |Falhou em descobrir automaticamente o código do site|
| 607 |A atribuição do local falhou; versão cliente superior à versão do site|
| 608 |Falhou em obter versão do Site dos Serviços de Domínio de Diretório Ativo e SLP|
| 609 |Falhou na versão do cliente|
| 700 |Atribuição de clientes conseguiu|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Sem identificação do Estado.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 100 | Estado da inscrição   |
| 101 | Inscrições agendadas   |
| 102 | Inscrições canceladas   |
| 105 | Inscrições iniciadas   |
| 106 | Inscrição conseguiu, mas não é prevista
| 107 | Inscrição conseguiu e é provisionada
| 108 | Inscrição sem utilizador ativo   |
| 110 | Inscrição falhou   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | Atualização do Windows para o estado do cliente do Negócios| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | Espaço do disco   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Sem identificação do Estado.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Sem identificação do Estado.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Sem identificação do Estado.

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | O cliente está a comunicar com sucesso com o ponto de gestão |
| 2 | O cliente não comunicou com o ponto de gestão |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |O cliente recuperou com sucesso o certificado da loja de certificados local    |
| 2 |Cliente não conseguiu recuperar o certificado da loja de certificados local |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Sem identificação do Estado.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Sem identificação do Estado.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Sem identificação do Estado.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Sem identificação do Estado.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Sem identificação do Estado.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Sem identificação do Estado.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Sem identificação do Estado.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Sem identificação do Estado.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Sem identificação do Estado.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Sem identificação do Estado.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Sem identificação do Estado.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Sem identificação do Estado.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Sem identificação do Estado.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Sem identificação do Estado.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Cliente não está pronto para o modo nativo  |
| 2 |Cliente pronto para o modo nativo     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | Êxito|
| 2 | Não foi bem sucedido. |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Sem identificação do Estado.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Sem identificação do Estado.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Sem identificação do Estado.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Sem identificação do Estado. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Conjunto de afinidade do utilizador       |
| 2 |Afinidade do utilizador removida       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Sem identificação do Estado.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Sem identificação do Estado.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1000  |Item de configuração conseguiu           |
| 1001 |Item de configuração bem sucedido já instalado         |
| 1002 |O item de configuração sucedeu ao pré-voo          |
| 1003 |Configuração Item estado rápido conseguiu          |
| 2000 |Item de configuração em andamento           |
| 2001 |Item de configuração em andamento à espera de conteúdo         |
| 2002 |Item de configuração em curso instalação          |
| 2003 |Item de configuração em curso espera reboot         |
| 2004 |Item de configuração em andamento à espera da janela de manutenção        |
| 2005 |Item de configuração em curso horário de espera         |
| 2006 |Item de configuração em andamento descarregando conteúdo dependente     |
| 2007 |Item de configuração em curso instalando dependências        |
| 2008 |Item de configuração em andamento enquanto se aguarda o reboot         |
| 2009 |Item de configuração em conteúdo em andamento descarregado         |
| 2010 |Item de configuração em andamento pendente de atualização         |
| 2011 |Item de configuração em andamento esperando reconectar o utilizador        |
| 2012 |Item de configuração em andamento à espera do utilizador assinar         |
| 2013 |Item de configuração em andamento à espera do sinal do utilizador         |
| 2014 |Item de configuração em andamento à espera de instalação         |
| 2015 |Item de configuração em andamento à espera de retry         |
| 2016 |Item de configuração em andamento à espera do presmode         |
| 2017 |Item de configuração em andamento à espera de orquestração        |
| 2018 |Item de configuração em andamento à espera da rede         |
| 2019 |Item de configuração em andamento até atualização VE         |
| 2020 |Item de configuração em curso atualizando VE         |
| 3.000 |Requisitos de artigo de configuração não cumpridos           |
| 3001 |Requisitos de Artigo de Configuração não cumpridos não aplicáveis        |
| 4000 |Artigo de configuração desconhecido           |
| 5000 |Erro de item de configuração            |
| 5001 |Avaliação de erro do item de configuração          |
| 5002 |Instalação de erro de configuração          |
| 5003 |Conteúdo de recuperação de erros de configuração         |
| 5004 |Configuração Erro de instalação de dependência         |
| 5005 |Configuração Erro de erro recuperando dependência de conteúdo        |
| 5006 |Regras de erro do item de configuração conflito          |
| 5007 |Erro do item de configuração à espera de retry          |
| 5008 |Erro de configuração desinstalando a supersedência        |
| 5009 |Erro de configuração do item descarregando substituído         |
| 5010 |Atualização de erro do item de configuração VE          |
| 5011 |Licença de instalação de erro de configuração         |
| 5012 |A recuperação de erros do item de configuração permite todas as aplicações fidedignas       |
| 5013 |Erro de item de configuração sem licenças disponíveis         |
| 5014 |Erro de configuração Do ERRO não suportado          |
| 6000 |Lançamento do Item de Configuração foi bem sucedido            |
| 6010 |Erro de lançamento do item de configuração            |
| 6020 |Lançamento de item de configuração desconhecido|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Sem identificação do Estado.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Sem identificação do Estado.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Sem identificação do Estado.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Sem identificação do Estado.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Sem identificação do Estado.

## <a name="1901-state_topictype_ep_am_health"></a>State_Topictype_Ep_Am_Health de 1901

Sem identificação do Estado.

## <a name="1902-state_topictype_ep_malware"></a>STATE_TOPICTYPE_EP_MALWARE de 1902

Sem identificação do Estado.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Sem identificação do Estado.

## <a name="2001-state_topictype_ep_client_deployment"></a>STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT de 2001

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Proteção do ponto final não gerida   |
| 2 |Proteção do ponto final à espera de instalação  |
| 3 |Proteção do ponto final gerida   |
| 4 |Instalação de proteção de pontofinal falhou  |
| 5 |Reinicialização da proteção do ponto final pendente  |
| 6 |Proteção do ponto final não suportada   |
| 7 |Proteção do Ponto Final cogerida   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION de 2002

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 |Estatuto de aplicação da política de proteção de pontos finais desconhecido    |
| 1 |Aplicação de política de proteção do ponto final foi bem sucedida    |
| 2 |Falha na aplicação da política de proteção do ponto final    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 0 |  Desconhecido    |
| 1 |  Ativa    |
| 2 |  Inativa    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | Wakeup Proxy não está instalado    |
| 2 | Wakeup Proxy está à espera da instalação   |
| 3 | Wakeup Proxy está instalado    |
| 4 | Instalação Wakeup Proxy falhou   |
| 5 | Wakeup Proxy está à espera de reiniciar   |
| 6 | Wakeup Proxy não é suportado neste SO  |
| 7 | Wakeup Proxy servidor opt-out   |
| 8 | Wakeup Proxy desinstalar falhou   |
| 9 | Wakeup Proxy tempo de execução não suportado   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Sem identificação do Estado.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Sem identificação do Estado.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Sem identificação do Estado.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
|0 | Conjunto de canal de notificação de impulso do Windows|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Sem identificação do Estado.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Sem identificação do Estado.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Sem identificação do Estado.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Sem identificação do Estado.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Sem identificação do Estado.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Sem identificação do Estado.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Sem identificação do Estado.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Sem identificação do Estado.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Sem identificação do Estado.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Sem identificação do Estado.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Sem identificação do Estado.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Sem identificação do Estado.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Desafio emitido         |
| 2 |Problema de desafio falhou        |
| 3 |Pedido de criação falhou        |
| 4 |Pedido de reclamação falhou        |
| 5 |Validação do desafio conseguiu       |
| 6 |Validação do desafio falhou       |
| 7 |Problema falhou         |
| 8 |Emissão pendente         |
| 9 |Emitido          |
| 10 |O processamento de resposta falhou       |
| 11 |Resposta pendente         |
| 12 |Inscrição conseguida         |
| 13 |Inscrição não é necessária         |
| 14 |Revoked          |
| 15 |Removido da coleção        |
| 16 |Renovar verificado         |
| 17 |Falha de instalação        |
| 18 |Instalado         |
| 19 |Eliminar falhado         |
| 20 |Eliminado         |
| 21 |Renovação solicitada        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Desafio emitido         |
| 2 |Problema de desafio falhou        |
| 3 |Pedido de criação falhou        |
| 4 |Pedido de reclamação falhou        |
| 5 |Validação do desafio conseguiu       |
| 6 |Validação do desafio falhou       |
| 7 |Problema falhou         |
| 8 |Emissão pendente         |
| 9 |Emitido          |
| 10 |O processamento de resposta falhou       |
| 11 |Resposta pendente         |
| 12 |Inscrição conseguida         |
| 13 |Inscrição não é necessária         |
| 14 |Revoked          |
| 15 |Removido da coleção        |
| 16 |Renovar verificado         |
| 17 |Falha de instalação        |
| 18 |Instalado         |
| 19 |Eliminar falhado         |
| 20 |Eliminado         |
| 21 |Renovação solicitada        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 | Configuração do pino de estado conseguiu       |
| 2 | Configuração do pino de estado falhou       |
| 3 | Configuração do pino de estado não suportada      |
| 4 | Configuração do pino de estado em curso      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Sem identificação do Estado.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Sem identificação do Estado.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Sem identificação do Estado.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Sem identificação do Estado.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Sem identificação do Estado.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Sem identificação do Estado.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Desafio emitido    |
| 2 |Problema de desafio falhou   |
| 3 |Pedido de criação falhou   |
| 4 |Pedido de reclamação falhou   |
| 5 |Validação do desafio conseguiu  |
| 6 |Validação do desafio falhou  |
| 7 |Problema falhou    |
| 8 |Emissão pendente    |
| 9 |Emitido     |
| 10 |O processamento de resposta falhou  |
| 11 |Resposta pendente    |
| 12 |Inscrição conseguida    |
| 13 |Inscrição não é necessária    |
| 14 |Revoked     |
| 15 |Removido da coleção   |
| 16 |Renovar verificado    |
| 17 |Falha de instalação   |
| 18 |Instalado    |
| 19 |Eliminar falhado    |
| 20 |Eliminado    |
| 21 |Renovação solicitada   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
|| 1 | Sucesso de conformidade    |
| 2 | Falha de conformidade no MP   |
| 3 | Falha de conformidade no cliente   |
| 4 | Falha de conformidade em Intune   |
| 5 | Falha de conformidade na AAD   |
| 6 | Conformidade comgmt Intune   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Peer Cache Source adicionado       |
| 2 |Fonte de cache de pares removida      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Fonte de cache peer desativada       |
| 2 |Peer Cache Source está ativo       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Descarregue o upload de dados agregados       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Upload de dados de rejeição de fonte de pares     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Sem identificação do Estado.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Sem identificação do Estado.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Sem identificação do Estado.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Sem identificação do Estado.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID de mensagem de estado     |  Descrição da mensagem do Estado |
|:-------------|:------|
| 1 |Atestado de saúde é apoiado      |
| 2 |Atestado de saúde não é suportado      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Sem identificação do Estado.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Sem identificação do Estado.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Sem identificação do Estado.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Sem identificação do Estado.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Sem identificação do Estado.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Sem identificação do Estado.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Sem identificação do Estado.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Sem identificação do Estado.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Sem identificação do Estado.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Sem identificação do Estado.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Sem identificação do Estado.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Sem identificação do Estado.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Sem identificação do Estado.

## <a name="next-steps"></a>Passos seguintes

- [Descrição das mensagens estatais no Gestor de Configuração](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Software atualiza livro branco de gestão para Gestor de Configuração](https://www.microsoft.com/download/details.aspx?id=44578)
