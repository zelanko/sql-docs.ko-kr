---
title: SQLBulk연산으로 행 삽입 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a6fa384292f02026b8390aa92525144dce6f549b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300113"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>SQLBulkOperations를 사용하여 행 삽입
**SQLBulkOperations를** 사용하여 데이터를 삽입하는 것은 바인딩된 응용 프로그램 버퍼의 데이터를 사용하기 때문에 **SQLBulkOperations를** 사용하여 데이터를 업데이트하는 것과 유사합니다.  
  
 새 행의 각 열에 값이 있으므로 길이/표시기 값이 SQL_COLUMN_IGNORE 모든 바인딩된 열과 모든 unbound 열은 NULL 값을 수락하거나 기본값을 가져야 합니다.  
  
 **SQLBulkOperations를**사용하여 행을 삽입하려면 응용 프로그램은 다음을 수행합니다.  
  
1.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 삽입할 행 수로 설정하고 바인딩된 응용 프로그램 버퍼에 새 데이터 값을 배치합니다. **SQLBulkOperations를**사용하여 긴 데이터를 보내는 방법에 대한 자세한 내용은 [긴 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조하십시오.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정합니다. 문자열 버퍼에 바인딩된 열에 대한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열에 대한 데이터의 바이트 길이 및 NULL로 설정될 모든 열에 대한 SQL_NULL_DATA. 응용 프로그램은 SQL_COLUMN_IGNORE 위해 기본값(있는 경우) 또는 NULL(그렇지 않은 경우)으로 설정될 해당 열의 길이/표시기 버퍼에서 값을 설정합니다.  
  
3.  SQL_ADD 설정된 *작업* 인수를 사용하여 **SQLBulkOperations를** 호출합니다.  
  
 **SQLBulkOperations가** 반환되면 현재 행은 변경되지 않습니다. 책갈피 열(열 0)이 바인딩된 경우 **SQLBulkOperations는** 해당 열에 바인딩된 행 집합 버퍼에 삽입된 행의 책갈피를 반환합니다.
