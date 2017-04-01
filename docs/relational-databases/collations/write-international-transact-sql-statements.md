---
title: "국가별 Transact-SQL 문 작성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "국가별 문 작성"
  - "Transact-SQL 국가별 고려 사항"
  - "국가별 고려 사항 [SQL Server], Transact-SQL"
  - "데이터베이스 엔진 국가별 고려 사항 [SQL Server], Transact-SQL"
  - "문 [SQL Server], 국가별"
  - "데이터베이스 국가별 고려 사항 [SQL Server], Transact-SQL"
  - "날짜 [SQL Server], 국가별 고려 사항"
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 국가별 Transact-SQL 문 작성
  다음 지침에 따라 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하는 데이터베이스 및 데이터베이스 응용 프로그램을 특정 언어에서 다른 언어로 이식하거나 여러 언어를 지원하도록 할 수 있습니다.  
  
-   **char**, **varchar** 및 **text** 데이터 형식을 사용하는 경우 모두 **nchar**, **nvarchar** 및 **nvarchar(max)**로 대체합니다. 이렇게 하면 코드 페이지 변환 문제가 발생하지 않습니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
-   월과 요일을 비교하고 연산하려면 문자열 이름 대신 숫자 형식의 날짜 부분을 사용하십시오. 언어 설정이 다르면 월과 요일에 대해 각기 다른 이름이 반환됩니다. 예를 들어 DATENAME(MONTH,GETDATE())은 언어가 영어(미국)로 설정되었을 경우 May를 반환하고 독일어로 설정되었을 경우 Mai를 반환하며 프랑스어로 설정되었을 경우에는 mai를 반환합니다. 대신 이름이 아닌 해당 월의 숫자를 사용하는 DATEPART 함수 등을 사용하십시오. 날짜 이름이 숫자 표시보다 의미를 쉽게 알 수 있으므로 사용자에게 표시되는 결과 집합을 만들 때에는 DATEPART 이름을 사용합니다. 그러나 특정 언어로 표시된 이름에 따라 달라지는 논리는 코딩하지 마십시오.  
  
-   INSERT 또는 UPDATE 문을 위한 입력이나 비교를 위해 날짜를 지정할 때 모든 언어 설정에서 동일하게 해석되는 상수를 사용하십시오.  
  
    -   ADO, OLE DB 및 ODBC 응용 프로그램은 다음과 같은 ODBC용 타임스탬프, 날짜 및 시간 이스케이프 절을 사용해야 합니다.  
  
         **{ ts'**yyyy**-***mm***-***dd**hh***:***mm***:***ss*[**.***fff*] **'}** 예: **{ ts'**1998**-**09**-**24 10**:**02**:**20**' }**  
  
         **{ d'** *yyyy* **-** *mm* **-** *dd* **'}** 예: **{ d'**1998**-**09**-**24**'}**  
  
         **{ t'** *hh* **:** *mm* **:** *ss* **'}** 예: **{ t'**10:02:20**'}**  
  
    -   다른 API나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 저장 프로시저, 트리거를 사용하는 응용 프로그램에서는 분리되지 않은 숫자 문자열을 사용해야 합니다. 예를 들어 19980924와 같은 *yyyymmdd* 를 사용합니다.  
  
    -   다른 API나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 저장 프로시저 및 트리거를 사용하는 응용 프로그램에서는 **time**, **date**, **smalldate**, **datetime**, **datetime2** 및 **datetimeoffset** 데이터 형식과 문자열 데이터 형식 간의 모든 변환에 명시적 스타일 매개 변수가 있는 CONVERT 문을 사용해야 합니다. 예를 들어 다음 문은 모든 언어 또는 날짜 형식 연결 설정에서 똑같이 해석됩니다.  
  
        ```  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
         자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
  