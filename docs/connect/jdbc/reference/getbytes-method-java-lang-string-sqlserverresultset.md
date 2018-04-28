---
title: getBytes 메서드 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ff617165-47f8-41c1-9c51-37ffc7714923
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef528555bc6158f79ccb757788df3a24874532b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getbytes-method-javalangstring-sqlserverresultset"></a>getBytes 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **바이트** Java 프로그래밍 언어의에서 배열입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public byte[] getBytes(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 배열을 **바이트** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBytes 메서드는 java.sql.ResultSet 인터페이스의 getBytes 메서드에 의해 지정 됩니다.  
  
 이 메서드를 사용하면 모든 열을 서버에서 읽어 온 원시 바이트로 검색할 수 있습니다. 이 메서드는 서버에 저장된 형식으로 서버에서 직접 바이트 배열을 반환합니다.  
  
 이전 버전의 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], SQLServerResultSet.getBytes를 사용 하 여 바이트 배열 간에 값을 변환할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식 **날짜**, **시간**,  **datetime2**, 또는 **datetimeoffset**합니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getBytes 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
