---
title: setBinaryStream 메서드 (SQLServerBlob) | Microsoft Docs
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
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c32868257eeebc4cfc24945d853e1440e34ee78
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841208"
---
# <a name="setbinarystream-method-sqlserverblob"></a>setBinaryStream 메서드(SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB 값을 쓰는 데 사용할 수 있는 스트림을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 BLOB 값에서 쓰기를 시작할 위치입니다.  
  
## <a name="return-value"></a>반환 값  
 출력 스트림입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 setBinaryStream 메서드는 java.sql.Blob 인터페이스의 setBinaryStream 메서드에 의해 지정 됩니다.  
  
 BLOB의 데이터는 출력 스트림에 의해 지정된 위치부터 덮어쓰여지며 BLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 바이트가 추가되고, 위치+2 이상(또는 0 이하)의 값을 전달하면 위치 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
