---
title: Método ICorDebugThread::GetCurrentException
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetCurrentException
helpviewer_keywords:
- ICorDebugThread::GetCurrentException method [.NET Framework debugging]
- GetCurrentException method [.NET Framework debugging]
ms.assetid: 331ed465-a195-4359-8584-b82c6098b29b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 82686fdd14783257987ec5bf9a24db7d87049d42
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33421740"
---
# <a name="icordebugthreadgetcurrentexception-method"></a>Método ICorDebugThread::GetCurrentException
Obtém um ponteiro de interface para um objeto ICorDebugValue que representa uma exceção que está atualmente sendo gerada pelo código gerenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetCurrentException (  
    [out] ICorDebugValue **ppExceptionObject  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppExceptionObject`  
 [out] Um ponteiro para o endereço de um `ICorDebugValue` que representa a exceção que está atualmente sendo gerada pelo objeto de código gerenciado.  
  
## <a name="remarks"></a>Comentários  
 O objeto de exceção existirá desde o momento em que a exceção é lançada até o término do `catch` bloco. Uma avaliação de função, que é executada pelos métodos ICorDebugEval, limpará o objeto de exceção na instalação e restaurá-lo após a conclusão.  
  
 Exceções podem ser aninhadas (por exemplo, se uma exceção será lançada em um filtro ou em uma avaliação de função), pode haver várias exceções pendentes em um único thread. `GetCurrentException` Retorna a exceção mais atual.  
  
 O objeto de exceção e o tipo podem ser alterado durante a vida útil da exceção. Por exemplo, depois que uma exceção do tipo x for lançada, o common language runtime (CLR) pode ficar sem memória e promovê-la a uma exceção de falta de memória.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
