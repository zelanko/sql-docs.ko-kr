---
title: EOS 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25bab5a0079b07e971200d28bc69e7b36b528523
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="eos-property"></a>EOS 속성
현재 위치가의 끝에 있는지 여부를 나타냅니다는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **부울** 현재 위치가 스트림 끝에 있는지 여부를 나타내는 값입니다. **EOS** 반환 **True** 반환에 있는 경우 추가 바이트 스트림; **False** 더 많은 바이트를 현재 위치 뒤에 있는 경우.  
  
 스트림 위치의 끝을 설정 하려면는 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 메서드. 현재 위치를 확인 하려면 사용 하 여는 [위치](../../../ado/reference/ado-api/position-property-ado.md) 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [EOS LineSeparator 속성 및 SkipLine 메서드 예제 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
