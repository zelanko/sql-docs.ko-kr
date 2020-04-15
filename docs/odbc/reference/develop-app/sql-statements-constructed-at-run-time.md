---
title: 런타임에 생성된 SQL 문 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301974"
---
# <a name="sql-statements-constructed-at-run-time"></a>런타임 시 생성된 SQL 문
임시 분석을 수행하는 응용 프로그램은 일반적으로 런타임에 SQL 문을 작성합니다. 예를 들어 스프레드시트를 사용하면 사용자가 데이터를 검색할 열을 선택할 수 있습니다.  
  
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
  
 런타임에 SQL 문을 일반적으로 구성하는 또 다른 응용 프로그램 클래스는 응용 프로그램 개발 환경입니다. 그러나 구성하는 문은 일반적으로 최적화및 테스트할 수 있는 빌드하는 응용 프로그램에서 하드 코딩됩니다.  
  
 런타임에 SQL 문을 생성하는 응용 프로그램은 사용자에게 엄청난 유연성을 제공할 수 있습니다. WHERE **절,** **ORDER BY** 절 또는 조인과 같은 일반적인 작업을 지원하지 않았던 앞의 예제에서 볼 수 있듯이 런타임에 SQL 문을 생성하는 것은 하드 코딩 문보다 훨씬 더 복잡합니다. 또한 이러한 응용 프로그램을 테스트하는 것은 임의의 수의 SQL 문을 생성할 수 있기 때문에 문제가 됩니다.  
  
 런타임에 SQL 문을 생성할 때 발생할 수 있는 단점은 하드 코딩된 문을 사용하는 것보다 문을 만드는 데 훨씬 더 많은 시간이 걸린다는 것입니다. 다행히도, 이것은 거의 우려. 이러한 응용 프로그램은 사용자 인터페이스집약적인 경향이 있으며 응용 프로그램에서 SQL 문을 생성하는 데 소요되는 시간은 일반적으로 사용자가 기준을 입력하는 데 소요되는 시간에 비해 작습니다.
