---
title: Monitorizar perfis de certificado
titleSuffix: Configuration Manager
description: Saiba como monitorizar o estado de conformidade dos perfis de certificado sinuoso do Gestor de Configuração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722299"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Como monitorizar os perfis de certificado no Gestor de Configuração

*Aplica-se a: Gestor de Configuração (ramo atual)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver Resultados de Conformidade na consola do Gestor de Configuração  

Para monitorizar a conformidade com o certificado SCEP não utilize a consola, em vez disso, utilize [relatórios](#view-compliance-results-by-using-reports). 

1. Na consola 'Gestor de Configuração', escolha**implementações** **de monitorização**>  .  

2. Selecione a implantação de juros do perfil do certificado.  

3. Reveja as informações de conformidade do certificado de resumo na página principal. Para obter informações mais detalhadas, selecione o perfil do certificado e, em seguida, no separador **Home,** no grupo **Deimplantação,** escolha **'Ver Status'** para abrir a página **'Status' de implantação.**  

    A página **Estado da Implementação** contém os seguintes separadores:  

   -   **Compatibilidade**: apresenta a compatibilidade do perfil de certificado com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que são compatíveis com o perfil de certificado. O painel **Detalhes de Ativos** também apresenta os utilizadores que são compatíveis com este perfil. Clique duas vezes num utilizador na lista para obter mais informações.  

       > [!IMPORTANT]  
       >  Um perfil de certificado não é avaliado se não for aplicável num dispositivo cliente. No entanto, é devolvido como compatível.  

   -   **Erro**: apresenta uma lista de todos os erros para a implementação do perfil de certificado selecionado com base no número de ativos que é afetado. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que geraram erros com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Clique duas vezes num utilizador na lista para mostrar mais informações.  

   -   **Não Compatível**: apresenta uma lista de todas as regras não compatíveis no perfil de certificado com base no número de ativos que é afetado. Pode fazer duplo clique numa regra para criar um nó temporário no nó **Utilizadores** da área de trabalho **Ativos e Compatibilidade** . Este nó contém todos os utilizadores que não são compatíveis com este perfil. Quando selecionar um utilizador, o painel **Detalhes do Ativo** apresenta os utilizadores que são afetados pelo problema selecionado. Faça duplo clique num utilizador da lista para visualizar mais informações sobre o problema.  

   -   **Desconhecido**: apresenta uma lista de todos os utilizadores que não comunicaram compatibilidade para a implementação do perfil de certificado selecionado, juntamente com o estado atual do cliente dos dispositivos.  

4. Na página **'Status' de implantação,** reveja informações detalhadas sobre a conformidade do perfil de certificado implantado. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

    O estado de inscrição do certificado é apresentado como um número. Utilize a tabela a seguir para compreender o que cada número significa:  


   | Estado da inscrição |                                                                                                                   Descrição                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         A inscrição foi efetuada com êxito e o certificado foi emitido.                                                                                          |
   |    0x00000002     |                                                                    O pedido foi apresentado e o registo está pendente ou o pedido foi emitido fora da banda.                                                                    |
   |    0x00000004     |                                                                                                          A inscrição tem de ser adiada.                                                                                                           |
   |    0x00000010     |                                                                                                               Ocorreu um erro.                                                                                                                |
   |    0x00000020     |                                                                                                        O estado de inscrição é desconhecido.                                                                                                        |
   |    0x00000040     | As informações de estado foram ignoradas. Isto pode ocorrer se<https://msdn.microsoft.com/windows/ms721572>uma autoridade de certificação "_security_certification_authority_gly" hyperlink não for válida ou não tiver sido selecionada para monitorização. |
   |    0x00000100     |                                                                                                           A inscrição foi negada.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Ver resultados de conformidade usando relatórios

As definições de conformidade no Gestor de Configuração incluem relatórios incorporados que pode utilizar para monitorizar informações sobre perfis de certificados. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deverá utilizar um caráter universal (%) ao utilizar os parâmetros **Filtro do dispositivo** e **Filtro do utilizador** nos relatórios de definições de compatibilidade.  

Para monitorizar a conformidade com o certificado SCEP, utilize estes relatórios de certificados ao abrigo do nó de informação Acesso aos **Recursos da Empresa:**  

-   Histórico de emissão de certificados  
-   Lista de recursos com certificados prestes a expirar  
-   Lista de recursos por estado de emissão de certificados  



 Para obter mais informações sobre como configurar relatórios no Gestor de Configuração, consulte [Introdução a relatórios](../../core/servers/manage/introduction-to-reporting.md).  
