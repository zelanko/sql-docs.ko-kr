---
title: SQLBulkOperations로 책갈피를 사용 하 여 행 업데이트 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c755297e8beadad92b5be81d78ca534bb96ecae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283201"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 업데이트
책갈피를 사용 하 여 행을 업데이트할 때 **SQLBulkOperations** 는 데이터 원본이 하나 이상의 테이블 행을 업데이트 하도록 합니다. 행은 바인딩된 책갈피 열의 책갈피에 의해 식별 됩니다. 행은 각 바인딩된 열에 대해 응용 프로그램 버퍼의 데이터를 사용 하 여 업데이트 됩니다 (열에 대 한 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 경우 제외). 바인딩되지 않은 열은 업데이트 되지 않습니다.  
  
 **SQLBulkOperations**로 책갈피를 사용 하 여 행을 업데이트 하려면 응용 프로그램:  
  
1.  업데이트할 모든 행의 책갈피를 검색 하 고 캐시 합니다. 책갈피와 열 단위 바인딩이 모두 사용 되는 경우 책갈피는 배열에 저장 됩니다. 책갈피와 행 단위 바인딩이 모두 사용 되는 경우 책갈피는 행 구조의 배열에 저장 됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 책갈피의 개수로 설정 하 고 책갈피 값 또는 책갈피의 배열을 포함 하는 버퍼를 열 0에 바인딩합니다.  
  
3.  새 데이터 값을 행 집합 버퍼에 배치 합니다. **SQLBulkOperations**를 사용 하 여 long 데이터를 전송 하는 방법에 대 한 자세한 내용은 [Long data 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조 하세요.  
  
4.  필요에 따라 각 열의 길이/표시기 버퍼에 값을 설정 합니다. 이는 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열의 데이터 바이트 길이, NULL로 설정 될 열에 대 한 SQL_NULL_DATA입니다.  
  
5.  SQL_COLUMN_IGNORE 업데이트 하지 않을 열의 길이/표시기 버퍼에 값을 설정 합니다. 응용 프로그램에서이 단계를 건너뛰고 기존 데이터를 다시 보낼 수 있지만이는 데이터를 읽을 때 잘린 데이터 원본에 값을 보내는 위험과 비효율적입니다.  
  
6.  SQL_UPDATE_BY_BOOKMARK로 설정 된 *Operation* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 합니다.  
  
 데이터 원본에 업데이트로 전송 되는 모든 행의 경우 응용 프로그램 버퍼에 올바른 행 데이터가 있어야 합니다. 가져오기를 통해 응용 프로그램 버퍼를 채운 경우 행 상태 배열이 유지 관리 되 고 행의 상태 값이 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 이면 잘못 된 데이터를 실수로 데이터 원본으로 보낼 수 있습니다.
