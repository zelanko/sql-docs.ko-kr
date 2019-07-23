---
title: getTables 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8dfd7f14d6006f5a41a7cd2a9b0cae4933804fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979216"
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
 *catalog*  
  
 카탈로그 이름이 포함하는 **문자열**입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *schema*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *tableName*  
  
 테이블 이름 패턴이 들어 있는 **문자열**입니다.  
  
 *types*  
  
 포함할 테이블의 형식이 들어 있는 문자열 배열입니다. Null은 모든 테이블 형식이 포함되어야 함을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getTables 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTables 메서드에 의해 지정됩니다.  
  
 getTables 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|**String**|테이블 스키마 이름입니다.|  
|TABLE_NAME|**String**|테이블 이름.|  
|TABLE_TYPE|**String**|테이블 형식입니다.|  
|REMARKS|**String**|테이블에 대한 설명입니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 열의 값을 반환하지 않습니다.|  
|TYPE_CAT|**String**|JDBC 드라이버에서는 지원되지 않습니다.|  
|TYPE_SCHEM|**String**|JDBC 드라이버에서는 지원되지 않습니다.|  
|TYPE_NAME|**String**|JDBC 드라이버에서는 지원되지 않습니다.|  
|SELF_REFERENCING_COL_NAME|**String**|JDBC 드라이버에서는 지원되지 않습니다.|  
|REF_GENERATION|**String**|JDBC 드라이버에서는 지원되지 않습니다.|  
  
> [!NOTE]  
>  getTables 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_tables(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getTables 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 Person.Contact 테이블에 대한 테이블 설명 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
