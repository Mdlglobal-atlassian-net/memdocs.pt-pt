---
title: Integração de MSfB de resolução de problemas
titleSuffix: Configuration Manager
description: Fornece sugestões e resoluções para resolver alguns dos problemas mais comuns com a Microsoft Store para integração de negócios e educação.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149095"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Troubleshoot a Microsoft Store para integração de negócios e educação com Gestor de Configuração

Este artigo fornece dicas e correções fundamentais para alguns dos principais problemas que poderá ter com a integração da Microsoft Store for Business and Education (MSfB) com o Gestor de Configuração.

Para obter mais informações sobre a utilização da Microsoft Store para Negócios e Educação com O Gestor de Configuração, consulte [Gerir aplicações da Microsoft Store para Negócios e Educação com O Gestor](manage-apps-from-the-windows-store-for-business.md)de Configuração .

## <a name="monitor"></a>Monitorizar

### <a name="component-status"></a>Estado do componente

Na consola 'Gestor de Configuração', vá ao espaço de trabalho **de monitorização,** expanda o **Estado do Sistema**e selecione o nó de Estado do **Componente.** Estado do monitor dos seguintes componentes:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Estado de sincronização

Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó microsoft **Store para negócios.** Verifique a coluna **Last Sync Status.**

### <a name="view-synchronized-apps"></a>Ver aplicativos sincronizados

Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a Gestão de **Aplicações,** e selecione o nó de Informações de **Licença para Apps de Loja.**


## <a name="log-files"></a>Ficheiros de registo

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

Este ficheiro de registo está localizado `\Logs` no ponto de ligação de serviço, no diretório de instalação do Gestor de Configuração. Grava informações sobre a comunicação com o serviço de nuvem. Estas informações incluem metadados, ícones, pacotes e recuperação de ficheiros de licença.

Para alterar o nível `LoggingLevel` de `0` registo, altere o valor para a chave de `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` registo. Para mais informações, consulte as opções de [registo de configuração](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

Este ficheiro de registo está localizado `\Logs` no ponto de ligação de serviço, no diretório de instalação do Gestor de Configuração. Se o serviço WSfBSyncWorker não tiver sido iniciado, ou iniciado e parado repetidamente, reveja as entradas neste ficheiro de registo.

> [!NOTE]
> Este ficheiro de registo é partilhado com outras funcionalidades.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

Este ficheiro de registo está localizado no servidor do site para o site de alto nível na hierarquia. Está no `\Logs` diretório de instalação do Diretor de Configuração. Regista informações sobre os seguintes processos:

- Insira as informações de metadados sincronizadas pelo componente BusinessAppProcessWorker na base de dados
- Processar ficheiros em`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

Este ficheiro de registo está localizado no servidor do site para o site de alto nível na hierarquia. Está no `\Logs` diretório de instalação do Diretor de Configuração. Se o serviço BusinessAppProcessWorker não tiver sido iniciado, ou se começar e parar repetidamente, reveja as entradas neste ficheiro de registo.



## <a name="last-sync-failed"></a>Última sincronização falhou

Quando o último estado de sincronização estiver *falhado,* comece por rever os [seguintes ficheiros](#log-files) de registo para identificar o sintoma:

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Em seguida, veja uma das seguintes secções para questões comuns:

- [Erro de autorização](#bkmk_fail-symptom1)
- [A chave secreta é inválida.](#bkmk_fail-symptom2)
- [Erro obtendo ficha de aplicação](#bkmk_fail-symptom3)
- [A localização do conteúdo não existe ou permissões incorretas](#bkmk_fail-symptom4)
- [Erro ocorreu fazendo pedido de http chamando método 'GET'](#bkmk_fail-symptom5)
- [Não pode escrever mais bytes para o tampão](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a>Erro de autorização

#### <a name="cause"></a>Causa

Este problema pode ocorrer se a aplicação configurada Azure Ative Directory (Azure AD) não tiver permissões para gerir a Microsoft Store for Business and Education para este inquilino.

#### <a name="workaround"></a>Solução

1. Inscreva-se como administrador no portal Microsoft Store for Business or Education.
1. Vá a **Definições,** e selecione ferramentas de **gestão.**
1. Se a aplicação não estiver listada, selecione **Adicionar uma ferramenta de gestão**. Em seguida, procure pelo nome e selecione a aplicação Azure AD associada ao mesmo ClientID que O Gestor de Configuração.
1. Se o estado não aparecer **Ativo,** selecione **Ativa** na secção **Ação.**
1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó microsoft **Store para negócios.** Sincronizar com a loja ou esperar que opróximo intervalo de sincronização ocorra.

> [!Tip]
> Para encontrar o ClientID no Gestor de Configuração:
>
> 1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços cloud,** e selecione o nó **de Diretório Ativo Azure Tennts.**
> 1. Selecione o inquilino que utiliza para a Microsoft Store para integração de negócios e educação.
> 1. No painel de resultados, encontre a aplicação correspondente e olhe para a coluna ID do **cliente.**

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>A chave secreta é inválida.

#### <a name="cause"></a>Causa

Este problema pode ocorrer se a chave secreta tiver expirado na aplicação Azure AD para a configuração da Microsoft Store for Business and Education.

#### <a name="resolution"></a>Resolução

Renovar a chave secreta para a aplicação Azure AD. Para mais informações, consulte [Renovar a chave secreta.](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew)

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>Erro obtendo ficha de aplicação

#### <a name="cause"></a>Causa

Este problema pode ocorrer se a aplicação conectada já não existir no Azure AD.

#### <a name="resolution"></a>Resolução

Eliminar e recriar a ligação à Microsoft Store para negócios e educação.

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó microsoft **Store para negócios.**
1. Selecione a ligação existente.
1. **Selecione Eliminar** na fita.

Em seguida, recriar a ligação. Para obter mais informações, veja os artigos seguintes:

- [Serviços Configure Azure](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Configurar a Microsoft Store para sincronização de negócios e educação](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a>A localização do conteúdo não existe ou permissões incorretas

#### <a name="cause"></a>Causa

Quando configura a ligação Microsoft Store for Business and Education, especifica uma quota de rede para armazenar conteúdo sincronizado. Esta questão pode ocorrer se esta parte não existir ou tiver permissões incorretas. A conta do computador para o ponto de ligação de serviço deve ser o proprietário deste diretório e quaisquer subdiretórios.<!-- memdocs#146 --> Se não for, verá um erro semelhante ao seguinte erro:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Para ver a localização que configura:

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó microsoft **Store para negócios.**

1. Selecione a conta e abra as suas **Propriedades**.

1. Mude para o separador **Configuração.** A definição de **Localização** mostra o caminho da rede para armazenar conteúdos de aplicações descarregados da Microsoft Store para Negócios e Educação.

#### <a name="workaround"></a>Solução

1. Se já não existe, crie a parte.

1. Verifique as permissões ntfs na pasta e as permissões na partilha da rede. Conceda a conta de computador do ponto de ligação de serviço **Ler** e **Escrever** permissões.

Se pretender reconfigurar a localização, elimine e recrie a ligação com a nova localização do conteúdo.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>Erro ocorreu fazendo pedido de http chamando método 'GET'

#### <a name="cause"></a>Causa

Este problema pode ocorrer se a sincronização de aplicações da loja demorou tanto tempo que o URL de conteúdo expirou.

#### <a name="workaround"></a>Solução

Voltar a tentar o processo de sincronização

1. Na consola De Configuração Manager, vá ao espaço de trabalho **da Administração,** expanda os **Serviços Cloud**e selecione o nó microsoft **Store para negócios.**
1. Selecione a ligação. Na fita, selecione **Sync da Microsoft Store for Business**.

A cada vez, deve continuar mais. Pode ser preciso várias repetições dependendo dos seguintes fatores:

- O número de aplicações offline
- O tamanho dos pacotes
- A velocidade da rede

A cada tentativa, deve ver o erro menos vezes. Se o número de erros não reduzir, há outro problema.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>Não pode escrever mais bytes para o tampão

#### <a name="cause"></a>Causa

Este problema pode ocorrer se o pacote da aplicação for superior a 500 MB. O Gestor de Configuração apenas suporta a sincronização automática de aplicações offline com pacotes inferiores a 500 MB.

#### <a name="workaround"></a>Solução

Não é possível sincronizar automaticamente estas aplicações, mas pode descarregar o conteúdo e criar manualmente a aplicação:

1. Obtenha o ID de aplicação de falha a partir da seguinte linha em **WSfbSynWorker.log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Inscreva-se como administrador no portal Microsoft Store for Business or Education. Encontre a página para esta aplicação.

    > [!Tip]
    > O URL para a página é semelhante a:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Selecione **Offline**, se ainda não estiver selecionado. Em seguida, selecione **Gerir**.

    1. Crie uma pasta separada na partilha de conteúdo da sua aplicação para todas as plataformas suportadas.

    1. Descarregue o pacote para a pasta do pacote.

    1. Descarregue o ficheiro de `.bin` licença codificado como ficheiro para a pasta do pacote.

    1. Descarregue todos os quadros necessários para a pasta do pacote.

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda a **Gestão**de Aplicações e selecione o nó de **Aplicações.**

1. [Criar uma aplicação,](create-applications.md)especificando manualmente as informações da aplicação.

    1. Crie um tipo de implementação para cada plataforma suportada que tenha descarregado anteriormente.

    1. Tipo: pacote de **aplicativos Windows\*(.appx, \*.appxbundle)**

    1. Especifique o appx/appxbundle para o pacote real de aplicações, e não um pacote de dependência necessário.

Confirme os seguintes dados na página final de **Informações sobre Importações:**

- **Ficheiro de licença:** Especifica o `.bin` ficheiro. Este ficheiro de licença é necessário para aplicações offline.
- **Dependências de aplicativos windows:** Verifique se todas as dependências necessárias são descarregadas para este pacote.


## <a name="sync-doesnt-run"></a>Sincronização não corre

Esta secção aborda os seguintes problemas de sincronização:

- Inicia-se manualmente o processo de sincronização, mas não funciona.
- O site não sincroniza automaticamente todos os dias

Comece por rever os [seguintes ficheiros](#log-files) de registo para identificar o sintoma:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

Em seguida, veja uma das seguintes secções para questões comuns:

- [Sincronização manual não começa](#bkmk_sync-symptom1)
- [Sincronização diária automática não funciona e erro de "desligar # trabalhadores" em SMS_BUSINESS_APP_PROCESS_MANAGER.log](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>Sincronização manual não começa

#### <a name="cause"></a>Causa

Este problema pode ocorrer se iniciar uma sincronização menos de 10 minutos após a sincronização anterior. Não se pode sincronizar com mais frequência do que a cada 10 minutos.

#### <a name="resolution"></a>Resolução

Aguarde pelo menos 10 minutos antes de iniciar outra sincronização.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>Sincronização diária automática não funciona e erro de "desligar # trabalhadores" em SMS_BUSINESS_APP_PROCESS_MANAGER.log

#### <a name="cause"></a>Causa

Este problema pode ocorrer se o componente SMS_BUSINESS_APP_PROCESS_MANAGER parar a linha WsfbSyncWorker. O erro pode `2` `4` especificar ou trabalhadores.

#### <a name="workaround"></a>Solução

Reinicie o serviço **de SMS_EXECUTIVE.**

Se não conseguir reiniciar o serviço principal, pare ambos os componentes com trabalhadores da MSfB e, em seguida, inicie os dois:

1. Abra o registo do Windows no servidor que executa o ponto de ligação ao serviço

1. Ir para `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Definir Operação Solicitada para **parar**.

    1. Atualizar para verificar Estado Atual = **Parado**.

1. Ir para `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Definir Operação Solicitada para **parar**.

    1. Atualizar para verificar Estado Atual = **Parado**.

1. Em **SMS_CLOUDCONNECTION**, definir Operação Solicitada para **Iniciar**.

1. Em **SMS_BUSINESS_APP_PROCESS_MANAGER**, definir Operação Solicitada para **Iniciar**.


## <a name="language-related-issues"></a>Questões relacionadas com a linguagem

Esta secção inclui as seguintes questões comuns:

- [Alterações na seleção de idiomas não são aplicadas](#bkmk_lang-symptom1)
- [Nem todos os idiomas selecionados estão presentes para todas as informações da licença](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>Alterações na seleção de idiomas não são aplicadas

#### <a name="cause"></a>Causa

Este problema pode ocorrer se a seleção de idiomas estiver em cache, e não for apurada após a alteração dos valores da propriedade.

#### <a name="workaround"></a>Solução

Para resolver este problema, reinicie o serviço **de SMS_Executive.**

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>Nem todos os idiomas selecionados estão presentes para todas as informações da licença

#### <a name="cause"></a>Causa

Este problema pode ocorrer se as informações da aplicação Microsoft Store for Business and Education não contiverem dados localizados para o idioma especificado.

#### <a name="workaround"></a>Solução

Adicione manualmente quaisquer idiomas em falta para aplicações criadas.


## <a name="offline-applications"></a>Aplicações offline

Esta secção inclui as seguintes questões comuns:

- [Não criar aplicação offline porque o conteúdo não pode ser verificado](#bkmk_off-symptom1)
- [Falha na instalação de aplicação criada a partir de informações de licença offline](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>Não criar aplicação offline porque o conteúdo não pode ser verificado

#### <a name="cause"></a>Causa

Este problema pode ocorrer se o conteúdo sincronizado para a aplicação offline for corrupto ou modificado.

#### <a name="workaround"></a>Solução

Comece uma nova sincronização. Quando a sincronização estiver concluída, deve verificar e descarregar quaisquer ficheiros de conteúdo incorretos.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>Falha na instalação de aplicação criada a partir de informações de licença offline

#### <a name="cause"></a>Causa

Este problema pode ocorrer se implementar a aplicação a um cliente que executa uma versão do Windows 10 mais cedo do que a versão 1511. As aplicações licenciadas offline da Microsoft Store for Business and Education só são suportadas na versão 1511 do Windows 1511 e posteriormente.

#### <a name="resolution"></a>Resolução

Instale a versão mais recente do Windows 10.


## <a name="next-steps"></a>Passos seguintes

Para encontrar ajuda adicional, consulte encontrar ajuda para utilizar o Gestor de [Configuração](../../core/understand/find-help.md).
