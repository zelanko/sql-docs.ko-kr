---
title: "SQLBulkOperations 사용 하 여 책갈피에서 행 삭제 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db7e04c5bf76855afdb24676c905c5cccbc60cbc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations 사용 하 여 책갈피에서 행 삭제
책갈피를 하 여 행을 삭제할 때 **SQLBulkOperations** 은 데이터 원본 테이블의 하나 이상의 선택 된 행을 삭제 합니다. 행 바인딩된 책갈피 열에서 책갈피도 식별 됩니다.  
  
 사용 하 여 책갈피에서 행을 삭제 하려면 **SQLBulkOperations**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  검색 하 고 삭제할 모든 행의 책갈피를 캐시 합니다. 책갈피; 배열에 저장 됩니다는 둘 이상의 책갈피 열 단위 바인딩을 사용 하는 경우 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  책갈피의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 책갈피를 0 열 배열 또는 책갈피 값을 포함 하는 버퍼를 바인딩합니다.  
  
3.  호출 **SQLBulkOperations** 와 *작업* SQL_DELETE_BY_BOOKMARK로 설정 합니다.

