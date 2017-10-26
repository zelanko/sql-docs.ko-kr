---
title: "getURL 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b18875a215c3854bef2e39ca2445c9299ad41c6e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스의 URL을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** URL이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getURL 메서드는 java.sql.DatabaseMetaData 인터페이스의 getURL 메서드에 의해 지정 됩니다.  
  
 사용 하는 경우는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스에서이 메서드는 반환는 **문자열** 다음 정보를 포함 하는 값:  
  
-   URL 값 "jdbc:sqlserver://"  
  
-   옵션 연결 속성 등 **serverName**, **instanceName**, 및 **포트 번호**  
  
-   다른 연결 속성을 설정 하 여 사용자 및 모든 연결 비어 있지 않은 또는 null이 아닌 드라이버를 사용 하 여 속성 제외 하 고 기본값 **userName**, **암호**, 및 **integratedSecurity**.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

