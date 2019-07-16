---
title: ODBC 정적 커서 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bcb7c39d39492b91c0b62c5eff2229eb5f61df6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987830"
---
# <a name="odbc-static-cursors"></a>ODBC 정적 커서
정적 커서는 결과 집합 static으로 표시 되는 하나입니다. 멤버 자격, 순서 또는 커서가 열린 후에 결과 집합의 값에 대 한 변경 내용이 일반적으로 감지 하지 못합니다. 예를 들어 정적 커서를 행 및 다른 응용 프로그램을 가져오는 다음 해당 행을 업데이트 합니다. 정적 커서는 행을 다시, 경우에 발견 하는 값을 다른 응용 프로그램에의 한 변경 되더라도 변경 되지 않습니다.  
  
 이렇게 하려면 필요 하지는 않지만 정적 커서는 자체 업데이트, 삭제 및 삽입을 검색할 수 있습니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 되는 특정 정적 커서에 이러한 변경 내용을 감지 하는 여부 **SQLGetInfo**합니다. 정적 커서는 업데이트, 삭제 및 삽입 하는 다른 검색 하지 않습니다.  
  
 SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정 된 행 상태 배열에는 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR 포함할 수 있습니다. 업데이트, 삭제 또는 커서 이러한 변경 내용을 감지할 수는 가정 하 고 커서에 의해 삽입 된 행에 대 한 SQL_ROW_UPDATED은 SQL_ROW_DELETED, 또는 SQL_ROW_ADDED 반환 합니다.  
  
 정적 커서는 일반적으로 결과 집합의 행을 잠그는 방식으로 또는 복사본을 만들어 구현 또는 집합 결과의 스냅숏. 행을 잠가 비교적 쉽게 수행할 수 있지만 동시성이 크게 감소 되는 단점이 있습니다. 복사본 큰 동시성에 대 한 허용 및 자체 업데이트, 삭제를 추적 하는 커서를 허용 하 고 복사본을 수정 하 여 삽입 합니다. 그러나 복사본을 더 많이 듭니다를 확인 하 고 다른 사용자가 해당 데이터는 변경 데이터의 분기 수입니다.
