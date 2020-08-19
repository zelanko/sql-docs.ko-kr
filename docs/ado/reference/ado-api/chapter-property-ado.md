---
description: Chapter 속성(ADO)
title: 장 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: rothja
ms.author: jroth
ms.openlocfilehash: ae595351ed6882bf67f543d61dc583d3350e6ce1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451015"
---
# <a name="chapter-property-ado"></a>Chapter 속성(ADO)
[ADORecordsetConstruction Interface](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) 개체의/에서 OLE DB **챕터** 개체를 가져오거나 설정 합니다. **Put_Chapter** 를 사용 하 여 **챕터** 개체를 설정 하는 경우 행의 하위 집합이 ADO [레코드 집합 개체](../../../ado/reference/ado-api/recordset-object-ado.md) 개체로 설정 됩니다. 이는 **행 집합**개체의 현재 챕터를 설정 합니다. 이 속성은 읽기/쓰기가 가능합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>매개 변수  
 *plChapter*  
 챕터의 핸들에 대 한 포인터입니다.  
  
 *LChapter*  
 챕터의 핸들입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK 및 E_FAIL를 포함 하 여 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
