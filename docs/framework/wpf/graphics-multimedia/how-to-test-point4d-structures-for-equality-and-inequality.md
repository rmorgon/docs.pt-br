---
title: Como testar estruturas Point4D para igualdade e desigualdade
ms.date: 03/30/2017
helpviewer_keywords:
- inequality [WPF], testing Point4D structures for
- equality [WPF], testing Point4D structures for
- testing [WPF], Point4D structures for equality
- Point4D structures [WPF], testing for inequality
- testing [WPF], Point4D structures for inequality
- Point4D structures [WPF], testing for equality
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
ms.openlocfilehash: 1ec844c8fb0aceaaec6030c2e9d5cb30cf984f43
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33559808"
---
# <a name="how-to-test-point4d-structures-for-equality-and-inequality"></a>Como testar estruturas Point4D para igualdade e desigualdade
Este exemplo mostra como testar <xref:System.Windows.Media.Media3D.Point4D> estruturas para igualdade e desigualdade.  
  
 O código a seguir ilustra como testar <xref:System.Windows.Media.Media3D.Point4D> estruturas para igualdade e desigualdade usando o <xref:System.Windows.Media.Media3D.Point4D> métodos de igualdade.  O <xref:System.Windows.Media.Media3D.Point4D> estruturas são testadas para igualdade usando a igualdade sobrecarregada (`==`) operador, em seguida, para desigualdade usando o operador de desigualdade sobrecarregado (`!=`) operador e, finalmente, uma <xref:System.Windows.Media.Media3D.Point3D> estrutura e um <xref:System.Windows.Media.Media3D.Point4D> estrutura são verificados para igualdade usando estático <xref:System.Windows.Media.Media3D.Point4D.Equals%2A> método.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>  
 <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>  
 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>
