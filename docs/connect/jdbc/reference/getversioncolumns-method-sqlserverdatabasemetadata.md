---
title: "getVersionColumns 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c9d53e85579d389a1b90f1f1b0b501104bb02ede
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>getVersionColumns 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  테이블에서 행 값이 업데이트될 때 자동으로 업데이트되는 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *카탈로그*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *스키마*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getVersionColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getVersionColumns 메서드에 의해 지정 됩니다.  
  
 GetVersionColumns 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|SCOPE|**짧은**|JDBC 드라이버에서는 지원되지 않습니다.|  
|COLUMN_NAME|**문자열**|열 이름입니다.|  
|DATA_TYPE|**짧은**|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**문자열**|데이터 형식의 이름입니다.|  
|COLUMN_SIZE|**int**|열의 전체 자릿수입니다.|  
|BUFFER_LENGTH|**int**|열의 길이(바이트)입니다.|  
|DECIMAL_DIGITS|**짧은**|열의 소수 자릿수입니다.|  
|PSEUDO_COLUMN|**짧은**|열이 의사 열인지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> versionColumnUnknown(0)<br /><br /> versionColumnNotPseudo(1)<br /><br /> versionColumnPseudo(2)|  
  
> [!NOTE]  
>  GetVersionColumns 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_datatype_info (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 Person.Contact 테이블에 자동으로 업데이트 되는 열에 대 한 정보를 반환할 getVersionColumns 메서드를 사용 하 여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
