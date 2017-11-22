---
title: "GetChildren 메서드 (ADO) | Microsoft Docs"
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
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords: GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f9af9b4cb1b4648acc75389f7d75cccdc46b96
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="getchildren-method-ado"></a>GetChildren 메서드 (ADO)
반환 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 해당 행 컬렉션의 자식을 나타내는 [레코드](../../../ado/reference/ado-api/record-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>반환 값  
 A **레코드 집합** 개체를 각 행이 현재 자식 나타내는 **레코드** 개체입니다. 예를 들어 자식은 **레코드** 나타냅니다 디렉터리 수 있다고 파일과 하위 디렉터리는 부모 디렉터리 내에 포함 합니다.  
  
## <a name="remarks"></a>주의  
 공급자에서 반환 된 어떤 열이 존재에 따라 결정 **레코드 집합**합니다. 예를 들어 문서 소스 공급자 리소스를 항상 반환 **레코드 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
