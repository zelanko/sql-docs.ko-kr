---
title: "SQLBulkOperations로 책갈피에서 행이 업데이트 | Microsoft Docs"
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
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4426465ea41b257a4805399b703f28ccc22d704b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations 사용 하 여 책갈피에서 업데이트 행
책갈피를 하 여 행을 업데이트할 때 **SQLBulkOperations** 은 데이터 원본 테이블의 하나 이상의 행을 업데이트 합니다. 행 바인딩된 책갈피 열에서 책갈피도 식별 됩니다. 행 (열에 대 한 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE) 제외 바인딩된 각 열에 대 한 응용 프로그램 버퍼에서 데이터를 사용 하 여 업데이트 됩니다. 바인딩되지 않은 열을 업데이트 되지 않습니다.  
  
 행을 업데이트 하 여 사용 하 여 책갈피 **SQLBulkOperations**, 응용 프로그램:  
  
1.  검색 하 고 업데이트할 모든 행의 책갈피를 캐시 합니다. 책갈피; 배열에 저장 됩니다는 둘 이상의 책갈피 열 단위 바인딩을 사용 하는 경우 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  책갈피의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 책갈피를 0 열 배열 또는 책갈피 값을 포함 하는 버퍼를 바인딩합니다.  
  
3.  행 집합 버퍼에 새 데이터 값을 배치합니다. 사용 하 여 긴 데이터를 보내는 방법에 대 한 내용은 **SQLBulkOperations**, 참조 [긴 데이터와 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
4.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이것이 이진 버퍼 및 SQL_NULL_DATA NULL로 설정할 수 있는 모든 열에 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS의 바이트 길이입니다.  
  
5.  SQL_COLUMN_IGNORE 하도록 업데이트 되지 않는 이러한 열의 길이/표시기 버퍼의 값을 설정 합니다. 응용 프로그램이 기존 데이터를 다시 전송 하 여이 단계를 건너뛸 수, 있지만이 비효율적 이며 잘렸습니다. 읽을 때 데이터 원본에 값을 보내는 위험 합니다.  
  
6.  호출 **SQLBulkOperations** 와 *작업* 인수 SQL_UPDATE_BY_BOOKMARK로 설정 합니다.  
  
 업데이트로 데이터 원본에 전송 된 모든 행에 대해 응용 프로그램 버퍼에 유효한 행 데이터가 있어야 합니다. 행 상태 배열이 유지 되 경우 응용 프로그램 버퍼를 인출 하 여 기록한 및은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 행에 대 한 상태 값이 잘못 된 데이터가 데이터 원본에 실수로 보낼 수 있습니다.

