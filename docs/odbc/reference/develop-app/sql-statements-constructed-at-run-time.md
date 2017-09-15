---
title: "런타임 시 구성 하는 SQL 문을 | Microsoft Docs"
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
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ccd79048c250c73867752ebaf0b2b7060a6c19b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-statements-constructed-at-run-time"></a>런타임 시 구성 하는 SQL 문
일반적으로 임시 분석을 수행 하는 응용 프로그램 런타임 시 SQL 문을 작성 합니다. 예를 들어 스프레드시트에서 데이터를 검색할 열을 선택 하는 사용자를 허용 수 있습니다.:  
  
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
  
 일반적으로 런타임 시 SQL 문을 생성 하는 응용 프로그램의 다른 클래스는 응용 프로그램 개발 환경입니다. 그러나 구성할 문을 작성 하는 것, 여기서은 일반적으로 최적화 된 및 테스트할 수 응용 프로그램에 하드 코드 됩니다.  
  
 런타임 시 SQL 문을 생성 하는 응용 프로그램 사용자에 게 엄청난 유연성을 제공할 수 있습니다. 와 같은 일반적인 작업에도 지원 하지 않는 이전 예제에서 볼 수 있듯이 **여기서** 절 **ORDER BY** 절 또는 런타임 시 SQL 문을 구성 하는 조인에는 훨씬 더 복잡 한 문보다 하드 코딩 합니다. 또한 이러한 응용 프로그램 테스트 문제가 될 수는 임의 개수의 SQL 문 생성할 수 있습니다.  
  
 런타임 시 SQL 문을 생성할 수 있다는 단점이 하드 코드 된 문을 사용 하 여 보다는 문을 생성 하는 데 훨씬 더 많은 시간이 걸리는 경우 다행히이 중요 하지 않은 작업은 거의 없습니다. 이러한 응용 프로그램 사용자 인터페이스를 많이 사용 하 고 응용 프로그램 소요 시간 경향이 SQL 문을 구성 작습니다. 일반적으로 사용자 입력 기준을 소요 시간과 비교 합니다.
