---
title: setSavepoint 메서드 (java.lang.String) | Microsoft Docs
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
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a38bd657439dab6c705c176b6bbe90ab5f643546
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
 [setSavepoint 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
