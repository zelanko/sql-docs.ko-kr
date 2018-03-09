---
title: "getSchemaName 메서드 (SQLServerResultSetMetaData) | Microsoft Docs"
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
apiname: SQLServerResultSetMetaData.getSchemaName
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 2d0063ab-d5d7-420f-b388-36d5169b1358
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 89291e2c92656dad0a45e2c10521582dcc6b3f51
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getschemaname-method-sqlserverresultsetmetadata"></a>getSchemaName 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열의 테이블 스키마 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getSchemaName(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 스키마 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSchemaName 메서드는 java.sql.ResultSetMetaData 인터페이스의 getSchemaName 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
