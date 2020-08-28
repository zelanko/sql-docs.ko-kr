---
description: 일괄 처리 모드
title: 일괄 처리 모드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: rothja
ms.author: jroth
ms.openlocfilehash: a2cda3a14dc51532d52184f8b2101981d4f36cd3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991604"
---
# <a name="batch-mode"></a>일괄 처리 모드
배치 모드는 **LockType** 속성이 **Adlockbatchoptimistic** 으로 설정 되 고 일괄 업데이트가 공급자에 의해 지원 되는 경우에 적용 됩니다. 특정 잠금 유형 설정은 커서 위치에 따라 사용할 수 없습니다. 예를 들어 **CursorLocation** 이 **adUseClient**로 설정 된 경우 비관적 잠금 유형을 사용할 수 없습니다. 반대로 커서 위치가 서버에 있는 경우에는 공급자가 일괄 처리 낙관적 잠금을 지원할 수 없습니다. 일괄 처리 업데이트는 키 집합 또는 정적 커서로만 사용 해야 합니다.  
  
 **UpdateBatch** 메서드는 복사 버퍼에 저장 된 **레코드 집합** 변경 내용을 서버에 전송 하 여 데이터 원본을 업데이트 하는 데 사용 됩니다. 다음 섹션에서는 일괄 처리 모드로 **레코드 집합** 을 열고, 복사 버퍼를 변경한 다음, **UpdateBatch**호출을 사용 하 여 변경 내용을 데이터 원본으로 보냅니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [업데이트 전송: UpdateBatch 메서드](./sending-the-updates-updatebatch-method.md)  
  
-   [업데이트된 레코드 필터링](./filtering-for-updated-records.md)  
  
-   [실패한 업데이트 처리](./dealing-with-failed-updates.md)  
  
-   [충돌 감지 및 해결](./detecting-and-resolving-conflicts.md)  
  
-   [레코드 집합 연결 끊기 및 다시 연결](./disconnecting-and-reconnecting-the-recordset.md)  
  
-   [조인된 결과 업데이트: 고유한 테이블](./updating-joined-results-unique-table.md)