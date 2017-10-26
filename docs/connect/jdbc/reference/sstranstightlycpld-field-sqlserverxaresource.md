---
title: "SSTRANSTIGHTLYCPLD 필드 (SQLServerXAResource) | Microsoft Docs"
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
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad4c44ab74c75a0f4d058edbad792cea721bdcd6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>SSTRANSTIGHTLYCPLD 필드(SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XID(XA 분기 트랜잭션 ID)가 다르지만 GTRID(전역 트랜잭션 ID)는 동일한 밀접하게 결합된 XA 트랜잭션을 허용하는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>필드 값  
 **int** 값 32768입니다.  
  
## <a name="remarks"></a>주의  
 각 트랜잭션은 XID(XA 분기 트랜잭션 ID)와 GTRID(전역 트랜잭션 ID)로 식별됩니다. 응용 프로그램이 Xid가 다르지만 gtrid는 동일한 밀접 하는 강력 하 게 결합 된 XA 트랜잭션을 사용할 수 있도록 설정 해야 합니다는 [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) XAResource.start 메서드의 flags 매개 변수에서 합니다. 이 플래그를 사용 하는 방법에 대 한 자세한 내용은 참조 [XA 트랜잭션 이해](../../../connect/jdbc/understanding-xa-transactions.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXAResource 필드](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [SQLServerXAResource 멤버](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 클래스](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

