---
description: GetChildren 메서드(ADO)
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
ms.openlocfilehash: 906c20d19143f4f1e8fe0b6c1e91585893acfa5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443585"
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

:::row:::
    :::column:::
        [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::
