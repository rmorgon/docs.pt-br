---
title: Classes base para implementar abstrações
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- abstractions [.NET Framework]
- base classes, abstractions
ms.assetid: 37a2d9a4-9721-482a-a40f-eee2c1d97875
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8c247ed7273687dbd61a6f19923b71e07e9ed960
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33571502"
---
# <a name="base-classes-for-implementing-abstractions"></a>Classes base para implementar abstrações
Estritamente falando, uma classe torna-se uma classe base quando outra classe é derivada. Para fins desta seção, no entanto, uma classe base é uma classe projetada principalmente para fornecer uma abstração comum ou para outras classes de reutilizar alguns implementação padrão embora herança. Classes base geralmente ficam no meio de hierarquias de herança entre uma abstração na raiz de uma hierarquia e várias implementações personalizadas na parte inferior.  
  
 Eles servem como auxiliares de implementação para implementar abstrações. Por exemplo, uma das abstrações do Framework para conjuntos ordenados de itens é o <xref:System.Collections.Generic.IList%601> interface. Implementando <xref:System.Collections.Generic.IList%601> não é trivial, e, portanto, o Framework fornece várias classes base, como <xref:System.Collections.ObjectModel.Collection%601> e <xref:System.Collections.ObjectModel.KeyedCollection%602>, que servirá como auxiliares para coleções personalizadas de implementação.  
  
 Classes base geralmente não são adequados para servir como abstrações por si só, porque eles tendem a contêm muita implementação. Por exemplo, o `Collection<T>` classe base contém muitas relacionado ao fato de que ele implementa não genérica de implementação `IList` interface (para integrar melhor coleções não genéricas) e ao fato de que é uma coleção de itens armazenados em memória em um de seus campos.  
  
 Como discutido anteriormente, as classes base podem fornecer ajuda inestimável para usuários que precisam implementar abstrações, mas ao mesmo tempo podem ser um risco significativo. Eles Adicionar área da superfície e aumentam a profundidade das hierarquias de herança e portanto conceitualmente complicam a estrutura. Portanto, as classes base devem ser usados somente se eles fornecem valor significativo para os usuários do framework. Eles devem ser evitados se eles fornecem valor apenas para os implementadores do framework, no qual caso delegação para uma implementação interna em vez de herança de uma classe base deve ser considerada altamente.  
  
 **✓ CONSIDER** abstrato as classes base tornando mesmo se eles não contêm membros abstratos. Isso claramente se comunica com os usuários que a classe destina-se exclusivamente a ser herdada.  
  
 **✓ CONSIDER** colocando classes base em um namespace separado dos tipos de cenário principal. Por definição, as classes base destinam-se para cenários de extensibilidade avançada e, portanto, não são interessantes para a maioria dos usuários.  
  
 **X AVOID** nomeando classes base com um sufixo "Base" se a classe é destinada para uso em APIs públicas.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*  
  
 *Reimpressas pela permissão de Pearson educação, Inc. de [diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008, Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*  
  
## <a name="see-also"></a>Consulte também  
 [Diretrizes de design do Framework](../../../docs/standard/design-guidelines/index.md)  
 [Designer voltado para extensibilidade](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
