---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f34ff1bba827678273590fdc1b39a001b5931644
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710830"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
줄 구분 기호가 쓸 문자열에 추가 되는지 여부를 지정 된 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|기본. 지정된 된 텍스트 문자열을 씁니다 (지정 된 합니다 *데이터* 매개 변수)에 **Stream** 개체입니다.|  
|**adWriteLine**|1|텍스트 문자열 및 줄 구분 기호 문자를 작성 한 **Stream** 개체입니다. 경우는 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성이 정의 되지 않은 다음 런타임 오류를 반환 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
