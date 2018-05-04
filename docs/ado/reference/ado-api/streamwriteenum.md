---
title: StreamWriteEnum | Microsoft Docs
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
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b81765d125680bc52a8e95adcb3828df36bfc0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="streamwriteenum"></a>StreamWriteEnum
선 구분 기호가에 작성 되는 문자열에 추가 되는지 여부를 지정 된 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|기본. 지정된 된 텍스트 문자열을 씁니다 (지정 된는 *데이터* 매개 변수)에 **스트림** 개체입니다.|  
|**adWriteLine**|1.|텍스트 문자열과 줄 구분 기호 문자를 씁니다는 **스트림** 개체입니다. 경우는 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성이 정의 되지 않은 다음 런타임에 오류를 반환 합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
