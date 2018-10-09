---
title: '3단계: Java를 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 9eed37349152b48ab49859b44cc23cb463d8541b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801381"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>3단계: Ruby를 사용하여 SQL과 연결된 개념 증명

이 예제에서는 개념만 고려 되어야 합니다.  샘플 코드를 이해 하기 쉽도록 간소화 되었습니다 및 Microsoft에서 권장 하는 모범 사례를 반드시 나타내지는지 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
합니다 [tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL Database에 연결 하는 데 사용 됩니다.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>2단계: 쿼리 실행  
  
복사 하 고 빈 파일에 다음 코드를 붙여넣습니다. 이름을 test.rb입니다. 다음 명령 프롬프트에서 다음 명령을 입력 하 여 실행 합니다.  
  
    ruby test.rb  
  
코드 샘플에는 [tinytds:: Result](https://github.com/rails-sqlserver/tiny_tds) 함수 로부터 결과 집합 쿼리를 SQL Database에 대해 검색 하는 합니다. 이 함수는 쿼리를 허용 하 고 결과 집합을 반환 합니다. 결과 집합을 사용 하 여 반복 되 [result.each do | 행 |](https://github.com/rails-sqlserver/tiny_tds)합니다.  
  
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
  
이 예제에서는 실행 하는 방법에에서는 [삽입](../../t-sql/statements/insert-transact-sql.md) 에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 하는 문을 [SQL 주입](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값입니다.    
  
TinyTDS와 Azure 함께 사용 하려면 것이 좋습니다 여러 실행 `SET` 문을 현재 세션에서 특정 정보를 처리 하는 방법을 변경 합니다. 권장 `SET` 문을 코드 샘플에 제공 됩니다. 예를 들어 `SET ANSI_NULL_DFLT_ON` 열의 null 허용 여부 상태가 명시적으로 명시 되지 않은 경우에 null 값을 허용 하기 위해 만든 새 열을 사용 하면 됩니다.  
  
Microsoft SQL Server에 맞게 [날짜/시간](../../t-sql/data-types/datetime-transact-sql.md) 형식에 사용 합니다 [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 해당 날짜/시간 형식으로 캐스팅 함수입니다.  
  
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
