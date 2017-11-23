---
title: "SQLBulkOperations 가진 행을 인출 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84b8e31821e1571da8272806c5fcd7f5563a4182
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>SQLBulkOperations 가진 행을 인출합니다.
에를 호출 하 여 책갈피를 사용 하 여 행 집합에 데이터를 따라 다시 인출 수 수 **SQLBulkOperations 합니다.** 가져와야 하는 행 바인딩된 책갈피 열에 있는 책갈피로 식별 됩니다. 열 값이 SQL_COLUMN_IGNORE는 페치 되지 않습니다.  
  
 수행 된 대량 인출 하려면 **SQLBulkOperations**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  검색 하 고 업데이트할 모든 행의 책갈피를 캐시 합니다. 책갈피; 배열에 저장 됩니다는 둘 이상의 책갈피 열 단위 바인딩을 사용 하는 경우 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 인출 하는 행 수로 설정 하 고 책갈피를 0 열 배열 또는 책갈피 값을 포함 하는 버퍼를 바인딩합니다.  
  
3.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이것이 이진 버퍼 및 SQL_NULL_DATA NULL로 설정할 수 있는 모든 열에 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS의 바이트 길이입니다. 응용 프로그램 (있는 경우)을 해당 기본값으로 설정 된 열 또는 NULL (하나는 그렇지 않습니다) 하는 경우 SQL_COLUMN_IGNORE에 길이/표시기 버퍼의 값을 설정 합니다.  
  
4.  호출 **SQLBulkOperations** 와 *작업* 인수 SQL_FETCH_BY_BOOKMARK로 설정 합니다.  
  
 특정 열에 대해 수행할 작업을 방지 하기 위해 행 작업 배열을 사용 하도록 응용 프로그램에 대 한 않아도가 됩니다. 응용 프로그램 하는 행에 대 한 책갈피만 바인딩된 책갈피 배열에 복사 하 여 인출 된 행을 선택 합니다.
