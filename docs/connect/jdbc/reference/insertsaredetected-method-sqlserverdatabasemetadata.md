---
title: "insertsAreDetected 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.insertsAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f296cc42-9d26-48c3-a360-bcf51c31f7fb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7419b32f18dd09e13ef9ba53b4ffe6056af52bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="insertsaredetected-method-sqlserverdatabasemetadata"></a>insertsAreDetected 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  메서드를 호출 하 여 표시 된 행 삽입을 검색할 수 아닌지 검색 [rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean insertsAreDetected(int type)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *type*  
  
 결과 집합 유형을 나타내는 정수이며, java.sql.ResultSet 또는 SQLServerResultSet에 정의된 다음 값 중 하나일 수 있습니다.  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet 형식  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet 형식  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 경우 행 삽입을 검색할 수 있습니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 insertsAreDetected 메서드는 java.sql.DatabaseMetaData 인터페이스의 insertsAreDetected 메서드에 의해 지정 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]모든 커서 유형에 대해 삽입 된 행을 검색 하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

