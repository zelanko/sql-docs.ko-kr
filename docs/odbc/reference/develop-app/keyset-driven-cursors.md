---
title: 키셋 기반 커서 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306208"
---
# <a name="keyset-driven-cursors"></a>키 집합 커서
키집합 기반 커서는 정적 커서와 동적 커서 사이에 있으며 변경 내용을 감지합니다. 정적 커서처럼 항상 결과 집합의 멤버 자격과 순서에 대한 변경 내용을 검색하지는 못합니다. 동적 커서와 마찬가지로 결과 집합의 행 값에 대한 변경 내용을 감지합니다(SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정된 트랜잭션 격리 수준에 따라 다수 있음).  
  
 키 집합 기반 커서가 열리면 전체 결과 집합에 대한 키가 저장됩니다. 이렇게 하면 결과 집합의 명백한 멤버 자격 및 순서가 수정됩니다. 커서가 결과 집합을 스크롤할 때 이 키 *집합의* 키를 사용하여 각 행의 현재 데이터 값을 검색합니다. 예를 들어 키집합 기반 커서가 행을 가져오고 다른 응용 프로그램이 해당 행을 업데이트한다고 가정합니다. 커서가 행을 다시 가져오는 경우 해당 키를 사용하여 행을 다시 가져오기 때문에 표시되는 값은 새 값입니다. 따라서 키 집합 기반 커서는 항상 자신과 다른 사용자가 변경한 내용을 감지합니다.  
  
 커서가 삭제된 행을 검색하려고 하면 이 행이 결과 집합의 "구멍"으로 나타납니다. 행의 키 값이 업데이트되면 행이 삭제된 다음 삽입된 것으로 간주되므로 이러한 행도 결과 집합의 구멍으로 나타납니다. 키집합 기반 커서는 다른 사용자가 삭제한 행을 항상 검색할 수 있지만 선택적으로 키 집합에서 자신을 삭제하는 행에 대한 키를 제거할 수 있습니다. 이렇게 하는 키집합 기반 커서는 자체 삭제를 검색할 수 없습니다. 특정 키 집합 기반 커서가 자체 삭제를 감지하는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고됩니다.  
  
 다른 사용자가 삽입한 행은 키 집합에 대한 키가 키 집합에 없기 때문에 키 집합 기반 커서에 표시되지 않습니다. 그러나 키 집합 기반 커서는 키 집합에 자신을 삽입하는 행에 대한 키를 선택적으로 추가할 수 있습니다. 이를 수행하는 키집합 기반 커서는 자체 삽입을 검색할 수 있습니다. 특정 키 집합 기반 커서가 자체 삽입을 감지하는지 여부는 **SQLGetInfo의**SQL_STATIC_SENSITIVITY 옵션을 통해 보고됩니다.  
  
 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정된 행 상태 배열은 모든 행에 대한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 또는 SQL_ROW_ERROR 포함할 수 있습니다. 업데이트, 삭제 또는 삽입된 것으로 감지되는 행에 대해 SQL_ROW_UPDATED, SQL_ROW_DELETED 또는 SQL_ROW_ADDED 반환합니다.  
  
 키집합 기반 커서는 일반적으로 결과 집합의 각 행에 대한 키가 포함된 임시 테이블을 만들어 구현됩니다. 커서도 행이 업데이트되었는지 여부를 결정해야 하므로 이 테이블에는 일반적으로 행 버전 지정 정보가 포함된 열도 포함됩니다.  
  
 원래 결과 집합을 스크롤하려면 키집합 기반 커서가 임시 테이블 위에 정적 커서를 엽니다. 원래 결과 집합에서 행을 검색하려면 커서는 먼저 임시 테이블에서 적절한 키를 검색한 다음 행의 현재 값을 검색합니다. 블록 커서를 사용하는 경우 커서는 여러 키와 행을 검색해야 합니다.
