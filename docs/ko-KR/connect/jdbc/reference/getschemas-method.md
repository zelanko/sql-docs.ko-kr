---
title: getSchemas 메서드 () | Microsoft Docs
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
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa596c462e8a5615b0c736ca7d81f05deb670235
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getschemas-method-"></a>getSchemas 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 데이터베이스에서 사용할 수 있는 스키마 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSchemas 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSchemas 메서드에 의해 지정 됩니다.  
  
 GetSchemas 메서드에 의해 반환 된 결과 집합에는 다음과 같은 정보가 포함 되어 있습니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**문자열**|스키마의 이름입니다.|  
|TABLE_CATALOG|**문자열**|스키마의 카탈로그 이름입니다.|  
  
 결과는 TABLE_CATALOG 및 TABLE_SCHEM 순으로 정렬됩니다. 각 행에는 첫 번째 열로 TABLE_SCHEM이 있고 두 번째 열로 TABLE_CATALOG가 있습니다.  
  
> [!NOTE]  
>  GetSchemas 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sys.schemas (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 GetSchemas 메서드를 사용 하 여 카탈로그 및 해당 관련된 스키마 이름에 대 한 정보를 반환 하는 방법은 다음 예제에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 연결 인수에 사용할 데이터베이스를 지정 하는 경우.  
  
```  
public static void executeGetSchemas(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getSchemas();  
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
  
  
