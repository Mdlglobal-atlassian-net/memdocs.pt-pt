---
title: Referência de definições BitLocker
titleSuffix: Configuration Manager
description: Todas as definições de gestão bitLocker disponíveis no Gestor de Configuração
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723930"
---
# <a name="bitlocker-settings-reference"></a>Referência de definições BitLocker

*Aplica-se a: Gestor de Configuração (ramo atual)*

<!-- 5925683 -->

As políticas de gestão bitLocker no Gestor de Configuração contêm os seguintes grupos políticos:

- Configuração
- Unidade do sistema operativo
- Unidade fixa
- Unidade amovível
- Gestão de clientes

As seguintes secções descrevem e sugerem configurações para as definições de cada grupo.

> [!NOTE]
> Estas definições baseiam-se na versão de Configuração Manager 2002. A versão 1910 não inclui todas estas definições.

## <a name="setup"></a>Configuração

As definições nesta página configuram opções globais de encriptação BitLocker.

### <a name="drive-encryption-method-and-cipher-strength"></a>Método de encriptação de unidade e força de cifra

*Configuração sugerida*: **Ativado** com o método de encriptação padrão ou maior.

> [!NOTE]
> A página de propriedades de **Configuração** inclui dois grupos de configurações para diferentes versões do Windows. Esta secção descreve os dois.

#### <a name="windows-81-devices"></a>Dispositivos Windows 8.1

Para dispositivos Windows 8.1, ative a opção para o método de **encriptação Drive e a força da cifra**, e selecione um dos seguintes métodos de encriptação:

- AES 128-bit com Difusor
- AES 256-bit com Difusor
- AES 128-bit (padrão)
- AES 256-bit

#### <a name="windows-10-devices"></a>Dispositivos Windows 10

Para dispositivos Windows 10, ative a opção para o método de **encriptação Drive e a força da cifra (Windows 10)**. Em seguida, selecione individualmente um dos seguintes métodos de encriptação para unidades de S, unidades de dados fixas e unidades de dados amovíveis:

- AES-CBC 128-bit
- AES-CBC 256-bit
- XTS-AES 128-bit (padrão)
- XTS-AES 256-bit

> [!TIP]
> O BitLocker utiliza a norma AES (Advanced Encryption Standard) como algoritmo de encriptação com comprimentos configuráveis de chave de 128 ou 256 bits. Nos dispositivos Windows 10, a encriptação AES suporta a corrente de blocos de cifra (CBC) ou o roubo de cifra (XTS).
>
> Se necessitar de utilizar uma unidade amovível em dispositivos que não executem o Windows 10, utilize a AES-CBC.

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Notas gerais de utilização para encriptação de unidade e força de cifra

- Se desativar ou não configurar estas definições, o BitLocker utiliza o método de encriptação predefinido.

- O Gestor de Configuração aplica estas definições quando liga o BitLocker.

- Se a unidade já estiver encriptada ou estiver em curso, qualquer alteração nestas definições de política não altera a encriptação de unidade no dispositivo.

- Se utilizar o valor predefinido, o relatório bitLocker Computer Compliance pode apresentar a força da cifra como **desconhecida**. Para contornar esta questão, ative esta definição e defina um valor explícito para a força da cifra.

### <a name="prevent-memory-overwrite-on-restart"></a>Evitar a sobreescrita da memória no reinício

*Configuração sugerida*: **Não configurado**

Configure esta política para melhorar o desempenho do reinício sem sobrepor os segredos bitLocker na memória no reinício.

Quando não configura esta política, o BitLocker remove os seus segredos da memória quando o computador reinicia.

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Validar a conformidade da regra de utilização do certificado de cartão inteligente

*Configuração sugerida*: **Não configurado**

Configure esta política para utilizar a proteção BitLocker baseada em certificados smartcard. Em seguida, especifique o **identificador**de objeto de certificado .

Quando não configura esta política, o BitLocker utiliza `1.3.6.1.4.1.311.67.1.1` o identificador de objeto predefinido para especificar um certificado.

### <a name="organization-unique-identifiers"></a>Identificadores únicos da organização

*Configuração sugerida*: **Não configurado**

Configure esta política para utilizar um agente de recuperação de dados baseado em certificados ou o leitor BitLocker To Go.

Quando não configura esta política, o BitLocker não utiliza o campo **de identificação.**

Se a sua organização necessitar de medições de segurança mais elevadas, configure o campo **de identificação.** Defina este campo em todos os dispositivos USB direcionados e alinhe-o com esta definição.

## <a name="os-drive"></a>Unidade do sistema Operativo

As definições desta página configuram as definições de encriptação para a unidade em que o Windows está instalado.

### <a name="operating-system-drive-encryption-settings"></a>Definições de encriptação de unidade de sistema operativo

*Configuração sugerida*: **Ativado**

Se ativar esta definição, o utilizador tem de proteger a unidade DE E e o BitLocker encripta a unidade. Se o desativar, o utilizador não pode proteger a unidade. Se não configurar esta política, a proteção BitLocker não é necessária na unidade de SO.

> [!NOTE]
> Se a unidade já estiver encriptada e desativar esta definição, o BitLocker desencripta a unidade.  

Se tiver dispositivos sem módulo de [plataforma fidedigna (TPM),](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node)utilize a opção de permitir o **BitLocker sem um TPM compatível (requer uma palavra-passe)**. Esta definição permite ao BitLocker encriptar a unidade OS, mesmo que o dispositivo não tenha um TPM. Se permitir esta opção, o Windows solicita ao utilizador que especifique uma palavra-passe BitLocker.

Em dispositivos com um TPM compatível, dois tipos de métodos de autenticação podem ser utilizados no arranque para fornecer uma proteção adicional para dados encriptados. Quando o computador começa, só pode utilizar o TPM para autenticação, ou também pode exigir a inscrição de um número de identificação pessoal (PIN). Configure as seguintes definições:

- **Selecione protetor para acionar**o sistema operativo: Configure-o para utilizar um TPM e PIN, ou apenas o TPM.

- **Configurar**o comprimento mínimo pin para o arranque : Se necessitar de um PIN, este valor é o comprimento mais curto que o utilizador pode especificar. O utilizador introduz este PIN quando o computador arranca para desbloquear a unidade. Por defeito, o `4`comprimento mínimo do PIN é .

> [!TIP]
> Para uma maior segurança, quando ativar dispositivos com protetor TPM + PIN, considere *desativar* as seguintes definições de política de grupo nas**Definições**de Sono de**Gestão** > de Energia do **Sistema:** > 
>
> - Permitir estados de espera (S1-S3) Ao dormir (ligado)
>
> - Permitir estados de espera (S1-S3) Ao dormir (na bateria)

### <a name="allow-enhanced-pins-for-startup"></a>Permitir PINs melhorados para arranque

*Configuração sugerida*: **Não configurado**

Configure o BitLocker para utilizar PINs de arranque melhorados. Estes PINs permitem a utilização de caracteres adicionais, tais como letras maiúsculas e minúsculas, símbolos, números e espaços. Esta definição aplica-se quando liga o BitLocker.

> [!IMPORTANT]
> Nem todos os computadores podem suportar PINs melhorados no ambiente de pré-arranque. Antes de ativar a sua utilização, avalie se os seus dispositivos são compatíveis com esta funcionalidade.

Se ativar esta definição, todos os novos PINs de arranque bitLocker permitem ao utilizador criar PINs melhorados.

- **Requerer PINs apenas aASCII**: Ajude a tornar os PINs melhorados mais compatíveis com computadores que limitam o tipo ou número de caracteres que pode introduzir no ambiente de pré-arranque.

Se desativar ou não configurar esta definição de política, o BitLocker não utiliza PINs melhorados.

### <a name="operating-system-drive-password-policy"></a>Política de senha de condução do sistema operativo

*Configuração sugerida*: **Não configurado**

Utilize estas definições para definir os constrangimentos das palavras-passe para desbloquear unidades de SISTEMA protegidas pelo BitLocker. Se permitir protetores não-TPM nas unidades DES, configure as seguintes definições:

- **Configure a complexidade da palavra-passe para unidades do sistema operativo**: Para impor requisitos de complexidade na palavra-passe, selecione Exigir complexidade de **palavra-passe**.

- **Comprimento mínimo da palavra-passe para acionar** `8`o sistema operativo : Por defeito, o comprimento mínimo é de .

- **Requerem senhas exclusivas a ASCII para unidades de SO amovíveis**

Se ativar esta definição de política, os utilizadores podem configurar uma palavra-passe que satisfaça os requisitos que define.

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Notas gerais de utilização para a política de senha de condução de OS

- Para que estas definições de requisitos de complexidade sejam eficazes, também ativar a definição de **palavra-passe** da política do grupo deve satisfazer os requisitos de complexidade na configuração de computador**Definições de** >  **definições** > de definições de**definições** > de**segurança** > Política de**palavra-passe**Definições de segurança .

- O BitLocker aplica estas definições quando o liga, não quando desbloqueia um volume. O BitLocker permite-lhe desbloquear uma unidade com qualquer um dos protetores que estão disponíveis na unidade.

- Se utilizar a política de grupo para permitir algoritmos compatíveis com fips para encriptação, hashing e assinatura, não pode permitir palavras-passe como protetor BitLocker.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Redefinir dados de validação da plataforma após a recuperação do BitLocker

*Configuração sugerida*: **Não configurado**

Controle se o Windows atualiza os dados de validação da plataforma quando começar após a recuperação do BitLocker.

Se ativar ou não configurar esta definição, o Windows atualiza os dados de validação da plataforma nesta situação.

Se desativar esta definição de política, o Windows não atualiza os dados de validação da plataforma nesta situação.

### <a name="pre-boot-recovery-message-and-url"></a>Mensagem de recuperação pré-arranque e URL

*Configuração sugerida*: **Não configurado**

Quando o BitLocker bloqueia a unidade OS, utilize esta definição para exibir uma mensagem de recuperação personalizada ou um URL no ecrã de recuperação bitLocker pré-arranque. Esta definição aplica-se apenas aos dispositivos do Windows 10.

Quando ativar esta definição, selecione uma das seguintes opções para a mensagem de recuperação pré-arranque:

- **Utilize a mensagem de recuperação predefinida e o URL**: Exiba a mensagem de recuperação do BitLocker predefinido e o URL no ecrã de recuperação bitLocker pré-arranque. Se configurar previamente uma mensagem de recuperação personalizada ou URL, utilize esta opção para reverter para a mensagem predefinida.

- **Utilize a mensagem de recuperação personalizada**: Inclua uma mensagem personalizada no ecrã de recuperação bitLocker pré-arranque.

  - **Opção de mensagem de recuperação personalizada**: Escreva a mensagem personalizada para exibir. Se também quiser especificar um URL de recuperação, inclua-o como parte desta mensagem de recuperação personalizada. O comprimento máximo da corda é de 32.768 caracteres.

- Utilize url **de recuperação personalizado**: Substitua o URL predefinido apresentado no ecrã de recuperação BitLocker pré-arranque.

  - **Opção URL**de recuperação personalizada : Escreva o URL para visualizar. O comprimento máximo da corda é de 32.768 caracteres.

> [!NOTE]
> Nem todos os caracteres e línguas são suportados no pré-arranque. Primeiro teste a sua mensagem personalizada ou URL para se certificar de que aparece corretamente no ecrã de recuperação bitLocker pré-arranque.

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Definições de aplicação da política de encriptação (unidade de OS)

*Configuração sugerida*: **Ativado**

Configure o número de dias que os utilizadores podem adiar a conformidade do BitLocker para a unidade de SO. O **período de carência de incumprimento** começa quando o Gestor de Configuração o deteta pela primeira vez como incompatível. Após o termo deste período de carência, os utilizadores não podem adiar a ação necessária ou solicitar uma isenção.

Se o processo de encriptação necessitar de entrada do utilizador, aparece no Windows uma caixa de diálogo que o utilizador não pode fechar até fornecer as informações necessárias. Futuras notificações de erros ou estatuto não terão esta restrição.

Se o BitLocker não necessitar da interação do utilizador para adicionar um protetor, após o período de carência expirar, o BitLocker inicia a encriptação em segundo plano.

Se desativar ou não configurar esta definição, o Gestor de Configuração não requer que os utilizadores cumpram as políticas do BitLocker.

Para fazer cumprir a política imediatamente, `0`estabeleça um período de carência de .

## <a name="fixed-drive"></a>Unidade fixa

As definições desta página configuram a encriptação para unidades adicionais de dados num dispositivo.

### <a name="fixed-data-drive-encryption"></a>Encriptação de unidade de dados fixos

*Configuração sugerida*: **Ativado**

Gerencie o seu requisito de encriptação de unidades de dados fixas. Se ativar esta definição, o BitLocker exige que os utilizadores coloquem todas as unidades de dados fixas sob proteção. Em seguida, encripta as unidades de dados.

Quando ativar esta política, ou ativa o desbloqueio automático ou as definições para a política de **palavra-passe de unidade de dados fixos**.

- **Configure o desbloqueio automático para**uma unidade de dados fixa: Permita ou exija que o BitLocker desbloqueie automaticamente qualquer unidade de dados encriptada. Para utilizar o desbloqueio automático, também requer que o BitLocker encripte a [unidade DE .](#os-drive)

Se não configurar esta definição, o BitLocker não exige que os utilizadores coloquem unidades de dados fixas sob proteção.

Se desativar esta definição, os utilizadores não podem colocar as suas unidades de dados fixas sob a proteção BitLocker. Se desativar esta política depois de o BitLocker encriptar unidades de dados fixas, o BitLocker desencripta as unidades de dados fixas.

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Negar o acesso a unidades fixas não protegidas pela BitLocker

*Configuração sugerida*: **Não configurado**

Requer proteção BitLocker para o Windows escrever dados para unidades fixas no dispositivo. O BitLocker aplica esta política quando a liga.

Quando activaesta definição:

- Se o BitLocker proteger uma unidade de dados fixa, o Windows monta-o com acesso à leitura e escrita.

- Para qualquer unidade de dados fixoque o BitLocker não proteja, o Windows monta-o como apenas leitura.

Quando não configura esta definição, o Windows monta todas as unidades de dados fixas com acesso a leitura e escrita.

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>Política de senha de condução de dados fixos

*Configuração sugerida*: **Não configurado**

Utilize estas definições para definir os constrangimentos das palavras-passe para desbloquear unidades de dados fixas protegidas pelo BitLocker.

Se ativar esta definição, os utilizadores podem configurar uma palavra-passe que satisfaça os requisitos definidos.

Para uma maior segurança, ative esta definição e, em seguida, configure as seguintes definições:

- **Requerer a palavra-passe para a unidade de dados fixos**: Os utilizadores têm de especificar uma palavra-passe para desbloquear uma unidade de dados fixa protegida pelo BitLocker.

- **Configure a complexidade da palavra-passe para unidades de dados fixas**: Para impor requisitos de complexidade na palavra-passe, selecione Exigir complexidade de **palavra-passe**.

- **Comprimento mínimo da palavra-passe para unidade de dados fixos**: Por defeito, o comprimento mínimo é `8`.

Se desativar esta definição, os utilizadores não podem configurar uma palavra-passe.

Quando a apólice não está configurada, o BitLocker suporta palavras-passe com as definições predefinidas. As definições padrão não incluem requisitos de complexidade de palavras-passe, e requerem apenas oito caracteres.

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Notas gerais de utilização para a política de senha de condução de dados fixos

- Para que estas definições de requisitos de complexidade sejam eficazes, também ativar a definição de **palavra-passe** da política do grupo deve satisfazer os requisitos de complexidade na configuração de computador**Definições de** >  **definições** > de definições de**definições** > de**segurança** > Política de**palavra-passe**Definições de segurança .

- O BitLocker aplica estas definições quando o liga, não quando desbloqueia um volume. O BitLocker permite-lhe desbloquear uma unidade com qualquer um dos protetores que estão disponíveis na unidade.

- Se utilizar a política de grupo para permitir algoritmos compatíveis com fips para encriptação, hashing e assinatura, não pode permitir palavras-passe como protetor BitLocker.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Definições de aplicação da política de encriptação (unidade de dados fixos)

*Configuração sugerida*: **Ativado**

Configure o número de dias que os utilizadores podem adiar a conformidade do BitLocker para unidades de dados fixos. O **período de carência de incumprimento** começa quando o Gestor de Configuração deteta pela primeira vez a unidade de dados fixos como incompatível. Não aplica a política fixa de condução de dados até que a unidade de SO esteja em conformidade. Após o termo do período de carência, os utilizadores não podem adiar a ação necessária ou solicitar uma isenção.

Se o processo de encriptação necessitar de entrada do utilizador, aparece no Windows uma caixa de diálogo que o utilizador não pode fechar até fornecer as informações necessárias. Futuras notificações de erros ou estatuto não terão esta restrição.

Se o BitLocker não necessitar da interação do utilizador para adicionar um protetor, após o período de carência expirar, o BitLocker inicia a encriptação em segundo plano.

Se desativar ou não configurar esta definição, o Gestor de Configuração não requer que os utilizadores cumpram as políticas do BitLocker.

Para fazer cumprir a política imediatamente, `0`estabeleça um período de carência de .

## <a name="removable-drive"></a>Unidade amovível

As definições desta página configuram encriptação para unidades amovíveis, tais como chaves USB.

### <a name="removable-data-drive-encryption"></a>Encriptação de unidade de dados amovível

*Configuração sugerida*: **Ativado**

Esta definição controla a utilização do BitLocker em unidades amovíveis.

- **Permitir que os utilizadores apliquem a proteção BitLocker em unidades de dados amovíveis:** Os utilizadores podem ligar a proteção BitLocker para uma unidade amovível.

- **Permitir que os utilizadores suspendam e descodiquem o BitLocker em unidades de dados amovíveis:** Os utilizadores podem remover ou suspender temporariamente a encriptação de unidade BitLocker de uma unidade amovível.

Quando ativa esta definição e permite que os utilizadores apliquem a proteção BitLocker, o cliente do Gestor de Configuração guarda informações de recuperação sobre unidades amovíveis para o serviço de recuperação no ponto de gestão. Este comportamento permite que os utilizadores recuperem a unidade se esquecerem ou perderem o protetor (palavra-passe).

Quando activaesta definição:

- Ativar as definições para a política de senha de **condução de dados amovíveis**

- *Desative* as seguintes definições de política de grupo no **Sistema** > **De acesso amovível ao armazenamento** para configurações de computador & utilizador:

  - **Todas as aulas de armazenamento amovíveis: Negar todos os acessos**
  - **Discos amovíveis: Negar o acesso à escrita**
  - **Discos amovíveis: Negar o acesso à leitura**

Se desativar esta definição, os utilizadores não podem utilizar o BitLocker em unidades amovíveis.

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Negar o acesso a unidades amovíveis não protegidas pela BitLocker

*Configuração sugerida*: **Não configurado**

Requer proteção BitLocker para o Windows escrever dados para unidades amovíveis no dispositivo. O BitLocker aplica esta política quando a liga.

Quando activaesta definição:

- Se o BitLocker proteger uma unidade amovível, o Windows monta-a com acesso à leitura e escrita.

- Para qualquer unidade amovível que o BitLocker não proteja, o Windows monta-o como apenas leitura.

- Se ativar a opção de **Negar o acesso a dispositivos configurados noutra organização,** o BitLocker apenas dá acesso por escrito a unidades amovíveis com campos de identificação que correspondam aos campos de identificação permitidos. Defina estes campos com a **Organização identifica configurações globais únicas** na página [de Configuração.](#setup)

Quando desativa ou não configura esta definição, o Windows monta todas as unidades amovíveis com acesso a leitura e escrita.

> [!NOTE]
> Pode anular esta definição com as definições de política de grupo no **Sistema** > de Acesso ao**Armazenamento Amovível**. Se ativar a definição da política de grupo **Dos discos Amovíveis: Negar o acesso à escrita,** então o BitLocker ignora esta definição de Gestor de Configuração.

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>Política de senha de condução de dados amovíveis

*Configuração sugerida*: **Ativado**

Utilize estas definições para definir os constrangimentos das palavras-passe para desbloquear unidades amovíveis protegidas pelo BitLocker.

Se ativar esta definição, os utilizadores podem configurar uma palavra-passe que satisfaça os requisitos definidos.

Para uma maior segurança, ative esta definição e, em seguida, configure as seguintes definições:

- **Requerer uma palavra-passe para uma unidade de dados amovível**: Os utilizadores têm de especificar uma palavra-passe para desbloquear uma unidade amovível protegida pelo BitLocker.

- **Configure a complexidade da palavra-passe para unidades de dados amovíveis**: Para impor requisitos de complexidade na palavra-passe, selecione Exigir complexidade de **palavra-passe**.

- **Comprimento mínimo da palavra-passe para a unidade** `8`de dados amovível : Por defeito, o comprimento mínimo é .

Se desativar esta definição, os utilizadores não podem configurar uma palavra-passe.

Quando a apólice não está configurada, o BitLocker suporta palavras-passe com as definições predefinidas. As definições padrão não incluem requisitos de complexidade de palavras-passe, e requerem apenas oito caracteres.

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Notas gerais de utilização para a política de senha de condução de dados amovíveis

- Para que estas definições de requisitos de complexidade sejam eficazes, também ativar a definição de **palavra-passe** da política do grupo deve satisfazer os requisitos de complexidade na configuração de computador**Definições de** >  **definições** > de definições de**definições** > de**segurança** > Política de**palavra-passe**Definições de segurança .

- O BitLocker aplica estas definições quando o liga, não quando desbloqueia um volume. O BitLocker permite-lhe desbloquear uma unidade com qualquer um dos protetores que estão disponíveis na unidade.

- Se utilizar a política de grupo para permitir algoritmos compatíveis com fips para encriptação, hashing e assinatura, não pode permitir palavras-passe como protetor BitLocker.

## <a name="client-management"></a>Gestão de clientes

As definições nesta página configuram serviços de gestão BitLocker e clientes.

### <a name="bitlocker-management-services"></a>Serviços de Gestão BitLocker

*Configuração sugerida*: **Ativado**

Quando ativa esta definição, o Gestor de Configuração faz automaticamente e silenciosamente o backup informação de recuperação chave na base de dados do site. Se desativar ou não configurar esta definição, o Gestor de Configuração não guarda informações de recuperação da chave.

- **Selecione informações de recuperação BitLocker para armazenar**: Configure o serviço de recuperação da chave para fazer o backback das informações de recuperação do BitLocker. Fornece um método administrativo de recuperação de dados encriptados pelo BitLocker, o que ajuda a prevenir a perda de dados devido à falta de informação chave.

- Permitir que as informações de **recuperação sejam armazenadas em texto simples**: Sem um certificado de encriptação de gestão BitLocker para o SQL Server, o Gestor de Configuração armazena as informações de recuperação chave em texto simples. Para mais informações, consulte [encriptar dados de recuperação](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- Frequência de verificação do estado do **cliente (minutos)**: Na frequência configurada, o cliente verifica as políticas de proteção bitLocker e o estado no computador e também confirma a chave de recuperação do cliente. Por padrão, o cliente do Gestor de Configuração atualiza as suas informações de recuperação BitLocker a cada 90 minutos.

### <a name="user-exemption-policy"></a>Política de isenção de utilizadores

*Configuração sugerida*: **Não configurado**

Configure um método de contacto para os utilizadores solicitarem uma isenção da encriptação BitLocker.

Se ativar esta definição de política, forneça as seguintes informações:

- **Dias máximos para adiar**: Quantos dias o utilizador pode adiar uma política forçada. Por padrão, este `7` valor é de dias (uma semana).

- **Método**de contacto : Especifique como os utilizadores podem solicitar uma isenção: URL, endereço de e-mail ou número de telefone.

- **Contacto**: Especifique o URL, o endereço de e-mail ou o número de telefone. Quando um utilizador pede uma isenção da proteção BitLocker, vê uma caixa de diálogo Windows com instruções sobre como aplicar. O Gestor de Configuração não valida a informação que introduz.

  - **URL**: Utilize o `https://website.domain.tld`formato URL padrão, . O Windows apresenta o URL como uma hiperligação.

  - **Endereço de e-mail**: `user@domain.tld`Utilize o formato de endereço de e-mail padrão, . O Windows apresenta o endereço `mailto:user@domain.tld?subject=Request exemption from BitLocker protection`como a seguinte hiperligação: .

  - **Número de telefone**: Especifique o número que pretende que os seus utilizadores liguem. O Windows apresenta o número `Please call <your number> for applying exemption`com a seguinte descrição: .

Se desativar ou não configurar esta definição, o Windows não exibe as instruções de pedido de isenção aos utilizadores.

> [!NOTE]
> O BitLocker gere isenções por utilizador, não por computador. Se vários utilizadores iniciarem sessão no mesmo computador, e qualquer utilizador não estiver isento, o BitLocker encripta o computador.

### <a name="url-for-the-security-policy-link"></a>URL para o link de política de segurança

*Configuração sugerida*: **Ativado**

Especifique um URL para exibir aos utilizadores como **a Política** de Segurança da Empresa no Windows. Utilize este link para fornecer aos utilizadores informações sobre os requisitos de encriptação. Mostra quando o BitLocker pede ao utilizador para encriptar uma unidade.

Se ativar esta definição, configure o URL de **ligação**da política de segurança .

Se desativar ou não configurar esta definição, o BitLocker não mostra o link da política de segurança.
