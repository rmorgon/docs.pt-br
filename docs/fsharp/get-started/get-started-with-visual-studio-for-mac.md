---
title: 'Introdução ao F # no Visual Studio para Mac'
description: 'Saiba como usar F # com o Visual Studio para Mac.'
ms.date: 07/03/2018
ms.openlocfilehash: 200c3a8fee072797a54d15d8989937f4cadb33e2
ms.sourcegitcommit: 59b51cd7c95c75be85bd6ef715e9ef8c85720bac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37874647"
---
# <a name="get-started-with-f-in-visual-studio-for-mac"></a>Introdução ao F # no Visual Studio para Mac

F # e as ferramentas do Visual F # têm suporte no Visual Studio para Mac IDE. Certifique-se de que você tenha [Visual Studio para Mac instalados](install-fsharp.md#install-f-with-visual-studio-for-mac).

## <a name="creating-a-console-application"></a>Criando um aplicativo de console

Um dos projetos mais básicos no Visual Studio para Mac é o aplicativo de Console.  Veja como fazer isso.  Após abrir o Visual Studio para Mac:

1. Sobre o **arquivo** , aponte para **nova solução**.

2.  Na caixa de diálogo Novo projeto, existem 2 modelos diferentes para o aplicativo de Console.  Há um em outros -> .NET que tem como alvo o .NET Framework.  O outro modelo está sob o .NET Core -> aplicativo que tem como alvo o .NET Core.  O modelo deve funcionar com a finalidade deste artigo.

3. Em um aplicativo de console, altere c# para F # se necessário.  Escolha o **próxima** botão Mover para frente!  

4. Dê um nome ao seu projeto e escolha as opções desejadas para o aplicativo.  Observe, o painel de visualização para o lado da tela que mostra a estrutura do diretório que será criada com base nas opções selecionadas.  

5. Clique em **Criar**.  Agora você verá um projeto F # no Gerenciador de soluções.

## <a name="writing-your-code"></a>Escrever seu código

Vamos começar escrevendo um código pela primeira vez.  Certifique-se de que o `Program.fs` arquivo está aberto e, em seguida, substitua seu conteúdo pelo seguinte:

[!code-fsharp[HelloSquare](../../../samples/snippets/fsharp/getting-started/hello-square.fs)]

No exemplo de código anterior, uma função `square` tenha sido definido, que usa uma entrada denominada `x` e multiplica por si só.  Como o F # usa [inferência](../language-reference/type-inference.md), o tipo de `x` não precisa ser especificado.  O compilador F # compreende os tipos em que a multiplicação é válida e atribuirá um tipo para `x` com base em como `square` é chamado.  Se você focalizar `square`, você deve ver o seguinte:

```
val square: x:int -> int
```

Esse é o que é conhecido como assinatura de tipo da função.  Ele pode ser lido como esta: "quadrado é uma função que usa um número inteiro denominado x e produz um número inteiro".  Observe que o compilador forneceu `square` as `int` tipo por ora - isso é porque a multiplicação não é genérica entre *todos os* tipos, mas em vez disso, é genérico em um conjunto fechado de tipos.  O compilador F # escolhido `int` neste ponto, mas ele se ajustará a assinatura de tipo se você chamar `square` com outro tipo de entrada, como um `float`.

Outra função, `main`, é definido, que é decorado com o `EntryPoint` atributo para indicar ao compilador F # que a execução do programa deve iniciar lá.  Ele segue a mesma convenção que outro [linguagens de programação C-style](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B), em que os argumentos de linha de comando podem ser passados para essa função, e um código inteiro será retornado (normalmente `0`).

É nessa função que podemos chamar o `square` função com um argumento de `12`.  O compilador F #, em seguida, atribui o tipo de `square` ser `int -> int` (ou seja, uma função que usa um `int` e produz um `int`).  A chamada para `printfn` é uma função de impressão formatada que usa uma cadeia de formato, semelhante a linguagens de programação C-style, parâmetros que correspondem aos especificados na cadeia de caracteres de formato e, em seguida, imprime o resultado e uma nova linha.

## <a name="running-your-code"></a>Execução do código

Você pode executar o código e ver os resultados clicando em **executados** no menu de nível superior e, em seguida **Start Without Debugging**.  Isso executará o programa sem depuração e permite que você veja os resultados.

Agora você deve ver o seguinte mostrado na janela de console que exibia o Visual Studio para Mac:

```
12 squared is 144!
```

Parabéns!  Criou seu primeiro projeto F # no Visual Studio para Mac, escrito que uma função F # impresso os resultados da chamada de função e execute o projeto para ver alguns resultados.

## <a name="using-f-interactive"></a>Usando F # interativo

Um dos melhores recursos do Visual F # de ferramentas no Visual Studio para Mac é a janela interativa do F #.  Ele permite que você envie código sobre a um processo em que você pode chamar esse código e ver o resultado de forma interativa.

Para começar a usá-lo, realce o `square` função definida em seu código.  Em seguida, clique em **editar** no menu de nível superior.  Em seguida, selecione **enviar seleção para o F # interativo**.  Isso executa o código na janela interativa do F #.  Como alternativa, você pode clique com botão direito na seleção e escolha **enviar seleção para o F # interativo**.  Você deverá ver a janela interativa do F # são exibidos com o seguinte:

```
>

val square : x:int -> int

>
```

Isso mostra a mesma assinatura de função para o `square` função, que você viu anteriormente quando você passava sobre a função.  Porque `square` é agora definido no processo de F # interativo, você pode chamá-lo com valores diferentes:

```
> square 12;;
val it : int = 144
>square 13;;
val it : int = 169
```

Isso executa a função, associa o resultado para um novo nome `it`e exibe o tipo e o valor de `it`.  Observe que você deve encerrar cada linha com `;;`.  Isso é como o F # interativo sabe quando a chamada da função for concluída.  Você também pode definir novas funções em F # interativo:

```
> let isOdd x = x % 2 <> 0;;

val isOdd : x:int -> bool

> isOdd 12;;
val it : bool = false
```

As opções acima define uma nova função, `isOdd`, que utiliza um `int` e verifica se ele for ímpar!  Você pode chamar essa função para ver o que ela retorna com entradas diferentes.  Você pode chamar funções em chamadas de função:

```
> isOdd (square 15);;
val it : bool = true
```

Você também pode usar o [operador de pipe avanço](../language-reference/symbol-and-operator-reference/index.md) para transmitir o valor para as duas funções:

```
> 15 |> square |> isOdd;;
val it : bool = true
```

O operador de pipe para uso futuro e muito mais, são abordadas em tutoriais posteriores.

Isso é apenas uma visão rápida sobre o que você pode fazer com o F # interativo.  Para saber mais, confira [programação interativa com F #](../tutorials/fsharp-interactive/index.md).

## <a name="next-steps"></a>Próximas etapas

Se você ainda não fez isso, confira a [Tour do F #](../tour.md), que aborda alguns dos principais recursos da linguagem F #.  Ele lhe dá uma visão geral de alguns dos recursos da linguagem F # e fornecem exemplos de código amplo que você pode copiar para o Visual Studio para Mac e executar.  Também existem alguns ótimos recursos externos, você pode usar, foi apresentada na [guia de F #](../index.md).

## <a name="see-also"></a>Consulte também
 [Visual F#](../index.md)  
 [Tour do F#](../tour.md)  
 [Referência da linguagem F #](../language-reference/index.md)  
 [Inferência de tipo](../language-reference/type-inference.md)  
 [Referência de símbolo e o operador](../language-reference/symbol-and-operator-reference/index.md)  
