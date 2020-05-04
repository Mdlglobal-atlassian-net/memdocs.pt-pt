---
title: Atualizar dispositivos Windows para uma versão diferente
titleSuffix: Configuration Manager
description: Utilize o Gestor de Configuração para atualizar automaticamente os dispositivos do Windows 10 para uma edição diferente do Windows.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77ef255a820104ef2042a370b5056677fddb9d12
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712233"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Atualize os dispositivos Windows para uma nova edição com o Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

A Política de Upgrade da **Edição** permite-lhe atualizar automaticamente os dispositivos do Windows 10 para uma edição diferente.

Os seguintes caminhos de atualização são suportados:

- Desde o Windows 10 Pro ao Windows 10 Enterprise
- Desde o Windows 10 Home ao Windows 10 Education
- Desde o Windows 10 Mobile ao Windows 10 Mobile Enterprise

Os dispositivos devem executar o software cliente do Gestor de Configuração. Os dispositivos [geridos](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) pelo MDM no local não são suportados.

## <a name="before-you-start"></a>Antes de começar

Antes de começar a atualizar os dispositivos para a versão mais recente, reveja os seguintes pré-requisitos:  

- Para edições de desktop do Windows 10: Uma chave de produto válida para a nova versão do Windows em todos os dispositivos que você alvo com a apólice. Esta chave do produto pode ser uma chave de ativação múltipla (MAK), ou uma chave genérica de licenciamento de volume (GVLK). Um GVLK também é referido como uma chave de configuração de cliente de serviço de gestão (KMS). Para mais informações, consulte [Plano de ativação](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)de volume . Para obter uma lista das teclas de configuração do cliente KMS, consulte o [apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. <!--496871-->  

- Para o Windows 10 Mobile: Um ficheiro de licença XML do Microsoft Volume Licensing Service Center (VLSC). Este ficheiro contém as informações de licenciamento para a nova versão do Windows em todos os dispositivos visados com a apólice.

- Para gerir este tipo de política, deve estar na função de segurança do **Administrador Completo** do Gestor de Configuração.

## <a name="configure-the-policy"></a>Configurar a política  

1. Na consola De Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione o nó de upgrade da **Edição do Windows 10.**  

2. No separador **Home** da fita, no grupo **Criar,** selecione **Create Edition Upgrade Policy**.  

3. Selecione **Criar Política**.  

4. Na página **Geral** do **Assistente para Criar Política de Atualização de Edição**, especifique as seguintes informações:  

    - **Nome** - Insira um nome para a política de upgrade da edição  

    - **Descrição** (opcional) - Opcionalmente, introduza uma descrição para a política que o ajuda a identificá-la na consola do Gestor de Configuração  

    - **SKU para atualizar dispositivo para** - A partir da lista de drop-down, selecione a edição-alvo do Windows 10 desktop ou Windows 10 Mobile  

    - **Informações de licença** - Selecione uma das seguintes opções:  

        - **Chave do produto** - Introduza uma chave de produto válida para a edição de desktop do Windows 10 target  

            > [!NOTE]  
            > Depois de criar uma política que contenha uma chave de produto, não pode editar a chave do produto mais tarde. O Gestor de Configuração obscurece a chave por razões de segurança. Para alterar a chave do produto, reintroduza toda a tecla.  

        - **Ficheiro de Licença** - Selecione **Navegar** para escolher um ficheiro de licença válido em formato XML. O Gestor de Configuração utiliza este ficheiro de licença para atualizar os dispositivos Móveis do Windows 10.  

5. Conclua o assistente.  

## <a name="deploy-the-policy"></a>Implementar a política  

1. Na consola De Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade e selecione o nó de upgrade da **Edição do Windows 10.**  

2. Selecione a política de atualização da edição do Windows 10 que pretende implementar. No separador **Home** da fita, no grupo **de implantação,** selecione **Deploy**.  

3. Escolha a recolha do dispositivo para a qual pretende implementar a apólice.

4. Selecione o horário pelo qual o cliente avalia a apólice.

5. Conclua o assistente.

## <a name="next-steps"></a>Passos seguintes

Monitorize esta implantação a partir do nó de **implantação** do espaço de trabalho **de monitorização.** Se vir erros que indiquem uma implementação infrutífera, por exemplo:

- **Não aplicável a este dispositivo**
- **Falha ao concluir a conversão do tipo de dados**

Estes erros não significam que a implantação falhou. Verifique no dispositivo-alvo que a atualização correu com sucesso.

Uma vez que o cliente avalia a política direcionada, aplica a atualização dentro de duas horas. [Algumas versões do Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) podem necessitar de um reinício nessa altura. Certifique-se de que informa todos os utilizadores para os quais implementa a apólice ou agende a política para funcionar fora do horário de trabalho dos utilizadores.

Se o seguinte erro aparecer no **DcmWmiProvider.log** no cliente, verifique se está a utilizar a chave adequada para o seu cenário de ativação. Para mais informações, consulte a secção [Antes de iniciar.](#before-you-start) Se estiver a utilizar um serviço de gestão de chaves (KMS) para ativação, [certifique-se](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)de utilizar uma chave de configuração do cliente KMS .  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Consulte também

- [Plano para ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Atualização de edição do Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Atualize as edições do Windows 10 ou desliga o modo S em dispositivos que utilizem o Microsoft Intune](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
