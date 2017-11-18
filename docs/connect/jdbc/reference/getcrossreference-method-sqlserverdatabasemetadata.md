---
title: "getCrossReference 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 70da15793b0a6f5e8687756404a45a23fd805161
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>getCrossReference 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 외래 키 테이블에서 지정된 기본 키 테이블의 기본 키 열을 참조하는 외래 키 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cat1*  
  
 A **문자열** 기본 키가 포함 된 테이블의 카탈로그 이름이 들어 있는입니다.  
  
 *schem1*  
  
 A **문자열** 기본 키가 포함 된 테이블의 스키마 이름이 들어 있는입니다.  
  
 *tab1*  
  
 A **문자열** 기본 키가 포함 된 테이블의 테이블 이름을 포함 하 합니다.  
  
 *cat2*  
  
 A **문자열** 외래 키가 포함 된 테이블의 카탈로그 이름이 들어 있는입니다.  
  
 *schem2*  
  
 A **문자열** 외래 키가 포함 된 테이블의 스키마 이름이 들어 있는입니다.  
  
 *tab2*  
  
 A **문자열** 외래 키가 포함 된 테이블의 테이블 이름을 포함 하 합니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getCrossReference 메서드는 java.sql.DatabaseMetaData 인터페이스의 getCrossReference 메서드에 의해 지정 됩니다.  
  
 GetCrossReference 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**문자열**|기본 키 테이블이 들어 있는 카탈로그의 이름입니다.|  
|PKTABLE_SCHEM|**문자열**|기본 키 테이블의 스키마 이름입니다.|  
|PKTABLE_NAME|**문자열**|기본 키 테이블의 이름입니다.|  
|PKCOLUMN_NAME|**문자열**|기본 키의 열 이름입니다.|  
|FKTABLE_CAT|**문자열**|외래 키 테이블이 들어 있는 카탈로그의 이름입니다.|  
|FKTABLE_SCHEM|**문자열**|외래 키 테이블의 스키마 이름입니다.|  
|FKTABLE_NAME|**문자열**|외래 키 테이블의 이름입니다.|  
|FKCOLUMN_NAME|**문자열**|외래 키의 열 이름입니다.|  
|KEY_SEQ|**짧은**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|UPDATE_RULE|**짧은**|SQL 작업이 업데이트일 때 외래 키에 적용되는 동작입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyNoAction(3)<br /><br /> importedKeyCascade(0)<br /><br /> importedKeySetNull(2)<br /><br /> importedKeySetDefault(4)<br /><br /> importedKeyRestrict(1)|  
|DELETE_RULE|**짧은**|SQL 작업이 삭제일 때 외래 키에 적용되는 동작입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyNoAction(3)<br /><br /> importedKeyCascade(0)<br /><br /> importedKeySetNull(2)<br /><br /> importedKeySetDefault(4)<br /><br /> importedKeyRestrict(1)|  
|FK_NAME|**문자열**|외래 키의 이름입니다.|  
|PK_NAME|**문자열**|기본 키의 이름입니다.|  
|DEFERRABILITY|**짧은**|커밋될 때까지 FOREIGN KEY 제약 조건의 확인을 지연시킬 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyInitiallyDeferred(5)<br /><br /> importedKeyInitiallyImmediate(6)<br /><br /> importedKeyNotDeferrable(7)|  
  
> [!NOTE]  
>  GetCrossReference 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_fkeys (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getCrossReference 메서드를 사용 하 여에 있는 Person.Contact 테이블과 HumanResources.Employee 테이블 간의 기본 및 외래 키 관계에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
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
  
  

