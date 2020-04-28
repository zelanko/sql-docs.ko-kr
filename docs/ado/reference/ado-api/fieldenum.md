---
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe89d90510e95468e18b0d744ff566f69654320
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932689"
---
# <a name="fieldenum"></a>FieldEnum
[Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 [fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에서 참조 되는 특수 필드를 지정 합니다.  
  
## <a name="remarks"></a>설명  
 이러한 상수는 **레코드**와 연결 된 특수 필드에 액세스할 수 있는 "바로 가기"를 제공 합니다. **Fields** 컬렉션에서 [field](../../../ado/reference/ado-api/field-object.md) 개체를 검색 한 다음 **필드** 개체의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 사용 하 여 해당 내용을 가져옵니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|**레코드**와 연결 된 기본 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체를 포함 하는 필드를 참조 합니다.|  
|**adRecordURL**|-2|현재 **레코드**에 대 한 절대 URL 문자열을 포함 하는 필드를 참조 합니다.|
