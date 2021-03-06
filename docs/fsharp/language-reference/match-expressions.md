---
title: 'Expressões Match (F #)'
description: 'Saiba como a expressão de correspondência do F # fornece controle ramificação com base na comparação de uma expressão com um conjunto de padrões.'
ms.date: 04/19/2018
ms.openlocfilehash: 22cc4b7a87a60d8a5dcbe05ac5abec5560a37516
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33565172"
---
# <a name="match-expressions"></a>Expressões Match

O `match` expressão fornece controle ramificação com base na comparação de uma expressão com um conjunto de padrões.

## <a name="syntax"></a>Sintaxe

```fsharp
// Match expression.
match test-expression with
| pattern1 [ when condition ] -> result-expression1
| pattern2 [ when condition ] -> result-expression2
| ...

// Pattern matching function.
function
| pattern1 [ when condition ] -> result-expression1
| pattern2 [ when condition ] -> result-expression2
| ...
```

## <a name="remarks"></a>Comentários

As expressões de correspondência de padrão permitem ramificação complexa com base na comparação de uma expressão de teste com um conjunto de padrões. No `match` expressão, o *expressão de teste* é comparado com cada padrão, por sua vez, e quando uma correspondência for encontrada, o correspondente *expressão resultante* é avaliada e o valor resultante é retornado como o valor da expressão de correspondência.

A função mostrada na sintaxe anterior de correspondência de padrão é uma expressão lambda em qual padrão de correspondência é executada imediatamente no argumento. A função mostrada na sintaxe anterior de correspondência de padrão é equivalente à seguinte.

```fsharp
fun arg ->
    match arg with
    | pattern1 [ when condition ] -> result-expression1
    | pattern2 [ when condition ] -> result-expression2
    | ...
```

Para obter mais informações sobre expressões lambda, consulte [expressões Lambda: A `fun` palavra-chave](functions/lambda-expressions-the-fun-keyword.md).

Todo o conjunto de padrões deve abranger todas as correspondências possíveis da variável de entrada. Frequentemente, você pode usar o padrão de curinga (`_`) como o último padrão para corresponder a quaisquer valores de entrada anteriormente não correspondentes.

O código a seguir ilustra algumas das maneiras em que o `match` expressão é usada. Para obter uma referência e exemplos de todos os padrões possíveis que podem ser usados, consulte [correspondência de padrões](pattern-matching.md).

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4601.fs)]

## <a name="guards-on-patterns"></a>Protege nos padrões

Você pode usar um `when` cláusula para especificar uma condição adicional que a variável deve atender para corresponder a um padrão. Essa cláusula é conhecida como um *proteger*. A seguinte expressão a `when` palavra-chave não é avaliado, a menos que uma correspondência é feita para o padrão associado a essa proteção.

O exemplo a seguir ilustra o uso de uma proteção para especificar um intervalo numérico para um padrão de variável. Observe que várias condições são combinadas usando operadores boolianos.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4602.fs)]

Observe que como valores diferentes de literais não podem ser usados no padrão, você deve usar um `when` cláusula se você tiver alguma parte da entrada em relação a um valor de comparar. Isso é mostrado no código a seguir:

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4603.fs)]

Observe que, quando um padrão de união é coberto por um protetor, a proteção se aplica a **todos os** de padrões, não apenas o último deles. Por exemplo, considerando o código a seguir, a proteção de `when a > 12` se aplica às `A a` e `B a`:

```fsharp
type Union =
    | A of int
    | B of int

let foo() =
    let test = A 42
    match test with
    | A a
    | B a when a > 41 -> a // the guard applies to both patterns
    | _ -> 1

foo() // returns 42
```

## <a name="see-also"></a>Consulte também

[Referência da Linguagem F#](index.md)  
[Padrões Ativos](active-patterns.md)  
[Correspondência Padrão](pattern-matching.md)  
