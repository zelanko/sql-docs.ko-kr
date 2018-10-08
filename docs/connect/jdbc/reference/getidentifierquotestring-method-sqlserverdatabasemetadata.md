---
title: getIdentifierQuoteString 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIdentifierQuoteString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dea35a0-56a8-412c-8cd3-6539527ff597
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 672246665ed978264ecf38ecb06b65ca12da86c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736711"
---
# <a name="getidentifierquotestring-method-sqlserverdatabasemetadata"></a>getIdentifierQuoteString 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL 식별자를 쿼리하는 데 사용되는 **문자열**을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getIdentifierQuoteString()  
```  
  
## <a name="return-value"></a>반환 값  
 따옴표 식별자가 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getIdentifierQuoteString 메서드는 java.sql.DatabaseMetaData 인터페이스의 getIdentifierQuoteString 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와 함께 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] JDBC 드라이버를 사용할 경우 이 메서드는 **따옴표** 식별자(“”)를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
