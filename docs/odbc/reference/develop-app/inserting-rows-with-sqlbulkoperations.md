---
title: SQLBulkOperations를 사용 하 여 행 삽입 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05b8f71d6f4c885c7dc64887dd92b1f600005ca7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138918"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>SQLBulkOperations를 사용하여 행 삽입
**SQLBulkOperations** 를 사용 하 여 데이터를 삽입 하는 것은 바인딩된 응용 프로그램 버퍼의 데이터를 사용 하므로 **SQLBulkOperations** 로 데이터를 업데이트 하는 것과 비슷합니다  
  
 그러면 새 행의 각 열에 값이 포함 되 고, SQL_COLUMN_IGNORE 길이/표시기 값과 모든 바인딩되지 않은 열은 NULL 값을 허용 하거나 기본값을 가져야 합니다.  
  
 **SQLBulkOperations**를 사용 하 여 행을 삽입 하기 위해 응용 프로그램은 다음을 수행 합니다.  
  
1.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 삽입할 행 수로 설정 하 고 새 데이터 값을 바인딩된 응용 프로그램 버퍼에 배치 합니다. **SQLBulkOperations**를 사용 하 여 long 데이터를 전송 하는 방법에 대 한 자세한 내용은 [Long data 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)를 참조 하세요.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼에 값을 설정 합니다. 이는 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열의 데이터 바이트 길이, NULL로 설정 될 열에 대 한 SQL_NULL_DATA입니다. 응용 프로그램은 기본값 (있는 경우) 또는 NULL (있는 경우 SQL_COLUMN_IGNORE)로 설정 될 열에 대 한 길이/표시기 버퍼의 값을 설정 합니다 (있는 경우).  
  
3.  SQL_ADD로 설정 된 *Operation* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 합니다.  
  
 **SQLBulkOperations** 가 반환 된 후에는 현재 행이 변경 되지 않습니다. 책갈피 열 (열 0)이 바인딩된 경우 **SQLBulkOperations** 는 해당 열에 바인딩된 행 집합 버퍼에 삽입 된 행의 책갈피를 반환 합니다.
