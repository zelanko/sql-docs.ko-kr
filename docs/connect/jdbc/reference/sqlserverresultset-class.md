---
title: SQLServerResultSet 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 71513f5e8006adffdb46b249f6358030d11b95a6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801510"
---
# <a name="sqlserverresultset-class"></a>SQLServerResultSet 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 결과 집합을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Remarks  
 결과 집합에는 클라이언트 쪽과 서버측의 두 가지 유형이 있습니다.  
  
 클라이언트 쪽 결과 집합은 결과가 클라이언트 프로세스 메모리 크기에 맞는 경우에 사용됩니다. 이러한 결과는 보다 빠른 성능을 제공하며 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 데이터베이스에서 이러한 결과를 전체적으로 읽을 수 있습니다. 이러한 결과 집합은 서버측 커서를 만들기 위한 오버헤드를 유발하지 않으므로 데이터베이스에 추가 부하를 주지 않습니다. 그러나 이러한 유형의 결과 집합은 업데이트할 수 없습니다.  
  
 서버측 결과 집합은 결과가 클라이언트 프로세스 메모리 크기에 맞지 않거나 결과 집합을 업데이트할 수 있도록 하려는 경우에 사용할 수 있습니다. 이 유형의 결과 집합을 사용하면 JDBC 드라이버에서는 서버측 커서를 만든 다음 사용자가 해당 결과 집합을 스크롤할 때 결과 집합의 행을 명시적으로 인출합니다.  
  
 SQLServerResultSet 클래스에서는 결과 집합을 네이티브 Java 데이터 형식 및 여러 Java 개체 형식으로 업데이트할 수 있게 해 주는 여러 메서드를 제공합니다.  
  
 이 클래스는 SQLServerResultSet 클래스, ISQLServerResultSet 인터페이스 및 java.sql.ResultSet 인터페이스에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
