---
title: "setSavepoint 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5674fa6b4bff1518a4b693b06980e40a2da463b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setsavepoint-method-javalangstring"></a>setSavepoint 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 트랜잭션에 지정 된 이름의 저장 점을 만들고 새 반환 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 점을 나타내는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sName*  
  
 A **문자열** 저장 점의 이름이 들어 있는 값입니다.  
  
## <a name="return-value"></a>반환 값  
 저장 점으로 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setSavePoint 메서드는 java.sql.Connection 인터페이스의 setSavePoint 메서드에 의해 지정 됩니다.  
  
 *sName* 인수에 의해 자동으로 이스케이프 됩니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setSavepoint 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
