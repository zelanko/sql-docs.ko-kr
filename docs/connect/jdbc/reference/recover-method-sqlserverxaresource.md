---
title: recover 메서드 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92d7b0db997a6b77b43efb6d8104f629bb5507e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976025"
---
# <a name="recover-method-sqlserverxaresource"></a>recover 메서드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  리소스 관리자에서 준비된 트랜잭션 분기 목록을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *flags*  
  
 다음 값 중 하나를 사용할 수 있는 **int** 값: XAResource. TMSTARTRSCAN 또는 xaresource. TMSTARTRSCAN 또는 xaresource. TMNOFLAGS 또는 xaresource. TMSTARTRSCAN | XAResource. TMENDRSCAN.  
  
## <a name="return-value"></a>반환 값  
 Xid 개체입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 이 recover 메서드는 javax.transaction.xa.XAResource 인터페이스의 recover 메서드에 의해 지정됩니다.  
  
 매개 변수 **플래그가** XAResource입니다. tmstartrscan 또는 XARESOURCE. tmstartrscan | XAResource. TMENDRSCAN, 복구 검사가 진행 중 이어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
