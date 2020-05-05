---
title: Perfis de certificado SCEP
titleSuffix: Configuration Manager
description: Saiba como usar perfis de certificado para fornecer dispositivos geridos com os certificados de que necessitam
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 159afbf2c5aae9516fc5244ee06a2aa484290c20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721760"
---
# <a name="create-certificate-profiles"></a>Criar perfis de certificado

*Aplica-se a: Gestor de Configuração (ramo atual)*

Utilize perfis de certificado sinuoso no Gestor de Configuração para fornecer dispositivos geridos com os certificados de que necessitam para aceder aos recursos da empresa. Antes de criar perfis de certificados, crie a infraestrutura de certificados conforme descrito na [infraestrutura de certificados de configuração](certificate-infrastructure.md).  

> [!TIP]
> Para dispositivos cogeridos, considere mover a carga de trabalho das políticas de acesso ao [ **Recurso** ](../../comanage/workloads.md#resource-access-policies) para Intune. Em seguida, utilize políticas intune para gerir estes certificados. Para mais informações, consulte [Como mudar as cargas de trabalho](../../comanage/how-to-switch-workloads.md).

Este artigo descreve como criar perfis de certificados de certificado de raiz e certificado simples (SCEP). Se quiser criar perfis de certificado PFX, consulte Criar perfis de [certificado PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

Para criar um perfil de certificado:

1. Inicie o Assistente de Perfil de Certificado.
1. Forneça informações gerais sobre o certificado.
1. Configure um certificado de autoridade de certificado seletiva (CA).  
1. Configure as informações do certificado SCEP.  
1. Especifique as plataformas suportadas para o perfil do certificado.

## <a name="start-the-wizard"></a>Inicie o assistente  

Para iniciar o Perfil de Criar Certificado:

1. Na consola de Configuração Manager, vá ao espaço de trabalho **de Ativos e Compliance,** expanda **as Definições**de Conformidade, expanda o Acesso aos **Recursos da Empresa**e, em seguida, selecione o nó de Perfis de **Certificado.**  

1. No separador **Home** da fita, no grupo **Criar,** selecione **Criar Perfil**de Certificado .  

## <a name="general"></a>Geral

Na página **Geral** do Assistente Criar Perfil de Certificado , especifique as seguintes informações:  

- **Nome**: introduza um nome exclusivo para o perfil do certificado. Pode utilizar até 256 carateres.  

- **Descrição**: Fornecer uma descrição que dê uma visão geral do perfil do certificado. Inclua também outras informações relevantes que ajudam a identificá-la na consola Do Gestor de Configuração. Pode utilizar até 256 carateres.  

- Especifique o tipo de perfil de certificado que pretende criar:

  - **Certificado CA fidedigno**: Selecione este tipo para implementar uma autoridade de certificação de raiz fidedigna (CA) ou um certificado ca intermédio para formar uma cadeia de confiança de certificado quando o utilizador ou dispositivo deve autenticar outro dispositivo. Por exemplo, o dispositivo poderá ser um servidor RADIUS (Remote Authentication Dial-In User Service) ou um servidor de rede privada virtual (VPN).
  
    Configure também um perfil de certificado CA confiável antes de criar um perfil de certificado SCEP. Neste caso, o certificado DE CA fidedigno deve ser para a AC que emite o certificado ao utilizador ou dispositivo.  

  - Definições simples do Protocolo de Inscrição de **Certificados (SCEP):** Selecione este tipo para solicitar um certificado para um utilizador ou dispositivo com o Protocolo de Inscrição de Certificado Simples e o Serviço de Inscrição de Dispositivos de Rede (NDES).

  - Definições de Intercâmbio de **Informações Pessoais PKCS #12 (PFX) - Import**: Selecione esta opção para importar um certificado PFX. Para mais informações, consulte os perfis de [certificados Import PFX](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - Definições de Troca de **Informações Pessoais PKCS #12 (PFX) - Criar**: Selecione esta opção para processar certificados PFX utilizando uma autoridade de certificados. Para mais informações, consulte Criar perfis de [certificadoS PFX](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Certificado DE CA fidedigno  

> [!IMPORTANT]  
> Antes de criar um perfil de certificado SCEP, configure pelo menos um perfil de certificado CA fidedigno.
>
> Após a implementação do certificado, se alterar algum destes valores, é solicitado um novo certificado:
>
> - Provedor de Armazenamento chave
> - Nome do modelo de certificado
> - Tipo de certificado
> - Formato do nome do requerente
> - Nome alternativo do sujeito
> - Período de validade do certificado
> - Utilização chave
> - Tamanho da chave
> - Utilização alargada da chave
> - Certificado Root CA

1. Na página **Certificado de AC fidedigna** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

    - **Ficheiro**de certificado : Selecione **Import,** e depois navegue para o ficheiro do certificado.  

    - **Armazenamento de destino**: para dispositivos que tenham mais do que um armazenamento de certificados, selecione onde pretende armazenar o certificado. Para dispositivos que têm apenas um armazenamento, esta definição é ignorada.  

2. Use o valor de **impressão digital** do Certificado para verificar se importou o certificado correto.  

## <a name="scep-certificates"></a>Certificados SCEP

### <a name="1-scep-servers"></a>1. Servidores SCEP

Na página **Servidores do SCEP** do Assistente para Criar Perfil de Certificado, especifique os URLs para os Servidores NDES que irão emitir certificados através do SCEP. Pode atribuir automaticamente um URL NDES com base na configuração do ponto de registo do certificado ou adicionar URLs manualmente.  

### <a name="2-scep-enrollment"></a>2. Inscrição scep

Complete a página de inscrição do **SCEP** do Assistente de Perfil de Certificado.

- **Tentativas**: Especifique o número de vezes que o dispositivo retenta automaticamente o pedido de certificado ao servidor NDES. Esta definição suporta o cenário em que um gestor de CA deve aprovar um pedido de certificado antes de ser aceite. Esta definição é normalmente utilizada para ambientes de alta segurança ou se tiver uma AC emissora autónoma, em vez de uma AC empresarial. Também poderá utilizar esta definição para fins de teste, para poder inspecionar as opções de pedido de certificado antes de a AC emissora processar o pedido de certificado. Utilize esta definição com a definição **Intervalo entre repetições (minutos)** .  

- **Atraso da tentativa (minutos)**: especifique o intervalo, em minutos, entre cada tentativa de inscrição quando utilizar a aprovação do gestor de AC antes de a AC emissora processar o pedido de certificado. Se utilizar a aprovação do gestor para efeitos de teste, especifique um valor baixo. Então não está à espera muito tempo que o dispositivo retente o pedido de certificado depois de aprovar o pedido.

    Se utilizar a aprovação do gestor numa rede de produção, especifique um valor mais elevado. Este comportamento permite tempo suficiente para o administrador da AC aprovar ou negar aprovações pendentes.  

- **Limiar da renovação (%)**: especifique a percentagem da duração do certificado que permanece antes de o dispositivo pedir renovação do certificado.  

- **Fornecedor de Armazenamento chave (KSP)**: Especifique onde a chave do certificado está armazenada. Escolha um dos seguintes valores:  

  - **Instalar no Trusted Platform Module (TPM) caso esteja presente**: instala a chave no TPM. Se o TPM não estiver presente, a chave está instalada no fornecedor de armazenamento para a chave do software.  

  - **Instalar no Trusted Platform Module (TPM) ou não instalar**: instala a chave no TMP. Se o módulo TPM não estiver presente, a instalação falha.  

  - **Instalar no Windows Hello for Business falha de outra forma**falha : Esta opção está disponível para dispositivos Windows 10. Permite-lhe armazenar o certificado na loja Windows Hello for Business, que está protegida por autenticação de vários fatores. Para mais informações, consulte [o Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Esta opção não suporta o logon do cartão Smart para a utilização da chave Melhorada na página Propriedades do Certificado.

  - **Instalar no Fornecedor de Armazenamento de Chaves**: instala a chave no fornecedor de armazenamento da chave de software.  

- **Dispositivos para inscrição**de certificados : Se implementar o perfil do certificado para uma recolha de utilizador, permita a inscrição do certificado apenas no dispositivo principal do utilizador ou em qualquer dispositivo para o qual o utilizador faça a inscrição.

    Se implementar o perfil do certificado numa recolha de dispositivos, permita a inscrição do certificado apenas para o utilizador principal do dispositivo, ou para todos os utilizadores que iniciarem o contrato com o dispositivo.  

### <a name="3-certificate-properties"></a>3. Propriedades de Certificado

Na página **Propriedades do Certificado** do Assistente para Criar Perfil de Certificado, especifique as seguintes informações:  

- **Nome**do modelo do certificado : Selecione o nome de um modelo de certificado que configuraem no NDES e adicionadoa a um CA emissor. Para navegar com sucesso em modelos de certificado, a sua conta de utilizador precisa **de ler** permissão para o modelo de certificado. Se não puder **procurar** o certificado, escreva o seu nome.  

  > [!IMPORTANT]
  > Se o nome do modelo de certificado contiver caracteres não ASCII, o certificado não está implantado. (Um exemplo destes caracteres é do alfabeto chinês.) Para se certificar de que o certificado é implantado, crie primeiro uma cópia do modelo de certificado na AC. Em seguida, mude o nome da cópia utilizando caracteres ASCII.  

  - Se *você navegar* para selecionar o nome do modelo de certificado, alguns campos na página povoam automaticamente a partir do modelo de certificado. Em alguns casos, não pode alterar estes valores a menos que escolha um modelo de certificado diferente.  

  - Se *escrever* o nome do modelo de certificado, certifique-se de que o nome corresponde exatamente a um dos modelos de certificado. Deve coincidir com os nomes listados no registo do servidor NDES. Certifique-se de que especifica o nome do modelo de certificado e não o nome de exibição do modelo de certificado.  

    Para encontrar os nomes dos modelos de certificado, `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP`navegue na seguinte chave de registo: . Ele lista os modelos de certificado como os valores para Modelo de **Encriptação,** **Modelo geral de propósito**, e modelo de **assinatura**. Por predefinição, o valor dos três modelos de certificado é **IPSECIntermediateOffline**, que é mapeado para o nome a apresentar de modelo **IPSec (Pedido offline)**.  

    > [!WARNING]  
    > Quando digita o nome do modelo de certificado, o Gestor de Configuração não pode verificar o conteúdo do modelo de certificado. Poderá selecionar opções que o modelo de certificado não suporta, o que pode resultar num pedido de certificado falhado. Quando este comportamento ocorrer, verá uma mensagem de erro para w3wp.exe no ficheiro CPR.log que o nome do modelo no pedido de assinatura de certificado (CSR) e o desafio não correspondem.  
    >
    > Quando digitar o nome do modelo de certificado especificado para o valor do Modelo Geral de **Propósito,** selecione o **precipherment chave** e as opções de **assinatura Digital** para este perfil de certificado. Se pretender ativar apenas a opção **de codificação chave** neste perfil de certificado, especifique o nome do modelo de certificado para a chave **EncryptionTemplate.** Da mesma forma, se pretender ativar apenas a opção **Assinatura digital** neste perfil de certificado, especifique o nome do modelo de certificado da chave **SignatureTemplate** .  

- **Tipo**de certificado : Selecione se irá implementar o certificado num dispositivo ou num utilizador.  

- **Formato de nome**de assunto : Selecione como o Gestor de Configuração cria automaticamente o nome do assunto no pedido de certificado. Se o certificado se destinar a um utilizador, pode também incluir o endereço de e-mail do utilizador no nome do requerente.

    > [!NOTE]  
    > Se selecionar o **número IMEI** ou **o número de série,** pode diferenciar entre diferentes dispositivos que são propriedade do mesmo utilizador. Por exemplo, estes dispositivos podem partilhar um nome comum, mas não um número IMEI ou número de série. Se o dispositivo não reportar um IMEI ou um número de série, o certificado é emitido com o nome comum.

- **Nome alternativo :** Especifique como o Gestor de Configuração cria automaticamente os valores para o nome alternativo do sujeito (SAN) no pedido de certificado. Por exemplo, se tiver selecionado um tipo de certificado de utilizador, pode incluir o nome principal de utilizador (UPN) no nome alternativo do requerente. Se o certificado de cliente autenticar para um Servidor de Política de Rede, detete o nome alternativo ao assunto para a UPN.  

- **Período de validade**do certificado : Se definir um período de validade personalizado na CA emissora, especifique o valor do tempo restante antes do termo do certificado.

    > [!TIP]
    > Definir um período de validade personalizado com a seguinte linha de comando:`certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Para mais informações sobre este comando, consulte infraestrutura de [certificados.](certificate-infrastructure.md)  

    Pode especificar um valor inferior ao período de validade no modelo de certificado especificado, mas não superior. Por exemplo, se o período de validade do certificado no modelo de certificado for de dois anos, pode especificar um valor de um ano, mas não um valor de cinco anos. O valor deve também ser inferior ao período de validade restante do certificado da AC emissora.  

- **Utilização de chave**: especifique as opções de utilização de chave para este certificado. Pode escolher uma das seguintes opções:  

  - **Cifragem de chaves**: permitir a troca de chaves apenas quando a chave for encriptada.  

  - **Assinatura digital**: permitir a troca de chaves apenas quando uma assinatura digital ajudar a proteger a chave.  

  Se procurou um modelo de certificado, não pode alterar estas definições, a menos que selecione um modelo de certificado diferente.  

  Configure o modelo de certificado selecionado com uma ou ambas as opções de utilização acima. Caso contrário, verá a seguinte mensagem no ficheiro de registo do ponto de registo do certificado, **Crp.log**: **Utilização chave em CSR e desafio não corresponde**  

- **Tamanho da chave (bits)**: selecione o tamanho da chave em bits.  

- **Utilização alargada da chave**: Adicione valores para o fim a que se destina o certificado. Na maioria dos casos, o certificado exige a **Autenticação de Cliente** para o utilizador ou dispositivo poder ser autenticado num servidor. Pode adicionar quaisquer outros usos chave, conforme necessário.  

- **Algoritmo hash**: selecione um dos tipos de algoritmo hash disponíveis para utilizar com este certificado. Selecione o maior nível de segurança que os dispositivos de ligação suportam.  

  > [!NOTE]  
  > O**SHA-2** suporta SHA-256, SHA-384 e SHA-512. O**SHA-3** suporta apenas SHA-3.  

- **Certificado Root CA**: Escolha um perfil de certificado CA raiz que configurau e implementou previamente para o utilizador ou dispositivo. Este certificado CA deve ser o certificado raiz para a AC que emitirá o certificado que está configurando neste perfil de certificado.  

  > [!IMPORTANT]  
  > Se especificar um certificado CA raiz que não seja implantado no utilizador ou dispositivo, o Gestor de Configuração não iniciará o pedido de certificado que está a configurar neste perfil de certificado.  

## <a name="supported-platforms"></a>Plataformas suportadas  

Na página plataformas **suportadas** do Assistente de Perfil de Certificado, selecione as versões OS onde pretende instalar o perfil do certificado. Escolha **Selecione todos** para instalar o perfil do certificado em todos os sistemas operativos disponíveis.

## <a name="next-steps"></a>Passos seguintes

O novo perfil de certificado aparece no nó de **Perfis de Certificado** no espaço de trabalho De Ativos e **Conformidade.** Está pronto para ser implantado para utilizadores ou dispositivos. Para mais informações, consulte [Como implementar perfis](deploy-wifi-vpn-email-cert-profiles.md).
