---
description: SearchDirectionEnum
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: dc30978b5ce157aa103e41f2b68dd8b36864f25a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989230"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
레코드 [집합](./recordset-object-ado.md)내에서 레코드 검색 방향을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|뒤로 검색 하 여 **레코드 집합**의 시작 부분에서 중지 합니다. 일치 항목을 찾을 수 없는 경우 레코드 포인터는 [BOF](./bof-eof-properties-ado.md)에 배치 됩니다.|  
|**adSearchForward**|1|앞으로 검색 하 여 **레코드 집합**의 끝에서 중지 합니다. 일치 하는 항목이 없으면 레코드 포인터가 [EOF](./bof-eof-properties-ado.md)에 배치 됩니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [Find 메서드(ADO)](./find-method-ado.md)