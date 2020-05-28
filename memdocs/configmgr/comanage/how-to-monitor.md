---
title: Monitorizar a cogestão
titleSuffix: Configuration Manager
description: Utilize o painel de cogestão para rever informações sobre dispositivos cogeridos.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e4516ca9baa7398322c204908c25248921a69d25
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268067"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Como monitorizar a cogestão no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Depois de ativar a cogestão, monitorize os dispositivos de cogestão utilizando os seguintes métodos:

- [Dashboard de cogestão](#co-management-dashboard)  

- [Políticas de implantação](#deployment-policies)

- [Dados do dispositivo WMI](#wmi-device-data)

## <a name="co-management-dashboard"></a>Dashboard de cogestão

A partir da versão 1802, veja um dashboard com informações sobre cogestão. O painel ajuda-o a rever máquinas cogeridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que possam precisar de atenção.<!--1356648-->

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Monitorização** e selecione o nó **de Co-management.**

A partir da versão 1810, o painel de cogestão é melhorado com informações mais detalhadas. <!--1358980-->

![Screenshot do painel de cogestão](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>Dispositivos cogeridos

*Aplica-se às versões 1802 e 1806*

Mostra a percentagem de dispositivos cogeridos em todo o seu ambiente.

![Azulejo de dispositivos cogeridos](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>Distribuição do Cliente OS

*Aplica-se a todas as versões* 

Mostra o número de dispositivos clientes por OS por versão. Utiliza os seguintes agrupamentos:  

- Windows 7 & 8.x
- Windows 10 inferior a 1709  
- Windows 10 1709 e acima  

    > [!Tip]  
    > O Windows 10, versão 1709 e mais tarde, é um pré-requisito para a cogestão.  

Passe por cima de uma secção de gráficos para mostrar a percentagem de dispositivos nesse grupo de SO.

![Azulejo de distribuição do Cliente OS](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>Estatuto de cogestão (donut)

*Aplica-se às versões 1802 e 1806*

Mostra a avaria do sucesso ou falha do dispositivo nas seguintes categorias:

- Sucesso, AD Azure híbrido Juntou-se
- Sucesso, Azure AD Juntou-se  
- Falha: Falha na inscrição automática  

Passe por cima de uma secção de gráficos para mostrar a percentagem de dispositivos nessa categoria.

![Estado de cogestão (donut) azulejo](media/co-management-dashboard/Co-management-status-graph.PNG)

Selecione uma secção de gráfico para visualizar a lista do dispositivo para essa categoria.

![Lista de dispositivos de falha de inscrição](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>Estatuto de cogestão (funil)

*Aplica-se à versão 1810 e posterior*

Um gráfico de funil que mostra o número de dispositivos com os seguintes estados do processo de inscrição:
  
- Dispositivos elegíveis
- Agendado  
- Inscrições iniciadas  
- Enrolled (Inscrito)  

![Estado de cogestão (funil) azulejo](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Estatuto de inscrição em cogestão

*Aplica-se à versão 1810 e posterior*

Mostra a avaria do estado do dispositivo nas seguintes categorias:

- Sucesso, híbrido Azure-joined AD  
- Sucesso, Azure AD-joined  
- Inscrição, híbrido Azure-joined AD  
- Falha, ad-ad híbrido Azure  
- Falha, Azure AD-joined  
- Sessão de utilizador pendente  

    > [!Note]  
    > A partir da versão 1906, para reduzir o número de dispositivos neste estado pendente, um novo dispositivo cogerido está agora automaticamente inscrito no serviço Microsoft Intune com base no seu *token* de dispositivo Azure AD. Não é preciso esperar que um utilizador inicie o contrato para a inscrição automática. Para suportar este comportamento, o dispositivo precisa de estar a executar o Windows 10, versão 1803 ou mais tarde.
    >
    > Se o token do dispositivo falhar, recua para o comportamento anterior com o token do utilizador. Procure no **ComanagementHandler.log** para obter a seguinte entrada:`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Selecione um estado no azulejo para perfurar até uma lista de dispositivos nesse estado.  

![Telha de estado de cogestão](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transição de carga de trabalho

*Aplica-se a todas as versões*

Apresenta um gráfico de barras com o número de dispositivos que transferiu para o Microsoft Intune para as cargas de trabalho disponíveis.

A lista de cargas horárias varia consocada por versão do Gestor de Configuração. Para obter mais informações, consulte cargas de trabalho capazes de [ser transitadas para Intune](workloads.md).

Passe por cima de uma secção de gráficos para mostrar o número de dispositivos em transição para a carga de trabalho. 

![Gráfico de barra de transição de carga](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Erros de inscrição

*Aplica-se à versão 1810 e posterior*

Esta tabela é uma lista de erros de inscrição dos dispositivos. Estes erros podem vir do componente MDM no Windows, do núcleo do Windows OS ou do cliente do Gestor de Configuração.

Há centenas de possíveis erros. A tabela que se segue enumera os erros mais comuns.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Erro | Descrição |
|---------|---------|
| 2147549183 (0x8000FF) | A inscrição no MDM ainda não foi configurada no Azure AD, ou o URL de inscrição não é esperado.<br><br>[Ativar a inscrição automática de dispositivos Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licença do utilizador está em mau estado bloqueando a inscrição<br><br>[Atribuir licenças a utilizadores](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Ao tentar inscrever-se automaticamente no Intune, mas a configuração da AD Azure não está totalmente aplicada. Esta questão deve ser transitória, uma vez que o dispositivo se retenta após um curto período de tempo. |
| 2149056554 (0x 8018002A )<br>&nbsp; | O utilizador cancelou a operação<br><br>Se a inscrição no MDM necessitar de autenticação multifactor, e o utilizador não tiver assinado com um segundo fator suportado, o Windows apresenta uma notificação de torrada ao utilizador para se inscrever. Se o utilizador não responder à notificação da torrada, este erro ocorre. Este problema deve ser transitório, uma vez que o Gestor de Configuração irá voltar a tentar e solicitar ao utilizador. Os utilizadores devem utilizar a autenticação de vários fatores quando iniciarem o seu sessão no Windows. Também os instrua a esperar este comportamento, e se solicitado, tomar medidas. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Gestão de dispositivos móveis geralmente não suportada | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | O servidor não conseguiu autenticar o utilizador<br><br> Não há ficha da AD Azure para o utilizador. Certifique-se de que o utilizador pode autenticar a AD Azure. |
| 2147942450 (0x 80070032)<br>&nbsp; | A inscrição automática do MDM só é suportada no Windows RS3 e acima.<br><br>Certifique-se de que o dispositivo satisfaz os [requisitos mínimos](overview.md#windows-10) para a cogestão. |
| 3400073293 | Resposta de conta de realm do utilizador ADAL desconhecida<br><br>Verifique a configuração do Anúncio Azure e certifique-se de que os utilizadores podem autenticar com sucesso. | 
| 3399548929 | Precisa de inscrição no utilizador<br><br>Esta questão deve ser transitória. Ocorre quando o utilizador assina rapidamente antes da tarefa de inscrição acontecer. | 
| 3400073236 | O pedido de ficha de segurança da ADAL falhou.<br><br>Verifique a configuração do Anúncio Azure e certifique-se de que os utilizadores podem autenticar com sucesso. |
| 2149122477 | Emissão genérica http |
| 3400073247 | A autenticação integrada do Windows aDAL só é suportada no fluxo federado<br><br>[Planeie o seu Diretório Ativo Azure híbrido aderir à implementação](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | O servidor ou procuração não foi encontrado.<br><br>Esta questão deve ser transitória, quando o cliente não consegue comunicar com nuvem. Se persistir, certifique-se de que o cliente tem uma conectividade consistente com o Azure. | 
| 2149056532 | Plataforma ou versão específica não é suportada<br><br>Certifique-se de que o dispositivo satisfaz os [requisitos mínimos](overview.md#windows-10) para a cogestão. |
| 2147943568 | Elemento não encontrado<br><br>Esta questão deve ser transitória. Se persistir, contacte o Microsoft Support. |
| 2192179208 | Não há recursos de memória suficientes para processar este comando.<br><br>Esta questão deve ser transitória, deve resolver-se quando o cliente se retentar. |
| 3399614467 | A concessão de autorização da ADAL falhou por esta afirmação<br><br>Verifique a configuração do Anúncio Azure e certifique-se de que os utilizadores podem autenticar com sucesso. |
| 2149056517 | Falha genérica do servidor de gestão, como erro de acesso DB<br><br>Esta questão deve ser transitória. Se persistir, contacte o Microsoft Support. |
| 2149134055 | Nome Winhttp não resolvido<br><br>O cliente não pode resolver o nome do serviço. Verifique a configuração do DNS. | 
| 2149134050 | tempo de tempo na internet<br><br>Esta questão deve ser transitória, quando o cliente não consegue comunicar com nuvem. Se persistir, certifique-se de que o cliente tem uma conectividade consistente com o Azure. |

Para mais informações, consulte [os Valores de Erro de Registo do MDM.](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants)

## <a name="deployment-policies"></a>Políticas de implantação

São criadas duas políticas no nó de **implantação** do espaço de trabalho de **monitorização.** Uma política é para o grupo piloto e outra para a produção. Estas políticas reportam apenas o número de dispositivos onde o Gestor de Configuração aplicou a política. Não consideram quantos dispositivos estão matriculados em Intune, o que é um requisito antes de os dispositivos poderem ser cogeridos.  

A política de produção (CoMgmtSettingsProd) é direcionada para a coleção **All Systems.** Tem uma condição de aplicabilidade que verifica o tipo de SISTEMA e a versão. Se o cliente for um servidor OS ou não o Windows 10, a apólice não se aplica e não são tomadas medidas.

## <a name="wmi-device-data"></a>Dados do dispositivo WMI

Consulta da classe **SMS_Client_ComanagementState** WMI no **ROOT\SMS\site_ &lt; SITECODE>** espaço de nome no servidor do site. Pode criar coleções personalizadas no Gestor de Configuração, que ajudam a determinar o estado da sua implementação de cogestão. Para obter mais informações sobre a criação de coleções personalizadas, consulte [Como criar coleções.](../core/clients/manage/collections/create-collections.md)

Os seguintes campos estão disponíveis na classe WMI:  

- **MachineId**: Um ID único do dispositivo para o cliente do Gestor de Configuração  

- **MDMMatriculado**: Especifica se o dispositivo está inscrito no MDM  

- **Autoridade**: A autoridade para a qual o dispositivo está matriculado  

- **ComgmtPolicyPresent**: Especifica se a política de cogestão do Gestor de Configuração existe no cliente. Se o valor **DOMDMEnrolled** for **0,** o dispositivo não é cogerido independentemente de a política de cogestão existir no cliente.  

Um dispositivo é cogerido quando o campo **MDMEnrolled** e os campos **ComgmtPolicyPresent** têm um valor de **1**.  
