---
title: getColumnPrivileges 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54f6ef742ac4d61e195e33590d7bdee6ebbc0739
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>getColumnPrivileges 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  테이블의 열에 대한 액세스 권한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schema*  
  
 A **문자열** 스키마 이름이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름이 들어 있는입니다.  
  
 *열*  
  
 A **문자열** 열 이름 패턴이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getColumnPrivileges 메서드는 java.sql.DatabaseMetaData 인터페이스의 getColumnPrivileges 메서드에 의해 지정 됩니다.  
  
 GetColumnPrivileges 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**문자열**|카탈로그 이름입니다.|  
|TABLE_SCHEM|**문자열**|테이블 스키마 이름입니다.|  
|TABLE_NAME|**문자열**|테이블 이름.|  
|COLUMN_NAME|**문자열**|열 이름입니다.|  
|GRANTOR|**문자열**|액세스 권한을 부여하는 개체입니다.|  
|GRANTEE|**문자열**|액세스 권한을 받는 개체입니다.|  
|PRIVILEGE|**문자열**|부여되는 액세스 권한의 유형입니다.|  
|IS_GRANTABLE|**문자열**|피부여자가 다른 사용자에게 액세스 권한을 부여할 수 있는지 여부를 나타냅니다.|  
  
> [!NOTE]  
>  GetColumnPrivileges 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_column_privileges (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getColumnPrivileges 메서드를 사용의 Person.Contact 테이블에 있는 FirstName 열에 대 한 액세스 권한을 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  
