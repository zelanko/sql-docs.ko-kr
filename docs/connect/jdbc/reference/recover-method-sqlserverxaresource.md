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
manager: craigg
ms.openlocfilehash: 8ec96cd3f56b1710268ae951e39e98866fe1bd54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826821"
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
  
 **int** 다음 값 중 하나를 수행 하는 값: XAResource.TMSTARTRSCAN 또는 XAResource.TMENDRSCAN 또는 XAResource.TMNOFLAGS XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN 합니다.  
  
## <a name="return-value"></a>반환 값  
 Xid 개체입니다.  
  
## <a name="exceptions"></a>예외  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 이 recover 메서드는 javax.transaction.xa.XAResource 인터페이스의 recover 메서드에 의해 지정됩니다.  
  
 경우 매개 변수 **플래그** 없거나 XAResource.TMSTARTRSCAN XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN, 복구 검색이 진행에서 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerXAResource 메서드](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
