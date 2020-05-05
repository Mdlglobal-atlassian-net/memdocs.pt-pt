---
title: Segurança e privacidade para implementação do SO
titleSuffix: Configuration Manager
description: Conheça as melhores práticas de segurança e privacidade para a implementação de SO no Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724427"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Segurança e privacidade para implementação de OS em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*

Este artigo contém informações de segurança e privacidade para a funcionalidade de implementação do SO no Gestor de Configuração.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a>Boas práticas de segurança para a implantação do OS  

Utilize as seguintes práticas de segurança para quando implementar sistemas operativos com o Gestor de Configuração:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementar controlos de acesso para proteger os suportes de dados de arranque

Ao criar suportes de dados de arranque, atribua sempre uma palavra-passe para ajudar a proteger os suportes de dados. Mesmo com uma palavra-passe, apenas encripta ficheiros que contenham informações confidenciais, e todos os ficheiros podem ser substituídos.  

Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente.  

Para ajudar a impedir que um cliente instale conteúdo ou adultere a política de cliente, o conteúdo é protegido por hash e tem de ser utilizado com a política original. Se o haxixe de conteúdo falhar ou verificar se o conteúdo corresponde à apólice, o cliente não utilizará os meios de arranque. Só o conteúdo é hashed. A apólice não é apressada, mas é encriptada e protegida quando especifica uma palavra-passe. Este comportamento dificulta que um intruso modifique com sucesso a política.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Use um local seguro quando criar meios de comunicação para imagens de SO

Se os utilizadores não autorizados tiverem acesso ao local, podem adulterar os ficheiros que cria. Também podem usar todo o espaço de disco disponível para que a criação dos meios de comunicação falhe.  


### <a name="protect-certificate-files"></a>Proteger ficheiros de certificados 

Proteja os ficheiros de certificado (.pfx) com uma senha forte. Se os armazenar na rede, proteja o canal de rede quando os importar para O Gestor de Configuração

Quando necessita de uma palavra-passe para importar o certificado de autenticação do cliente que utiliza para meios de saque, esta configuração ajuda a proteger o certificado de um intruso.  

Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere o ficheiro de certificado.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloquear ou revogar quaisquer certificados comprometidos 

Se o certificado de cliente estiver comprometido, bloqueie o certificado do Gestor de Configuração. Se for um certificado PKI, revogue-o.  

Para implementar um OS utilizando meios de sabotados e bota PXE, deve ter um certificado de autenticação de cliente com uma chave privada. Se esse certificado for comprometido, bloqueie o certificado no nó **Certificados** da área de trabalho de **Administração**, nó **Segurança**.  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Proteja o canal de comunicação entre o servidor do site e o Fornecedor SMS

Quando o Fornecedor SMS estiver afastado do servidor do site, fixe o canal de comunicação para proteger as imagens de arranque.

Quando modifica as imagens de arranque e o Fornecedor SMS está a funcionar num servidor que não é o servidor do site, as imagens de boot são vulneráveis a ataques. Proteja o canal de rede entre estes computadores utilizando a assinatura SMB ou IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Ativar pontos de distribuição para comunicação de cliente PXE apenas em segmentos de rede seguros

Quando um cliente envia um pedido de arranque PXE, não tem como certificar-se de que o pedido é servido por um ponto de distribuição compatível com PXE. Este cenário apresenta os seguintes riscos de segurança:  

- Um ponto de distribuição não autorizado que responda a pedidos PXE poderia fornecer uma imagem adulterada aos clientes.  

- Um atacante pode lançar um ataque man-in-the-middle contra o protocolo TFTP que é usado pelo PXE. Este ataque pode enviar código malicioso com os ficheiros sO. O intruso também poderia criar um cliente fraudulento para fazer pedidos TFTP diretamente para o ponto de distribuição.  

- Um atacante poderia utilizar um cliente malicioso para lançar um ataque denial-of-service contra o ponto de distribuição.  

Utilize a defesa em profundidade para proteger os segmentos de rede onde os clientes acedem a pontos de distribuição ativados por PXE.  

> [!WARNING]  
>  Devido a estes riscos de segurança, não permita um ponto de distribuição para a comunicação PXE quando está numa rede não confiável, como uma rede de perímetro.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configurar pontos de distribuição PXE ativados para responder a pedidos PXE apenas em interfaces de rede especificadas  

Se permitir que o ponto de distribuição responda a pedidos PXE em todas as interfaces de rede, esta configuração poderá expor o serviço PXE a redes não fidedignas  


### <a name="require-a-password-to-pxe-boot"></a>Exigir uma palavra-passe para efetuar o arranque PXE

Quando necessita de uma palavra-passe para a bota PXE, esta configuração adiciona um nível extra de segurança ao processo de arranque PXE. Esta configuração ajuda a salvaguardar contra clientes fraudulentos que se juntam à hierarquia do Gestor de Configuração.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Restringir o conteúdo em imagens de OS utilizadas para bota PXE ou multicast

Não inclua aplicações de linha de negócio ou software que contenha dados sensíveis numa imagem que utiliza para botas PXE ou multicast.  

Devido aos riscos de segurança inerentes envolvidos com a bota PXE e o multicast, reduza os riscos se um computador fraudulento descarregar a imagem de SO.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Restringir o conteúdo instalado por variáveis de sequência de tarefas

Não inclua aplicações de linha de negócio ou software que contenha dados sensíveis em pacotes de aplicações que instala utilizando variáveis de sequências de tarefas.  

Quando implementa software utilizando variáveis de sequências de tarefas, pode ser instalado em computadores e utilizadores que não estejam autorizados a receber esse software.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Proteja o canal de rede ao migrar estado de utilizador

Quando migrar o estado do utilizador, proteja o canal de rede entre o cliente e o ponto de migração do Estado utilizando a assinatura SMB ou o IPsec.  

Após a ligação inicial através de HTTP, os dados da migração de estado de utilizador são transferidos utilizando SMB. Se não proteger o canal de rede, um intruso pode ler e modificar estes dados.  


### <a name="use-the-latest-version-of-usmt"></a>Use a versão mais recente do USMT

Utilize a versão mais recente da Ferramenta de Migração do Estado utilizador (USMT) que o Gestor de Configuração suporta.  

A versão mais recente do USMT fornece melhoramentos de segurança e um maior controlo ao migrar dados de estado do utilizador.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Elimine manualmente as pastas nos pontos de migração do Estado quando as desativar  

Ao remover uma pasta de ponto de migração estatal na consola do Gestor de Configuração nas propriedades do ponto de migração do estado, o site não elimina a pasta física. Para proteger os dados de migração do estado do utilizador da divulgação de informação, remova manualmente a parte da rede e elimine a pasta.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Não configure a política de eliminação para apagar imediatamente o estado do utilizador  

Se configurar a política de eliminação do ponto de migração do Estado para remover imediatamente os dados marcados para a eliminação, e se um intruso conseguir recuperar os dados do estado do utilizador antes do computador válido, o site elimina imediatamente os dados do estado do utilizador. Defina o **Eliminar depois de ** intervalo de modo a ser suficientemente longo para verificar o sucesso do restauro dos dados de estado de utilizador.  


### <a name="manually-delete-computer-associations"></a>Excluir manualmente associações informáticas 

Elimine manualmente as associações informáticas quando a restauração dos dados de migração do estado do utilizador estiver completa e verificada.

O Gestor de Configuração não remove automaticamente as associações de computadores. Ajudar a proteger a identidade dos dados do Estado do utilizador, apagando manualmente associações informáticas que já não são necessárias.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Fazer manualmente cópias de segurança dos dados de migração de estado de utilizador no ponto de migração de estado  

O Backup do Gestor de Configuração não inclui os dados de migração do estado do utilizador na cópia de segurança do site.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementar controlos de acesso para proteger os suportes de dados pré-configurados  

Controle o acesso físico ao suporte de dados para impedir que um atacante utilize ataques criptográficos para obter o certificado de autenticação de cliente e dados confidenciais.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementar controlos de acesso para proteger o processo de processamento de imagens do computador de referência  

Certifique-se de que o computador de referência que utiliza para capturar imagens de OS está num ambiente seguro. Utilize controlos de acesso adequados para que software inesperado ou malicioso não possa ser instalado e inadvertidamente incluído na imagem capturada. Quando capturar a imagem, certifique-se de que a localização da rede de destino está segura. Este processo ajuda a certificar-se de que a imagem não pode ser adulterada depois de a capturar.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Instalar sempre as atualizações de segurança mais recentes no computador de referência  

Se o computador de referência tiver as atualizações de segurança mais recentes, isso ajudará a reduzir a janela de vulnerabilidade dos novos computadores durante o primeiro arranque.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementar controlos de acesso ao implantar um SISTEMA para um computador desconhecido

Se tiver de implantar um SISTEMA num computador desconhecido, implemente controlos de acesso para evitar que computadores não autorizados se conectem à rede.  

O fornecimento de computadores desconhecidos fornece um método conveniente para implantar novos computadores a pedido. Mas também pode permitir que um intruso se torne eficientemente um cliente de confiança na sua rede. Limite o acesso físico à rede e monitorize os clientes para detetar computadores não autorizados. 

Os computadores que respondem a uma implementação de SO iniciado pelo PXE podem ter todos os dados destruídos durante o processo. Este comportamento pode resultar numa perda de disponibilidade de sistemas que são inadvertidamente reformados.  


### <a name="enable-encryption-for-multicast-packages"></a>Ativar a encriptação de pacotes multicast  

Para cada pacote de implementação de SO, pode ativar a encriptação quando o Gestor de Configuração transfere o pacote utilizando o multicast. Esta configuração ajuda a evitar que os computadores fraudulentos se juntem à sessão multicast. Também ajuda a evitar que os atacantes adulteram a transmissão.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Monitorizar pontos de distribuição multicast ativados não autorizados  

Se os atacantes puderem ter acesso à sua rede, podem configurar servidores multicast fraudulentos para falsificar a implementação do OS.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Ao exportar sequências de tarefas para uma localização de rede, proteja a localização e o canal de rede

Limite quem pode aceder à pasta de rede.  

Utilize a assinatura SMB ou IPsec entre a localização de rede e o servidor de site para impedir que um atacante adultere a sequência de tarefas exportada.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Se utilizar a sequência de tarefas como conta, tome precauções adicionais de segurança

Se utilizar a sequência de [tarefas como conta,](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)tome as seguintes medidas de precaução:  

- Utilize uma conta com o mínimo de permissões necessárias.  

- Não utilize a conta de acesso à rede para esta conta.  

- Nunca torne a conta num administrador do domínio.  

- Nunca configure perfis itinerantes para essa conta. Quando a sequência de tarefas é executado, descarrega o perfil de roaming para a conta, o que deixa o perfil vulnerável ao acesso no computador local.  

- Limite o âmbito da conta. Por exemplo, criar diferentes sequências de tarefas executadas como explicações para cada sequência de tarefas. Se uma conta estiver comprometida, apenas os computadores clientes a que essa conta tem acesso estão comprometidos. Se a linha de comando necessitar de acesso administrativo no computador, considere criar uma conta de administrador local apenas para a sequência de tarefas executada como conta. Crie esta conta local em todos os computadores que executam a sequência de tarefas e elimine a conta assim que já não seja necessária.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Restringir e monitorizar os utilizadores administrativos a quem é concedida a função de segurança do gestor de implementação do SO

Os utilizadores administrativos a quem seja concedida a função de segurança do gestor de **implementação** do SISTEMA podem criar certificados auto-assinados. Estes certificados podem então ser usados para personificar um cliente e obter a política do cliente do Gestor de Configuração.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Utilize o ENHANCED HTTP para reduzir a necessidade de uma conta de acesso à rede

A partir da versão 1806, quando ativa o [Enhanced HTTP,](../../core/plan-design/hierarchy/enhanced-http.md)vários cenários de implementação de OS não requerem uma conta de acesso à rede para descarregar conteúdo a partir de um ponto de distribuição. Para obter mais informações, consulte as [sequências de tarefas e a conta de acesso à rede](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Questões de segurança para a implantação do OS  

Embora a implementação do OS possa ser uma forma conveniente de implementar os sistemas operativos e configurações mais seguros para computadores na sua rede, tem os seguintes riscos de segurança:  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgação de informações e denial-of-service  

Se um intruso conseguir obter o controlo da sua infraestrutura de Gestor de Configuração, pode executar quaisquer sequências de tarefas. Este processo pode incluir a formatação dos discos rígidos de todos os computadores clientes. As sequências de tarefas podem ser configuradas para conter informações confidenciais, tais como contas que tenham permissões para aderir ao domínio e chaves de licenciamento em volume.  


### <a name="impersonation-and-elevation-of-privileges"></a>Representação e elevação de privilégios  

As sequências de tarefas permitem associar um computador ao domínio, o que poderá fornecer acesso autenticado de rede a um computador não autorizado. 

Proteja o certificado de autenticação do cliente que é utilizado para meios de sequência de tarefas de arranque e para a implementação de boot SPXE. Ao capturar um certificado de autenticação de cliente, este processo dá a um intruso a oportunidade de obter a chave privada no certificado. Este certificado permite-lhes fazer-se passar por um cliente válido na rede. Neste cenário, o computador não autorizado pode transferir a política, que pode conter dados confidenciais.  

Se os clientes utilizarem a conta de acesso à rede para aceder aos dados armazenados no ponto de migração do Estado, estes clientes partilham efetivamente a mesma identidade. Poderiam aceder aos dados de migração do Estado de outro cliente que usa a conta de acesso à rede. Os dados são encriptados para poderem ser lidos apenas pelo cliente original, mas podem ser adulterados ou eliminados.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>A autenticação do cliente para o ponto de migração do Estado é conseguida utilizando um token De Configuração que é emitido pelo ponto de gestão.  

O Gestor de Configuração não limita nem gere a quantidade de dados armazenados no ponto de migração do Estado. Um intruso poderia preencher o espaço de disco disponível e causar uma negação de serviço.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Se utilizar variáveis de coleção, os administradores locais podem ler informações potencialmente confidenciais  

Embora as variáveis de recolha ofereçam um método flexível para implementar sistemas operativos, esta funcionalidade pode resultar na divulgação de informação.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a>Informações de privacidade para implementação de OS  

Além de implementar um SO para computadores sem um, o Gestor de Configuração pode ser usado para migrar os ficheiros e configurações dos utilizadores de um computador para outro. O administrador configura as informações para transferência, incluindo ficheiros de dados pessoais, definições de configuração e cookies do browser.  

O Gestor de Configuração armazena a informação num ponto de migração do Estado e encripta-a durante a transmissão e armazenamento. Só o novo computador associado à informação do Estado pode recuperar a informação armazenada. Se o novo computador perder a chave para recuperar a informação, um administrador do Gestor de Configuração com a Informação de Recuperação de **Visualizações** corretamente em objetos de instância de associação de computador pode aceder à informação e associá-la a um novo computador. Depois de o novo computador restaurar as informações do Estado, elimina os dados após um dia, por padrão. Pode configurar o momento de remoção dos dados marcados para eliminação pelo ponto de migração de estado. O Gestor de Configuração não armazena as informações de migração do Estado na base de dados do site, e não a envia para a Microsoft.  

Se utilizar os meios de arranque para implementar imagens de OS, utilize sempre a opção predefinida para proteger a palavra-passe dos meios de arranque. A palavra-passe encripta todas as variáveis armazenadas na sequência de tarefas, mas informações não armazenadas numa variável poderão ficar sujeitas a divulgação.  

A implementação do OS pode utilizar sequências de tarefas para executar muitas tarefas diferentes durante o processo de implementação, o que inclui a instalação de aplicações e atualizações de software. Quando configurar sequências de tarefas, também deve estar ciente das implicações de privacidade da instalação de software.  

O Gestor de Configuração não implementa a implementação do OS por padrão. Requer vários passos de configuração antes de recolher informações do estado do utilizador ou criar sequências de tarefas ou imagens de arranque.  

Antes de configurar a implementação do OS, considere os seus requisitos de privacidade.  



## <a name="see-also"></a>Consulte também

[Dados de diagnóstico e de utilização](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Segurança e privacidade do Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
