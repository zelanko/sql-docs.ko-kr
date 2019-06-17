---
title: 키 집합 커서 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6dc5a164220befb534368eace4f51f4dbd84e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213446"
---
# <a name="keyset-driven-cursors"></a>키 집합 커서
키 집합 커서는 변경 내용을 검색 하는 능력에 정적 및 동적 커서 사이 존재 합니다. 정적 커서처럼 항상 결과 집합의 멤버 자격과 순서에 대한 변경 내용을 검색하지는 못합니다. 동적 커서와 같은 결과 (SQL_ATTR_TXN_ISOLATION 연결 특성에서 설정한 대로 트랜잭션 격리 수준)에 따라 집합의 행의 값이 변경 검색지 않습니다 하지.  
  
 키 집합 커서를 열 때 전체 결과 집합에 대 한 키 저장 이 결과 집합의 순서와 명백한 멤버 자격을 수정합니다. 키를 사용 하 여이 커서 결과 집합을 스크롤하면 *keyset* 각 행에 대 한 현재 데이터 값을 검색 합니다. 예를 들어 키 집합 커서 행 및 다른 응용 프로그램을 가져오는 다음 해당 행을 업데이트 합니다. 커서를 다시 행을 발견 하는 값을 경우 새 키를 사용 하는 행에 따라 다시 인출 하기 때문에. 이 때문에 키 집합 커서는 항상 자신 및 다른 사용자가 변경한 내용을 검색 합니다.  
  
 커서가 삭제 된 행을 검색할 때이 행 결과 집합에 "구멍"으로 나타납니다. 행의 키는 키 집합에 있지만 행은 결과 집합에 더 이상 존재하지 않습니다. 행에서 키 값이 업데이트 되 면 이러한 행 결과 집합의 구멍으로도 표시 되도록 행 삭제 되 고 그런 다음 삽입으로 간주 됩니다. 키를 필요에 따라 제거할 수 있지만 키 집합 커서는 항상 검색 하 고 다른 사용자가 삭제 된 행, 행에 대 한 자체에서 삭제 된 키 집합입니다. 이 작업을 수행 하는 키 집합 커서는 자체에서 삭제를 검색할 수 없습니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 되는 특정 키 집합 커서는 자체 삭제를 검색 하는 여부 **SQLGetInfo**합니다.  
  
 키 집합에 이러한 행에 대 한 키 존재 하므로 다른 사용자가 삽입 된 행 키 집합 커서 표시 되지 않습니다. 하지만 키 집합 커서 키 필요에 따라 추가 행에 대 한 삽입 자체 키 집합에 있습니다. 이 작업을 수행 하는 키 집합 커서는 자체 삽입을 검색할 수 있습니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 되는 특정 키 집합 커서는 자체 삽입을 검색 하는 여부 **SQLGetInfo**합니다.  
  
 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정 된 행 상태 배열에는 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR 포함할 수 있습니다. 삭제 또는 삽입 SQL_ROW_UPDATED은 SQL_ROW_DELETED, 또는 업데이트를 검색 하는 행에 대 한 SQL_ROW_ADDED 반환 합니다.  
  
 키 집합 커서는 결과 집합의 각 행에 대 한 키를 포함 하는 임시 테이블을 만들어 일반적으로 구현 됩니다. 커서를이 테이블에 행 버전 관리 정보를 사용 하 여 열 일반적으로 업데이트 된 행에 있는지 여부를 결정 해야 합니다 때문에.  
  
 키 집합 커서는 원래 결과 집합에 대해 스크롤을 임시 테이블을 통해 정적 커서를 엽니다. 원래 결과 집합의 행을 검색 하려면 커서 먼저 임시 테이블에서 적절 한 키를 검색 하 고 행에 대 한 현재 값을 검색 합니다. 블록 커서를 사용 하면 커서는 여러 키와 행 검색 해야 합니다.
