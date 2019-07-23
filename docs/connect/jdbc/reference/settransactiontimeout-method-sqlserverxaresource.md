---
title: setTransactionTimeout 메서드 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 481843393f15998df059bb7a732c64010b2c8bf0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972284"
---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 개체에 대한 현재 트랜잭션 시간 제한 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *초*  
  
 **int** 값입니다.  
  
## <a name="return-value"></a>반환 값  
 제한 시간이 성공적으로 설정되었으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 이 setTransactionTimeout 메서드는 javax.sql 리소스 인터페이스의 setTransactionTimeout 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
