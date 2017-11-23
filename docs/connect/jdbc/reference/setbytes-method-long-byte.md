---
title: "setBytes 메서드 (long, 바이트) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerBlob.setBytes (long.byte[])
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e554122e5435a42f3c35c9a94904c6a329b23e82
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setbytes-method-long-byte"></a>setBytes 메서드 (long, 바이트)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 바이트 배열을 BLOB의 지정된 위치부터 쓴 다음 쓴 바이트 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 BLOB에 데이터를 쓰기 시작할 위치(1부터 시작)입니다.  
  
 *바이트*  
  
 BLOB에 쓸 바이트의 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 A **긴** 쓴 바이트 수를 지정 하는 값입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 setBytes 메서드는 java.sql.Blob 인터페이스의 setBytes 메서드에 의해 지정 됩니다.  
  
 데이터는 지정된 위치부터 덮어쓰여지며 BLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 바이트가 추가되고, 위치+2 이상(또는 0 이하)의 값을 전달하면 위치 오류가 발생합니다. 길이가 0 인 전달 **바이트** 배열 바이트 작성 된 0이 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setBytes 메서드 &#40; SQLServerBlob &#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
