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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928639"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
줄 구분 기호가 쓸 문자열에 추가 되는지 여부를 지정 된 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|기본. 지정된 된 텍스트 문자열을 씁니다 (지정 된 합니다 *데이터* 매개 변수)에 **Stream** 개체입니다.|  
|**adWriteLine**|1|텍스트 문자열 및 줄 구분 기호 문자를 작성 한 **Stream** 개체입니다. 경우는 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 속성이 정의 되지 않은 다음 런타임 오류를 반환 합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 이러한 상수는 ADO/wfc 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [WriteText 메서드](../../../ado/reference/ado-api/writetext-method.md)
