---
title: "3 단계: Ruby를 사용 하 여 SQL에 연결 하는 개념 증명 | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: a645a57cac6eef7507aed9ea81df9fc75eb32dd4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>3 단계: Ruby를 사용 하 여 SQL에 연결 하는 개념 증명

이 예제에서는 개념 증명을 고려 되어야 합니다.  샘플 코드의 명확성을 위해 간소화 되 고 Microsoft에서 권장 모범 사례 나타내지는지 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
[TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL 데이터베이스에 연결 하는 데 사용 됩니다.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>2 단계: 쿼리를 실행 합니다.  
  
복사 하는 빈 파일에 다음 코드를 붙여 넣습니다. Test.rb 호출 합니다. 다음 명령 프롬프트에서 다음 명령을 입력 하 여 실행 합니다.  
  
    ruby test.rb  
  
코드 예제에서는 [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL 데이터베이스에 대해 집합 쿼리에서 결과 검색 하는 데 사용 됩니다. 이 함수는 쿼리를 허용 하 고 결과 집합을 반환 합니다. 사용 하 여 결과 집합에는 반복 되 [result.each 않습니다 | 행 |](https://github.com/rails-sqlserver/tiny_tds)합니다.  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>행을 삽입 하는 3 단계:  
  
이 예제를 실행 하는 방법을 표시 됩니다는 [삽입](/sql-docs/docs/t-sql/statements/insert-transact-sql) 문을에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 [SQL 주입](/sql-docs/docs/relational-databases/tables/primary-and-foreign-key-constraints) 값입니다.    
  
TinyTDS에서 Azure를 사용 하려면 것이 좋습니다 여러 실행 `SET` 현재 세션에서 특정 정보를 처리 하는 방법을 변경 하려면 문을 합니다. 권장 `SET` 문 코드 샘플에 제공 됩니다. 예를 들어 `SET ANSI_NULL_DFLT_ON` 열의 null 허용 여부 상태가 명시적으로 명시 되지 않은 경우에 null 값을 허용 하기 위해 만든 새 열을 허용 합니다.  
  
Microsoft SQL Server에 맞춰 [datetime](http://msdn.microsoft.com/library/ms187819.aspx) 사용 하 여, 형식에서 [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 해당 날짜/시간 형식으로 캐스팅 하는 함수입니다.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```

