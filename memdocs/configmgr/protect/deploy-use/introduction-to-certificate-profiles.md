---
title: Introdução aos perfis de certificado
titleSuffix: Configuration Manager
description: Saiba como funcionam os perfis de certificado no Gestor de Configuração com serviços de certificados de diretório ativo.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 35269e7c727031a9cd66072985f3d9ec362978cf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722306"
---
# <a name="introduction-to-certificate-profiles-in-configuration-manager"></a>Introdução aos perfis de certificado no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Os perfis de certificado funcionam com os Serviços de Certificado de Diretório Ativo e com a função do Serviço de Inscrição de Dispositivos de Rede (NDES). Crie e implemente certificados de autenticação para dispositivos geridos para que os utilizadores possam aceder facilmente a recursos organizacionais. Por exemplo, pode criar e implementar perfis de certificados para fornecer os certificados necessários para os utilizadores se conectarem a ligações VPN e sem fios.

Os perfis de certificadopodem configurar automaticamente os dispositivos de utilizador para acesso a recursos organizacionais, tais como redes Wi-Fi e servidores VPN. Os utilizadores podem aceder a estes recursos sem instalar manualmente certificados ou utilizar um processo fora de banda. Os perfis de certificado ajudam a garantir recursos porque pode utilizar configurações mais seguras que são suportadas pela sua infraestrutura de chave pública (PKI). Por exemplo, requer a autenticação do servidor para todas as ligações Wi-Fi e VPN porque implementou os certificados necessários nos dispositivos geridos.

Os perfis de certificado fornecem as seguintes funcionalidades de gestão:  

- Inscrição e renovação de certificados de uma autoridade de certificação (CA) para dispositivos que executam diferentes tipos e versões de SO. Estes certificados podem então ser utilizados para ligações Wi-Fi e VPN.  

- Implantação de certificados de AC de raiz fidedigna e certificados de AC intermédios. Estes certificados configuram uma cadeia de confiança em dispositivos para ligações VPN e Wi-Fi quando é necessária a autenticação do servidor.  

- Monitorização e criação de relatórios sobre os certificados instalados.  

**Exemplo 1:** Todos os colaboradores precisam de se ligar a hotspots Wi-Fi em vários locais de escritório. Para facilitar a ligação do utilizador, implemente primeiro os certificados necessários para se ligar ao Wi-Fi. Em seguida, implemente perfis Wi-Fi que referenciam o certificado.  

**Exemplo 2:** Tem um PKI no lugar. Pretende mover-se para um método mais flexível e seguro de implantação de certificados. Os utilizadores precisam de aceder aos recursos organizacionais a partir dos seus dispositivos pessoais sem comprometer a segurança. Configure perfis de certificadocom configurações e protocolos que são suportados para a plataforma específica do dispositivo. Os dispositivos podem então solicitar automaticamente estes certificados a partir de um servidor de inscrição virado para a Internet. Em seguida, configure os perfis VPN para usar estes certificados para que o dispositivo possa aceder a recursos organizacionais.  

## <a name="types"></a>Tipos

Existem três tipos de perfis de certificado:  

- **Certificado CA fidedigno**: Implante um certificado ca de raiz fidedigna ou certificado ca intermédio. Estes certificados formam uma cadeia de confiança quando o dispositivo deve autenticar um servidor.  

- **Protocolo de Inscrição simples de Certificado (SCEP)**: Solicite um certificado para um dispositivo ou utilizador utilizando o protocolo SCEP. Este tipo requer a função do Serviço de Inscrição de Dispositivos de Rede (NDES) num servidor que executa o Windows Server 2012 R2 ou mais tarde.

    Para criar um perfil de certificado de protocolo de inscrição simples **de certificado (SCEP),** crie primeiro um perfil de **certificado DE CA fidedigno.**

- **Troca de informações pessoais (.pfx)**: Solicite um certificado .pfx (também conhecido como PKCS #12) para um dispositivo ou utilizador.<!--1321368--> Existem dois métodos para criar perfis de certificados PFX:

  - [Credenciais](../../mdm/deploy-use/import-pfx-certificate-profiles.md) de importação dos certificados existentes
  - [Definir uma](../../mdm/deploy-use/create-pfx-certificate-profiles.md) autoridade de certificado para processar pedidos

  > [!Note]  
  > O Gestor de Configuração não ativa esta funcionalidade opcional por padrão. Tem de ativar esta função antes de a utilizar. Para mais informações, consulte [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

  Pode utilizar a Microsoft ou confiar como autoridades de certificados para certificados de troca de **informações pessoais (.pfx).**

## <a name="requirements"></a>Requisitos

Para implementar perfis de certificado que utilizem O SCEP, instale o ponto de registo do certificado num servidor do sistema do site. Instale também um módulo de política para o NDES, o Módulo de Política do Gestor de Configuração, num servidor que executa o Windows Server 2012 R2 ou mais tarde. Este servidor requer a função de Serviços de Certificado de Diretório Ativo. Também requer um NDES em funcionamento acessível aos dispositivos que requerem os certificados. Se os seus dispositivos precisarem de se inscrever para certificados a partir da internet, então o seu servidor NDES deve estar acessível a partir da internet. Por exemplo, para ativar com segurança o tráfego para o servidor NDES a partir da internet, pode utilizar o Proxy de [Aplicação Azure](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).

Os certificados PFX também requerem um ponto de registo de certificado. Especifique igualmente a autoridade do certificado (CA) para o certificado e as respetivas credenciais de acesso. Pode especificar a Microsoft ou a Entrust como autoridades de certificados.  

Para obter mais informações sobre como o NDES suporta um módulo de política para que o Gestor de Configuração possa implementar certificados, consulte a Utilização de um Módulo de Política com o Serviço de [Inscrição de Dispositivos](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn473016\(v=ws.11\))de Rede .

Dependendo dos requisitos, o Gestor de Configuração suporta a implementação de certificados para diferentes lojas de certificados em vários tipos de dispositivos e sistemas operativos. São suportados os seguintes dispositivos e sistemas operativos:  

- Windows 10

- Windows 10 Mobile

- Windows 8.1  

- Windows Phone 8.1  

> [!NOTE]  
> Utilize o Gestor de Configuração no local DOM para gerir o Windows Phone 8.1 e Windows 10 Mobile. Para mais informações, consulte o [MDM no local.](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)

Um cenário típico para o Gestor de Configuração é instalar certificados CA de raiz fidedigna para autenticar servidores Wi-Fi e VPN. As ligações típicas utilizam os seguintes protocolos:

- Protocolos de autenticação: EAP-TLS, EAP-TTLS e PEAP
- Protocolos de túneis VPN: IKEv2, L2TP/IPsec e Cisco IPsec

Um certificado CA de raiz empresarial deve ser instalado no dispositivo antes que o dispositivo possa solicitar certificados utilizando um perfil de certificado SCEP.  

Pode especificar definições num perfil de certificado SCEP para solicitar certificados personalizados para diferentes ambientes ou requisitos de conectividade. O Assistente de **Perfil de Certificado criar** tem duas páginas para os parâmetros de inscrição. A primeira, **Inscrição SCEP,** inclui configurações para o pedido de inscrição e onde instalar o certificado. A segunda, **Propriedades do Certificado**, descreve o certificado pedido.  

## <a name="deploy"></a>Implementação

Quando implementa um perfil de certificado SCEP, o cliente do Gestor de Configuração processa a apólice. Em seguida, solicita uma senha de desafio SCEP do ponto de gestão. O dispositivo cria um par de chaves público/privado e gera um pedido de assinatura de certificado (RSE). Envia este pedido para o servidor NDES. O servidor NDES reencaminha o pedido para o sistema de site de ponto de registo de certificados através do módulo de política NDES. O ponto de registo do certificado valida o pedido, verifica a senha de impugnação do SCEP e verifica que o pedido não foi adulterado. Em seguida, aprova ou nega o pedido. Se aprovado, o servidor NDES envia o pedido de assinatura para a autoridade de certificados conectado (CA) para a assinatura. O AC assina o pedido e, em seguida, devolve o certificado ao dispositivo solicitado.

Implementar perfis de certificado para coleções de utilizador ou dispositivo. Pode especificar a loja de destino para cada certificado. As regras de aplicabilidade determinam se o dispositivo pode instalar o certificado.

Quando implementa um perfil de certificado para uma recolha de utilizadores, a [afinidade](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) do dispositivo de utilizador determina qual dos dispositivos dos utilizadores instala os certificados. Quando implementa um perfil de certificado com um certificado de utilizador para uma recolha de dispositivos, por padrão cada um dos principais dispositivos dos utilizadores instala os certificados. Para instalar o certificado em qualquer um dos dispositivos dos utilizadores, altere este comportamento na página de inscrição do **SCEP** do Assistente de Perfil de **Formulário**. Se os dispositivos estiverem num grupo de trabalho, o Gestor de Configuração não implementa certificados de utilizador.  

## <a name="monitor"></a>Monitorizar

Pode monitorizar as implementações de perfis de certificado sondo, visualizando resultados ou relatórios de conformidade. Para mais informações, consulte [Como monitorizar os perfis de certificado](monitor-certificate-profiles.md).

## <a name="automatic-revocation"></a>Revogação automática

O Gestor de Configuração revoga automaticamente os certificados de utilizador e computador que foram implementados utilizando perfis de certificado nas seguintes circunstâncias:  

- O dispositivo é retirado da gestão do Gestor de Configuração.  

- O dispositivo está bloqueado da hierarquia do Gestor de Configuração.  

Para revogar os certificados, o servidor do site envia um comando de revogação à autoridade de certificação emissora. O motivo da revogação é **Cessar a Operação**.

> [!NOTE]
> Para revogar corretamente um certificado, a conta do computador para o site de alto nível da hierarquia precisa da permissão para **emitir e gerir certificados** na AC.
>
> Para uma maior segurança, também pode restringir os gestores de CA na AC. Em seguida, apenas forneça permissões a esta conta no modelo de certificado específico que utiliza para os perfis SCEP no site.

## <a name="next-steps"></a>Passos seguintes

- [Criar perfis de certificado](create-certificate-profiles.md)

- [Configurar a infraestrutura de certificados](certificate-infrastructure.md)
