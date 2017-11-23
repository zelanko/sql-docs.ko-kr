---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: AllowNullsEnum
helpviewer_keywords: AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9bbf4b48843d897003774e75e5148881b020f47
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="allownullsenum"></a>AllowNullsEnum
Null 값이 있는 레코드는 인덱싱되어 있는지 여부를 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|인덱스에서 항목 키 열이 null을 허용 합니다. Null 값을 키 열에 입력 하는 경우 항목의 인덱스에 삽입 됩니다.|  
|**adIndexNullsDisallow**|1.|기본. 인덱스 키 열이 null 항목 수 없습니다. Null 값을 키 열에 입력 하는 경우 오류가 발생 합니다.|  
|**adIndexNullsIgnore**|2|인덱스는 null 키를 포함 하는 항목을 삽입 하지 않습니다. 키 열에 입력 된 값에 null 값 항목이 무시 되 고 오류가 발생 하지 않습니다.|  
|**adIndexNullsIgnoreAny**|4|인덱스 항목 일부 키 열에 null 값을 삽입 하지 않습니다. 여러 열이 있는 인덱스에 대 한 일부 열에 null 값을 입력 하는 경우에 키 항목 무시 되 고 오류가 발생 하지 않습니다.|  
  
## <a name="applies-to"></a>적용 대상  
 [IndexNulls 속성(ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
