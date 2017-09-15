---
title: "getSQLKeywords 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getSQLKeywords
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a2a0dfbb-11ec-429f-aea6-8f44148ebb8e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35e4a13f00a95becbfa4637c13e93cba6750d2a5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlkeywords-method-sqlserverdatabasemetadata"></a>getSQLKeywords 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스의 SQL 키워드 중 SQL92 키워드와 중복되지 않는 모든 키워드의 쉼표로 구분된 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getSQLKeywords()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** SQL 키워드가 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSQLKeywords 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSQLKeywords 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
