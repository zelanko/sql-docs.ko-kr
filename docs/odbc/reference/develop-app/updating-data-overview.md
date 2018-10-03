---
title: 데이터 업데이트 개요 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3edbd41bc5361d864abcc7d631a90521af98ef01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777832"
---
# <a name="updating-data-overview"></a>데이터 업데이트 개요
SQL 문을 실행 하 여 또는 호출 하 여 응용 프로그램 데이터를 업데이트할 수 있습니다 **SQLSetPos** 하거나 **SQLBulkOperations**합니다. **업데이트**, **삭제**, 및 **삽입** 문 데이터 원본에 직접 작업할 및 드라이버에서 일반적으로 지원 됩니다. 업데이트 검색 및 delete 문을 변경 하려면 행에 대 한 사양 포함 합니다. 배치 업데이트 및 delete 문 및 **SQLSetPos** 커서를 통해 데이터 원본에서 역할 및 널리 지원 됩니다.  
  
 커서 결과 집합을이 섹션에서 설명 하는 방법에 대 한 변경 내용을 감지할 수 있는지 여부를 구현 하는 방법 및 커서의 유형에 따라 달라 집니다. 정방향 전용 커서 행 다시 방문 하지 않습니다 하 고 변경 내용을 검색 하지 않습니다. 스크롤 가능 커서 변경을 검색할 수 있는지 여부에 대 한 자세한 내용은 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [UPDATE, DELETE 및 INSERT 문](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문 시뮬레이션](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos를 사용하여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations로 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
