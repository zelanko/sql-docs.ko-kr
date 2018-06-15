---
title: 매개 변수가 없는 저장된 프로시저를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7db021b9d3fdf875c2c6074159b56d8e6cb0fd14
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851238"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>매개 변수가 없는 저장 프로시저 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  가장 간단한의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 호출할 수 있는 저장된 프로시저는 매개 변수를 포함 하 고 단일 결과 집합을 반환 합니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 이러한 종류의 저장된 프로시저를 호출 하 고 반환 되는 데이터를 처리 하는 데 사용할 수 있는 클래스입니다.  
  
 JDBC 드라이버를 사용 하 여 매개 변수가 없는 저장된 프로시저를 호출 하는 경우 사용 해야는 `call` SQL 이스케이프 시퀀스입니다. 에 대 한 구문에서 `call` 매개 변수가 없는 이스케이프 시퀀스는 다음과 같습니다.  
  
 `{call procedure-name}`  
  
> [!NOTE]  
>  SQL 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)합니다.  
  
 예를 들어에서 다음과 같은 저장된 프로시저를 만들는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
CREATE PROCEDURE GetContactFormalNames   
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName   
   FROM Person.Contact  
END  
```  
  
 이 저장 프로시저는 하나의 데이터 열이 들어 있는 단일 결과 집합을 반환하며 이는 Person.Contact 테이블의 상위 10개 연락처의 제목, 이름, 성으로 구성되어 있습니다.  
  
 다음 예에서 열린 연결을는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된 및 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드는 GetContactFormalNames 저장 프로시저를 호출 하는 데 사용 됩니다.  
  
```  
public static void executeSprocNoParams(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
  
      while (rs.next()) {  
         System.out.println(rs.getString("FormalName"));  
      }  
      rs.close();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
