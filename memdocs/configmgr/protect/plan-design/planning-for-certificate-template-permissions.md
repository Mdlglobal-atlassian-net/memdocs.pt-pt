---
title: Permissões de modelo de certificado de planeamento
titleSuffix: Configuration Manager
description: Saiba mais sobre o planeamento das permissões que precisa para configurar os modelos de certificado que o Gestor de Configuração utiliza.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 91434b70ca514430ab4cfd6815186bc6d6bc33db
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210133"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Planejamento de permissões de modelo de certificado para perfis de certificado no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


As seguintes informações podem ajudá-lo a planear como configurar permissões para os modelos de certificado que o Gestor de Configuração utiliza quando implementa perfis de certificado.  

## <a name="default-security-permissions-and-considerations"></a>Considerações e permissões de segurança predefinidas  
 As permissões de segurança predefinidas que são necessárias para os modelos de certificado que o Gestor de Configuração utilizará para solicitar certificados para utilizadores e dispositivos são as seguintes:  

- Leitura e Inscrição para a conta usada pelo conjunto aplicacional do Serviço de Inscrição de Dispositivos de Rede  

- Leia para a conta que executa a consola De Configuração Manager  

  Para obter mais informações sobre estas permissões de segurança, consulte [a configuração da infraestrutura de certificados.](../deploy-use/certificate-infrastructure.md)  

  Quando utiliza esta configuração predefinida, os utilizadores e os dispositivos não podem solicitar diretamente certificados dos modelos de certificados e todos os pedidos devem ser iniciados pelo Serviço de Inscrição de Dispositivos de Rede. Esta é uma restrição importante, pois estes modelos de certificados devem ser configurados com a opção **Fornecer no pedido** no Requerente do certificado, o que significa que existe um risco de representação se um utilizador não autorizado ou um dispositivo comprometido solicitar um certificado. Na configuração predefinida, o Serviço de Inscrição de Dispositivos de Rede tem de iniciar este pedido. No entanto, este risco de representação permanece se o serviço que executa o Serviço de Inscrição de Dispositivos de Rede estiver comprometido. Para ajudar a evitar este risco, siga todos os procedimentos recomendados de segurança relativos ao Serviço de Inscrição de Dispositivos de Rede e ao computador que executa este serviço de função.  

  Se as permissões de segurança predefinidas não cumprirem os seus requisitos empresariais, tem outra opção para configurar as permissões de segurança nos modelos de certificados: pode adicionar permissões de Leitura e Inscrição para utilizadores e computadores.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Adicionar permissões de Leitura e Inscrição para utilizadores e computadores  
 Adicionar permissões de Leitura e Inscrição para utilizadores e computadores pode ser apropriado se uma equipa separada gerir a sua equipa de infraestrutura da autoridade de certificação (CA) e essa equipa separada quer que o Gestor de Configuração verifique que os utilizadores têm uma conta de Serviços de Domínio de Diretório Ativo válida antes de lhes enviar um perfil de certificado para solicitar um certificado de utilizador. Para esta configuração, tem de especificar um ou mais grupos de segurança que contenham os utilizadores e conceder a estes grupos permissões de Leitura e Inscrição nos modelos de certificados. Neste cenário, o administrador da AC gere o controlo de segurança.  

 Do mesmo modo, é possível especificar um ou mais grupos de segurança que contenham contas de computador e conceder a estes grupos permissões de Leitura e Inscrição nos modelos de certificados. Se implementar um perfil de certificado de computador num computador que seja membro de domínio, a conta desse computador terá de receber permissões de Leitura e Inscrição. Estas permissões não são necessárias se o computador não for membro do domínio. Por exemplo, se se trata de um computador de grupo de trabalho ou de um dispositivo móvel pessoal.  

 Embora esta configuração utilize um controlo de segurança adicional, não a aconselhamos como procedimento recomendado. A razão é que os utilizadores ou proprietários especificados dos dispositivos podem solicitar certificados independentemente do Gestor de Configuração e valores de fornecimento para o certificado Sujeito que possam ser usados para personificar outro utilizador ou dispositivo.  

 Além disso, se especificar contas que não podem ser autenticadas no momento em que ocorre o pedido de certificado, o pedido de certificado falhará por predefinição. Por exemplo, o pedido de certificado falhará se o servidor que executar o Serviço de Inscrição de Dispositivos de Rede estiver numa floresta do Active Directory que não é fidedigna para a floresta que contém o servidor do sistema de sites do ponto de registro de certificados. Pode configurar o ponto de registo de certificados para continuar se não for possível autenticar uma conta por não existir resposta do controlador de domínio. No entanto, este não é um procedimento recomendado de segurança.  

 De notar que, se o ponto de registo de certificados estiver configurado para verificar permissões de conta e se um controlador de domínio estiver disponível e rejeitar o pedido de autenticação (por exemplo, a conta está bloqueada ou foi eliminada), o pedido de inscrição de certificados falhará.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Para verificar permissões de Leitura e Inscrição para utilizadores e computadores membros de domínio  

1.  No servidor do sistema do site que acolhe o ponto de registo do certificado, crie a seguinte chave de registo DWORD para ter um valor de 0: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Se não for possível autenticar uma conta por não existir resposta do controlador de domínio e pretender ignorar a verificação das permissões:  

    -   No servidor do sistema do site que acolhe o ponto de registo do certificado, crie a seguinte chave de registo DWORD para ter um valor de 1: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessNegado  

3.  Na AC emissora, no separador **Segurança** das propriedades do modelo de certificado, adicione um ou mais grupos de segurança para conceder permissões de Leitura e Inscrição às contas de utilizador ou de dispositivo.  
