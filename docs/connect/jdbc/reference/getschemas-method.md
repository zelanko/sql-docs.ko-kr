---
description: getSchemas 메서드()
title: getSchemas 메서드() | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8918b4806972ff6cf1cbb08250149049ecbec6b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434675"
---
# <a name="getschemas-method-"></a>getSchemas 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 데이터베이스에서 사용할 수 있는 스키마 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>Return Value  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getSchemas 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSchemas 메서드에 의해 지정됩니다.  
  
 getSchemas 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|이름|Type|설명|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|스키마의 이름입니다.|  
|TABLE_CATALOG|**String**|스키마의 카탈로그 이름입니다.|  
  
 결과는 TABLE_CATALOG 및 TABLE_SCHEM 순으로 정렬됩니다. 각 행에는 첫 번째 열로 TABLE_SCHEM이 있고 두 번째 열로 TABLE_CATALOG가 있습니다.  
  
> [!NOTE]  
>  getSchemas 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sys.schemas(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 연결 인수로 사용할 데이터베이스를 지정할 경우 getSchemas 메서드를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 카탈로그 및 해당 관련 스키마에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
