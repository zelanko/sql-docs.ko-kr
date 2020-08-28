---
description: StringFormatEnum
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fe580d45d20c65c313cd87b3fb47ef63bb349ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988424"
---
# <a name="stringformatenum"></a>StringFormatEnum
[레코드 집합](./recordset-object-ado.md) 을 문자열로 검색할 때 형식을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adClipString**|2|행 *구분 기호*, *columndelimiter*열, Null 값을 *nullexpr*로 구분 합니다. [GetString](./getstring-method-ado.md) 메서드의이 세 매개 변수는 *StringFormat* **adClipString**에만 사용할 수 있습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>적용 대상  
 [GetString 메서드(ADO)](./getstring-method-ado.md)