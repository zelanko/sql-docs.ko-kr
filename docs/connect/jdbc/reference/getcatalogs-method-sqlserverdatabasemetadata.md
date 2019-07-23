---
title: getCatalogs 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 786f55e436b9582eaed875f8c7cd265b1d3e2cc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953450"
---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>getCatalogs 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  연결된 서버에서 사용할 수 있는 카탈로그 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getCatalogs 메서드는 java.sql.DatabaseMetaData 인터페이스의 getCatalogs 메서드에 의해 지정됩니다.  
  
> [!NOTE]  
>  SQL Azure에서 **SQLServerDatabaseMetaData**을 호출 하려면 master 데이터베이스에 연결 해야 합니다. SQL Azure는 사용자 데이터베이스에서 전체 카탈로그 집합을 반환하는 기능을 지원하지 않습니다. **SQLServerDatabaseMetaData** 는 데이터베이스 뷰를 사용 하 여 카탈로그를 가져옵니다. [Database_usage (Azure SQL Database)](../../../relational-databases/system-catalog-views/sys-database-usage-azure-sql-database.md) 의 사용 권한에 대 한 설명을 참조 하 여 SQL Azure에서 **SQLServerDatabaseMetaData** 동작을 이해 하십시오.  
  
 getCatalogs 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 시스템 데이터베이스를 비롯한 카탈로그의 이름입니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 getCatalogs 메서드를 사용하여 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 시스템 데이터베이스를 비롯한 모든 데이터베이스의 이름을 반환하는 방법을 보여 줍니다.  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
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
  
  
