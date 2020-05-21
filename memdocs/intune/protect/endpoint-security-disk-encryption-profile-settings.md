---
title: Intune endpoint security disk definições de política de encriptação de disco de segurança / Microsoft Docs
description: Definições de política de encriptação de disco de segurança endpoint para BitLocker e FileVault no Microsoft Intune
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
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633289"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Definições de política de encriptação de disco para segurança de ponto final em Intune

Ver as definições que pode configurar em perfis para a política de *encriptação* do disco no nó de segurança Endpoint de Intune como parte de uma política de [segurança endpoint](../protect/endpoint-security-policy.md).

Plataformas e perfis suportados:

- **macOS**:
  - Perfil: **FileVault**
- **Windows 10 e mais tarde:**
  - Perfil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Encriptação

**Ativar fileVault**  
- **Não configurado** *(predefinido)*
- **Sim** - Ativar a encriptação completa do disco utilizando xTS-AES 128 com FileVault em dispositivos que executam o macOS 10.13 e mais tarde. O FileVault está ativado quando o utilizador assina fora do dispositivo.

  Quando definido para *Sim,* pode configurar configurações adicionais para FileVault.

  - Tipo de **chave de recuperação** 
     As chaves de recuperação *das chaves pessoais* são criadas para dispositivos. Configure as seguintes definições para a chave pessoal:

    - **Rotação da chave de recuperação pessoal**  
      Especifique com que frequência a chave de recuperação pessoal de um dispositivo girará. Pode selecionar o padrão de **Não configurado,** ou um valor de **1** a **12** meses.
    - **Descrição da localização da chave de recuperação pessoal**  
      Especifique uma mensagem curta para o utilizador que explique como pode recuperar a sua chave de recuperação pessoal. O utilizador vê esta mensagem no seu sinal no ecrã quando é solicitado a introduzir a sua chave de recuperação pessoal se uma palavra-passe for esquecida.

  - **Número de vezes permitidos para contornar**  
    Detete o número de vezes que um utilizador pode ignorar as instruções para ativar o FileVault antes de o FileVault ser necessário para que o utilizador faça o início.
    - **Não configurado** *(predefinido*) - A encriptação no dispositivo é necessária antes da próxima inscrição ser permitida.
    - **1** a **10** - Permita que um utilizador ignore a solicitação de 1 a 10 vezes antes de necessitar de encriptação no dispositivo.
    - **Sem limite, sempre solicitado** - O utilizador é solicitado para ativar o FileVault, mas a encriptação nunca é necessária.

  - **Permitir o adiamento até assinar**  
    - **Não configurado** *(predefinido)*
    - **Sim** - Adique a solicitação para ativar o FileVault até que o utilizador se apresente.  

  - **Desativar o pedido de sinalização**  
    Evite a solicitação ao utilizador que solicita que ative o FileVault quando assinar. Quando programado para desativar, o aviso de inscrição é desativado e, em vez disso, o utilizador é solicitado quando faz o início.
    - **Não configurado** *(predefinido)*
    - **Sim** - Desative a solicitação para ativar o FileVault que aparece no sign-out.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker – Definições de Base

- **Ativar encriptação completa do disco para OS e unidades de dados fixas**  
  CSP: [RequirerDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Se a unidade foi encriptada antes desta política aplicada, não são tomadas medidas adicionais. Se o método de encriptação e as opções corresponderem ao desta política, a configuração deve devolver o sucesso. Se uma opção de configuração BitLocker em vigor não corresponder a esta política, a configuração provavelmente devolverá um erro.
  
  Para aplicar esta política a um disco já encriptado, desencriptar a unidade e reaplicar a política de MDM. O predefinido do Windows não é exigir encriptação de unidade BitLocker. No entanto, no Azure AD Join e na Microsoft Account (MSA) a encriptação automática de registo/login pode aplicar-se permitindo o BitLocker na encriptação xTS-AES de 128 bits.

  - **Não configurado** *(predefinido)*- Não ocorre a aplicação do BitLocker.
  - **Sim** - Impor o uso do BitLocker.

- **Exigir que os cartões de armazenamento sejam encriptados (apenas para dispositivos móveis)**  
  CSP: [RequirerStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Esta definição aplica-se apenas aos dispositivos Windows Mobile e Mobile Enterprise SKU.
  - **Não configurado** *(predefinido*) - A definição retorna ao padrão DO, que não é para exigir encriptação do cartão de armazenamento.
  - **Sim** - A encriptação nos cartões de armazenamento é necessária para dispositivos móveis.

- **Ocultar pronta sobre encriptação de terceiros**  
  CSP: [AllowWarningForOtherDiskCrypton](https://go.microsoft.com/fwlink/?linkid=872525)

  Se o BitLocker estiver ativado num sistema já encriptado por um produto de encriptação de terceiros, poderá tornar o dispositivo inutilizável. A perda de dados pode ocorrer e poderá ter de reinstalar o Windows. É altamente sugerido para nunca ativar o BitLocker num dispositivo que tenha encriptação de terceiros instalada ou ativada.

  Por predefinição, o assistente de configuração BitLocker solicita aos utilizadores que confirmem que não existe encriptação de terceiros.

  - **Não configurado** *(predefinido*) – O assistente de configuração BitLocker apresenta um aviso e solicita aos utilizadores que confirmem que não existe encriptação de terceiros.
  - **Sim** - Ocultar o pedido dos assistentes de configuração BitLocker dos utilizadores.

  Se forem necessárias funcionalidades de ativação silenciosa BitLocker, o aviso de encriptação de terceiros deve ser ocultado, uma vez que quaisquer fluxos de trabalho de ativação silenciosa solado de prontas pausas necessárias.

  Quando definido para *Sim,* pode configurar a seguinte definição:

  - **Permitir que os utilizadores padrão permitam a encriptação durante o Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Não configurados** (*predefinidos)*– Durante o Azure Ative Directory Join (AADJ) cenários de ativação silenciosa, os utilizadores não precisam de ser administradores locais para ativar o BitLocker.
    - **Sim** - A definição é deixada como padrão do cliente, que é exigir acesso administrativo local para ativar o BitLocker.

    Para a ativação não silenciosa e cenários de Piloto Automático, o utilizador deve ser um administrador local para completar o assistente de configuração BitLocker.

- **Ativar a senha de recuperação orientada pelo cliente para**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Adicionar Conta de Trabalho (AWA, formalmente Unidos no Local de Trabalho) os dispositivos não são suportados para a rotação da chave.
  - **Não configurado** *(predefinido)*– O cliente não roda as teclas de recuperação bitLocker.
  - **Desativado**
  - **Dispositivos azure ad-join**
  - **Dispositivos Azure AD e Híbridos unidos**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker - Definições de unidade fixa

- **Política de unidade fixa BitLocker**  
  [Definições de Política de Grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Recuperação de unidade fixa**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Controle como as unidades de dados fixas protegidas pelo BitLocker são recuperadas na ausência das informações de chave de arranque necessárias.

    - **Não configuradas** *(predefinido*) - As opções de recuperação por predefinição são suportadas, incluindo o agente de recuperação de dados (DRA). O utilizador final pode especificar opções de recuperação e as informações de recuperação não são apoiadas no Diretório Ativo do Azure.
    - **Configurar** – Permitir o acesso à configuração de várias técnicas de recuperação de unidades.

    Quando definido para *configurar* as seguintes definições estão disponíveis:

    - **Chave de criação de utilizadores de recuperação**  
      - **Bloqueado** *(predefinido)*
      - **Necessário**
      - **Permitido**

    - **Configure pacote de recuperação BitLocker**
      - **Password e Key** *(predefinido*) - Inclua tanto a palavra-passe de recuperação bitLocker que é usada por administradores e utilizadores para desbloquear unidades protegidas, e pacotes chave de recuperação que são usados por administradores para fins de recuperação de dados) no Diretório Ativo.
      - **Apenas palavra-passe** - Os pacotes chave de recuperação podem não estar acessíveis quando necessário.

    - **Exigir dispositivo para fazer o backback informação de recuperação para o Azure Ad**
      - **Não configurado** *(predefinido*) - A ativação bitLocker será completada mesmo que a chave de recuperação de cópia sinuosa para a Azure AD falhe. Isto pode resultar em que nenhuma informação de recuperação seja armazenada externamente.
      - **Sim** - O BitLocker não completará a ativação até que as chaves de recuperação tenham sido guardadas com sucesso para o Diretório Ativo Azure.

    - **Criação de senha de recuperação do utilizador**  
      - **Bloqueado** *(predefinido)*
      - **Necessário**
      - **Permitido**

    - **Ocultar opções de recuperação durante a configuração do BitLocker**
      - **Não configurado** *(predefinido)*- Permita ao utilizador aceder a opções de recuperação extra.
      - **Sim** - Bloqueie o utilizador final de escolher opções de recuperação extra, tais como chaves de recuperação de impressão durante o assistente de configuração BitLocker.

    - **Ativar o BitLocker após a armazenar informações de recuperação**
      - **Não configurado** *(predefinido)*  
      - **Sim**

    - **Bloquear a utilização de um agente de recuperação de dados baseado em certificados (DRA)**
      - **Não configurado** *(predefinido*) - Permita a instalação da DRA. A criação de DRA requer uma empresa PKI e Objetos de Política de Grupo para implementar o agente e certificados dra.
      - **Sim** - Bloqueie a capacidade de utilizar o Agente de Recuperação de Dados (DRA) para recuperar as unidades ativadas pelo BitLocker.

  - **Bloquear o acesso a unidades de dados fixas não protegidas pelo BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Esta definição está disponível quando a política de *unidade fixa BitLocker* está definida para *configurar*.

    - **Não configurados** *(predefinido*) - Os dados podem ser escritos em unidades fixas não encriptadas.
    - **Sim** - O Windows não permitirá que quaisquer dados sejam escritos a unidades fixas que não estejam protegidas pelo BitLocker. Se uma unidade fixa não for encriptada, o utilizador terá de completar o assistente de configuração BitLocker para a unidade antes de ser concedido o acesso ao escrita.

  - **Configurar o método de encriptação para unidades de dados fixas**  
    CSP: [EncriptaçãoMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Configure o método de encriptação e a força da cifra para discos de discos de discos fixos de unidades de dados. *XTS- AES 128-bit* é o método de encriptação padrão do Windows e o valor recomendado.

    - **Não configurado** *(predefinido)*
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker - Definições de unidade osso

- **Política de condução do sistema BitLocker**  
  CSP: Definições de [política do grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configurar** *(padrão)*  
  - **Não configurado**

  Quando definido para *configurar,* pode configurar as seguintes definições:

  - **Autenticação de arranque necessária**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Não configurado** *(predefinido)*
    - **Sim** - Configure os requisitos adicionais de autenticação no arranque do sistema, incluindo a utilização de módulos de plataforma fidedigna (TPM) ou requisitos PIN de arranque.

    Quando definido para *Sim,* pode configurar as seguintes definições:

    - **Startup TPM compatível**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      É aconselhável exigir um TPM para o BitLocker. Esta definição só se aplica quando ativa o BitLocker pela primeira vez e não tem efeito se o BitLocker já estiver ativado.

      - **Blocked** *(predefinido)*- O BitLocker não utiliza o TPM.
      - **Necessário** - O BitLocker só permite se um TPM estiver presente e utilizável.
      - **Permitido** - O BitLocker utiliza o TPM se estiver presente.

    - **PIN de arranque tpm compatível**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** *(predefinido*) - Bloqueie a utilização de um PIN.
      - **Necessário** - Exija um PIN e um TPM presentes para ativar o BitLocker.
      - **Permitido** - O BitLocker utiliza o TPM se estiver presente e permite configurar um PIN de arranque pelo utilizador.

      Para cenários de ativação silenciosa, deve definir isto para *Bloqueado*. Os cenários de ativação silenciosa (incluindo o Autopilot) não serão bem sucedidos quando a interação do utilizador for necessária.

    - **Chave de arranque TPM compatível**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** *(predefinido*) - Bloqueie a utilização de teclas de arranque.
      - **Necessário** - Exija uma chave de arranque e o TPM esteja presente para ativar o BitLocker.
      - **Permitido** - O BitLocker utiliza o TPM se estiver presente e permite que esteja presente uma chave de arranque (como uma unidade USB) para desbloquear as unidades.

      Para cenários de ativação silenciosa, deve definir isto para *Bloqueado*. Os cenários de ativação silenciosa (incluindo o Autopilot) não serão bem sucedidos quando a interação do utilizador for necessária.

    - **Chave de arranque TPM compatível e PIN**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Bloqueado** *(predefinido*) - Bloqueie a utilização de uma chave de arranque e de uma combinação PIN.
      - **Necessário** - Exija que o BitLocker tenha uma chave de arranque e o pin presente para se ativar.
      - **Permitido** - O BitLocker utiliza o TPM se estiver presente e permite uma chave de arranque) e uma combinação PIN.

      Para cenários de ativação silenciosa, deve definir isto para *Bloqueado*. Os cenários de ativação silenciosa (incluindo o Autopilot) não serão bem sucedidos quando a interação do utilizador for necessária.

    - **Desative o BitLocker em dispositivos onde o TPM é incompatível**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Se não houver TPM presente, o BitLocker necessita de uma palavra-passe ou unidade USB para o arranque.

      Esta definição só se aplica quando ativa o BitLocker pela primeira vez e não tem efeito se o BitLocker já estiver ativado.

      - **Não configurado** *(predefinido)*
      - **Sim** - Bloqueie o BitLocker de ser configurado sem um chip TPM compatível.

    - **Ativar a mensagem de recuperação do preboot e o url**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configuração

      - **Não configurado** *(predefinido*) – Utilize as informações de recuperação pré-arranque do BitLocker.
      - **Sim** – Ative a configuração de uma mensagem de recuperação e URL personalizados de recuperação pré-arranque para ajudar os seus utilizadores a entender como encontrar a sua senha de recuperação. A mensagem de pré-arranque e o URL são vistos pelos utilizadores quando estão bloqueados fora do seu PC em modo de recuperação.

      Quando definido para *Sim,* pode configurar as seguintes definições:

      - **Mensagem de recuperação de preboot**  
        Especifique uma mensagem de recuperação pré-arranque personalizada.

      - **Url de recuperação de preboot**  
        Especifique um URL de recuperação pré-arranque personalizado.

    - **Recuperação de unidade de sistema**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Não configurado** *(predefinido)*  
      - **Configurar** - Ativar a configuração de configurações adicionais.

      Quando definido para *configurar* as seguintes definições estão disponíveis:

      - **Chave de criação de utilizadores de recuperação**  
        - **Bloqueado** *(predefinido)*
        - **Necessário**
        - **Permitido**

      - **Configure pacote de recuperação BitLocker**
        - **Password e Key** *(predefinido*) - Inclua tanto a palavra-passe de recuperação bitLocker que é usada por administradores e utilizadores para desbloquear unidades protegidas, e pacotes chave de recuperação que são usados por administradores para fins de recuperação de dados) no Diretório Ativo.
        - **Apenas palavra-passe** - Os pacotes chave de recuperação podem não estar acessíveis quando necessário.

      - **Exigir dispositivo para fazer o backback informação de recuperação para o Azure Ad**
        - **Não configurado** *(predefinido*) - A ativação bitLocker será completada mesmo que a chave de recuperação de cópia sinuosa para a Azure AD falhe. Isto pode resultar em que nenhuma informação de recuperação seja armazenada externamente.
        - **Sim** - O BitLocker não completará a ativação até que as chaves de recuperação tenham sido guardadas com sucesso para o Diretório Ativo Azure.

      - **Criação de senha de recuperação do utilizador**  
        - **Bloqueado** *(predefinido)*
        - **Necessário**
        - **Permitido**

      - **Ocultar opções de recuperação durante a configuração do BitLocker**
        - **Não configurado** *(predefinido)*- Permita ao utilizador aceder a opções de recuperação extra.
        - **Sim** - Bloqueie o utilizador final de escolher opções de recuperação extra, tais como chaves de recuperação de impressão durante o assistente de configuração BitLocker.

      - **Ativar o BitLocker após a armazenar informações de recuperação**
        - **Não configurado** *(predefinido)*  
        - **Sim**

      - **Bloquear a utilização de um agente de recuperação de dados baseado em certificados (DRA)**
        - **Não configurado** *(predefinido*) - Permita a instalação da DRA. A criação de DRA requer uma empresa PKI e Objetos de Política de Grupo para implementar o agente e certificados dra.
        - **Sim** - Bloqueie a capacidade de utilizar o Agente de Recuperação de Dados (DRA) para recuperar as unidades ativadas pelo BitLocker.

    - **Comprimento mínimo do PIN**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Especifique o comprimento pin de arranque mínimo quando o TPM + PIN for necessário durante a ativação do BitLocker. O comprimento PIN deve estar entre 4 e 20 dígitos.

      Se não configurar esta definição, os utilizadores podem configurar um PIN de arranque de qualquer comprimento (entre 4 e 20 dígitos)

      Esta definição só se aplica quando ativa o BitLocker pela primeira vez e não tem efeito se o BitLocker já estiver ativado.

  - **Configurar o método de encriptação para unidades do Sistema Operativo**  
   CSP: [EncriptaçãoMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Configure o método de encriptação e a força da cifra para unidades de SO. *XTS- AES 128-bit* é o método de encriptação padrão do Windows e o valor recomendado.

    - **Não configurado** *(predefinido)*
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker - Definições de unidade amovível

- **Configurar o método de encriptação para unidades do Sistema Operativo**  
  CSP: Definições de [política do grupo BitLocker](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Não configurado** *(predefinido)*  
  - **Configurar**

  Quando definido para *configurar,* pode configurar as seguintes definições.

  - **Configurar o método de encriptação para unidades de dados amovíveis**  
    CSP: [EncriptaçãoMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Selecione o método de encriptação desejado para discos de unidades de dados amovíveis.

    - **Não configurado** *(predefinido)*
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Block write acesso a unidades de dados amovíveis não protegidos pelo BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Não configurados** *(predefinido*) - Os dados podem ser escritos para unidades amovíveis não encriptadas.
    - **Sim** - O Windows não permite que os dados sejam escritos para unidades amovíveis que não estão protegidas pelo BitLocker. Se uma unidade amovível inserida não estiver encriptada, o utilizador deve completar o assistente de configuração BitLocker antes de o acesso de escrita ser concedido para conduzir.

    - **Block write acesso a unidades de dados amovíveis não protegidos pelo BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Não configurado** *(predefinido*) - Qualquer unidade encriptada BitLocker pode ser utilizada.
      - **Sim** - Bloqueie o acesso a unidades amovíveis a menos que tenham sido encriptados num computador propriedade da sua organização.

## <a name="next-steps"></a>Próximos passos

[Política de segurança de endpoint para encriptação de disco](../protect/endpoint-security-disk-encryption-policy.md)
