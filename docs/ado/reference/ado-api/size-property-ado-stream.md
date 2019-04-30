---
title: Size 속성 (ADO Stream) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d35af0315460af8b110c7af38934e5d196a5c895
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192798"
---
# <a name="size-property-ado-stream"></a>Size 속성(ADO 스트림)
바이트 수가 스트림의 크기를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **긴** 바이트 수에서를 스트림의 크기를 지정 하는 값입니다. 기본값 스트림의 크기를 알 수 없는 경우를 스트림 또는-1의 크기는 합니다.  
  
## <a name="remarks"></a>Remarks  
 **크기** 오픈 에서만 사용할 수 있습니다 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  비트에 저장할 수는 **Stream** 개체, 시스템 리소스에 의해서만 제한 됩니다. 경우는 **Stream** 로 나타낼 수 있습니다 보다 더 많은 비트가 포함을 **긴** 값 **크기** 잘리고 따라서 정확 하 게 나타내지 합니다 길이의**Stream**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Size 속성(ADO 매개 변수)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
