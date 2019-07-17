---
title: SQLBulkOperations로 행을 삽입 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138918"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>SQLBulkOperations를 사용하여 행 삽입
사용 하 여 데이터 삽입 **SQLBulkOperations** 사용 하 여 데이터를 업데이트 하는 것과 비슷합니다 **SQLBulkOperations** 바인딩된 응용 프로그램 버퍼에서 데이터를 사용 하기 때문에 있습니다.  
  
 새 행의 각 열 값이 있도록 SQL_COLUMN_IGNORE 길이/표시기 값을 사용 하 여 열에 바인딩된 모든 및 바인딩되지 않은 모든 열의 NULL 값을 허용 하거나 기본값이 있습니다.  
  
 행을 삽입할 **SQLBulkOperations**, 다음을 수행 하는 응용 프로그램:  
  
1.  삽입할 행의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 새 데이터 값을 바인딩된 응용 프로그램 버퍼에 배치 합니다. 긴 데이터를 전송 하는 방법에 대 한 내용은 **SQLBulkOperations**를 참조 하십시오 [Long 데이터 및 SQLSetPos 및 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)합니다.  
  
2.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이 값은 이진 버퍼를 NULL로 설정할 열에 SQL_NULL_DATA를 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이입니다. 응용 프로그램 (있는 경우) 해당 기본값으로 설정 된 열 또는 SQL_COLUMN_IGNORE NULL (하나, 없는 경우)의 길이/표시기 버퍼의 값을 설정 합니다.  
  
3.  호출 **SQLBulkOperations** 사용 하 여 합니다 *작업* 인수 SQL_ADD로 설정 합니다.  
  
 이후에 **SQLBulkOperations** 반환 현재 행이 변경 되지 않습니다. 책갈피 열 (0)이 바인딩되어 **SQLBulkOperations** 행 집합 버퍼에 삽입된 된 행의 책갈피는 해당 열에 바인딩된 반환 합니다.
