---
title: "updatesAreDetected 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.updatesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb541175-d3a5-4bca-b327-64e2270c0df1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0e0b2a6ac15c1798eb999482ef6f07c6aabd73d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatesaredetected-method-sqlserverdatabasemetadata"></a>updatesAreDetected 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  검색을 호출 하 여 표시 되는 행 업데이트를 검색할 수 여부는 [rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean updatesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *type*  
  
 **int** 하는 결과 집합 유형을 나타내는, java.sql.ResultSet 또는 SQLServerResultSet에 정의 된 다음 값 중 하나일 수 있습니다.  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet 형식  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet 형식  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 경우 행 업데이트를 검색할 수 있습니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updatesAreDetected 메서드는 java.sql.DatabaseMetaData 인터페이스의 updatesAreDetected 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

