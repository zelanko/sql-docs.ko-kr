---
title: getTableTypes 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getTableTypes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0f5dc57-07b8-4811-ab1a-80a524bfdb42
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bb52a365bedc945395400daa11ab6ca6f724726
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839268"
---
# <a name="gettabletypes-method-sqlserverdatabasemetadata"></a>getTableTypes 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 데이터베이스에서 사용할 수 있는 테이블 형식을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getTableTypes()  
```  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTableTypes 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTableTypes 메서드에 의해 지정 됩니다.  
  
 getTableTypes 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_TYPE|**문자열**|테이블 형식입니다.|  
  
> [!NOTE]  
>  getTableTypes 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서의 "sp_tables(Transact-SQL)"를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 연결 문자열에 데이터베이스가 지정된 경우 getTableTypes 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 테이블 형식 정보를 반환하는 방법을 보여줍니다.  
  
```  
public static void executeGetTableTypes(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTableTypes();  
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
  
  
