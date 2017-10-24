---
title: "모드를 일괄 처리 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92e249a7c2d5b0c01e291f4829d5c4f8c580fb2c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="batch-mode"></a>일괄 처리 모드
일괄 처리 모드가 설정 되어 때는 **LockType** 속성이 **adLockBatchOptimistic** 공급자 일괄 처리 업데이트를 지원 합니다. 특정 잠금 유형 설정은 커서 위치에 따라 사용할 수 있습니다. 예를 들어, 비관적 잠금 유형에 사용할 수 없는 경우는 **앞** 로 설정 된 **adUseClient**합니다. 반대로, 공급자는 커서 위치는 서버에 있으면 일괄 처리 낙관적 잠금을 지원할 수 없습니다. 키 집합 또는 정적 커서에만 사용 하 여 업데이트 하는 일괄 처리를 사용 해야 합니다.  
  
 **UpdateBatch** 메서드는 보내는 데 사용 되 **레코드 집합** 변경 내용이 데이터 소스를 업데이트 하려면 서버에 복사 버퍼에 유지 합니다. 다음 섹션에서 열립니다는 **레코드 집합** 일괄 처리 모드에서 복사 버퍼에 변경을 수행 하 고 다음에 대 한 호출을 사용 하 여 데이터 원본에 변경 내용을 보내는 **UpdateBatch**합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [업데이트 전송: UpdateBatch 메서드](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [업데이트된 레코드 필터링](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [실패한 업데이트 처리](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [충돌 감지 및 해결](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [레코드 집합 연결 끊기 및 다시 연결](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [JOIN 결과 업데이트: 고유한 테이블](../../../ado/guide/data/updating-joined-results-unique-table.md)

