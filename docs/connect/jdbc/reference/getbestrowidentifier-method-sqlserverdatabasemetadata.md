---
title: getBestRowIdentifier 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 462de181aca55cce38d1e26f7932fe0003a0c323
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730327"
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
  
 카탈로그 이름이 포함하는 **문자열**입니다.  
  
 *schema*  
  
 스키마 이름을 포함하는 **문자열**입니다.  
  
 *table*  
  
 테이블 이름이 들어 있는 **문자열**입니다.  
  
 *범위*  
  
 관심 있는 범위를 나타내는 **int**입니다. 값에는 다음이 포함될 수 있습니다.  
  
 bestRowTemporary(0)  
  
 bestRowTransaction(1)  
  
 bestRowSession(2)  
  
 *nullable*  
  
 Null 허용 열을 포함하려면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getBestRowIdentifier 메서드는 java.sql.DatabaseMetaData 인터페이스의 getBestRowIdentifier 메서드에 의해 지정 됩니다.  
  
 getBestRowIdentifier 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|SCOPE|short|반환된 결과의 범위입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> bestRowTemporary(0)<br /><br /> bestRowTransaction(1)<br /><br /> bestRowSession(2)|  
|COLUMN_NAME|String|열 이름입니다.|  
|DATA_TYPE|short|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|String|데이터 형식의 이름입니다.|  
|COLUMN_SIZE|ssNoversion|열의 전체 자릿수입니다.|  
|BUFFER_LENGTH|ssNoversion|버퍼 길이입니다.|  
|DECIMAL_DIGITS|short|열의 소수 자릿수입니다.|  
|PSEUDO_COLUMN|short|열이 의사 열인지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> bestRowUnknown(0)<br /><br /> bestRowNotPseudo(1)<br /><br /> bestRowPseudo(2)|  
  
## <a name="example"></a>예제  
 다음 예제에서는 getBestRowIdentifier 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스의 Person.Contact 테이블에 가장 적합한 행 식별자에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
