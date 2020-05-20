---
title: GetChildren 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: rothja
ms.author: jroth
ms.openlocfilehash: 605fb2e2afbd73a8a5509102ae98f348aad90bcb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760069"
---
# <a name="getchildren-method-ado"></a>GetChildren 메서드(ADO)
행이 컬렉션 [레코드](../../../ado/reference/ado-api/record-object-ado.md)의 자식을 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Return Value  
 각 행이 현재 **Record** 개체의 자식을 나타내는 **레코드 집합** 개체입니다. 예를 들어 디렉터리를 나타내는 **레코드** 의 자식은 부모 디렉터리 내에 포함 된 파일 및 하위 디렉터리입니다.  
  
## <a name="remarks"></a>설명  
 공급자는 반환 된 **레코드 집합**에 존재 하는 열을 결정 합니다. 예를 들어 문서 소스 공급자는 항상 리소스 **레코드 집합**을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
