---
title: 레코드로 이동 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cead84eed4e7689d6b5df907b6a61ef07ab74e8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924921"
---
# <a name="jumping-to-a-record"></a>레코드로 이동
합니다 [이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드를 사용 하면에서 앞 이나 뒤로 이동할 수 있습니다 합니다 **레코드 집합** 다음 구문을 사용 하 여 레코드의 지정 된 수:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>설명  
 합니다 **이동** 메서드는 모든 지원 **레코드 집합** 개체입니다.  
  
 경우는 *NumRecords* 인수가 0 보다 큰 레코드의 현재 위치를 앞으로 이동 (의 끝에 다가가 합니다 **Recordset**). 하는 경우 *NumRecords* 가 현재 레코드 위치 뒤로 이동 0 보다 작은 (의 시작 부분을 향해 합니다 **레코드 집합**).  
  
 경우는 **이동** 호출에서 현재 레코드 위치 첫 번째 레코드 앞의 위치를 이동, ADO의 첫 번째 레코드 앞의 위치는 현재 레코드를 설정 합니다. 합니다 **레코드 집합** (**BOF** 됩니다 **True**). 이전 버전과 경우 이동 하려고 합니다 **BOF** 속성은 이미 **True** 오류를 생성 합니다.  
  
 경우는 **이동** 호출 지점에 마지막 레코드 뒤에 현재 레코드 위치를 이동는, ADO의 마지막 레코드 다음 위치에 현재 레코드를 설정 합니다 **Recordset** (**EOF** 됩니다 **True**). 경우에 앞으로 이동 하려고 합니다 **EOF** 속성이 이미 **True** 오류를 생성 합니다.  
  
 호출을 **이동** 빈 메서드에서 **레코드 집합** 개체에 오류가 발생 합니다.  
  
 책갈피를 전달 하는 경우는 *시작* 인수에이 책갈피를 사용 하 여 레코드를 기준으로 이동 가정 합니다 **레코드 집합** 개체에서 책갈피를 지원 합니다. 책갈피를 사용 하 여 가져온 합니다 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성입니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 사용 중인 경우는 **CacheSize** 로컬로 전달 공급자에서 레코드를 캐시 하는 속성을 *NumRecords* 그룹 외부의 현재 캐시 된 레코드의 현재 레코드 위치를 이동 하는 인수 대상 레코드에서 시작 하는 레코드의 새 그룹을 검색 하는 ADO를 강제로 수행 합니다. 합니다 **CacheSize** 새로 검색된 된 그룹의 크기를 결정 하는 속성 및 대상 레코드는 첫 번째 레코드를 검색 합니다.
