---
title: "storesLowerCaseQuotedIdentifiers 메서드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.storesLowerCaseQuotedIdentifiers
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3e104c9e-66d4-436b-8b5b-a00ff667c95b
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8b2bb8ea6754293a1b31d2bb4f769a283506a5f9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata"></a>storesLowerCaseQuotedIdentifiers 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 따옴표로 묶이고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되지 않는 것으로 처리하고 소문자로 저장하는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean storesLowerCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 는 식별자가 소문자로 저장 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 storesLowerCaseQuotedIdentifiers 메서드는 java.sql.DatabaseMetaData 인터페이스의 storesLowerCaseQuotedIdentifiers 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
