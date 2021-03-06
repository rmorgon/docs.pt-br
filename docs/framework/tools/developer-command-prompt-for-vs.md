---
title: Prompt de Comando do Desenvolvedor para o Visual Studio
ms.date: 06/18/2018
helpviewer_keywords:
- command prompt, Windows SDK
- Visual Studio command prompt
- command prompt, Visual Studio
- SDK command prompt
- tools [.NET Framework], setting environment variables
- environment variables, setting for tools
- developer command prompt
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8e64facffd4face929b28d660ffd5210f127c3bd
ms.sourcegitcommit: c217b067985905cb21eafc5dd9a83568d7ff4e45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36315219"
---
# <a name="developer-command-prompt-for-visual-studio"></a>Prompt de Comando do Desenvolvedor para o Visual Studio

O Prompt de Comando do Desenvolvedor do Visual Studio define automaticamente as variáveis de ambiente que permitem usar as ferramentas do .NET Framework com facilidade. O Prompt de Comando do Desenvolvedor é instalado com as edições completa ou Community do Visual Studio. Ele não é instalado com as versões Express do Visual Studio.

> [!div class="button"]
[Baixar o Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="searching-for-the-command-prompt-on-your-machine"></a>Procurar o prompt de comando no computador

Você pode ver vários prompts de comando, dependendo da versão do Visual Studio e dos SDKs adicionais instalados. Por exemplo, as versões 64 bits do Visual Studio oferecem prompts de comando 32 e 64 bits. (As versões de 32 e 64 bits da maioria das ferramentas são iguais; porém, algumas ferramentas fazem alterações específicas em ambientes de 32 e 64 bits.) Se as etapas abaixo não funcionarem, você poderá tentar [Localizar manualmente os arquivos em seu computador](#manually-locating-the-files-on-your-machine) ou [Executar o prompt de comando de dentro do Visual Studio](#running-command-prompt-from-inside-visual-studio).

### <a name="in-windows-10"></a>No Windows 10

1. Na caixa de pesquisa da barra de tarefas, comece a digitar o nome da ferramenta, por exemplo, `dev` ou `developer command prompt`. Será exibida uma lista dos aplicativos instalados que correspondem ao padrão de pesquisa. Se você estiver procurando por um prompt de comando diferente, experimente digitar um termo de pesquisa diferente, como `prompt`.

2. Escolha o **Prompt de Comando do Desenvolvedor** (ou o prompt de comando que você deseja usar).

### <a name="in-windows-81"></a>No Windows 8.1

1. Abra a tela **Iniciar** pressionando a tecla do logotipo do Windows ![Logotipo do Windows](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") no seu teclado, por exemplo.

2. Na tela **Iniciar**, pressione `CTRL + TAB` para abrir a lista **Aplicativos** e digite `V`. Isso mostra uma lista que inclui todos os prompts de comando do Visual Studio instalados.

3. Escolha o **Prompt de Comando do Desenvolvedor** (ou o prompt de comando que você deseja usar).

### <a name="in-windows-8"></a>No Windows 8

1. Abra a tela **Iniciar** pressionando a tecla do logotipo do Windows ![Logotipo do Windows](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") no seu teclado, por exemplo.

2. Na tela **Iniciar**, pressione a tecla do logotipo do Windows ![Logotipo do Windows](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") `+ Z`.

3. Escolha o ícone **Exibição de aplicativos** na parte inferior da tela e digite `V`. Isso mostra uma lista que inclui todos os prompts de comando do Visual Studio instalados.

4. Escolha o **Prompt de Comando do Desenvolvedor** (ou o prompt de comando que você deseja usar).

### <a name="in-windows-7"></a>No Windows 7

1. Escolha **Iniciar**, expanda **Todos os Programas** e expanda **Microsoft Visual Studio**.

2. Dependendo da versão do Visual Studio que você instalou, escolha **Ferramentas do Visual Studio**, **Prompt de Comando do Visual Studio** ou o prompt de comando que você deseja usar.

Se você tiver outros SDKs instalados, como o [SDK do Windows 10](https://developer.microsoft.com/windows/downloads/windows-10-sdk) ou [versões anteriores](https://developer.microsoft.com/windows/downloads/sdk-archive), poderá ver prompts de comando adicionais para arquiteturas ARM, x86 ou x64. Consulte a documentação das ferramentas individuais para determinar qual versão do prompt de comando você deve usar.

## <a name="manually-locating-the-files-on-your-machine"></a>Localizar manualmente os arquivos em seu computador

Normalmente, os atalhos para os prompts de comando que você instalou são colocados na pasta **Menu Iniciar** do Visual Studio, como em C:\ProgramData\Microsoft\Windows\MenuIniciar\Programas\Visual Studio 2017\Visual Studio Tools. Porém, se por algum motivo a pesquisa do prompt de comando não gerar os resultados esperados, você poderá tentar localizar manualmente o atalho em seu computador. Tente pesquisar pelo nome do arquivo do prompt de comando, como *VsDevCmd.bat* ou acesse a pasta Tools, como C:\Arquivos de Programas (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools (o caminho mudará conforme seu local de instalação, edição e versão do Visual Studio).

## <a name="running-command-prompt-from-inside-visual-studio"></a>Executar o prompt de comando de dentro do Visual Studio

Para facilitar o acesso, você pode adicionar o Prompt de Comando do Visual Studio Developer ou qualquer outro prompt de comando ao menu Ferramentas no Visual Studio, adicionando-o à lista de ferramentas externas. Faça isso da seguinte forma:

1. Abra o Visual Studio.

2. Selecione o menu **Ferramentas** e escolha **Ferramentas Externas**.

3. Na caixa de diálogo **Ferramentas Externas**, escolha o botão **Adicionar**. Uma nova entrada é exibida.

4. Insira um **Título** para o novo item de menu, como `Command Prompt`.

5. No campo **Comando**, especifique o arquivo que você deseja iniciar, como `%comspec%` ou `C:\Windows\System32\cmd.exe`.

6. No campo **Argumentos**, especifique em que ponto encontrar o prompt de comando específico que você deseja usar como `/k "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools\VsDevCmd.bat"` (esse comando inicializa o Prompt de Comando do Desenvolvedor que é instalado com o Visual Studio 2017 Enterprise). Altere este valor de acordo com a sua versão, edição e local de instalação do Visual Studio.

7. Escolha um valor para o campo **Diretório inicial**, como **Diretório do Projeto**.

8. Escolha o botão **OK**.

Depois disso, o novo item de menu será adicionado e você poderá acessar o prompt de comando no menu **Ferramentas**.

## <a name="see-also"></a>Consulte também

 [Ferramentas](../../../docs/framework/tools/index.md)  
 [Gerenciando ferramentas externas](/visualstudio/ide/managing-external-tools)  
