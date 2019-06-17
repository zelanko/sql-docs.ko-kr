---
title: setAsciiStream 메서드 (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aebc713ab5256527571eb1a4277caa74e53623d7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765053"
---
# <a name="setasciistream-method-sqlservernclob"></a>setAsciiStream 메서드(SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 위치에서부터 ASCII 문자를 이 **java.sql.NClob** 개체가 나타내는 **NCLOB** 값에 쓰는 데 사용할 스트림을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 **NCLOB** 개체에 쓰기 시작할 위치이며, 첫 번째 위치는 1입니다.  
  
## <a name="return-value"></a>반환 값  
 ASCII로 인코드된 문자를 쓸 수 있는 스트림을 나타내는 OutputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setAsciiStream 메서드 setAsciiStream java.sql.NClob 인터페이스의 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerNClob 메서드](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 멤버](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 클래스](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
