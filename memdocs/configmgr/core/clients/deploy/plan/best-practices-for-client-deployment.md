---
title: Boas práticas de implementação do cliente
titleSuffix: Configuration Manager
description: Obtenha as melhores práticas para a implementação do cliente no Gestor de Configuração.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713339"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Boas práticas para implementação de clientes em Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilizar a instalação de cliente baseada em atualização de software para computadores do Active Directory  
 Este método de implementação do cliente utiliza as tecnologias windows existentes, integra-se com a sua infraestrutura de Diretório Ativo, requer a menor configuração em Configuração Manager, é o mais fácil de configurar para firewalls, e é o mais seguro. Ao utilizar grupos de segurança e filtragem de WMI para a configuração da Política de Grupo, também tem muita flexibilidade para controlar quais os computadores que instalam o cliente do Gestor de Configuração.  

 Para obter mais informações, veja [Como Instalar Clientes do Configuration Manager Utilizando a Instalação Baseada em Atualizações de Software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Expandir o esquema do Active Directory e publicar o site para que possa executar o CCMSetup sem opções da linha de comandos  
 Quando estende o esquema de Diretório Ativo para Gestor de Configuração e o site é publicado para Ative Directory Domain Services, muitas propriedades de instalação de clientes são publicadas para Ative Directory Domain Services. Se um computador conseguir localizar estas propriedades de instalação do cliente, pode usá-las durante a implementação do cliente do Gestor de Configuração. Como estas informações são geradas automaticamente, o risco de erro humano associado à introdução manual das propriedades de instalação é eliminado.  

 Para mais informações, consulte sobre as propriedades de [instalação do cliente publicadas nos Serviços de Domínio de Diretório Ativo.](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Utilize um lançamento faseado para gerir o uso do CPU  
 Minimize o efeito dos requisitos de processamento do CPU no servidor do site utilizando um lançamento faseado dos clientes. Implementar clientes fora do horário comercial para que outros serviços tenham mais largura de banda disponível durante o dia e os utilizadores não sejam interrompidos se o seu computador abrandar ou necessitar de um reinício.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Ativar a atualização automática após a conclusão da implementação principal do cliente  
 [As atualizações automáticas](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) do cliente são úteis quando se pretende atualizar um pequeno número de computadores clientes que podem ter sido perdidos pelo seu método principal de instalação do cliente, talvez porque estavam offline. 

> [!NOTE]  
>  Melhorias de desempenho no Gestor de Configuração podem permitir-lhe utilizar upgrades automáticos como um método primário de atualização do cliente. No entanto, o desempenho dependerá da infraestrutura da hierarquia, como por exemplo o número de clientes.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilizar SMSMP e FSP se instalar o cliente com propriedades client.msi  
 A propriedade SMSMP especifica o ponto de gestão inicial com que o cliente deverá comunicar, removendo a dependência de soluções de localização de serviços tais como os Serviços de Domínio do Active Directory, DNS e WINS.  

 Utilize a propriedade FSP e instale um ponto de estado de contingência para que possa monitorizar a instalação e atribuição de clientes e identificar eventuais problemas de comunicação.  

 Para mais informações sobre estas opções, consulte sobre as propriedades de [instalação do cliente.](../../../../core/clients/deploy/about-client-installation-properties.md)  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Instale pacotes de idiomas do cliente antes de instalar os clientes  
Recomendamos que instale pacotes de idioma do cliente antes de implementar o cliente. Se instalar pacotes de [idiomas](../../../../core/servers/deploy/install/language-packs.md) de cliente (para permitir idiomas adicionais) num site após a instalação de clientes, tem de reinstalar os clientes antes de poderem utilizar esses idiomas. Para os clientes de dispositivos móveis, deve limpar o dispositivo móvel e matriculá-lo novamente.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Preparar previamente os certificados PKI necessários  
 Para gerir dispositivos na Internet, dispositivos móveis inscritos e computadores Mac, terá de possuir certificados PKI nos sistemas de sites (pontos de gestão e pontos de distribuição) e nos dispositivos cliente. Em redes em ambiente de produção, poderá ser necessário solicitar a aprovação da gestão de alterações para utilizar novos certificados, reiniciar os servidores do sistema de sites ou os utilizadores poderão ter de terminar e reiniciar sessão para a nova associação a grupo. Além disso, poderá ter que permitir tempo suficiente para a replicação das permissões de segurança e eventuais novos modelos de certificado.  

 Para obter mais informações sobre os certificados PKI necessários, consulte [os requisitos de certificado PKI para O Gestor](../../../../core/plan-design/network/pki-certificate-requirements.md)de Configuração .  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Antes de instalar os clientes, configure todas as definições de cliente e janelas de manutenção necessárias  
 Embora possa [configurar as definições](../../../../core/clients/deploy/configure-client-settings.md) do cliente e janelas de manutenção antes ou depois de os clientes serem instalados, é melhor configurar as definições necessárias antes de instalar os clientes para que sejam usadas assim que o cliente seja instalado. 

 Configure as janelas de manutenção para servidores e dispositivos Windows Embedded para garantir a continuidade do negócio para dispositivos críticos. As janelas de manutenção garantirão que as atualizações de software necessárias e o software antimalware não reiniciem o computador durante o horário comercial.  

> [!IMPORTANT]  
>  Para os computadores com o Windows 10 que pretende proteger com o Filtro de Escrita Unificado (UWF), deve configurar o dispositivo para UWF antes de instalar o cliente. Isto permite ao Gestor de Configuração instalar o cliente com um fornecedor credencial personalizado que bloqueia os utilizadores de baixos direitos de iniciar sessão no dispositivo durante o modo de manutenção.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planeje a sua experiência de inscrição de utilizadores para computadores Mac e dispositivos móveis   
 Se os utilizadores inscreverem os seus próprios computadores Mac e dispositivos móveis com o Gestor de Configuração, planeie a experiência do utilizador. Por exemplo, pode escrever o processo de instalação e inscrição utilizando uma página web para que os utilizadores introduzam a quantidade mínima de informação necessária e enviem instruções com um link por e-mail.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Utilize filtros de escrita baseados em ficheiros para dispositivos incorporados no Windows 
 É provável que ocorram ressincronizações de mensagens de estado em dispositivos incorporados que utilizem Filtros de Escrita Avançados (EWF). Se tiver apenas alguns dispositivos incorporados que utilizem Filtros de Escrita Avançados, poderá não reparar nesta questão. No entanto, se tiver muitos dispositivos incorporados que ressincronizem as respetivas informações, enviando por exemplo inventários completos em vez de alterações ao inventário, isso poderá gerar um aumento notório dos pacotes de rede e um processamento superior na CPU do servidor do site.  

 Quando tiver uma escolha do tipo de filtro de escrita para ativar, escolha filtros de escrita baseados em ficheiros e configure exceções para persistir no estado do cliente e dados de inventário entre o reinício do dispositivo para a eficiência da rede e cpu no cliente do Gestor de Configuração. Para obter mais informações sobre os filtros de escrita, consulte [Planplanning para implementação de clientes em dispositivos Incorporados](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)windows .  

 Para mais informações sobre o número máximo de clientes Windows Embedded suportado por um site primário, veja [Sistemas operativos suportados por clientes e dispositivos](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
