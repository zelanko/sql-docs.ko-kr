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
ms.openlocfilehash: 4cc9de1481cc683bddafe2f92959977319600f6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928639"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
줄 구분 기호가 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Default. *데이터* 매개 변수에 의해 지정 된 지정 된 텍스트 문자열을 **스트림** 개체에 씁니다.|  
|**adWriteLine**|1|텍스트 문자열과 줄 구분선 문자를 **스트림** 개체에 씁니다. [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성이 정의 되지 않은 경우 런타임 오류가 반환 됩니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
