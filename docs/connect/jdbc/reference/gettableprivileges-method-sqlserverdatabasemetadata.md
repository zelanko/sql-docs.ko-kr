---
title: getTablePrivileges 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bdea6926543bd95fa66c4b73a48736a3b685859e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810091"
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>getTablePrivileges 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그, 스키마 또는 테이블 이름 패턴에 사용할 수 있는 각 테이블에 대한 액세스 권한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 카탈로그 이름이 포함하는 **문자열**입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *schema*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *table*  
  
 테이블 이름 패턴이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getTables 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTables 메서드에 의해 지정됩니다.  
  
 getTablePrivileges 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|카탈로그 이름입니다.|  
|TABLE_SCHEM|**String**|테이블 스키마 이름입니다.|  
|TABLE_NAME|**String**|테이블 이름.|  
|GRANTOR|**String**|액세스 권한을 부여하는 개체입니다.|  
|GRANTEE|**String**|액세스 권한을 받는 개체입니다.|  
|PRIVILEGE|**String**|부여되는 액세스 권한의 유형입니다.|  
|IS_GRANTABLE|**String**|피부여자가 다른 사용자에게 액세스 권한을 부여할 수 있는지 여부를 나타냅니다.|  
  
> [!NOTE]  
>  getTablePrivileges 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_table_privileges(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getTablePrivileges 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 Person.Contact 테이블에 대한 액세스 권한을 반환하는 방법을 보여 줍니다.  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
