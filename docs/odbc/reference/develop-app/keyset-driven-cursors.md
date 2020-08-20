---
description: 키 집합 커서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c34432481eeafd6bed938dcd1275e33583d33cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476595"
---
# <a name="keyset-driven-cursors"></a>키 집합 커서
키 집합 커서는 변경 내용을 검색 하는 기능에서 정적 커서와 동적 커서 사이에 있습니다. 정적 커서처럼 항상 결과 집합의 멤버 자격과 순서에 대한 변경 내용을 검색하지는 못합니다. 동적 커서와 같이 결과 집합의 행 값에 대 한 변경 내용을 검색 합니다 (SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정 됨).  
  
 키 집합 커서를 열 때 전체 결과 집합에 대 한 키를 저장 합니다. 이렇게 하면 결과 집합의 멤버 및 순서가 명확 하 게 수정 됩니다. 커서는 결과 집합을 스크롤할 때이 키 *집합* 의 키를 사용 하 여 각 행에 대 한 현재 데이터 값을 검색 합니다. 예를 들어 키 집합 커서에서 행을 인출 하 고 다른 응용 프로그램에서 해당 행을 업데이트 한다고 가정 합니다. 커서가 행을 refetches 하는 경우 해당 키를 사용 하 여 행을 다시 사용 하기 때문에 새 값이 표시 됩니다. 이로 인해 키 집합 커서는 항상 자신이 변경한 내용 및 다른 커서를 검색 합니다.  
  
 커서가 삭제 된 행을 검색 하려고 하면이 행이 결과 집합에 "구멍"으로 표시 됩니다. 행 키가 키 집합에 있지만 결과 집합에 행이 더 이상 존재 하지 않습니다. 행의 키 값이 업데이트 되는 경우 행이 삭제 된 후 삽입 된 것으로 간주 되므로 이러한 행도 결과 집합에 구멍으로 표시 됩니다. 키 집합 커서는 다른 사용자가 삭제 한 행을 항상 검색할 수 있지만, 선택적으로 키 집합에서 삭제 되는 행의 키를 제거할 수 있습니다. 이를 수행 하는 키 집합 커서는 자신의 삭제를 검색할 수 없습니다. 특정 키 집합 커서에서 자체 삭제를 감지 하는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다.  
  
 키 집합에 해당 행에 대 한 키가 없기 때문에 다른 사용자가 삽입 한 행은 키 집합 커서에 표시 되지 않습니다. 그러나 키 집합 커서는 선택적으로 삽입 하는 행의 키를 키 집합에 추가할 수 있습니다. 이를 수행 하는 키 집합 커서는 자체 삽입을 감지할 수 있습니다. 특정 키 집합 커서에서 자체 삽입을 감지 하는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다.  
  
 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 지정 된 행 상태 배열에는 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 또는 SQL_ROW_ERROR 포함 될 수 있습니다. 업데이트, 삭제 또는 삽입 됨으로 검색 되는 행에 대 한 SQL_ROW_UPDATED, SQL_ROW_DELETED 또는 SQL_ROW_ADDED를 반환 합니다.  
  
 키 집합 커서는 일반적으로 결과 집합의 각 행에 대 한 키가 포함 된 임시 테이블을 만들어 구현 합니다. 커서는 행이 업데이트 되었는지 여부도 결정 해야 하기 때문에이 테이블에는 행 버전 관리 정보를 포함 하는 열도 포함 되어 있습니다.  
  
 원래 결과 집합을 스크롤할 때 키 집합 커서는 임시 테이블에 대해 정적 커서를 엽니다. 원래 결과 집합에서 행을 검색 하기 위해 커서는 먼저 임시 테이블에서 적절 한 키를 검색 한 다음 해당 행에 대 한 현재 값을 검색 합니다. 블록 커서를 사용 하는 경우 커서는 여러 키와 행을 검색 해야 합니다.
