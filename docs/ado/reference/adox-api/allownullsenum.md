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
ms.openlocfilehash: 48e9d8c40d2ab76b902d285526fcd9e9abf7be07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967333"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Null 값이 있는 레코드를 인덱싱할 지 여부를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|인덱스는 키 열이 null 인 항목을 허용 합니다. 키 열에 null 값이 입력 되 면 해당 항목이 인덱스에 삽입 됩니다.|  
|**adIndexNullsDisallow**|1|기본값 인덱스는 키 열이 null 인 항목을 허용 하지 않습니다. 키 열에 null 값이 입력 되 면 오류가 발생 합니다.|  
|**adIndexNullsIgnore**|2|인덱스는 null 키가 포함 된 항목을 삽입 하지 않습니다. 키 열에 null 값이 입력 되 면 해당 항목은 무시 되 고 오류가 발생 하지 않습니다.|  
|**adIndexNullsIgnoreAny**|4|인덱스는 일부 키 열에 null 값이 있는 항목을 삽입 하지 않습니다. 열이 여러 개 있는 인덱스의 경우 일부 열에 null 값이 입력 되 면 해당 항목은 무시 되 고 오류가 발생 하지 않습니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [IndexNulls 속성(ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
