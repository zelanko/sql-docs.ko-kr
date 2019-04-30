---
title: SQLBulkOperations로 책갈피 별로 행 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f0c59324542793301965c7d3555cf35ad40f5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194392"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 업데이트
책갈피에서 행을 업데이트할 때 **SQLBulkOperations** 데이터 원본에서 테이블의 하나 이상의 행을 업데이트 합니다. 행 바인딩된 책갈피 열에 책갈피를 통해 식별 됩니다. 행 (열에 대 한 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE) 제외 바인딩된 각 열에 대 한 응용 프로그램 버퍼에 데이터를 사용 하 여 업데이트 됩니다. 바인딩되지 않은 열을 업데이트 되지 않습니다.  
  
 로 책갈피 별로 행 업데이트 **SQLBulkOperations**, 응용 프로그램:  
  
1.  검색 하 고 업데이트할 모든 행의 책갈피를 캐시 합니다. 둘 이상의 책갈피가 열 단위 바인딩을 사용 하 고 책갈피; 배열에 저장 됩니다. 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  책갈피의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 책갈피 또는 책갈피를 0 열에 배열을 포함 하는 버퍼를 바인딩합니다.  
  
3.  행 집합 버퍼에 새 데이터 값을 배치합니다. 긴 데이터를 전송 하는 방법에 대 한 내용은 **SQLBulkOperations**를 참조 하십시오 [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
4.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이 값은 이진 버퍼를 NULL로 설정할 열에 SQL_NULL_DATA를 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이입니다.  
  
5.  SQL_COLUMN_IGNORE 업데이트할 필요가 있는 해당 열의 길이/표시기 버퍼의 값을 설정 합니다. 응용 프로그램이 기존 데이터를 다시 전송 하 여이 단계를 건너뛸 수, 있지만이 비효율적 이며 잘렸습니다. 읽을 때 데이터 원본에 값을 보내는 위험 합니다.  
  
6.  호출 **SQLBulkOperations** 사용 하 여 합니다 *작업* 인수 SQL_UPDATE_BY_BOOKMARK로 설정 합니다.  
  
 업데이트로 데이터 원본에 전송 되는 모든 행에 대해 응용 프로그램 버퍼가 유효한 행 데이터가 있어야 합니다. 행 상태 배열이 유지 관리 하는 경우 응용 프로그램 버퍼를 인출 하 여 채워진를 행에 대 한 상태 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW은 잘못 된 데이터가 데이터 원본에 실수로 보낼 수 있습니다.
