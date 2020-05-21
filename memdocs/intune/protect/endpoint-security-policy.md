---
title: Gerir as políticas de segurança do ponto final no Microsoft Intune / Microsoft Docs
description: Saiba como os Administradores de Segurança podem usar as políticas e perfis de Segurança endpoint para se concentrar na configuração de segurança dos dispositivos no Microsoft Endpoint Manager.
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
ms.openlocfilehash: 0e6a1f30d482e4811e02a8166e87aca4d1f23207
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431283"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Gerir a segurança do dispositivo com políticas de segurança de ponto final no Microsoft Intune

Como administrador de segurança, utilize as políticas de segurança da *segurança Endpoint* da Intune para configurar a segurança do dispositivo sem a sobrecarga de navegar no corpo maior e na gama de configurações encontradas nos perfis de configuração do dispositivo e nas linhas de base de segurança.

Cada tipo de política suporta um ou mais perfis. Os perfis são onde configura as definições e pode agrupar configurações para diferentes plataformas, ou para diferentes áreas de foco na área de política maior.

Encontrará estas políticas no *âmbito do Manage* no nó de segurança **Endpoint** do centro de administração do Microsoft [Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

![Gerir políticas](./media/endpoint-security-policy/endpoint-security-policies.png)

Seguem-se breves descrições de cada tipo de política de segurança de ponto final. Para saber mais sobre eles, incluindo os perfis disponíveis para cada um, siga os links para conteúdos dedicados a cada tipo de política:

- [Antivírus](../protect/endpoint-security-antivirus-policy.md) - As políticas antivírus ajudam os administradores de segurança a concentrarem-se na gestão do grupo discreto de definições antivírus para dispositivos geridos. Para utilizar a política Antivírus, integre o Intune com a Microsoft Defender Advanced Threat Protection (Defender ATP) como uma solução de Defesa de Ameaças Móveis.

- [Encriptação do disco](../protect/endpoint-security-disk-encryption-policy.md) - Os perfis de encriptação do disco de segurança endpoint focam-se apenas nas definições que são relevantes para um método de encriptação incorporado em dispositivos, como fileVault ou BitLocker. Este foco facilita a gestão de configurações de encriptação do disco sem ter de navegar por uma série de configurações não relacionadas.

- [Firewall](../protect/endpoint-security-firewall-policy.md) - Utilize a política de firewall de segurança de ponto final em Intune para configurar uma firewall incorporada para dispositivos que executam macOS e Windows 10. As firewalls incorporadas incluem o BitLocker para dispositivos Windows e FileVault para macOS.

- [Deteção e resposta](../protect/endpoint-security-edr-policy.md) de ponto final - Quando integrar o Defender ATP com o Intune, utilize as políticas de segurança de ponto final para deteção e resposta de pontofinal (EDR) para gerir as definições edr e dispositivos de bordo para o Defender ATP.

- [Redução da superfície do ataque](../protect/endpoint-security-asr-policy.md) - Quando o antivírus Defender estiver a ser utilizado nos seus dispositivos Windows 10, utilize políticas de segurança de ponto final intune para a redução da superfície de ataque para gerir essas definições para os seus dispositivos.

- [Proteção de Conta](../protect/endpoint-security-account-protection-policy.md) - As políticas de proteção de conta ajudam-no a proteger a identidade e as contas dos seus utilizadores. A política de proteção de conta está focada nas definições para Windows Hello e Credential Guard, que faz parte da identidade do Windows e gestão de acesso.

As seguintes secções aplicam-se a todas as políticas de segurança do ponto final.

## <a name="create-an-endpoint-security-policy"></a>Criar uma política de segurança de ponto final

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecione **a segurança endpoint** e, em seguida, selecione o tipo de política que pretende configurar e, em seguida, selecione **Create Policy**. Escolha entre os seguintes tipos de políticas:
   - Antivírus
   - Disk encryption (Encriptação de discos)
   - Firewall
   - Endpoint detection and response (Deteção e resposta de pontos finais)
   - Attack surface reduction (Redução da superfície de ataque)
   - Account protection (Proteção de contas)

3. Introduza as seguintes propriedades:
   - **Plataforma**: Escolha a plataforma para a qual está a criar a política. As opções disponíveis dependem do tipo de política selecionado:
     - macOS
     - Windows 10 e posterior
   - **Perfil**: Escolha entre os perfis disponíveis para a plataforma selecionada. Para obter informações sobre os perfis, consulte a secção dedicada neste artigo para o seu tipo de política escolhido.

4. Selecione **Criar**.

5. Na página **Basics,** introduza um nome e descrição para o perfil e, em seguida, escolha **Seguinte**.

6. Na página de configurações de **Configuração,** expanda cada grupo de definições e configure as definições que pretende gerir com este perfil.

   Quando terminar as definições de configuração, selecione **Next**.

7. Na página **scope tags,** escolha **Selecione etiquetas** de âmbito para abrir o painel *de etiquetas Select para* atribuir etiquetas de âmbito ao perfil.
  
   Selecione **Seguinte** para continuar.

8. Na página **de Atribuiçãos,** selecione os grupos que receberão este perfil. Para obter mais informações sobre a atribuição de perfis, consulte os perfis de [utilizador e dispositivo de atribuição](../configuration/device-profile-assign.md).

   Selecione **Seguinte**.

9. Na página **Review + criar** página, quando terminar, escolha **Criar**. O novo perfil é apresentado na lista quando seleciona o tipo de política para o perfil que criou.

## <a name="duplicate-a-policy"></a>Duplicar uma política

As políticas de segurança endpoint apoiam a duplicação para criar uma cópia da política original. Um cenário quando duplicar uma política é útil, é se precisar de atribuir políticas semelhantes a diferentes grupos, mas não quer recriar manualmente toda a política. Em vez disso, pode duplicar a política original e, em seguida, introduzir apenas as alterações que a nova política exige. Só pode alterar um cenário específico e o grupo a que a política é atribuída.

Ao criar um duplicado, dará à cópia um novo nome. A cópia é feita com as mesmas configurações de definição e etiquetas de âmbito que a original, mas não terá nenhuma atribuição. Terá de editar a nova política mais tarde para criar atribuições.  

Os seguintes tipos de políticas suportam a duplicação:

- Antivírus
- Disk encryption (Encriptação de discos)
- Firewall
- Endpoint detection and response (Deteção e resposta de pontos finais)
- Attack surface reduction (Redução da superfície de ataque)
- Account protection (Proteção de contas)

Depois de criar a nova política, reveja e edite a política para fazer alterações na sua configuração.

### <a name="to-duplicate-a-policy"></a>Para duplicar uma política

1. Inscreva-se no centro de administração do [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecione a política que pretende copiar. Em seguida, selecione **Duplicar** ou selecione a elipse **(...**) à direita da política e selecione **Duplicate**.
3. Forneça um **novo nome** para a apólice e, em seguida, selecione **Guardar**.

### <a name="to-edit-a-policy"></a>Para editar uma política

1. Selecione a nova política e, em seguida, selecione **Propriedades**.
2. Selecione Definições para expandir uma lista das definições de configuração na política. Não é possível modificar as definições desta vista, mas pode rever a forma como estão configuradas.
3. Para modificar a política, selecione **Editar** para cada categoria onde pretende fazer uma alteração:
   - Noções básicas
   - Atribuições
   - Scope tags (Etiquetas de âmbito)
   - Definições de configuração
4. Depois de ter feito alterações, selecione **Guardar** para guardar as suas edições.  As edimas para uma categoria devem ser salvas antes de poder introduzir editas em categorias adicionais.

## <a name="manage-conflicts"></a>Gerir conflitos

Muitas das definições do dispositivo que pode gerir com políticas de segurança endpoint (políticas de segurança) que pode gerir através de outros tipos de políticas no Intune. Estes outros tipos de políticas incluem a política de *configuração* do dispositivo e *as linhas de base de segurança.* Uma vez que pode gerir uma definição com vários tipos de políticas diferentes ou múltiplos casos do mesmo tipo de política, esteja preparado para identificar e resolver conflitos políticos caso um dispositivo não adere às configurações que espera.

- As linhas de base de segurança podem definir um valor não predefinido para uma definição que cumpra a configuração recomendada que os endereços de base.
- Outros tipos de políticas, incluindo as políticas de segurança do ponto final, estabelecem um valor de *Não configurado* por padrão. Estes outros tipos de políticas exigem que configure explicitamente as definições da política.

Independentemente do método político, gerir a mesma definição no mesmo dispositivo através de múltiplos tipos de políticas, ou através de múltiplos casos do mesmo tipo de política pode resultar em conflitos que devem ser evitados.

A informação nos seguintes links pode ajudá-lo a identificar e resolver conflitos:

- [Resolução de problemas de políticas e perfis no Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorize as suas linhas de base de segurança](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Próximos passos

[Gerir a segurança do ponto final em Intune](../protect/endpoint-security.md)
