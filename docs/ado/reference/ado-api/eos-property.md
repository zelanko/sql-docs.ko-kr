---
title: EOS 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 10b7ee78cb9903ccf0794a197a0679c226141641
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698252"
---
# <a name="eos-property"></a>EOS 속성
현재 위치가 끝에 있는지 여부를 나타내는 합니다 [스트림을](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **부울** 현재 위치가 스트림의 맨 끝에 있는지 여부를 나타내는 값입니다. **EOS** 반환 **True** 반환에 있는 경우 더 이상 바이트 스트림에서 **False** 경우 더 많은 바이트를 현재 위치를 수행 합니다.  
  
 스트림 위치의 끝을 설정 하려면 사용 합니다 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 메서드. 현재 위치를 확인 하려면 사용 합니다 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [EOS 및 LineSeparator 속성 SkipLine 메서드 예제 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
