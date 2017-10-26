---
title: "getTables 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbf35aeec7b5626b380fc654995d181fe124811
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>getTables 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그, 스키마 또는 테이블 이름 패턴에 사용할 수 있는 테이블에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *카탈로그*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *스키마*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *테이블 이름*  
  
 A **문자열** 테이블 이름 패턴이 들어 있는입니다.  
  
 *형식*  
  
 포함할 테이블의 형식이 들어 있는 문자열 배열입니다. Null은 모든 테이블 형식이 포함되어야 함을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTables 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTables 메서드에서 지정 됩니다.  
  
 GetTables 메서드에서 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**문자열**|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|**문자열**|테이블 스키마 이름입니다.|  
|TABLE_NAME|**문자열**|테이블 이름.|  
|TABLE_TYPE|**문자열**|테이블 형식입니다.|  
|REMARKS|**문자열**|테이블에 대한 설명입니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이 열에 대 한 값을 반환 하지 않습니다.  |  
|TYPE_CAT|**문자열**|JDBC 드라이버에서는 지원되지 않습니다.|  
|TYPE_SCHEM|**문자열**|JDBC 드라이버에서는 지원되지 않습니다.|  
|TYPE_NAME|**문자열**|JDBC 드라이버에서는 지원되지 않습니다.|  
|SELF_REFERENCING_COL_NAME|**문자열**|JDBC 드라이버에서는 지원되지 않습니다.|  
|REF_GENERATION|**문자열**|JDBC 드라이버에서는 지원되지 않습니다.|  
  
> [!NOTE]  
>  GetTables 메서드에서 반환 된 데이터에 대 한 자세한 내용은 "sp_tables (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getTables 메서드를 사용 하 여 Person.Contact 테이블에 대 한 테이블 설명 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
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
  
  

