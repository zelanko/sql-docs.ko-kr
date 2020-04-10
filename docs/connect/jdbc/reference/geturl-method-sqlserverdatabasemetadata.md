---
title: getURL 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fcb66851-db5f-4ae8-b728-d129480b6f42
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 526eb87409eaf08c8947e1a85c4e4ef68247daff
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910650"
---
# <a name="geturl-method-sqlserverdatabasemetadata"></a>getURL 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스의 URL을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>Return Value  
 URL을 포함하는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getURL 메서드는 java.sql.DatabaseMetaData 인터페이스의 getURL 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 데이터베이스와 함께 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 경우 이 메서드는 다음 정보가 들어 있는 **문자열** 값을 반환합니다.  
  
-   URL 값 "jdbc:sqlserver://"  
  
-   선택적 연결 속성(예: **serverName**, **instanceName** 및 **portNumber**)  
  
-   사용자가 설정한 기타 연결 속성과 비어 있지 않거나 null이 아닌 드라이버 기본값을 갖는 모든 연결 속성(**userName**, **password** 및 **integratedSecurity** 제외)  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
