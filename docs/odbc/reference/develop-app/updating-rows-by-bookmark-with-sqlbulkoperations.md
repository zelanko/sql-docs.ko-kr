---
title: SQLBulkOperations를 통해 책갈피별로 행 업데이트 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283201"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 업데이트
책갈피별로 행을 업데이트할 때 **SQLBulkOperations는** 데이터 원본이 테이블의 하나 이상의 행을 업데이트합니다. 행은 바인딩된 책갈피 열의 책갈피로 식별됩니다. 행은 각 바인딩된 열에 대한 응용 프로그램 버퍼의 데이터를 사용하여 업데이트됩니다(열의 길이/표시기 버퍼의 값이 SQL_COLUMN_IGNORE 경우 제외). 언바운드 열은 업데이트되지 않습니다.  
  
 **SQLBulkOperations**, 응용 프로그램을 사용하여 책갈피별로 행을 업데이트하려면 다음을 수행합니다.  
  
1.  업데이트할 모든 행의 책갈피를 검색하고 캐시합니다. 두 개 이상의 책갈피와 열별 바인딩이 사용되는 경우 책갈피는 배열에 저장됩니다. 책갈피와 행별 바인딩이 두 개 이상 사용되는 경우 책갈피는 행 구조의 배열에 저장됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 책갈피 수로 설정하고 책갈피 값 또는 책갈피 배열을 포함하는 버퍼를 열 0에 바인딩합니다.  
  
3.  행 집합 버퍼에 새 데이터 값을 배치합니다. **SQLBulkOperations를**사용하여 긴 데이터를 보내는 방법에 대한 자세한 내용은 [긴 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조하십시오.  
  
4.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정합니다. 문자열 버퍼에 바인딩된 열에 대한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열에 대한 데이터의 바이트 길이 및 NULL로 설정될 모든 열에 대한 SQL_NULL_DATA.  
  
5.  SQL_COLUMN_IGNORE 위해 업데이트할 열의 길이/표시기 버퍼에 값을 설정합니다. 응용 프로그램이 이 단계를 건너뛰고 기존 데이터를 다시 보낼 수 있지만 이는 비효율적이며 읽을 때 잘린 데이터 원본으로 값을 보낼 위험이 있습니다.  
  
6.  SQL_UPDATE_BY_BOOKMARK 설정된 *작업* 인수를 사용하여 **SQLBulkOperations를** 호출합니다.  
  
 업데이트로 데이터 원본으로 전송되는 모든 행에 대해 응용 프로그램 버퍼에는 유효한 행 데이터가 있어야 합니다. 응용 프로그램 버퍼가 가져오기로 채워진 경우 행 상태 배열이 유지되고 행의 상태 값이 SQL_ROW_DELETED 경우 SQL_ROW_ERROR 또는 SQL_ROW_NOROW 잘못된 데이터가 실수로 데이터 원본으로 전송될 수 있습니다.
