---
title: getProcedures 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 054ce4f6f646f873d4aff05fbe1d31aa9903ded9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980745"
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
  
 카탈로그 이름이 포함하는 **문자열**입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *sSchema*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *proc*  
  
 프로시저 이름 패턴이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getProcedures 메서드는 java.sql.DatabaseMetaData 인터페이스의 getProcedures 메서드에 의해 지정됩니다.  
  
 getProcedures 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|Type|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|지정된 저장 프로시저가 있는 데이터베이스의 이름입니다.|  
|PROCEDURE_SCHEM|**String**|저장 프로시저의 스키마입니다.|  
|PROCEDURE_NAME|**String**|저장 프로시저의 이름입니다.|  
|NUM_INPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_OUTPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_RESULT_SETS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|REMARKS|**String**|프로시저 열에 대한 설명입니다.<br /><br /> <br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 열의 값을 반환하지 않습니다.|  
|PROCEDURE_TYPE|**smallint**|저장 프로시저의 형식입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> SQL_PT_UNKNOWN(0)<br /><br /> SQL_PT_PROCEDURE(1)<br /><br /> SQL_PT_FUNCTION(2)|  
  
> [!NOTE]  
>  getProcedures 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_stored_procedures(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getProcedures 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 uspGetBillOfMaterials 저장 프로시저에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
