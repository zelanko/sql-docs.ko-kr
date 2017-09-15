---
title: "키 집합 커서 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7cbd7ca159b09ee1482139ef76bfff48115a62bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="keyset-driven-cursors"></a>키 집합 구동 커서
변경 내용을 검색 하는 기능에는 정적 및 동적 커서 사이 있는 키 집합 커서입니다. 정적 커서와 같은 검색 되지 않으면 항상의 멤버 자격과 결과 집합의 순서를 변경 합니다. 동적 커서 등 결과 (영향 SQL_ATTR_TXN_ISOLATION 연결 특성에서 설정한 대로 트랜잭션의 격리 수준) 집합의 값 행의 변경 내용을 검색지 않습니다 것.  
  
 전체 결과 집합에 대 한 키를 저장 한 키 집합 커서를 열 때 결과 집합의 순서와 명백한 멤버 자격을 수정합니다. 키 사용 하 여이 커서 결과 집합을 스크롤하면 *키 집합* 각 행에 대 한 현재 데이터 값을 검색 합니다. 예를 들어 키 집합 커서는 행 및 다른 응용 프로그램을 인출 다음 해당 행을 업데이트 합니다. 경우 커서 다시 행을 발견 하는 값은 새 키를 사용 하 여 행에 따라 다시 인출 하기 때문에 합니다. 이 때문에 키 집합 커서는 항상 자신 및 다른 사용자가 변경한을 검색 합니다.  
  
 이 행 결과 집합의 "구멍"으로 표시 되는 커서는 삭제 된 행을 검색 하려고 하면:, 키 집합에 있는 행에 대 한 키가 존재 하지만 행 결과 집합에 존재 하지 않습니다. 행에서 키 값이 업데이트 되는 경우 행을 결과 집합에 허점이으로 표시 되므로 행 삭제 되 고 그런 다음 삽입으로 간주 됩니다. 키 키 집합 커서는 다른 사용자가 삭제 된 행을 항상 검색할 수 있는 동안 선택적으로 제거할 수 행에 대 한 자체에서 삭제 키 집합입니다. 이 작업을 수행 하는 키 집합 커서는 자체에서 삭제를 검색할 수 없습니다. 특정 키 집합 커서는 자체 삭제를 검색 하는 여부 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다 **SQLGetInfo**합니다.  
  
 키 집합에 이러한 행에 대 한 키 않기 때문에 다른 사용자가 삽입 된 행 키 집합 커서에 표시 되지 않습니다. 그러나 키 집합 커서 추가할 수는 선택적으로 키에 대 한 행을 삽입 자체 키 집합에 있습니다. 이 작업을 수행 하는 키 집합 커서는 자신의 삽입을 검색할 수 있습니다. 특정 키 집합 커서는 자체 삽입을 검색 하는 여부 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다 **SQLGetInfo**합니다.  
  
 행 상태 배열이 SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, 또는 SQL_ROW_ERROR 포함할 수 있습니다. SQL_ROW_UPDATED은 SQL_ROW_DELETED, 또는 SQL_ROW_ADDED로 업데이트 되 고 행에 대 한 삭제 또는 삽입을 반환 합니다.  
  
 키 집합 커서는 결과 집합의 각 행에 대 한 키가 포함 된 임시 테이블을 만들어 일반적으로 구현 됩니다. 커서 행 업데이트 되었는지 여부를 결정 해야,이 테이블 열이 행 버전 관리 정보로 일반적으로 포함 됩니다.  
  
 원래 결과 집합에 대해 스크롤해야 키 집합 커서는 임시 테이블에 대해 정적 커서를 엽니다. 따라서 원래 결과 집합의 행을 검색 하려면 커서 먼저 임시 테이블에서 적절 한 키를 검색 하 고 행에 대 한 현재 값을 검색 합니다. 블록 커서를 사용 하는 경우 커서는 여러 개의 키와 행 검색 해야 합니다.
