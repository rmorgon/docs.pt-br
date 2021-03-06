---
title: Rastreamento analítico habilitado dinamicamente
ms.date: 03/30/2017
ms.assetid: 58b63cfc-307a-427d-b69d-9917ff9f44ac
ms.openlocfilehash: 68152741541fdbc048ba290cfb956babaed2e0d7
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33803483"
---
# <a name="dynamically-enabling-analytic-tracing"></a>Rastreamento analítico habilitado dinamicamente
Usando as ferramentas fornecidas com o sistema operacional Windows, você pode habilitar ou desabilitar o rastreamento dinamicamente usando o rastreamento de eventos para Windows (ETW). Para todos os [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] serviços Windows Communication Foundation (WCF), o rastreamento analítico pode ser habilitado e desabilitado dinamicamente sem modificar o arquivo do aplicativo Web. config ou reiniciar o serviço. Isso permite que o aplicativo que emite os eventos de rastreamento para permanecer inalterado.  
  
 Opções de rastreamento do WCF podem ser configuradas de maneira semelhante. Por exemplo, você pode alterar o nível de severidade de **erro** para **informações** sem afetar o aplicativo. Isso pode ser feito usando as seguintes ferramentas:  
  
-   **Logman** – uma ferramenta de linha de comando para configurar, controlar e consultar dados de rastreamento. Para obter mais informações, consulte [Logman criar rastreamento](http://go.microsoft.com/fwlink/?LinkId=165426) e [Logman Update rastreamento](http://go.microsoft.com/fwlink/?LinkId=165427).  
  
-   **Visualizar eventos** -ferramenta de gerenciamento gráfico do Windows para exibir os resultados de rastreamento. Para obter mais informações, consulte [serviços WCF e rastreamento de eventos para Windows](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md) e [Visualizador de eventos](http://go.microsoft.com/fwlink/?LinkId=165428).  
  
-   **PerfMon** – ferramenta de gerenciamento gráfico do Windows que usa contadores de contadores de monitor de rastreamento e os efeitos do rastreamento sobre o desempenho. Para obter mais informações, consulte [criar um dados coletor definir manualmente](http://go.microsoft.com/fwlink/?LinkId=165429).  
  
### <a name="keywords"></a>Palavras-chave  
 Ao usar o <xref:System.ServiceModel.Activation.Configuration.ServiceModelActivationSectionGroup.Diagnostics%2A> classe, as mensagens de rastreamento geralmente são filtradas pelo nível de severidade (por exemplo, erro, aviso e informações) do .NET Framework. ETW oferece suporte ao conceito de nível de severidade, mas apresenta um mecanismo flexível, novo filtro usando palavras-chave. Palavras-chave são valores arbitrários de textuais que permitem que os eventos de rastreamento de fornecer um contexto adicional sobre o que significa que o evento.  
  
 Para rastreamento analítico do WCF, cada evento de rastreamento tem dois tipos de palavras-chave. Primeiro, cada evento tem um ou mais palavras-chave de cenário. Essas palavras-chave indicam os cenários que esse evento é destinado para dar suporte. Há três palavras-chave de cenário, cada criado para uma finalidade específica, conforme mostrado na tabela a seguir. Filtrar usando palavras-chave pode ser alterado dinamicamente sem afetar o serviço WCF. Isso significa que você pode alterar dinamicamente seu cenário de rastreamento atual e a quantidade de você coletar as informações de rastreamento. Por exemplo, você pode alterar `HealthMonitoring` para `Troubleshooting` e aumentar a granularidade de evento de rastreamento.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|`HealthMonitoring`|Muito simples, mínima de rastreamento que lhe permite monitorar a atividade do serviço.|  
|`EndToEndMonitoring`|Eventos usados para oferecer suporte a rastreamento de fluxo de mensagem.|  
|`Troubleshooting`|Eventos mais granulares em torno dos pontos de extensibilidade do WCF.|  
  
 O segundo grupo de palavras-chave definir qual componente do [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] emitido o evento.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|`UserEvents`|Eventos emitidos pelo código do usuário e não o [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)].|  
|`ServiceModel`|Eventos emitidos pelo tempo de execução WCF.|  
|`ServiceHost`|Eventos emitidos pelo host de serviço.|  
|`WCFMessageLogging`|Eventos de log de mensagens do WCF.|  
  
## <a name="see-also"></a>Consulte também  
 [Serviços do WCF e Rastreamento de Eventos para Windows](../../../../../docs/framework/wcf/samples/wcf-services-and-event-tracing-for-windows.md)
