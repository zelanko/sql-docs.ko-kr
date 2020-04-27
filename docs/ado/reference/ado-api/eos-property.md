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
ms.openlocfilehash: 5a19856c957ee0c003e934ff8b2632aa28e32d33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918922"
---
# <a name="eos-property"></a>EOS 속성
현재 위치가 [스트림의](../../../ado/reference/ado-api/stream-object-ado.md)끝에 있는지 여부를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 현재 위치가 스트림의 끝에 있는지 여부를 나타내는 **부울** 값을 반환 합니다. **EOS** 는 스트림에 더 이상 바이트가 없으면 **True** 를 반환 합니다. 현재 위치 뒤에 더 많은 바이트가 있는 경우 **False** 를 반환 합니다.  
  
 스트림 위치의 끝을 설정 하려면 [SetEOS](../../../ado/reference/ado-api/seteos-method.md) 메서드를 사용 합니다. 현재 위치를 확인 하려면 [position](../../../ado/reference/ado-api/position-property-ado.md) 속성을 사용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [EOS 및 LineSeparator 속성 및 SkipLine 메서드 예제 (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
