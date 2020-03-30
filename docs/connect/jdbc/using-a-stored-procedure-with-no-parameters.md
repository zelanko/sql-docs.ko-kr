---
title: 매개 변수가 없는 저장 프로시저 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01f59f44d42af1d0880df48b043080525d9821ee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027017"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>매개 변수가 없는 저장 프로시저 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

호출할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 중 가장 간단한 형식은 매개 변수가 없고 단일 결과 집합을 반환하는 형식입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이러한 종류의 저장 프로시저를 호출하여 반환되는 데이터를 처리하는 데 사용할 수 있는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스를 제공합니다.

JDBC 드라이버를 사용하여 매개 변수가 없는 저장 프로시저를 호출하려면 `call` SQL 이스케이프 시퀀스를 사용해야 합니다. 매개 변수가 없는 `call` 이스케이프 시퀀스의 구문은 다음과 같습니다.

`{call procedure-name}`

> [!NOTE]  
> SQL 이스케이프 시퀀스에 대한 자세한 내용은 [SQL 이스케이프 시퀀스 사용](../../connect/jdbc/using-sql-escape-sequences.md)을 참조하세요.

이에 대한 예로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음 저장 프로시저를 만듭니다.

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

이 저장 프로시저는 하나의 데이터 열이 들어 있는 단일 결과 집합을 반환하며 이는 Person.Contact 테이블의 상위 10개 연락처의 제목, 이름, 성으로 구성되어 있습니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 사용하여 GetContactFormalNames 저장 프로시저를 호출합니다.

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>참고 항목

[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)
