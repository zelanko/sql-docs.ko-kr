---
title: 실패 한 업데이트 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d442a9c397ad184658f9101343e139697c9b3756
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925633"
---
# <a name="dealing-with-failed-updates"></a>실패한 업데이트 처리
업데이트를 종료 하는 경우 오류를 해결 하는 방법은 오류 및 응용 프로그램의 논리에 대 한 특성 및 심각도에 따라 달라 집니다. 그러나 데이터베이스가 다른 사용자와 공유 되는 경우 일반적인 오류는 다른 사용자가 필드를 수정 하는 것입니다. 이러한 유형의 오류를 충돌 이라고 합니다. ADO에서이 상황을 감지 하 고 오류를 보고 합니다.  
  
## <a name="remarks"></a>설명  
 업데이트 오류가 발생 하면 오류 처리 루틴에 트래핑 됩니다. 충돌 하는 행만 표시 되도록 adFilterConflictingRecords 상수를 사용 하 여 레코드 집합을 필터링 합니다. 이 예제에서 오류 해결 전략은 단순히 저자의 성과 이름을 인쇄 하는 것입니다 (au_fname 및 au_lname).  
  
 사용자에 게 업데이트 충돌을 경고 하는 코드는 다음과 같습니다.  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>참고 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
