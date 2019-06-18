---
title: SQLServerBlob 생성자(SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aff7392d2aceab631e5e53cd446696f8ce15ab43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66773102"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 생성자(SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 및 **byte** 배열이 지정된 경우 [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) 클래스의 새 인스턴스를 초기화합니다.  
  
> [!NOTE]  
>  JDBC 드라이버 버전 2.0에서는 이 메서드가 사용되지 않습니다. 대신 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) 메서드를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결*  
  
 SQLServerConnection 개체입니다.  
  
 *data*  
  
 **바이트** 배열입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerBlob 생성자](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
