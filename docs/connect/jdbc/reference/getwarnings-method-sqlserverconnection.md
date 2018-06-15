---
title: getWarnings 메서드 (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.getWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 15af39bf-6285-44cc-a021-7341e7a055c4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f232461aafbb9c5c5d35ac04e0723e968ea7ea8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839617"
---
# <a name="getwarnings-method-sqlserverconnection"></a>getWarnings 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 호출에서 보고 된 첫 번째 경고 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>반환 값  
 SQLWarning 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getWarnings 메서드는 java.sql.Connection 인터페이스의 getWarnings 메서드에 의해 지정 됩니다.  
  
 이후의 경고 첫 번째 SQLWarning에 연결 되며 getNextWarning 메서드를 사용 하 여 호출 됩니다. 닫혀 있는 연결에 대해 호출될 경우에는 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
