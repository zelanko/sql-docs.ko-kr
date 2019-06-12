---
title: setSavepoint 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.releaseSavepoint
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6b625ea-c7ce-4a32-a9e0-6d2b4321bfd8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f0888759172d95614a5c4d9aa96898f89a0e3068
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765585"
---
# <a name="releasesavepoint-method-sqlserverconnection"></a>releaseSavepoint 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 현재 트랜잭션에서 제거합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 현재 이 메서드가 지원되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void releaseSavepoint(java.sql.Savepoint savepoint)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *저장점*  
  
 저장 점 제거할 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 releaseSavepoint 메서드는 java.sql.Connection 인터페이스의 releaseSavepoint 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
