---
title: "SQLServerStatement 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b10213cf711ba2900888e5bd722a71475c0c97de
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 문 기능의 기본 구현을 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>주의  
 SQLServerStatement 클래스는 JDBC의 준비 된 문과 호출 가능한 문에 대 다양 한 기본 클래스 구현 메서드도 제공 합니다. SQLServerStatement 클래스의 기본 역할은 SQL 문을 실행 하 고 반환 된 업데이트 횟수와 결과 집합을 사용자 응용 프로그램입니다.  
  
 이 클래스는 SQLServerStatement 클래스, ISQLServerStatement 인터페이스 및 java.sql.Statement 인터페이스에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

