---
title: getCrossReference 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bae60cb90c0459b5a221f88f463cfda0a520f47e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600861"
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
  
 기본 키가 포함된 테이블의 카탈로그 이름이 들어 있는 **문자열**입니다.  
  
 *schem1*  
  
 기본 키가 포함된 테이블의 스키마 이름이 들어 있는 **문자열**입니다.  
  
 *tab1*  
  
 기본 키가 포함된 테이블의 테이블 이름이 들어 있는 **문자열**입니다.  
  
 *cat2*  
  
 외래 키가 포함된 테이블의 카탈로그 이름이 들어 있는 **문자열**입니다.  
  
 *schem2*  
  
 외래 키가 포함된 테이블의 스키마 이름이 들어 있는 **문자열**입니다.  
  
 *tab2*  
  
 외래 키가 포함된 테이블의 테이블 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getCrossReference 메서드는 java.sql.DatabaseMetaData 인터페이스의 getCrossReference 메서드에 의해 지정 됩니다.  
  
 getCrossReference 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|기본 키 테이블이 들어 있는 카탈로그의 이름입니다.|  
|PKTABLE_SCHEM|**String**|기본 키 테이블의 스키마 이름입니다.|  
|PKTABLE_NAME|**String**|기본 키 테이블의 이름입니다.|  
|PKCOLUMN_NAME|**String**|기본 키의 열 이름입니다.|  
|FKTABLE_CAT|**String**|외래 키 테이블이 들어 있는 카탈로그의 이름입니다.|  
|FKTABLE_SCHEM|**String**|외래 키 테이블의 스키마 이름입니다.|  
|FKTABLE_NAME|**String**|외래 키 테이블의 이름입니다.|  
|FKCOLUMN_NAME|**String**|외래 키의 열 이름입니다.|  
|KEY_SEQ|**short**|기본 키가 여러 열로 구성된 경우 열의 시퀀스 번호입니다.|  
|UPDATE_RULE|**short**|SQL 작업이 업데이트일 때 외래 키에 적용되는 동작입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyNoAction(3)<br /><br /> importedKeyCascade(0)<br /><br /> importedKeySetNull(2)<br /><br /> importedKeySetDefault(4)<br /><br /> importedKeyRestrict(1)|  
|DELETE_RULE|**short**|SQL 작업이 삭제일 때 외래 키에 적용되는 동작입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyNoAction(3)<br /><br /> importedKeyCascade(0)<br /><br /> importedKeySetNull(2)<br /><br /> importedKeySetDefault(4)<br /><br /> importedKeyRestrict(1)|  
|FK_NAME|**String**|외래 키의 이름입니다.|  
|PK_NAME|**String**|기본 키의 이름입니다.|  
|DEFERRABILITY|**short**|커밋될 때까지 FOREIGN KEY 제약 조건의 확인을 지연시킬 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> importedKeyInitiallyDeferred(5)<br /><br /> importedKeyInitiallyImmediate(6)<br /><br /> importedKeyNotDeferrable(7)|  
  
> [!NOTE]  
>  getCrossReference 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_fkeys(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getCrossReference 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 포함된 Person.Contact 테이블과 HumanResources.Employee 테이블 간의 기본 및 외래 키 관계에 대한 정보를 반환합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
