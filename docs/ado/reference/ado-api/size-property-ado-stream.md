---
description: Size 속성(ADO 스트림)
title: Size 속성 (ADO 스트림) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dc2f09b6c5f6fd784ab5c4ca29a7596b838e38fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989104"
---
# <a name="size-property-ado-stream"></a>Size 속성(ADO 스트림)
스트림의 크기 (바이트 수)를 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 스트림의 크기 (바이트 수)를 지정 하는 **Long** 값을 반환 합니다. 기본값은 스트림의 크기 이며 스트림의 크기를 알 수 없는 경우에는-1입니다.  
  
## <a name="remarks"></a>설명  
 **크기** 는 열려 있는 [스트림](./stream-object-ado.md) 개체에만 사용할 수 있습니다.  
  
> [!NOTE]
>  모든 수의 비트는 시스템 리소스에 의해서만 제한 되는 **스트림** 개체에 저장할 수 있습니다. **스트림에** **Long** 값으로 표현할 수 있는 것 보다 많은 비트가 포함 된 경우 **크기가** 잘리고 **스트림의**길이를 정확 하 게 나타내지 않습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Size 속성(ADO 매개 변수)](./size-property-ado-parameter.md)