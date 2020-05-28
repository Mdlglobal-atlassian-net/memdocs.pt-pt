---
title: Implementar a gestão do BitLocker
titleSuffix: Configuration Manager
description: Implemente o agente de gestão BitLocker para clientes do Gestor de Configuração e o serviço de recuperação para pontos de gestão
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ebd847e44c1acd87c316514ec9919f8a6690a647
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428578"
---
# <a name="deploy-bitlocker-management"></a>Implementar a gestão do BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!--3601034-->

A gestão bitLocker no Gestor de Configuração inclui os seguintes componentes:

- **Agente de gestão BitLocker**: O Gestor de Configuração ativa este agente num dispositivo quando [cria uma apólice](#create-a-policy) e [implementa-a para uma recolha](#deploy-a-policy).

- **Serviço de recuperação**: O componente do servidor que recebe dados de recuperação BitLocker dos clientes. Para mais informações, consulte [o serviço de recuperação.](#recovery-service)

Antes de criar e implementar políticas de gestão bitLocker:

- Rever os [pré-requisitos](../../plan-design/bitlocker-management.md#prerequisites)

- Se necessário, [criptografe as chaves de recuperação](encrypt-recovery-data.md) na base de dados do site

## <a name="create-a-policy"></a>Criar uma política

Quando cria e implementa esta política, o cliente do Gestor de Configuração ativa o agente de gestão BitLocker no dispositivo.

> [!NOTE]
> Para criar uma política de gestão BitLocker, precisa do papel de **Administrador Completo** no Gestor de Configuração.

1. Na consola De Configuração Manager, vá ao espaço de trabalho **De Ativos e Compliance,** expanda a **Proteção endpoint,** e selecione o nó **bitLocker Management.**

1. Na fita, selecione **Create BitLocker Management Control Policy**.

1. Na página **Geral,** especifique um nome e descrição opcional. Selecione os componentes para ativar os clientes com esta política:  

    - **Unidade do sistema operativo**: Gerir se a unidade de SO está encriptada

    - **Unidade Fixa**: Gerir a encriptação para unidades de dados adicionais num dispositivo

    - **Unidade Amovível**: Gerir a encriptação para unidades que pode remover de um dispositivo, como uma chave USB

    - **Gestão do Cliente**: Gerir a cópia de segurança do serviço de recuperação chave das informações de recuperação de encriptação bitLocker Drive  

1. Na página **de Configuração,** configure as seguintes definições globais para encriptação bitLocker drive:

    > [!NOTE]
    > O Gestor de Configuração aplica estas definições quando ativa o BitLocker. Se a unidade já estiver encriptada ou estiver em curso, qualquer alteração nestas definições de política não altera a encriptação de unidade no dispositivo.
    >
    > Se desativar ou não configurar estas definições, o BitLocker utiliza o método de encriptação predefinido (AES 128-bit).

    - Para dispositivos Windows 8.1, ative a opção para o método de **encriptação Drive e a força da cifra**. Em seguida, selecione o método de encriptação.

    - Para dispositivos Windows 10, ative a opção para o método de **encriptação Drive e a força da cifra (Windows 10)**. Em seguida, selecione individualmente o método de encriptação para unidades de S, unidades de dados fixas e unidades de dados amovíveis.

    Para obter mais informações sobre estas e outras definições nesta página, consulte a [referência Definições - Configuração](../../tech-ref/bitlocker/settings.md#setup).

1. Na página **de Unidade do Sistema Operativo,** especifique as seguintes definições:  

    - **Definições**de encriptação de unidade do sistema operativo : Se ativar esta definição, o utilizador tem de proteger a unidade OS e o BitLocker encripta a unidade. Se o desativar, o utilizador não pode proteger a unidade.  

    Em dispositivos com um TPM compatível, dois tipos de métodos de autenticação podem ser utilizados no arranque para fornecer uma proteção adicional para dados encriptados. Quando o computador começa, só pode utilizar o TPM para autenticação, ou também pode exigir a inscrição de um número de identificação pessoal (PIN). Configure as seguintes definições:

    - **Selecione protetor para acionar**o sistema operativo: Configure-o para utilizar um TPM e PIN, ou apenas o TPM.

    - **Configurar**o comprimento mínimo pin para o arranque : Se necessitar de um PIN, este valor é o comprimento mais curto que o utilizador pode especificar. O utilizador introduz este PIN quando o computador arranca para desbloquear a unidade. Por defeito, o comprimento mínimo do PIN é `4` .

    Para obter mais informações sobre estas e outras definições nesta página, consulte a [referência Definições - Unidade OS](../../tech-ref/bitlocker/settings.md#os-drive).

1. Na página **Unidade Fixa,** especifique as seguintes definições:

    - **Encriptação**de unidade de dados fixos : Se ativar esta definição, o BitLocker exige que os utilizadores coloquem todas as unidades de dados fixas sob proteção. Em seguida, encripta as unidades de dados. Quando ativar esta política, ou ativa o desbloqueio automático ou as definições para a política de **palavra-passe de unidade de dados fixos**.

    - **Configure o desbloqueio automático para**uma unidade de dados fixa: Permita ou exija que o BitLocker desbloqueie automaticamente qualquer unidade de dados encriptada. Para utilizar o desbloqueio automático, também requer que o BitLocker encripte a unidade DES.

    Para obter mais informações sobre estas e outras definições nesta página, consulte a [referência Definições - Unidade fixa](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. Na página **Unidade Removível,** especifique as seguintes definições:

    - **Encriptação de unidade de dados amovível**: Quando ativa esta definição, e permite que os utilizadores apliquem a proteção BitLocker, o cliente do Gestor de Configuração guarda informações de recuperação sobre unidades amovíveis para o serviço de recuperação no ponto de gestão. Este comportamento permite que os utilizadores recuperem a unidade se esquecerem ou perderem o protetor (palavra-passe).

    - **Permitir que os utilizadores apliquem a proteção BitLocker em unidades de dados amovíveis:** Os utilizadores podem ligar a proteção BitLocker para uma unidade amovível.

    - **Política de palavra-passe de unidade de dados amovível**: Utilize estas definições para definir os constrangimentos das palavras-passe para desbloquear unidades amovíveis protegidas pelo BitLocker.

    Para obter mais informações sobre estas e outras definições nesta página, consulte a [referência Definições - Unidade Amovível](../../tech-ref/bitlocker/settings.md#removable-drive).

1. Na página **de Gestão** de Clientes, especifique as seguintes definições:

    > [!IMPORTANT]
    > Se não tiver um ponto de gestão com um website ativado por HTTPS, não configure esta definição. Para mais informações, consulte [o serviço de recuperação.](#recovery-service)

    - **Configure os Serviços de Gestão BitLocker**: Quando ativa esta definição, o Gestor de Configuração faz automaticamente e silenciosamente o backup informação de recuperação chave na base de dados do site. Se desativar ou não configurar esta definição, o Gestor de Configuração não guarda informações de recuperação da chave.

        - **Selecione informações de recuperação BitLocker para armazenar:** Configure-as para utilizar uma palavra-passe de recuperação e um pacote chave, ou apenas uma palavra-passe de recuperação.

        - Permitir que as informações de **recuperação sejam armazenadas em texto simples**: Sem um certificado de encriptação de gestão BitLocker, o Gestor de Configuração armazena as informações de recuperação chave em texto simples. Para mais informações, consulte [encriptar dados de recuperação](encrypt-recovery-data.md).

    Para obter mais informações sobre estas e outras definições nesta página, consulte a [referência Definições - Gestão do Cliente](../../tech-ref/bitlocker/settings.md#client-management).

1. Conclua o assistente.

Para alterar as definições de uma política existente, escolha-a na lista e selecione **Propriedades**.

Quando se cria mais do que uma política, pode configurar a sua prioridade relativa. Se implementar várias políticas para um cliente, utiliza o valor prioritário para determinar as suas definições.

## <a name="deploy-a-policy"></a>Implementar uma política

1. Escolha uma política existente no nó **bitLocker Management.** Na fita, selecione **Deploy**.

1. Selecione uma coleção de dispositivos como alvo da implementação.

1. Se pretender que o dispositivo possa encriptar ou desencriptar as suas unidades a qualquer momento, selecione a opção de permitir a **reparação fora da janela de manutenção**. Se a coleção tiver janelas de manutenção, ainda remedia esta política bitLocker.

1. Configure um horário **simples** ou **personalizado.** Por predefinição, o cliente avalia a sua conformidade com esta política a cada 12 horas.

1. Selecione **OK** para implementar a política.

Pode criar múltiplas implementações da mesma política. Para ver informações adicionais sobre cada implementação, selecione a política no nó **bitLocker Management** e, em seguida, no painel de detalhes, mude para o separador **Implementações.**

## <a name="monitor"></a>Monitorizar

Consulte as estatísticas básicas de conformidade sobre a implementação de políticas no painel de detalhes do nó **bitLocker Management:**

- Contagem de conformidade
- Contagem de falhas
- Contagem de incumprimento

Mude para o separador **De implantação** para ver a percentagem de conformidade e a ação recomendada. Selecione a colocação e, em seguida, na fita, selecione **'Ver Status**. Esta ação muda a vista para o espaço de trabalho **de monitorização,** o nó de **implantações.** À semelhança da implementação de outras implementações de políticas de configuração, pode ver o estado de conformidade mais detalhado nesta perspetiva.

Para entender por que razão os clientes estão a reportar não conformes com a política de gestão bitLocker, consulte [códigos de incumprimento](../../tech-ref/bitlocker/non-compliance-codes.md).

Para obter mais informações sobre resolução de problemas, consulte [Troubleshoot BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Utilize os seguintes registos para monitorizar e resolver problemas:

### <a name="client-logs"></a>Registos de clientes

- Registo de eventos MBAM: no Windows Event Viewer, navegue em Aplicações e Serviços > Microsoft > O Windows > MBAM.  Para mais informações, consulte os registos de [eventos bitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [registos de eventos do Cliente](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler.log** in client logs path, `%WINDIR%\CCM\Logs` por padrão

### <a name="management-point-logs-recovery-service"></a>Registos de pontos de gestão (serviço de recuperação)

- Registo de eventos de serviço de recuperação: no Windows Event Viewer, navegue para Aplicações e Serviços > Microsoft > Windows > MBAM-Web. Para mais informações, consulte os registos de [eventos bitLocker](../../tech-ref/bitlocker/about-event-logs.md) e [registos de eventos do Servidor](../../tech-ref/bitlocker/server-event-logs.md).

- Registos de rastreios do serviço de recuperação:`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Serviço de recuperação

O serviço de recuperação BitLocker é um componente de servidor que recebe dados de recuperação bitLocker dos clientes do Gestor de Configuração. O site implementa o serviço de recuperação quando cria uma política de gestão BitLocker. O Gestor de Configuração instala automaticamente o serviço de recuperação em cada ponto de gestão com um website ativado por HTTPS.

O Gestor de Configuração armazena as informações de recuperação na base de dados do site. Sem um certificado de encriptação de gestão BitLocker, o Gestor de Configuração armazena as informações de recuperação chave em texto simples.

Para mais informações, consulte [encriptar dados de recuperação](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Considerações sobre a migração

Se utilizar atualmente a Microsoft BitLocker Administration and Monitoring (MBAM), poderá migrar perfeitamente a gestão para o Gestor de Configuração. Quando implementa as políticas de gestão bitLocker no Gestor de Configuração, os clientes enviam automaticamente chaves de recuperação e pacotes para o serviço de recuperação do Gestor de Configuração.

> [!IMPORTANT]
> Quando migrar do MBAM autónomo para a gestão bitLocker do Gestor de Configuração, se necessitar de funcionalidades existentes de MBAM autónomo, não reutilize servidores MBAM ou componentes autónomos com gestão bitLocker do Gestor de Configuração. Se reutilizar estes servidores, o MBAM autónomo deixará de funcionar quando a gestão do Gestor de Configuração BitLocker instalar os seus componentes nesses servidores. Não execute o script MBAMWebSiteInstaller.ps1 para configurar os portais BitLocker em servidores MBAM autónomos. Quando configurar a gestão bitLocker do Gestor de Configuração, utilize servidores separados.

### <a name="group-policy"></a>Política de grupo

- As definições de gestão BitLocker são totalmente compatíveis com as definições de política do grupo MBAM. Se os dispositivos receberem as definições de política do grupo e as políticas do Gestor de Configuração, configure-os para corresponder.

- O Gestor de Configuração não implementa todas as definições de política do grupo MBAM. Se configurar configurações adicionais na política de grupo, o agente de gestão BitLocker nos clientes do Gestor de Configuração honra estas definições.

### <a name="tpm-password-hash"></a>TPM password hash

- Os clientes anteriores do MBAM não fazem o upload do hash de senha TPM para O Gestor de Configuração. O cliente só envia o hash de senha TPM uma vez.

- Se precisar de migrar esta informação para o serviço de recuperação do Gestor de Configuração, limpe o TPM no dispositivo. Depois de reiniciar, irá enviar o novo hash de senha TPM para o serviço de recuperação.

### <a name="re-encryption"></a>Reencriptação

O Gestor de Configuração não encripta as unidades que já estão protegidas com encriptação de unidade bitLocker. Se implementar uma política de gestão BitLocker que não corresponda à proteção atual da unidade, reporta como incompatível. A unidade ainda está protegida.

Por exemplo, utilizou o MBAM para encriptar a unidade sem proteção PIN, mas a política do Gestor de Configuração requer um PIN. A unidade não está em conformidade com a política, mesmo que a unidade esteja encriptada.

Para contornar este comportamento, desative primeiro o BitLocker no dispositivo. Em seguida, implemente uma nova política com as novas definições.

## <a name="co-management-and-intune"></a>Cogestão e Intune

<!-- SCCMDocs#2321 -->

O manipulador de clientes do Gestor de Configuração para o BitLocker é consciente de cogestão. Se o dispositivo for cogerido e mudar a carga de trabalho de [Proteção de Ponto](../../../comanage/workloads.md#endpoint-protection) final para Intune, então o cliente do Gestor de Configuração ignora a sua política BitLocker. O dispositivo obtém a política de encriptação do Windows a partir de Intune.

Quando mudar as autoridades de gestão de encriptação, planeie [a reencriptação.](#re-encryption)

Para mais informações sobre a gestão do BitLocker com o Intune, consulte os seguintes artigos:

- [Utilize encriptação do dispositivo com Intune](../../../../intune/protect/encrypt-devices.md)
- [Problemas bitLocker políticas no Microsoft Intune](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Próximos passos

[Configurar relatórios e portais BitLocker](setup-websites.md)
