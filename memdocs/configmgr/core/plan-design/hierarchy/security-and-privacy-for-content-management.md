---
title: Segurança e privacidade na gestão de conteúdos
titleSuffix: Configuration Manager
description: Otimizar a segurança e privacidade para a gestão de conteúdos no Gestor de Configuração.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 067922149ef268aeb6cd562816aaa4971e184fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720857"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Segurança e privacidade para gestão de conteúdos em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo contém informações de segurança e privacidade para gestão de conteúdos no Gestor de Configuração. 



##  <a name="security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Melhores práticas de segurança para gestão de conteúdo  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Vantagens e desvantagens de HTTPS ou HTTP para pontos de distribuição intranet
Para pontos de distribuição na intranet, considere as vantagens e desvantagens da utilização de HTTPS e HTTP. Na maioria dos cenários, a utilização de http e contas de acesso a pacotes para autorização fornece mais segurança do que usar HTTPS com encriptação mas sem autorização. No entanto, se o conteúdo incluir dados confidenciais que pretende encriptar durante a transferência, utilize o HTTPS.  

-   **Quando utiliza https para um ponto**de distribuição, o Gestor de Configuração não utiliza contas de acesso ao pacote para autorizar o acesso ao conteúdo, mas o conteúdo é encriptado quando é transferido pela rede.  

-   Quando utiliza o HTTP para um ponto de **distribuição,** pode utilizar contas de acesso ao pacote para autorização, mas o conteúdo não é encriptado quando é transferido para a rede.  

A partir da versão 1806, considere ativar o **ENHANCED HTTP** para o site. Esta funcionalidade permite que os clientes utilizem a autenticação do Diretório Ativo Azure para comunicar em segurança com um ponto de distribuição HTTP. Para mais informações, consulte [O HTTP Melhorado](enhanced-http.md).

#### <a name="protect-the-client-authentication-certificate-file"></a>Proteja o ficheiro de certificado de autenticação do cliente
Se utilizar um certificado de autenticação de cliente PKI em vez de um certificado autoassinado para o ponto de distribuição, proteja o ficheiro de certificado (.pfx) com uma palavra-passe segura. Se armazenar o ficheiro na rede, proteja o canal de rede quando importar o ficheiro para o Gestor de Configuração.

Quando necessita de uma palavra-passe para importar o certificado de autenticação do cliente que o ponto de distribuição utiliza para comunicar com pontos de gestão, esta configuração ajuda a proteger o certificado de um intruso. Utilize a assinatura do Bloco de Mensagens do Servidor (SMB) ou o IPsec entre a localização da rede e o servidor do site para evitar que um intruso adulterar o ficheiro do certificado.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Remova a função do ponto de distribuição do servidor do site
Por predefinição, a configuração do Gestor de Configuração instala um ponto de distribuição no servidor do site. Os clientes não têm de comunicar diretamente com o servidor do site. Para reduzir a superfície de ataque, atribua a função do ponto de distribuição a outros sistemas do site e remova-a do servidor do site.  

#### <a name="secure-content-at-the-package-access-level"></a>Conteúdo seguro ao nível do acesso ao pacote
A partilha de pontos de distribuição permite ler o acesso a todos os utilizadores. Para restringir os utilizadores que podem aceder ao conteúdo, utilize contas de acesso aos pacotes quando o ponto de distribuição estiver configurado para HTTP. Esta configuração não se aplica a pontos de distribuição na nuvem, que não suportam contas de acesso a pacotes. Para mais informações, consulte contas de [acesso ao Pacote](accounts.md#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configure o IIS na função do ponto de distribuição
Se o Gestor de Configuração instalar o IIS quando adicionar uma função de sistema de site de pontode distribuição, remova a redirecção de HTTP ou os Scripts e Ferramentas de Gestão IIS quando a instalação do ponto de distribuição estiver concluída. O ponto de distribuição não requer reorientação http ou Scripts e Ferramentas de Gestão IIS. Para reduzir a superfície de ataque, remova estes serviços de função para a função do servidor web.  Para obter mais informações sobre os serviços de função para a função de servidor web para pontos de distribuição, consulte os [pré-requisitos](../configs/site-and-site-system-prerequisites.md)do sistema do Site e do site .  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Detete permissões de acesso ao pacote quando criar o pacote
Uma vez que as alterações nas contas de acesso dos ficheiros do pacote só se tornam eficazes quando redistribui o pacote, detetete cuidadosamente as permissões de acesso ao pacote quando criar o pacote pela primeira vez. Esta configuração é importante quando o pacote é grande ou distribuído em muitos pontos de distribuição, e quando a capacidade de largura de banda da rede para distribuição de conteúdo é limitada.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implementar controlos de acesso para proteger os meios que contenham conteúdo pré-encenado
O conteúdo pré-encenado é comprimido, mas não encriptado. Um intruso poderia ler e modificar os ficheiros que são descarregados para dispositivos. Os clientes do Gestor de Configuração rejeitam conteúdos que são adulterados, mas ainda assim descarregam-no.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importar conteúdo pré-encenado com ExtractContent
Apenas importe conteúdo pré-encenado utilizando a ferramenta de linha de comando ExtractContent.exe. Para evitar adulteração e elevação de privilégios, utilize apenas a ferramenta de linha de comando autorizada que vem com o Gestor de Configuração.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Proteja o canal de comunicação entre o servidor do site e a localização da fonte do pacote
Utilize a assinatura IPsec ou SMB entre o servidor do site e a localização da fonte do pacote quando criar aplicações e pacotes. Esta configuração ajuda a evitar que um intruso adulterar os ficheiros de origem.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Remova os diretórios virtuais padrão para website personalizado com a função de ponto de distribuição
Se alterar a opção de configuração do site para utilizar um website personalizado em vez do website predefinido após a instalação de uma função de ponto de distribuição, remova os diretórios virtuais predefinidos. Quando muda do website padrão para um website personalizado, o Gestor de Configuração não remove os antigos diretórios virtuais. Remova os seguintes diretórios virtuais que o Gestor de Configuração originalmente criou no website predefinido:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Para pontos de distribuição na nuvem, proteja os detalhes e certificados de subscrição do Azure
Quando utilizar pontos de distribuição em nuvem, proteja os seguintes itens de alto valor:
- O nome do utilizador e a palavra-passe para a sua subscrição Azure
- O certificado de gestão Azure 
- O certificado de serviço de ponto de distribuição em nuvem

Guarde os certificados de forma segura. Se os procurar sobre a rede quando configurar o ponto de distribuição da nuvem, utilize a assinatura IPsec ou SMB entre o servidor do sistema do site e a localização de origem.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Para a continuidade do serviço, monitorize a data de validade dos certificados de ponto de distribuição em nuvem
O Gestor de Configuração não o avisa quando os certificados importados para o ponto de distribuição da nuvem estão prestes a expirar. Monitorize as datas de validade independentemente do Gestor de Configuração. Certifique-se de que renova e, em seguida, importa os novos certificados antes da data de validade. Esta ação é importante se adquirir um certificado de autenticação de servidor a um fornecedor público externo, porque poderá necessitar de mais tempo para adquirir um certificado renovado.  

 Se um dos certificados expirar, o Cloud Services Manager gera a mensagem de estado ID **9425**. O ficheiro CloudMgr.log contém uma entrada que indica que o certificado **está em estado expirado,** com a data de validade também registada na UTC.  



## <a name="security-considerations-for-content-management"></a>Considerações de segurança para gestão de conteúdo  

Considere os seguintes pontos no planeamento da gestão de conteúdos:  

-   Os clientes só validam o conteúdo depois de descarregados.  

     Os clientes do Gestor de Configuração validam o hash no conteúdo apenas depois de descarregadopara o seu cache de cliente. Se um intruso adulterar a lista de ficheiros para descarregar ou com o próprio conteúdo, o processo de descarregamento pode ocupar uma largura de banda considerável da rede, apenas para que o cliente elimine o conteúdo quando encontrar o hash inválido.  

-   Quando utiliza pontos de distribuição em nuvem, o acesso ao conteúdo é automaticamente restrito à sua empresa. Não é possível restringi-lo ainda mais a utilizadores ou grupos selecionados.  

-   Quando utiliza pontos de distribuição em nuvem, os clientes são autenticados pelo ponto de gestão e depois usam um token de Configuração Manager para aceder a pontos de distribuição em nuvem. O símbolo é válido por oito horas. Este comportamento significa que se bloquear um cliente porque já não é de confiança, pode continuar a descarregar conteúdo de um ponto de distribuição na nuvem até que o período de validade deste token tenha expirado. Neste momento, o ponto de gestão não emitirá outro símbolo para o cliente porque o cliente está bloqueado.  

     Para evitar que um cliente bloqueado descarregue conteúdo dentro desta janela de oito horas, pare o serviço de nuvem. Na consola de Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda **os Serviços cloud**e selecione o nó de Pontos de Distribuição de **Nuvem.**  



##  <a name="privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informações de privacidade da gestão de conteúdo  

 O Gestor de Configuração não inclui quaisquer dados do utilizador nos ficheiros de conteúdo, embora um utilizador administrativo possa optar por fazer esta ação.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](fundamental-concepts-for-content-management.md)  

- [Segurança e privacidade para gestão de aplicações](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

- [Segurança e privacidade para atualizações de software](../../../sum/plan-design/security-and-privacy-for-software-updates.md)  

- [Segurança e privacidade para implementação do SO](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  
