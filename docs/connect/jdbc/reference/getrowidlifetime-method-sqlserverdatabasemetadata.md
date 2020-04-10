---
title: getRowIdLifetime 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 317c0b44-fe3f-4142-9cab-e40e4c4fe070
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a158a2219e855add57523b20184c6f90df598a84
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921784"
---
# <a name="getrowidlifetime-method-sqlserverdatabasemetadata"></a>getRowIdLifetime 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL RowId 데이터 형식이 지원되는지 여부를 나타내는 상태를 반환합니다. 이 데이터 형식이 지원되는 경우 이 메서드는 RowId 개체가 유효한 상태로 있는 수명을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.RowIdLifetime getRowIdLifetime()  
```  
  
## <a name="return-value"></a>Return Value  
 RowIdLifetime 개체입니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0 릴리스에서 이 메서드는 java.sql.RowIdLifetime.ROWID_UNSUPPORTED 값을 반환합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getRowIdLifetime 메서드는 java.sql.DatabaseMetaData 인터페이스의 getRowIdLifetime 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
