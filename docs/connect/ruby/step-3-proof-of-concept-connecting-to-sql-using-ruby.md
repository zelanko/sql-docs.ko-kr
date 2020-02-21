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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67992492"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>3단계: Ruby를 사용하여 SQL에 연결하는 개념 증명

이 예제는 개념 증명으로만 간주해야 합니다.  이 샘플 코드는 명확하게 하기 위해 단순화되었으며 반드시 Microsoft에서 권장하는 모범 사례를 대표하지는 않습니다.  
  
## <a name="step-1--connect"></a>1단계:  연결  
  
[TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL Database에 연결하는 데 사용됩니다.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>2단계:  쿼리 실행  
  
다음 코드를 복사하여 빈 파일에 붙여넣습니다. 이름을 test.rb로 지정합니다. 그런 다음 명령 프롬프트에서 다음 명령을 입력하여 실행합니다.  
  
    ruby test.rb  
  
코드 샘플에서 [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) 함수는 SQL Database에 대한 쿼리에서 결과 집합을 검색하는 데 사용됩니다. 이 함수는 쿼리를 허용하고 결과 집합을 반환합니다. 이 결과 집합은 [result.each do |row|](https://github.com/rails-sqlserver/tiny_tds)를 사용하여 반복됩니다.  
  
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
  
## <a name="step-3--insert-a-row"></a>3단계:  행 삽입  
  
이 예제에서는 [INSERT](../../t-sql/statements/insert-transact-sql.md) 명령문을 안전하게 실행하고 [SQL injection](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값으로부터 애플리케이션을 보호하는 매개 변수를 전달하는 방법을 보여줍니다.    
  
TinyTDS와 Azure를 함께 사용하려면 여러 `SET` 문을 실행하여 현재 세션에서 특정 정보를 처리 하는 방법을 변경하는 것이 좋습니다. 권장되는 `SET` 문이 코드 샘플에 제공됩니다. 예를 들어 `SET ANSI_NULL_DFLT_ON` 에서는 열의 Null 허용 여부 상태가 명시적으로 지정되지 않은 경우에도 Null 값을 허용하도록 새 열을 만들 수 있습니다.  
  
Microsoft SQL Server [datetime](../../t-sql/data-types/datetime-transact-sql.md) 형식에 맞게 [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 함수를 사용하여 해당 날짜/시간 형식으로 캐스팅합니다.  
  
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
