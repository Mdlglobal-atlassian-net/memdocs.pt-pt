---
title: Avaliação de compatibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre a avaliação da compatibilidade para aplicações do Windows e controladores no Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7b2bff4f8365693c86540c9b0578307340f13a49
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268900"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Avaliação da compatibilidade no Desktop Analytics

As avaliações de atualização em soluções anteriores eram genéricas, por exemplo: Necessidade de Atenção ou Correção disponíveis. Não fornece qualquer indicador visual sobre como priorizar apps ou controladores com problemas ou atualizar insights. Desktop Analytics substitui esta funcionalidade por Risco de **Compatibilidade**. O Desktop Analytics mostra a avaliação das aplicações apenas na vista de implementação para um cenário de pré-upgrade. Classifica as aplicações com base em insights que a Microsoft obtém das máquinas incluídas num plano de implementação atual.

Desktop Analytics utiliza as seguintes categorias de avaliação de compatibilidade:

- **Baixo**: O serviço não encontrou sinais para colocar esta aplicação em risco para uma atualização do Windows. É provável que funcione no o-os-alvo como está.

- **Médio**: O Analytics indica que a aplicação pode ter prejudicado a funcionalidade, embora a reparação seja provável.

- **Alta**: A aplicação é quase certa de falhar durante ou após a atualização. Pode precisar de uma reparação.

- **Desconhecido**: A aplicação não foi avaliada. Não existem outras ideias, tais como *Questões Conhecidas* de MS ou *Ready for Windows*.

Na lista de ativos de aplicação ou condutor num plano de implementação, verá este valor para cada ativo na coluna Risco de **Compatibilidade.**

## <a name="app-risk-assessment"></a>Avaliação do risco da aplicação

![Diagrama de fontes de avaliação de risco de aplicação](media/app-risk-assessment-sources.png)

Existem várias fontes que desktop Analytics usa para gerar a classificação de avaliação para aplicações:

- [Microsoft conheceu problemas](#microsoft-known-issues)
- [Pronto para Windows](#ready-for-windows)
- [Insights avançados](#advanced-insights)

Pode encontrar a avaliação de cada fonte na aplicação no Desktop Analytics. Na lista de ativos da aplicação num plano de implementação, selecione uma aplicação individual para abrir as suas propriedades flyout pane. Verá uma recomendação geral e um nível de avaliação. A secção de **fatores** de risco de compatibilidade mostra os pormenores destas avaliações.

> [!TIP]
> Se os detalhes da aplicação não mostrarem a avaliação da compatibilidade, pode ser porque a definição de Detalhes das **Versões** da Aplicação está desligada. Está desligado por padrão, e combina todas as versões de apps com o mesmo nome e editor. O serviço ainda faz avaliações de risco de compatibilidade para cada versão. Ligue os detalhes das **versões da App** para ver a avaliação do risco de compatibilidade para uma versão específica da aplicação. Para mais informações, consulte [os ativos do Plano.](about-deployment-plans.md#plan-assets)

## <a name="microsoft-known-issues"></a>Microsoft conheceu problemas

O Desktop Analytics analisa a base de dados de compatibilidade de aplicações da Microsoft para quaisquer problemas conhecidos. Utiliza esta base de dados para determinar quaisquer blocos de compatibilidade existentes para aplicações publicamente disponíveis da Microsoft ou de outras editoras. Este controlo aplica-se apenas ao osso-alvo para o plano de implementação que selecionar.

Você verá os seguintes problemas sobre as propriedades da aplicação painel como **questões conhecidas em MS**:

### <a name="asset-is-removed-during-upgrade"></a>O ativo é removido durante a atualização

O Windows detetou problemas de compatibilidade com uma aplicação ou controlador. O ativo não vai migrar para a nova versão solista. Não é necessária qualquer ação para que a atualização continue. Instale uma versão compatível da aplicação ou do controlador na nova versão S.

<!-- 3594545 -->
O Windows pode remover parcial ou totalmente estes ativos:

- Remoção completa: A configuração do Windows remove completamente a aplicação ou o controlador do dispositivo durante a atualização.
- Remoção parcial: A configuração do Windows remove parcialmente a aplicação ou o controlador do dispositivo. Tem de desinstalá-lo manualmente depois de atualizar o Windows.

Em ambos os casos, depois de atualizar o Windows, o utilizador não pode utilizar a aplicação ou o hardware associado ao controlador.

Para ver esta recomendação no portal Desktop Analytics:

1. Num plano de implantação, selecione **Preparar piloto**.
1. Selecione o separador **Apps.**
1. Selecione uma aplicação e, em seguida, veja os fatores de risco de compatibilidade e recomendações no painel lateral.

[![Screenshot da recomendação de ativos no portal Desktop Analytics](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Atualização de bloqueio

O Windows detetou problemas de bloqueio e não consegue remover a aplicação durante a atualização. Pode não funcionar na nova versão so. Antes de atualizar, retire a aplicação. Reinstale e teste na nova versão S.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloquear a atualização, mas pode ser reinstalado após a atualização

A aplicação é compatível com a nova versão so, mas não migra. Remova a aplicação antes de atualizar o Windows. Reinstale-o na nova versão S.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloquear a tualização, atualizar aplicação para a versão mais recente

A versão existente da aplicação não é compatível com a nova versão S e não migra. Está disponível uma versão compatível da aplicação. Atualize a aplicação antes de atualizar.

### <a name="disk-encryption-blocking-upgrade"></a>Atualização de bloqueio de encriptação do disco

As funcionalidades de encriptação da aplicação bloqueiam a atualização. Desative a funcionalidade de encriptação antes de atualizar o Windows e ative-a após a atualização.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Não funciona com o novo Sistema operativo, mas não bloqueia a atualização

A aplicação não é compatível com a nova versão S, mas não bloqueia a atualização. Não é necessária qualquer ação para que a atualização continue. Instale uma versão compatível da aplicação na nova versão S.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Não funciona com o novo SISTEMA, e vai bloquear a tualização

A aplicação não é compatível com a nova versão Se e bloqueará a atualização. Retire a aplicação antes de atualizar. Pode estar disponível uma versão compatível da aplicação.

### <a name="evaluate-application-on-new-os"></a>Avaliar a aplicação em novo SO

O Windows vai migrar a aplicação, mas detetou problemas que podem afetar o desempenho da aplicação na nova versão DO. Não é necessária qualquer ação para que a atualização continue. Teste a aplicação na nova versão S.

### <a name="may-block-upgrade-test-application"></a>Pode bloquear a tualização, aplicação de teste

O Windows detetou problemas que podem interferir com a atualização, mas precisam de mais investigação. Teste o comportamento da aplicação durante a atualização. Se bloquear a atualização, retire-a antes de atualizar. Em seguida, reinstale-o e teste na nova versão S.

### <a name="multiple"></a>Vários

Vários problemas afetam a aplicação. Selecione **Consulta** para ver detalhes sobre os problemas detetados pelo Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstalar a aplicação após a atualização

A aplicação é compatível com a nova versão S, mas é necessário reinstalá-la depois de atualizar o Windows. O processo de atualização remove a aplicação. Não é necessária qualquer ação para que a atualização continue. Reinstale a aplicação na nova versão S.

### <a name="safeguards"></a>Salvaguardas

<!-- 5746559 -->

Os dados de compatibilidade do Windows classificam algumas aplicações e controladores com uma *salvaguarda*– o que pode fazer com que a atualização para o Windows 10 falhe ou recue. O Windows também pode fazer o upgrade, mas remove a aplicação ou o controlador. O Desktop Analytics pode agora ajudá-lo a identificar estas salvaguardas com antecedência, para que possa remediar o ativo antes de implementar a atualização.

1. No portal Desktop Analytics, selecione um plano de implementação.

1. Selecione **os ativos** do Plano no menu e mude para o separador **Apps.**

1. Filtre a coluna de nomes para mostrar itens com valores que contenham a palavra `Safeguard` . Selecione o resultado para ver mais informações.

    > [!NOTE]
    > Esta entrada não é uma aplicação real que está instalada nos seus dispositivos. É um espaço reservado para ajudar a identificar aplicações ou condutores no seu ambiente com a etiqueta de compatibilidade de salvaguarda.

1. Na secção de recomendação, selecione o link para *Saber mais*. Este link abre o website do Windows com a lista atual de apps ou controladores com a etiqueta de salvaguarda.

1. Compare a lista publicada atual com a lista de ativos no seu ambiente. Remediar quaisquer aplicações ou controladores potencialmente problemáticos, atualizando para uma versão compatível.

[![Screenshot da app Safeguard em Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Pronto para Windows

O Estado de Adoção baseia-se em informações de dispositivos comerciais que partilham dados com a Microsoft. O estado está integrado com declarações de suporte de fornecedores de software.

O Desktop Analytics fornece o estado de adoção de cada versão de um ativo encontrado em dispositivos comerciais. Este estado não inclui dados de dispositivos de consumo ou dispositivos que não partilhem dados. O estado pode não ser representativo da taxa de adoção em todos os dispositivos do Windows 10.

As categorias possíveis são:

- **Altamente adotados:** Pelo menos 100.000 dispositivos comerciais do Windows 10 instalaram esta aplicação.

- **Adotado**: Pelo menos 10.000 dispositivos comerciais do Windows 10 instalaram esta aplicação.

- **Dados insuficientes**: Demasiados dispositivos comerciais do Windows 10 estão a partilhar informações para esta aplicação para a Microsoft categorizar a sua adoção.

- **Programador**de contactos : Pode haver problemas de compatibilidade com esta versão da aplicação. A Microsoft recomenda contactar o fornecedor de software para saber mais.

- **Desconhecido**: Não há nenhuma informação disponível para esta versão desta aplicação. A informação pode estar disponível para outras versões da aplicação.

### <a name="support-statement"></a>Declaração de apoio

Se o fornecedor de software suportar uma ou mais versões desta aplicação no Windows 10, verá esta declaração no painel de propriedades da aplicação. Na secção fatores de risco de compatibilidade, veja a **declaração de apoio**.

## <a name="advanced-insights"></a>Insights avançados

Desktop Analytics também pode detetar problemas usando os seguintes insights adicionais:

### <a name="adopted-version-available"></a>Versão adotada disponível

Há outra versão desta aplicação que é altamente adotada por outros clientes. Este sinal utiliza dados de adoção do ecossistema Windows. Se existirem bloqueadores de upgrade com a sua versão atual, considere implementar a versão alternativa. Para encontrar versões adotadas de aplicações alternativas, consulte a saúde da aplicação em "Prepare a Produção".

### <a name="driver-dependency"></a>Dependência do condutor

A aplicação depende de um motorista. O Desktop Analytics recomenda a aplicação para testes piloto para descobrir quaisquer regressões. Se tiver algum problema, contacte a editora para solicitar uma versão compatível com o Windows 10.

### <a name="additional-insights"></a>Insights adicionais

<!-- 4021225 -->
Quando atualiza o site do Gestor de Configuração e os clientes para a versão 1906, os clientes também reportam estas informações adicionais, quando o nível de dados de diagnóstico é definido para Enhanced Limited:

> [!Important]  
> Para tirar o máximo partido das novas funcionalidades do Gestor de Configuração, depois de atualizar o site, também atualize os clientes para a versão mais recente. Este cenário não é funcional até que a versão do cliente seja também a mais recente.

#### <a name="16-bit-apps"></a>Aplicativos de 16 bits

Retire todos os componentes de 16 bits das aplicações e substitua-os por equivalentes de 32 bits ou 64 bits. Para mais informações, consulte [o Windows Vista e o Windows Server 2008 Developer Story: Application Compatibilidade Cookbook](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)).

A outra opção é ativar o NT Virtual DOS Machine (NTVDM) para suporte no Windows 10.

#### <a name="requires-admin-privileges"></a>Requer privilégios administrativos

A aplicação exige que o utilizador tenha acesso administrativo ao dispositivo. Utilize um manifesto de aplicação para estas aplicações que requeiram permissões de administrador. Para mais informações, consulte Criar e incorporar um manifesto de [aplicação.](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))

O Desktop Analytics recomenda a aplicação para testes piloto para descobrir quaisquer regressões.

#### <a name="java-dependency"></a>Dependência de Java

Muitas aplicações java dependem de um Java Runtime Environment (JRE) instalado separadamente. Embora as versões JRE mais antigas possam continuar a funcionar no Windows 10, a Oracle apenas suporta as versões JRE mais recentes. A utilização de um JRE não apoiado mais antigo pode ter vulnerabilidades de segurança. Verifique se a sua aplicação está em funcionamento nas versões JRE mais recentes.

#### <a name="not-dpi-aware"></a>Não-DPI consciente

A aplicação pode ter problemas de exibição com resoluções avançadas de ecrã no Windows 10. Utilize um manifesto de aplicação para evitar quaisquer problemas com resoluções de DPI elevadas. Para mais informações, consulte [os manifestos da Aplicação](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

O Desktop Analytics recomenda a aplicação para testes piloto para descobrir quaisquer regressões.

#### <a name="silverlight-framework"></a>Quadro silverlight

A Microsoft recomenda que as aplicações não baseadas no navegador não utilizem silverlight. A data de fim de apoio para Silverlight 5 é outubro de 2021.

A maioria dos navegadores web atuais não suportasilverlight.

| Browser | Suporte |
|---------|---------|
| Google Chrome | Fim do apoio: setembro de 2015 |
| Firefox | Fim do apoio: março de 2017 |
| Microsoft Edge | Sem plugin disponível |

O Desktop Analytics recomenda a aplicação para testes piloto para descobrir quaisquer regressões.

#### <a name="net-framework-1011"></a>.Quadro líquido 1.0/1.1

A versão .NET Framework 1.0 não é suportada no Windows 10. A versão 1.1 não é compatível no Windows 10. Se a aplicação for de um editor de terceiros, contacte o fornecedor para solicitar uma versão compatível com o Windows 10. Caso contrário, reenvolva a aplicação para utilizar uma versão suportada de .NET.

#### <a name="net-framework-2030"></a>.Quadro líquido 2.0/3.0

As estruturas .NET 2.0 e 3.5 são suportadas no Windows 10. Poderá ser necessário ativar a funcionalidade Windows. Para mais informações, consulte [Instalar a .NET Framework 3.5 no Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acesso à UI

As aplicações com acesso uI podem contornar os níveis de controlo da interface do utilizador para impulsionar a entrada para janelas de privilégios mais elevados no ambiente de trabalho. Utilize apenas esta definição para aplicações de tecnologia de assistência à interface do utilizador.

Se não estiver a utilizar funcionalidades de acessibilidade na sua aplicação, coloque a bandeira de acesso UI no manifesto da aplicação para falso. Para mais informações, consulte Criar e incorporar um manifesto de [aplicação.](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))

O Desktop Analytics recomenda a aplicação para testes piloto para descobrir quaisquer regressões.

## <a name="driver-risk-assessment"></a>Avaliação do risco do condutor

O Desktop Analytics também lista e grupos por disponibilidade de quaisquer controladores que não migrarão para a versão S.

Pode encontrar a avaliação no controlador em Desktop Analytics. Na lista de ativos do condutor num plano de implementação, selecione um condutor individual para abrir as suas propriedades. Verá uma recomendação geral e um nível de avaliação. A secção de **fatores** de risco de compatibilidade mostra os pormenores destas avaliações.

| Disponibilidade do condutor | Ação necessária? | O que representa | Orientação |
|---------------------|------------------|---------------|----------|
| Disponível na caixa | Não, só para a consciência | A versão atualmente instalada de uma aplicação ou controlador não migra para a nova versão S. Uma versão compatível é instalada com a nova versão S. | Não é necessária qualquer ação para que a atualização continue. |
| Importação a partir de Atualização do Windows | Sim | A versão atualmente instalada de um controlador não migra para a nova versão S. Uma versão compatível está disponível no Windows Update. | Se o computador receber automaticamente as atualizações do Windows Update, não é necessária qualquer ação. Caso contrário, importe um novo controlador do Windows Update depois de atualizar o Windows. |
| Disponível na caixa e a partir do Windows Update | Sim | A versão atualmente instalada de um controlador não migra para a nova versão S. Apesar de um novo controlador estar instalado durante a atualização, uma versão mais recente está disponível no Windows Update. | Se o computador receber automaticamente as atualizações do Windows Update, não é necessária qualquer ação. Caso contrário, importe um novo controlador do Windows Update depois de atualizar o Windows. |
| Consulte o fornecedor | Sim | O controlador não migra para a nova versão DO e o Desktop Analytics não consegue localizar uma versão compatível. | Para obter uma solução, consulte o fornecedor independente de hardware (IHV) que fabrica o controlador, ou o fabricante de equipamentos originais (OEM) que forneceu o dispositivo. |

## <a name="see-also"></a>Consulte também

O FastTrack Center Benefit para o Windows 10 proporciona acesso à **Aplicação desktop Assure**. Este benefício é um novo serviço projetado para resolver problemas com o Windows 10 e microsoft 365 Apps para compatibilidade empresarial. Para mais informações, consulte [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
