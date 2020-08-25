---
description: StreamWriteEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 343e5fd45a32e45cda342ab01feb64f379054486
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777162"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
줄 구분 기호가 [스트림](./stream-object-ado.md) 개체에 쓰여진 문자열에 추가 되는지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|기본값 *데이터* 매개 변수에 의해 지정 된 지정 된 텍스트 문자열을 **스트림** 개체에 씁니다.|  
|**adWriteLine**|1|텍스트 문자열과 줄 구분선 문자를 **스트림** 개체에 씁니다. [LineSeparator](./lineseparator-property-ado.md) 속성이 정의 되지 않은 경우 런타임 오류가 반환 됩니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [WriteText 메서드](./writetext-method.md)