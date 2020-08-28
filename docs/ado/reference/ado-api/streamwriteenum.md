---
description: StreamWriteEnum
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c09a15f5c5aba9d36f038304b68cc1e64112ade3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988444"
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