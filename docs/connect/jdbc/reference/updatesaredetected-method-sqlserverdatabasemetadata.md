---
title: updatesAreDetected 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.updatesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb541175-d3a5-4bca-b327-64e2270c0df1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4fa6361afd8e1f262f1accbdb377fccf9ae701c6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919665"
---
# <a name="updatesaredetected-method-sqlserverdatabasemetadata"></a>updatesAreDetected 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) 클래스의 [rowUpdated](../../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 호출하여 표시된 행 업데이트를 검색할 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean updatesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *type*  
  
 결과 집합 유형을 나타내는 **int**이며, java.sql.ResultSet 또는 SQLServerResultSet에 정의된 다음 값 중 하나일 수 있습니다.  
  
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
  
## <a name="return-value"></a>Return Value  
 행 업데이트를 검색할 수 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updatesAreDetected 메서드는 java.sql.DatabaseMetaData 인터페이스의 updatesAreDetected 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
