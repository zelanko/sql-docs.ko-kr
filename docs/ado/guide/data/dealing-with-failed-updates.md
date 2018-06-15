---
title: 실패 한 업데이트 처리 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e5a20e0527f8b30035aef7ff86a90378039b69
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270192"
---
# <a name="dealing-with-failed-updates"></a>실패 한 업데이트 처리
오류가 발생 한 업데이트 완료 하는 경우 오류를 해결 하는 방법을 특성 및 오류의 심각도 및 응용 프로그램의 논리에 따라 다릅니다. 그러나 데이터베이스와 공유 하는 다른 사용자가 일반적인 오류를 수행 하기 전에 필드를 수정 다른 사용자는 합니다. 이러한 종류의 오류 충돌을 이라고 합니다. ADO에서이 상황을 감지 하 고 오류를 보고 합니다.  
  
## <a name="remarks"></a>Remarks  
 업데이트 오류가 있는 경우 오류 처리 루틴에 고정 합니다. 충돌 하는 행만 볼 수 있도록 adFilterConflictingRecords 상수와 레코드 집합을 필터링 합니다. 이 예제에서는 오류 해결 전략은 단지 인쇄 작성자의 성과 이름 (au_fname 및 au_lname).  
  
 사용자 업데이트 충돌을 경고 하는 코드는 다음과 같습니다.  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>관련 항목  
 [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)
