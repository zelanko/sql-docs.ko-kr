---
title: "SQLServerBlob 생성자 (SQLServerConnection, byte) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76b8fe0d719a2eb5f53fe20502d0cd3fe35ca6eb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 생성자 (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  새 인스턴스를 초기화는 [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) 지정 되 면 클래스는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 및 **바이트** 배열입니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0에서는 이 메서드가 사용되지 않습니다. 대신를 사용 하 여는 [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결*  
  
 
          SQLServerConnection 개체입니다.  
  
 *데이터*  
  
 A **바이트** 배열입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerBlob 생성자](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

