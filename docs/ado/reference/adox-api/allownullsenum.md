---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 53fadcddd49ebf68949da0a7dca3cb37da0b5d93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708609"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Null 값을 사용 하 여 레코드는 인덱싱되어 있는지 여부를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|인덱스에서 항목의 키 열에 null을 허용 합니다. 키 열에는 null 값을 입력 하는 경우 항목의 인덱스에 삽입 됩니다.|  
|**adIndexNullsDisallow**|1|기본. 인덱스 키 열에 null 항목을 허용 하지 않습니다. 키 열에는 null 값을 입력 하는 경우 오류가 발생 합니다.|  
|**adIndexNullsIgnore**|2|인덱스는 null 키가 포함 된 항목을 삽입 하지 않습니다. 키 열에는 null 값을 입력 하는 경우 항목 무시 되 고 오류가 발생 하지 않습니다.|  
|**adIndexNullsIgnoreAny**|4|인덱스는 일부 키 열에 null 값이 있는 항목을 삽입 하지 않습니다. 다중 열 인덱스의 일부 열에 null 값을 입력 하는 경우에 키 항목 무시 되 고 오류가 발생 하지 않습니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [IndexNulls 속성(ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
