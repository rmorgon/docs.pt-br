---
title: "Instru&#231;&#227;o With...End With (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.With"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "palavra-chave End, instruções With...End With"
  - "execução, no objeto"
  - "instruções, repetindo"
  - "Estruturas de loop, e instruções With...End With"
  - "objetos [Visual Basic], acessando"
  - "bloco With"
  - "Palavra-chave with"
  - "Instrução With"
  - "Instrução With, aninhamento"
  - "instruções With...End With"
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
caps.latest.revision: 34
caps.handback.revision: 34
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Instru&#231;&#227;o With...End With (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Executa uma série de instruções que referenciam repetidamente um único objeto ou estrutura de modo que as instruções possam usar uma sintaxe simplificada para acessar membros do objeto ou estrutura.  Ao usar uma estrutura, você só poderá ler os valores dos membros ou invocar métodos, e obterá um erro se tentar atribuir valores aos membros de uma estrutura usada em uma instrução `With...End With`.  
  
## Sintaxe  
  
```  
With objectExpression  
    [ statements ]  
End With  
```  
  
## Partes  
  
|||  
|-|-|  
|Termo|Definição|  
|`objectExpression`|Obrigatório.  Uma expressão que avalia como um objeto.  A expressão pode ser arbitrariamente complexa e é avaliada apenas uma vez.  A expressão pode ser avaliada como qualquer tipo de dados, inclusive tipos elementares.|  
|`statements`|Opcional.  Uma ou mais instruções entre `With` e `End With` que podem fazer referência a membros de um objeto que é gerado pela avaliação de `objectExpression`.|  
|`End With`|Obrigatório.  Finaliza a definição do bloco `With`.|  
  
## Comentários  
 Usando `With...End With`, você pode executar uma série de instruções em um objeto especificado sem especificar o nome do objeto várias vezes.  Dentro de um bloco de instrução `With`, você pode especificar um membro do objeto que começa com um ponto, como se o objeto de instrução `With` o precedesse.  
  
 Por exemplo, para alterar várias propriedades diferentes em um único objeto, coloque as instruções de atribuição de propriedade dentro do bloco `With...End With`, fazendo referência ao objeto apenas uma vez em vez de uma vez para cada atribuição de propriedade.  
  
 Se seu código acessar o mesmo objeto em várias instruções, você ganhará os seguintes benefícios usando a instrução `With`:  
  
-   Você não precisa avaliar várias vezes uma expressão complexa ou atribuir o resultado a uma variável temporária para fazer referência a seus membros várias vezes.  
  
-   Você torna seu código mais legível eliminando expressões aplicáveis repetitivas.  
  
 O tipo de dados de `objectExpression` pode ser qualquer tipo de classe ou estrutura, ou até mesmo um tipo elementar do Visual Basic, como `Integer`.  Se `objectExpression` resultar em algo diferente de um objeto, você só poderá ler os valores de seus membros ou invocar métodos, e obterá um erro se tentar atribuir valores aos membros de uma estrutura usada em uma instrução `With...End With`.  Esse é o mesmo erro que você obteria se invocasse um método que retornasse uma estrutura e imediatamente acessasse e atribuísse um valor a um membro do resultado da função, como `GetAPoint().x = 1`.  O problema em ambos os casos é que a estrutura só existe na pilha de chamadas, e não há maneira de um membro da estrutura alterada nessas situações gravar em um local de modo que qualquer outro código no programa possa observar a alteração.  
  
 `objectExpression` é avaliada uma vez, ao entrar no bloco.  Você não pode reatribuir `objectExpression` de dentro do bloco `With`.  
  
 Dentro de um bloco `With`, você pode acessar os métodos e as propriedades de apenas o objeto especificado sem qualificá\-los.  Você pode usar métodos e propriedades de outros objetos, mas deverá qualificá\-los com seus nomes de objeto.  
  
 Você pode colocar uma instrução `With...End With` dentro de outra.  As instruções `With...End With` aninhadas podem ser confusas se os objetos que estão sendo referidos não são claros em termos de contexto.  Você deve fornecer uma referência totalmente qualificada a um objeto que esteja em um bloco `With` externo quando o objeto é referenciado dentro de um bloco `With` interno.  
  
 Você não pode ramificar em uma instrução `With` de fora do bloco.  
  
 A menos que o bloco contenha um loop, as instruções são executadas somente uma vez.  Você pode aninhar diferentes tipos de estruturas de controle.  Para obter mais informações, consulte [Estruturas de controle aninhadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
> [!NOTE]
>  Você também pode usar a palavra\-chave `With` em inicializadores de objetos.  Para obter mais informações e exemplos, consulte [Inicializadores de objeto: tipos nomeados e anônimos](../Topic/Object%20Initializers:%20Named%20and%20Anonymous%20Types%20\(Visual%20Basic\).md) e [Tipos anônimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
>   
>  Se você estiver usando um bloco `With` somente para inicializar as propriedades ou os campos de um objeto que acabou de instanciar, considere usar um inicializador do objeto como alternativa.  
  
## Exemplo  
 No exemplo a seguir, cada bloco `With` executa uma série de instruções em um único objeto.  
  
 [!code-vb[VbVbalrWithStatement#2](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_1.vb)]  
  
## Exemplo  
 O exemplo a seguir aninha instruções `With…End With`.  Na instrução `With` aninhada, a sintaxe faz referência ao objeto interno.  
  
 [!code-vb[VbVbalrWithStatement#1](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_2.vb)]  
  
## Consulte também  
 <xref:System.Collections.Generic.List%601>   
 [Estruturas de controle aninhadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Inicializadores de objeto: tipos nomeados e anônimos](../Topic/Object%20Initializers:%20Named%20and%20Anonymous%20Types%20\(Visual%20Basic\).md)   
 [Tipos anônimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)