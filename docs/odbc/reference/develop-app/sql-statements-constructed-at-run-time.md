---
title: 런타임 시 생성 된 SQL 문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0573851ee93bda4aa33e8645148cf2ee66200bee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848101"
---
# <a name="sql-statements-constructed-at-run-time"></a>런타임 시 생성된 SQL 문
일반적으로 임시 분석을 수행 하는 응용 프로그램 런타임 시 SQL 문을 작성 합니다. 예를 들어, 스프레드시트 사용자 데이터를 검색할 열을 선택할 수 있습니다.  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 일반적으로 런타임 시 SQL 문을 생성 하는 다른 수준의 응용 프로그램은 응용 프로그램 개발 환경입니다. 그러나 구성할 문을 작성 하는 것에 일반적으로 최적화 하 고 수 테스트 응용 프로그램에 하드 코딩 됩니다.  
  
 런타임 시 SQL 문을 생성 하는 응용 프로그램 사용자에 게 상당한 유연성을 제공할 수 있습니다. 와 같은 일반적인 작업에도 지원 하지 않는 이전 예제에서 볼 수 있듯이 **여기서** 절 **ORDER BY** 절 또는 조인에 런타임 시 SQL 문 생성은 크게 복잡 문보다 하드 코딩 합니다. 또한 이러한 응용 프로그램을 테스트 이므로 문제가 있는 임의 개수의 SQL 문 생성할 수 있습니다.  
  
 런타임 시 SQL 문을 생성 하는 잠재적인 단점은 하드 코드 된 문을 사용 하 여 보다 문을 생성 하는 데 훨씬 더 많은 시간이 걸리는 경우 다행 스럽게도이 문제가 거의 없습니다. 이러한 응용 프로그램 사용자 인터페이스를 많이 사용 되며 응용 프로그램 소요 시간 경향이 SQL 문 생성은 일반적으로 작지만 사용자 입력 조건과 데 걸린 시간을 비교 합니다.
