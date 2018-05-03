---
title: getBestRowIdentifier 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e75b1beeeb287d125f3669f130de0014ec9ee0b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>getBestRowIdentifier 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  테이블의 열 중 행을 고유하게 식별하는 최적의 열 집합에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schema*  
  
 A **문자열** 스키마 이름이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름이 들어 있는입니다.  
  
 *범위*  
  
 **int** 관심 있는 범위를 나타내는입니다. 값에는 다음이 포함될 수 있습니다.  
  
 bestRowTemporary(0)  
  
 bestRowTransaction(1)  
  
 bestRowSession(2)  
  
 *Null 허용*  
  
 **true 이면** null 허용 열을 포함 하도록 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBestRowIdentifier 메서드는 java.sql.DatabaseMetaData 인터페이스의 getBestRowIdentifier 메서드에 의해 지정 됩니다.  
  
 GetBestRowIdentifier 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|SCOPE|short|반환된 결과의 범위입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> bestRowTemporary(0)<br /><br /> bestRowTransaction(1)<br /><br /> bestRowSession(2)|  
|COLUMN_NAME|문자열|열 이름입니다.|  
|DATA_TYPE|short|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|문자열|데이터 형식의 이름입니다.|  
|COLUMN_SIZE|int|열의 전체 자릿수입니다.|  
|BUFFER_LENGTH|int|버퍼 길이입니다.|  
|DECIMAL_DIGITS|short|열의 소수 자릿수입니다.|  
|PSEUDO_COLUMN|short|열이 의사 열인지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> bestRowUnknown(0)<br /><br /> bestRowNotPseudo(1)<br /><br /> bestRowPseudo(2)|  
  
## <a name="example"></a>예제  
 다음 예제에서는 getBestRowIdentifier 메서드를 사용 하 여 Person.Contact 테이블에 대 한 최상의 행 식별자에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
