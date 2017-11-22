---
title: SearchDirectionEnum | Microsoft Docs
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
f1_keywords: SearchDirectionEnum
helpviewer_keywords: SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4d5e78b7f636c4fb6094a217a0b1249babe9b2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
내에서 레코드 검색의 방향을 지정는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|뒤로 검색의 시작 부분에서 중지 된 **레코드 집합**합니다. 일치 하는 항목이 없는 경우 레코드 포인터에 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)합니다.|  
|**adSearchForward**|1.|검색의 끝에서 중지를 앞으로 **레코드 집합**합니다. 일치 하는 항목이 없는 경우 레코드 포인터에 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>적용 대상  
 [Find 메서드(ADO)](../../../ado/reference/ado-api/find-method-ado.md)
