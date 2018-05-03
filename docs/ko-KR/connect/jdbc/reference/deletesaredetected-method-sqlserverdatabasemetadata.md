---
title: deletesAreDetected 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.deletesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2cae17d96bae15b85dcd9258a0fcb4c45254aa0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>deletesAreDetected 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  표시 되는 행의 삭제 여부를 검색을 호출 하 여 검색할 수는 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean deletesAreDetected(int type)  
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
 **true 이면** 빈 행은 삭제 된 행을 대체 하는 경우. **false** 경우 삭제 된 행이 제거 됩니다.  
  
 사용 하는 경우는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스에서이 메서드는 반환 **true** TYPE_SS_SCROLL_KEYSET 커서에 대해 및 **false** 다른 모든 결과 집합 유형에 대 한 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 deletesAreDetected 메서드는 java.sql.DatabaseMetaData 인터페이스의 deletesAreDetected 메서드에 의해 지정 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 검색이 정방향 및 동적 커서에 대해 일시적 이기는 하지만 모든 업데이트 가능 커서 유형에 대해 삭제 된 행을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
