---
title: Gerir dispositivos com MDM no local
titleSuffix: Configuration Manager
description: Proteja os dados do dispositivo com limpeza completa, limpeza seletiva, bloqueio remoto ou reset da código de acesso utilizando a gestão de dispositivos móveis do Gestor de Configuração no local (MDM).
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721872"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Gerir dispositivos e proteger dados com MDM no local no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os dispositivos móveis podem armazenar dados sensíveis e fornecer fácil acesso a muitos recursos organizacionais. Para ajudar a proteger dispositivos e dados, utilize o Gestor de Configuração para as seguintes ações de gestão do dispositivo:

- **Limpeza completa**: Restaurar o dispositivo nas suas definições de fábrica

- **Limpeza seletiva**: Remova apenas dados organizacionais

- **Redefinição**da código de acesso: Remova ou reset a senha quando um utilizador a esquece

- **Bloqueio remoto**: Ajude a fixar um dispositivo que possa estar perdido

## <a name="full-wipe"></a>Eliminação completa  

Quando necessitar de proteger um dispositivo perdido ou quando se aposentar um dispositivo de uso ativo, pode iniciar uma limpeza completa nele. Esta ação restaura o dispositivo às suas faltas de fábrica. Remove todos os dados e definições organizacionais e do utilizador.

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo que pretende limpar.

1. Na fita, no grupo Dispositivo, selecione **Remote Device Actions**, e, em seguida, escolha **Retire/Wipe**.

1. Na janela **Retire from Configuration Manager,** selecione a opção de **limpar o dispositivo móvel e retirá-lo do Gestor de Configuração**.

## <a name="selective-wipe"></a>Eliminação seletiva

Para remover apenas dados organizacionais de um dispositivo, inicie uma limpeza seletiva.

### <a name="behaviors-by-os-version"></a>Comportamentos por versão OS

As tabelas que se seguem descrevem quais os dados removidos e o efeito nos dados que permanecem no dispositivo após uma limpeza seletiva.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8.1 e Windows RT

|Conteúdo|Comportamento de limpeza seletiva|  
|-------|--------|
|Apps e dados associados instalados pelo Gestor de Configuração|Desinstala as aplicações e remove quaisquer teclas de carga lateral. Revoga a chave de encriptação para aplicações que utilizam o Windows Selective Wipe, e os dados já não estão acessíveis.|
|Perfis de VPN e de Wi-Fi|Remove os perfis|
|Certificados|Remove e revoga os certificados|
|Definições|Remove os requisitos|
|Perfis de e-mail|Remove o e-mail que está habilitado para o EFS, que inclui a aplicação Mail para e-mail e anexos Windows.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8.0 e Windows Phone 8.1

|Conteúdo|Comportamento de limpeza seletiva|  
|-------|--------|
|Aplicativos da empresa e dados associados instalados pelo Gestor de Configuração|Desinstala as aplicações e remove dados de aplicações organizacionais.|
|Perfis de VPN e de Wi-Fi|Remove os perfis para Windows 10 Mobile e Windows Phone 8.1|
|Certificados|Remove os certificados para Windows Phone 8.1|
|Perfis de e-mail|Remove os perfis (exceto o Windows Phone 8.0)|

As seguintes definições também são removidas dos dispositivos Windows 10 Mobile e Windows Phone 8.1:  

- **Palavra-passe obrigatória para desbloquear os dispositivos móveis**  
- **Permitir palavras-passe simples**  
- **Comprimento mínimo da palavra-passe**  
- **Tipo obrigatório de palavra-passe**
- **Expiração da Palavra-passe (dias)**  
- **Memorizar histórico de palavras-passe**  
- **Número de falhas de início de sessão consecutivas permitidas antes de o dispositivo ser apagado**  
- **Minutos de inatividade antes da palavra-passe ser exigida**  
- **Tipo obrigatório de palavra-passe – número mínimo de conjuntos de carateres**  
- **Permitir câmara**
- **Encriptação obrigatória no dispositivo móvel**  
- **Permitir armazenamento amovível**  
- **Permitir browser**  
- **Permitir loja de aplicações**  
- **Permitir captura de ecrã**  
- **Permitir geolocalização**  
- **Permitir Conta Microsoft**  
- **Permitir copiar e colar**  
- **Permitir partilha de Wi-Fi**  
- **Permitir ligação automática a hotspots Wi-Fi**  
- **Permitir relatórios de hotspots Wi-Fi**  
- **Permitir a reposição de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

### <a name="start-a-selective-wipe"></a>Inicie uma limpeza seletiva

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo que pretende limpar.

1. Na fita, no grupo Dispositivo, selecione **Remote Device Actions**, e, em seguida, escolha **Retire/Wipe**.

1. Na janela **Retire from Configuration Manager,** selecione a seguinte opção: **Limpe o conteúdo da empresa e retire o dispositivo móvel do Gestor de Configuração**.

### <a name="recommendations-for-selective-wipe"></a>Recomendações para limpeza seletiva

- Para obter uma limpeza de e-mail com sucesso, configurar perfis de e-mail para dispositivos Windows Phone 8.1.

- Para uma limpeza bem-sucedida de apps, certifique-se de que as aplicações são distribuídas através da gestão de aplicações de dispositivos móveis.

## <a name="passcode-reset"></a>Repor código de acesso

Se um utilizador esquecer a sua senha, utilize esta ação para forçar uma nova senha temporária no dispositivo. Também pode remover completamente a senha. A seguinte tabela indica como a reposição de códigos de acesso funciona em diferentes plataformas móveis.

| Versão do SO | Repor código de acesso |
|------------|----------------|
| Windows 10 | Não suportado |
| Windows 10 mobile | Suportados, excluindo dispositivos azure ative diretórios |
| Windows Phone 8 e Windows Phone 8.1 | Suportado |
| Windows RT 8.1 | Não suportado |
| Windows 8.1 | Não suportado |

> [!Note]
> Inicie a ação de reset da código de acesso a partir do site de alto nível. Por exemplo, se utilizar um site de administração central, só pode fazer a ação nesse site. Se estiver a usar um local primário autónomo, só pode fazer a ação a partir desse site.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Redefinir remotamente a senha num dispositivo móvel

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo ou dispositivos em que pretende repor o código de acesso.

1. Na fita, no grupo Dispositivo, selecione **Remote Device Actions**, e, em seguida, escolha **reset de código de acesso**.  

### <a name="show-the-state-of-the-passcode-reset"></a>Mostrar o estado da reposição da código de acesso  

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo ou dispositivos em que pretende mostrar o estado da reposição do código de acesso.

1. Na fita, no grupo Dispositivo, selecione **Remote Device Actions**, e, em seguida, escolha Mostrar a **Palavra-passe .**  

## <a name="remote-lock"></a>Bloqueio remoto

Se um utilizador perder o dispositivo, pode bloquear o dispositivo remotamente. A tabela seguinte indica como o bloqueio remoto funciona em diferentes plataformas móveis.  

|Versão do SO|Bloqueio remoto|
|----------|-----------|
|Windows 10|Não suportado|
|Windows Phone 8 e Windows Phone 8.1|Suportado|
|Windows RT 8.1|Suportado, se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|
|Windows 8.1|Suportado, se o utilizador atual do dispositivo for o mesmo utilizador que inscreveu o dispositivo.|

> [!Note]
> Inicie a ação de bloqueio remoto a partir do local de nível superior. Por exemplo, se utilizar um site de administração central, só pode fazer a ação nesse site. Se estiver a usar um local primário autónomo, faça a ação a partir desse site.

### <a name="remotely-lock-a-mobile-device"></a>Bloqueie remotamente um dispositivo móvel

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo ou dispositivos a bloquear.

1. Na fita, no grupo Dispositivo, selecione **As ações**do dispositivo remoto e, em seguida, escolha o bloqueio **remoto**. Confirme a ação.

### <a name="show-the-state-of-the-remote-lock"></a>Mostre o estado da fechadura remota

1. Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de Ativos e Compliance** e escolha o nó de **Dispositivos.** Também pode escolher **As Coleções** de Dispositivos e selecionar uma coleção da qual o dispositivo é membro.

1. Selecione o dispositivo em que pretende mostrar o estado do bloqueio remoto.

1. Na fita, no grupo Dispositivo, selecione **Remote Device Actions**, e, em seguida, escolha mostrar estado de bloqueio **remoto**.
