---
description: LineSeparator 속성(ADO)
title: LineSeparator 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bd1e14d5c7ebc84ea4736da08296eca0e02ea38
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990724"
---
# <a name="lineseparator-property-ado"></a>LineSeparator 속성(ADO)
텍스트 [스트림](./stream-object-ado.md) 개체에서 줄 구분 기호로 사용할 이진 문자를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **스트림에**사용 되는 줄 구분 기호 문자를 나타내는 [LineSeparatorsEnum](./lineseparatorsenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **Adcrlf**입니다.  
  
## <a name="remarks"></a>설명  
 **LineSeparator** 은 텍스트 **스트림의**내용을 읽을 때 줄을 해석 하는 데 사용 됩니다. [SkipLine](./skipline-method.md) 메서드를 사용 하 여 줄을 건너뛸 수 있습니다.  
  
 **LineSeparator** 은 텍스트 **스트림** 개체 ([Type](./type-property-ado-stream.md) is **adTypeText**)에만 사용 됩니다. **형식이** **adtypebinary**인 경우이 속성은 무시 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [스트림 개체(ADO)](./stream-object-ado.md)