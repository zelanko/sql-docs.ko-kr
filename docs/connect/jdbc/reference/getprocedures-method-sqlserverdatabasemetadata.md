---
title: "getProcedures 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getProcedures
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61aa101a7b43662b049497b091414ee13a3674bf
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>getProcedures 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그, 스키마 또는 저장 프로시저 이름 패턴에 사용할 수 있는 저장 프로시저에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCatalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *스키마*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *proc*  
  
 A **문자열** 프로시저 이름 패턴이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getProcedures 메서드는 java.sql.DatabaseMetaData 인터페이스의 getProcedures 메서드에서 지정 됩니다.  
  
 GetProcedures 메서드에서 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**문자열**|지정된 저장 프로시저가 있는 데이터베이스의 이름입니다.|  
|PROCEDURE_SCHEM|**문자열**|저장 프로시저의 스키마입니다.|  
|PROCEDURE_NAME|**문자열**|저장 프로시저의 이름입니다.|  
|NUM_INPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_OUTPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_RESULT_SETS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|REMARKS|**문자열**|프로시저 열에 대한 설명입니다.<br /><br /> <br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이 열에 대 한 값을 반환 하지 않습니다.|  
|PROCEDURE_TYPE|**smallint**|저장 프로시저의 형식입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> SQL_PT_UNKNOWN(0)<br /><br /> SQL_PT_PROCEDURE(1)<br /><br /> SQL_PT_FUNCTION(2)|  
  
> [!NOTE]  
>  GetProcedures 메서드에서 반환 된 데이터에 대 한 자세한 내용은 "sp_stored_procedures (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getProcedures 메서드를 사용 하 여의 uspGetBillOfMaterials 저장 프로시저에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  
