---
title: "getPrimaryKeys 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getPrimaryKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eea9de761a2c7efb4b47c4032ae3f6ac6814cdc0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>getPrimaryKeys 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 테이블의 기본 키 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cat*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *스키마*  
  
 A **문자열** 스키마 이름이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getPrimaryKeys 메서드는 java.sql.DatabaseMetaData 인터페이스의 getPrimaryKeys 메서드에 의해 지정 됩니다.  
  
 GetPrimaryKeys 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|문자열|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|문자열|테이블의 스키마입니다.|  
|TABLE_NAME|문자열|테이블의 이름입니다.|  
|COLUMN_NAME|문자열|열 이름입니다.|  
|KEY_SEQ|short|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|PK_NAME|문자열|기본 키의 이름입니다.|  
  
> [!NOTE]  
>  GetPrimaryKeys 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_pkeys (TRANSACT-SQL)"의 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getPrimaryKeys 메서드를 사용 하 여 Person.Contact 테이블에 대 한 기본 키에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
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
  
  

