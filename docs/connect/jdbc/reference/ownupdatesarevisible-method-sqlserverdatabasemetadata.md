---
title: ownUpdatesAreVisible 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.ownUpdatesAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eacbb1a8-ac9a-4f44-832e-ae0af476522e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 799b8834e8b7de236e7e835dff921db33a71d8a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841088"
---
# <a name="ownupdatesarevisible-method-sqlserverdatabasemetadata"></a>ownUpdatesAreVisible 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  결과 집합 자체의 업데이트 내용이 표시되는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean othersUpdatesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *type*  
  
 결과 집합 유형을 나타내는 정수이며, java.sql.ResultSet 또는 SQLServerResultSet에 정의된 다음 값 중 하나일 수 있습니다.  
  
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
 **true 이면** 이면 업데이트가 표시 됩니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 ownUpdatesAreVisible 메서드는 java.sql.DatabaseMetaData 인터페이스의 ownUpdatesAreVisible 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
