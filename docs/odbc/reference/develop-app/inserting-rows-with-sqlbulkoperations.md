---
title: "SQLBulkOperations 가진 행을 삽입 | Microsoft Docs"
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
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd79255e4cda68d1fd4d425544702e589f44336b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="inserting-rows-with-sqlbulkoperations"></a>SQLBulkOperations 있는 행 삽입
데이터 삽입 **SQLBulkOperations** 사용 하 여 데이터를 업데이트 하는 것과 비슷합니다 **SQLBulkOperations** 바인딩된 응용 프로그램 버퍼에서 데이터를 사용 하기 때문에 있습니다.  
  
 새 행의 각 열 값이 0이 되도록 모든 바운드 열 SQL_COLUMN_IGNORE 길이/표시기 값으로 및 바인딩되지 않은 열을 모든 NULL 값이 허용 하거나 기본값을 갖고 있어야 합니다.  
  
 있는 행을 삽입 **SQLBulkOperations**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성 삽입 행의 수로 설정 되 고 바인딩된 응용 프로그램 버퍼에 새 데이터 값을 배치 합니다. 사용 하 여 긴 데이터를 보내는 방법에 대 한 내용은 **SQLBulkOperations**, 참조 [긴 데이터와 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이것이 이진 버퍼 및 SQL_NULL_DATA NULL로 설정할 수 있는 모든 열에 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS의 바이트 길이입니다. 응용 프로그램 (있는 경우)을 해당 기본값으로 설정 된 열 또는 NULL (하나는 그렇지 않습니다) 하는 경우 SQL_COLUMN_IGNORE에 길이/표시기 버퍼의 값을 설정 합니다.  
  
3.  호출 **SQLBulkOperations** 와 *작업* 인수 SQL_ADD로 설정 합니다.  
  
 후 **SQLBulkOperations** 반환, 현재 행이 변경 되지 않습니다. 책갈피 열 (열 0)에 바인딩된 경우 **SQLBulkOperations** 행 집합 버퍼에 삽입된 된 행의 책갈피는 해당 열에 바인딩된 반환 합니다.
