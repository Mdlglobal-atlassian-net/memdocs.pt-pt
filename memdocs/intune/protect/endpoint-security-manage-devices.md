---
title: Gerir dispositivos com segurança de ponto final no Microsoft Intune / Microsoft Docs
description: Saiba como os Administradores de Segurança podem usar o nó de Segurança Endpoint para visualizar dispositivos e agir para geri-los no Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8171eb3cf484c61e2b99046b36553a633d92044e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431247"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Gerir dispositivos com segurança de ponto final no Microsoft Intune

Como administrador de segurança, utilize a visão *de Todos os dispositivos* no centro de administração do Microsoft Endpoint Manager para rever e agir para gerir os seus dispositivos. A vista apresenta uma lista de todos os seus dispositivos do seu Diretório Ativo Azure (Azure AD). Isto inclui dispositivos que são geridos por Intune, Gestor de Configuração, e através [da cogestão](https://docs.microsoft.com/configmgr/comanage/overview) tanto pelo Intune como pelo Gestor de Configuração. Os dispositivos podem estar na nuvem e a partir da sua infraestrutura no local quando integrados com o seu Azure AD.

 Para encontrar a vista, abra o centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) e selecione segurança **Endpoint**  >  **Todos os dispositivos**.

A visualização inicial *de Todos os dispositivos* exibe os seus dispositivos e inclui informações-chave sobre cada um:

- Como o dispositivo é gerido
- Estado de conformidade
- Detalhes do sistema operativo
- Quando o dispositivo registou pela última vez
- E mais

![Toda a vista do dispositivo no centro de administração](./media/endpoint-security-manage-devices/all-device-view.png)

Ao visualizar os detalhes do dispositivo, pode selecionar um dispositivo para perfurar para obter mais informações.

## <a name="available-details-by-management-type"></a>Detalhes disponíveis por tipo de gestão

Ao visualizar dispositivos no centro de administração do Microsoft Endpoint Manager, considere como o dispositivo é gerido. A fonte de gestão afeta a informação que é apresentada no centro de administração e quais as ações disponíveis para gerir o dispositivo.

Considere os seguintes campos:

- **Gerida por** – Esta coluna identifica como o dispositivo é gerido. As opções geridas incluem:

  - **MDM** - Estes dispositivos são geridos pela Intune. Os dados de conformidade são recolhidos e reportados pela Intune ao centro de administração.

  - **ConfigMgr** – Estes dispositivos aparecem no centro de administração do Microsoft Endpoint Manager quando utiliza o *anexo do arrendatário* para adicionar os dispositivos que gere com o Gestor de Configuração. Para ser gerido, o dispositivo deve executar o cliente do Gestor de Configuração e ser:

    - Num Grupo de Trabalho (AAD juntou-se e não só)
    - Domínio Unido
    - AAD híbrido juntou-se (juntou-se à AD e AAD)

    O estado de conformidade dos dispositivos geridos pelo Gestor de Configuração não é visível no centro de administração do Microsoft Endpoint Manager.

    Para mais informações, consulte [O Inquilino Habilitar anexar](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions) na documentação do Gestor de Configuração.

  - **Agente MDM/ConfigMgr** – Estes dispositivos estão sob cogestão entre Intune e O Gestor de Configuração.

    Com a cogestão, [você escolhe diferentes cargas de trabalho de cogestão](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) para determinar quais os aspetos geridos pelo Gestor de Configuração ou pelo Intune. Estas escolhas afetarão quais as políticas que o dispositivo aplica e como os dados de conformidade são comunicados ao centro de administração.

    Por exemplo, pode usar o Intune para configurar a política para Antivírus, Firewall e Encriptação. Estes tipos de políticas são considerados políticas para a proteção do *ponto final.* Para ter um dispositivo cogerido utilize as políticas Intune e não as políticas do Gestor de Configuração, defina o slider de cogestão para a Proteção de Endpoint para *Intune* ou *Pilot Intune*. Se o slider estiver definido para O Gestor de Configuração, o dispositivo utiliza as políticas e definições do 'Gestor de Configuração'.

- **Conformidade**: A conformidade é avaliada contra as políticas de conformidade que são atribuídas ao dispositivo. A origem destas políticas e que informação está na consola depende da forma como o dispositivo é gerido; Intune, Gestor de Configuração ou cogestão. Para que os dispositivos cogeridos reportem a conformidade, defina o slider de cogestão para a conformidade do dispositivo para Intune ou Pilot Intune.  

  Após a conformidade ser reportada ao centro de administração para um dispositivo, pode perfurar os detalhes para ver detalhes adicionais. Quando um dispositivo não estiver em conformidade, insto os seus detalhes para obter informações sobre quais as políticas que não estão em conformidade. Essa informação pode ajudá-lo a investigar e ajudá-lo a colocar o dispositivo em conformidade.

- **Última verificação**: Este campo identifica a última vez que o dispositivo reportou o seu estado.

## <a name="review-a-devices-policy"></a>Rever uma política de dispositivos

Ao visualizar a lista de dispositivos, pode selecionar um dispositivo para perfurar para obter mais informações sobre o mesmo, abrindo a página *de visão geral* do dispositivo.

A partir da página de visão geral de um dispositivo, pode selecionar a configuração de **segurança endpoint** para visualizar as políticas de segurança do ponto final que se aplicam a esse dispositivo. Os detalhes da política estão disponíveis para dispositivos geridos por MDM e Intune.

![Ver detalhes da política de segurança do ponto final](./media/endpoint-security-manage-devices/view-policy-details.png)

Os dispositivos geridos pelo Gestor de Configuração não apresentam detalhes da política. Para visualizar informações adicionais para estes dispositivos, utilize a consola 'Gestor de Configuração'.

## <a name="remote-actions-for-devices"></a>Ações remotas para dispositivos

As ações remotas são ações que pode iniciar ou aplicar a um dispositivo a partir do centro de administração do Microsoft Endpoint Manager. Quando visualiza detalhes para um dispositivo, pode aceder a ações remotas que se aplicam ao dispositivo.

As ações remotas exibem-se na parte superior da página *de visão geral* dos dispositivos. As ações que não podem ser exibidas devido ao espaço limitado no ecrã estão disponíveis selecionando a elipse do lado direito:

![Ver ações adicionais](./media/endpoint-security-manage-devices/view-additional-actions.png)

As ações remotas disponíveis dependem da forma como o dispositivo é gerido:

- **Intune**: Todas as [ações remotas intune](../remote-actions/device-management.md) que se aplicam à plataforma do dispositivo estão disponíveis.  
- **Gestor de Configuração**: Pode utilizar as seguintes ações do Gestor de Configuração:

  - Política de Máquina sincronizada
  - Política de Utilizador sincronizado
  - Ciclo de Avaliação de Aplicações

- **Cogestão:** Pode aceder tanto às ações remotas intune como às ações do Gestor de Configuração.

Algumas das ações remotas intune podem ajudar a proteger dispositivos ou salvaguardar dados que possam estar no dispositivo. Com ações remotas pode:

- Bloqueie um dispositivo
- Redefinir um dispositivo
- Remover dados da empresa
- Scan para malware fora de uma execução programada
- Teclas BitLocker rotativas

As seguintes ações remotas intune são do interesse do administrador de segurança, e são um subconjunto da [lista completa](../remote-actions/device-inventory.md#view-the-device-details). Nem todas as ações estão disponíveis para todas as plataformas de dispositivos. Os links vão para conteúdos que fornecem detalhes aprofundados para cada ação.

- [Dispositivo de sincronização](../remote-actions/device-sync.md) – Faça o check-in imediatamente com o Intune. Quando um dispositivo faz o check-in, recebe quaisquer ações ou políticas pendentes que lhe tenham sido atribuídas.  

- [Reiniciar](../remote-actions/device-restart.md) – Force um dispositivo Windows 10 para reiniciar, dentro de cinco minutos. O proprietário do dispositivo não será automaticamente notificado do reinício e poderá perder o trabalho.

- [Quick Scan](../configuration/device-restrictions-windows-10.md) – Have Defender executar uma varredura rápida do dispositivo para malware e, em seguida, submeter os resultados para Intune. Uma análise rápida analisa locais comuns onde pode haver malware registado, como chaves de registo e pastas de arranque conhecidas do Windows.

- [Digitalização completa](../configuration/device-restrictions-windows-10.md) – O Defender executa uma varredura do dispositivo para malware e, em seguida, submeta os resultados para Intune. Uma varredura completa analisa locais comuns onde pode haver malware registado, e também digitaliza todos os ficheiros e pastas do dispositivo.

- Atualizar a inteligência de segurança do Windows Defender – O dispositivo atualize as definições de malware para o Antivírus Do Microsoft Defender. Esta ação não começa uma tomografia.

- [Rotação da tecla BitLocker](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – Rode remotamente a chave de recuperação BitLocker de um dispositivo que executa a versão 1909 do Windows 10 ou mais tarde.

Também pode utilizar ações de **dispositivos** a granel para gerir algumas ações como *Retire* e *Wipe* para vários dispositivos ao mesmo tempo. [As ações a granel](../remote-actions/bulk-device-actions.md) estão disponíveis na vista *de Todos os dispositivos.* Selecionará a plataforma, ação e, em seguida, especificará até 100 dispositivos.

![Selecione ações a granel](./media/endpoint-security-manage-devices/select-bulk-actions.png)

As opções que gere para os dispositivos não têm efeito até que o dispositivo faça o check-in com o Intune.

## <a name="next-steps"></a>Próximos passos

[Gerir a segurança do ponto final em Intune](../protect/endpoint-security.md)