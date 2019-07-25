---
title: '3단계: Ruby를 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992492"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>3단계: Ruby를 사용하여 SQL과 연결된 개념 증명

이 예는 개념 증명 으로만 간주 해야 합니다.  이 샘플 코드는 명확 하 게 하기 위해 단순화 되었으며 Microsoft에서 권장 하는 모범 사례를 나타내지는 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
[TinyTDS:: Client](https://github.com/rails-sqlserver/tiny_tds) 함수를 사용 하 여 SQL Database에 연결 합니다.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>2단계: 쿼리 실행  
  
다음 코드를 복사 하 여 빈 파일에 붙여 넣습니다. It 테스트를 호출 합니다. 그런 다음 명령 프롬프트에서 다음 명령을 입력 하 여 실행 합니다.  
  
    ruby test.rb  
  
코드 샘플에서 [TinyTds:: result](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL Database에 대 한 쿼리에서 결과 집합을 검색 하는 데 사용 됩니다. 이 함수는 쿼리를 허용 하 고 결과 집합을 반환 합니다. 결과 집합은 결과를 사용 하 여 반복 됩니다 [. 각 작업은 | row |](https://github.com/rails-sqlserver/tiny_tds)입니다.  
  
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
  
## <a name="step-3--insert-a-row"></a>3 단계: 행 삽입  
  
이 예제에서는 [SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) [삽입](../../t-sql/statements/insert-transact-sql.md) 값 으로부터 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 실행 하는 방법을 확인 합니다.    
  
Azure에서 TinyTDS를 사용 하려면 여러 `SET` 문을 실행 하 여 현재 세션에서 특정 정보를 처리 하는 방법을 변경 하는 것이 좋습니다. 권장 `SET` 문은 코드 샘플에 제공 됩니다. 예를 들어 `SET ANSI_NULL_DFLT_ON` 는 열의 null 허용 여부 상태가 명시적으로 명시 되지 않은 경우에도 새 열이 null 값을 허용 하도록 허용 합니다.  
  
Microsoft SQL Server [datetime](../../t-sql/data-types/datetime-transact-sql.md) 형식에 맞추려면 [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 함수를 사용 하 여 해당 날짜/시간 형식으로 캐스팅 합니다.  
  
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
