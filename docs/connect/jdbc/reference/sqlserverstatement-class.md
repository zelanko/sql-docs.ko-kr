---
title: SQLServerStatement 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7488efcb3392623e6f54cff440a16494c10e0a69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705351"
---
# <a name="sqlserverstatement-class"></a>SQLServerStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 문 기능의 기본 구현을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerStatement 클래스는 JDBC의 준비된 문과 호출 가능한 문에 대한 다양한 기본 클래스 구현 메서드도 제공합니다. SQLServerStatement 클래스의 기본 역할은 SQL 문을 실행한 다음, 업데이트 횟수와 결과 집합을 사용자 응용 프로그램에 반환하는 것입니다.  
  
 이 클래스는 SQLServerStatement 클래스, ISQLServerStatement 인터페이스 및 java.sql.Statement 인터페이스에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
