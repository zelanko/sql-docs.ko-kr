---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a5c1c3869b144bb770ca893595986288b07aa596
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711449"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
내에서 레코드 검색 방향을 지정 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|시작 부분에서 중지, 검색 된 **레코드 집합**합니다. 일치 하는 항목이 없으면 레코드 포인터의 위치가 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)합니다.|  
|**adSearchForward**|1|끝날 때 중지, 검색에서 전달 된 **레코드 집합**합니다. 일치 하는 항목이 없으면 레코드 포인터의 위치가 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>적용 대상  
 [Find 메서드(ADO)](../../../ado/reference/ado-api/find-method-ado.md)
