---
title: getURL 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fd0cfcf85edcab84d6488dd733f72fdbebfe8b6
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784072"
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스의 URL을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>반환 값  
 URL을 포함하는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getURL 메서드는 java.sql.DatabaseMetaData 인터페이스의 getURL 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와 함께 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]를 사용할 경우 이 메서드는 다음 정보가 들어 있는 **문자열** 값을 반환합니다.  
  
-   URL 값 "jdbc:sqlserver://"  
  
-   선택적 연결 속성을 같은 **serverName**를 **instanceName**, 및 **portNumber**  
  
-   사용자가 설정한 기타 연결 속성과 비어 있지 않거나 null이 아닌 드라이버 기본값을 갖는 모든 연결 속성(**userName**, **password** 및 **integratedSecurity** 제외)  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
