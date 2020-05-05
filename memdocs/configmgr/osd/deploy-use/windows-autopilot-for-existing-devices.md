---
title: Windows Autopilot para os dispositivos existentes
titleSuffix: Configuration Manager
description: Utilize uma sequência de tarefas do Gestor de Configuração para reimagem e disponibilize um dispositivo Windows 7 para o modo conduzido pelo utilizador do Windows Autopilot
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724210"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para os dispositivos existentes
<!--3607717, fka 1358333-->

*Aplica-se a: Gestor de Configuração (ramo atual)*

O [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) fornece uma forma de as organizações enviarem dispositivos Windows 10 frescos e intocados diretamente para o utilizador final e definir o fluxo de provisionamento que o utilizador passa para obter um dispositivo seguro e produtivo do Windows 10. O dispositivo está registado no serviço De Piloto Automático do Windows, para que possa atribuir o perfil de Piloto Automático do Windows necessário. Este perfil define a experiência fora da caixa (OOBE) para esse dispositivo. 

[O Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível com o Windows 10, versão 1809 ou posterior. Esta funcionalidade permite-lhe reimagem e fornecer um dispositivo Windows 7 para o [modo de utilização do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma única sequência de tarefas nativa do Gestor de Configuração. 



## <a name="prerequisites"></a>Pré-requisitos

- Adquira os meios de instalação para a versão 1809 do Windows 10, ou mais tarde. Em seguida, crie uma imagem osso do Gestor de Configuração. Para mais informações, consulte [Gerir imagens do OS](../get-started/manage-operating-system-images.md).

- No Microsoft Intune, crie perfis para o Windows Autopilot. Para mais informações, consulte [Os dispositivos Do Windows em Intune utilizando o Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Um dispositivo ainda não registado no serviço De Piloto Automático do Windows. Se o dispositivo já estiver registado, o perfil atribuído tem precedência. O perfil autopiloto para dispositivos existentes só se aplica se o perfil online se esgotar.



## <a name="create-the-configuration-file"></a>Criar o ficheiro de configuração

1. Num dispositivo Windows com conectividade de internet, abra uma janela de comando administrativa PowerShell e execute os seguintes comandos:  

    1. Instale os módulos necessários e aceite instruções para continuar  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Inscreva-se em Intune com credenciais de administrador  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Recupere todos os perfis do Windows Autopilot associados ao seu inquilino Intune  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Crie um ficheiro de configuração para cada perfil. Os ficheiros são nomeados para o nome de exibição do perfil e guardados no ambiente de trabalho do utilizador atual.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > O ficheiro de configuração só pode conter um perfil. Cada perfil deve estar dentro `{}`de suportes encaracolados .  

2. Guarde um dos perfis para um ficheiro codificado ansi chamado **AutopilotConfigurationFile.json**. Guarde-o para um local adequado como fonte de pacote de Gestor de Configuração.  

    > [!Tip]  
    > Se utilizar o PowerShell cmdlet **Out-File** para redirecionar a saída JSON para um ficheiro, utiliza a codificação Unicode por defeito. Este cmdlet também pode truncar longas linhas. Utilize o cmdlet **de definição de conteúdo** com o `-Encoding ASCII` parâmetro para definir a codificação de texto adequada.   
    > 
    > O Windows Notepad utiliza a codificação ANSI por padrão.  

3. Crie um pacote de Gestor de Configuração que contenha este ficheiro. Não requer um programa. Para mais informações, consulte [Criar um pacote](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > O Windows requer que este ficheiro se chame **AutopilotConfigurationFile.json**. Para utilizar mais de um perfil Autopilot, crie pacotes separados do Gestor de Configuração.  



## <a name="create-the-task-sequence"></a>Criar a sequência de tarefas

1. Na consola do Gestor de Configuração, vá ao espaço de trabalho da Biblioteca de **Software,** expanda **os Sistemas Operativos**e selecione o nó de sequências de **tarefas.** Selecione Criar sequência de **tarefas** na fita.  

2. Na **página Criar nova sequência** de tarefas, selecione a opção de implementar o **Windows Autopilot para dispositivos existentes**.  

3. Na página de **informação** da sequência de tarefas, especifique um nome, adicione opcionalmente uma descrição e selecione uma imagem de arranque. Para obter mais informações sobre as versões de imagem de boot suportadas, consulte [suporte para o Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. Na página De instalar o **Windows,** selecione o **pacote imagem**do Windows 10 . Em seguida, configure as seguintes definições:  

    - **Índice de imagem**: Selecione empresa, educação ou profissional, conforme exigido pela sua organização  

    - Ative a opção de **partilha e formato do computador-alvo antes** de instalar o sistema operativo  

    - **Configure a sequência de tarefas para utilização com o Bitlocker**: Se ativar esta opção, a sequência de tarefas inclui os passos necessários para ativar o Bitlocker  

    - **Chave do produto**: Se precisar especificar uma chave do produto para a ativação do Windows, introduza-a aqui  

    - Selecione uma das seguintes opções para configurar a conta de administrador local no Windows 10:  
        - **Gera a palavra-passe do administrador local aleatoriamente e desativa a conta em todas as plataformas de suporte (recomendada)**
        - **Ativar a conta e especificar a palavra-passe do administrador local**

5. Na página **Configure Network,** selecione a opção **de juntar um grupo de trabalho**. Esta sequência de tarefas utiliza a ferramenta de preparação do sistema Windows (sysprep). Se o dispositivo estiver unido a um domínio, a sysprep falha.  

6. Na página **de 'Configuração de Instalação',** adicione todas as propriedades de instalação necessárias para o seu ambiente.  

    > [!Tip]  
    > A sequência de tarefas só necessita desta informação se forem necessários componentes do cliente do Gestor de Configuração durante a sequência de tarefas antes de o sysprep ser executado. Por exemplo, para instalar atualizações ou aplicações de software. Se não estás a fazer estas ações, o cliente não é necessário. É desinstalado antes que a sequência de tarefas seja siforrou.  

7. A página **de atualizações Incluir** seleciona por padrão a opção de **não instalar quaisquer atualizações**de software .  

    > [!Tip]  
    > Utilize o serviço de imagem offline para manter a imagem atualizada com as mais recentes atualizações de qualidade do Windows 10. Para mais informações, consulte [Aplicar atualizações](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)de software para uma imagem de OS .  

8. Na página de instalações , pode selecionar aplicações para instalar durante a sequência de **tarefas.** No entanto, a Microsoft recomenda que espelhe a abordagem da imagem de assinatura com este cenário. Depois das disposições do dispositivo com o Autopilot, aplique todas as aplicações e configurações da cogestão do Microsoft Intune ou do Configuration Manager. Este processo proporciona uma experiência consistente entre os utilizadores que recebem novos dispositivos e aqueles que utilizam o Windows Autopilot para dispositivos existentes.  

8. Na página de Preparação do **Sistema,** selecione o pacote que inclui o ficheiro de configuração do Piloto Automático. Por predefinição, a sequência de tarefas reinicia o computador depois de ser executado no Windows Sysprep. Também pode selecionar a opção de desligar o **computador após a conclusão desta sequência**de tarefas . Esta opção permite-lhe preparar um dispositivo e depois entregá-lo a um utilizador para uma experiência de Piloto Automático consistente.  

9. Conclua o assistente.  

Se editar a sequência de tarefas, é semelhante à sequência de tarefas padrão para aplicar uma imagem de OS existente. Esta sequência de tarefas inclui os seguintes passos adicionais:  

- **Aplicar a configuração do Windows Autopilot**: Este passo aplica o ficheiro de configuração do Piloto Automático a partir da embalagem especificada. Não é um novo tipo de passo, é um passo da Linha de **Comando executar** para copiar o ficheiro.  

- **Prepare o Windows para capturar**: Este passo executa o Windows Sysprep e tem a definição de desligar o computador depois de executar esta **ação**. Para mais informações, consulte [Prepare o Windows para capturar](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

O Windows Autopilot para a sequência de tarefas dos dispositivos existentes resulta num dispositivo que se juntou ao Diretório Ativo Azure (Azure AD). 

> [!NOTE]  
> Com a versão 1903 do Windows 10 e a versão 1909, o Autopilot tem um problema conhecido onde a Sysprep elimina o ficheiro **AutopilotConfigurationFile.json.** Se utilizar este método para implementar a versão 1903 do Windows 10 ou a versão 1909, edite esta sequência de tarefas e efetuaas as seguintes alterações:
>
> 1. Desative o **'Prepare misote' para o** passo de captura.
> 2. Imediatamente após o desativado Preparar o Windows para o passo **de captura,** adicione um novo passo da Linha de **Comando run.** Configure-o para executar a seguinte linha de comando:`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Para mais informações, consulte [o Windows Autopilot - questões conhecidas](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Utilize o movimento da pasta OneDrive for Business [conhecida](https://docs.microsoft.com/onedrive/redirect-known-folders) para se certificar de que os dados do utilizador estão atualizados antes da atualização do Windows 10.



## <a name="next-steps"></a>Passos seguintes

Utilize a cogestão para melhorar as funcionalidades de gestão dos seus dispositivos Windows 10. O segundo caminho para a cogestão é através do fornecimento moderno com o Windows Autopilot. Para obter mais informações, veja os artigos seguintes:

- [O que é a cogestão?](../../comanage/overview.md)
- [Caminhos para a cogestão](../../comanage/quickstart-paths.md)
- [Windows Autopilot com cogestão](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Consulte também

- [Inscreva dispositivos Windows em Intune utilizando o Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)
