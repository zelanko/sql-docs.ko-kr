---
description: SearchDirectionEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 918261998fec061f8f977a8a2dfc614166f564f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442165"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)내에서 레코드 검색 방향을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|뒤로 검색 하 여 **레코드 집합**의 시작 부분에서 중지 합니다. 일치 항목을 찾을 수 없는 경우 레코드 포인터는 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)에 배치 됩니다.|  
|**adSearchForward**|1|앞으로 검색 하 여 **레코드 집합**의 끝에서 중지 합니다. 일치 하는 항목이 없으면 레코드 포인터가 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)에 배치 됩니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [Find 메서드(ADO)](../../../ado/reference/ado-api/find-method-ado.md)
