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
ms.openlocfilehash: 0701218b5ef489d1f8962ffadc9409986a0c36c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942813"
---
# <a name="updating-data-overview"></a>데이터 업데이트 개요
응용 프로그램은 SQL 문을 실행 하거나 **SQLSetPos** 또는 **SQLBulkOperations**를 호출 하 여 데이터를 업데이트할 수 있습니다. **UPDATE**, **DELETE**및 **INSERT** 문은 데이터 원본에서 직접 작동 하며 일반적으로 드라이버에서 지원 됩니다. 검색 된 update 및 delete 문에는 변경할 행 사양이 포함 되어 있습니다. 위치 지정 update 및 delete 문과 **SQLSetPos** 는 커서를 통해 데이터 원본에 대해 작동 하며 광범위 하 게 지원 됩니다.  
  
 이 섹션에서 설명 하는 메서드를 사용 하 여 커서에서 결과 집합에 대 한 변경 내용을 검색할 수 있는지 여부는 커서의 형식 및 구현 방법에 따라 달라 집니다. 앞 으로만 이동 가능한 커서는 행을 다시 방문 하지 않으므로 변경 내용을 검색 하지 않습니다. 스크롤할 수 있는 커서가 변경 내용을 검색할 수 있는지 여부에 대 한 자세한 내용은 [스크롤 가능한 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [UPDATE, DELETE 및 INSERT 문](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [현재 위치 업데이트 및 Delete 문 시뮬레이션](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [영향을 받는 행 수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos를 사용하여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations로 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
