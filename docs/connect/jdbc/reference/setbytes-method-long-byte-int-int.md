---
title: setBytes 메서드 (long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04162acd8f204306d60b5af73637a5835b818861
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes 메서드 (long, byte, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 바이트 배열의 전체 또는 일부 내용을 지정된 시작 위치, 오프셋 및 길이에 따라 BLOB에 쓴 다음 쓴 바이트 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 BLOB에 데이터를 쓰기 시작할 위치(1부터 시작)입니다.  
  
 *바이트*  
  
 BLOB에 쓸 바이트의 배열입니다.  
  
 *offset*  
  
 바이트 오프셋 배열에서 데이터를 읽기 시작할 위치의 **바이트** 배열입니다.  
  
 *len*  
  
 바이트 배열에서 BLOB으로 읽어 올 바이트 수입니다.  
  
## <a name="return-value"></a>반환 값  
 **int** 쓴 바이트 수가 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 setBytes 메서드는 java.sql.Blob 인터페이스의 setBytes 메서드에 의해 지정 됩니다.  
  
 데이터는 지정된 위치부터 덮어쓰여지며 CLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 바이트가 추가되고, 위치+2 이상(또는 0 이하)의 값을 전달하면 위치 오류가 발생합니다. 길이가 0 인 전달 **바이트** 배열 바이트 작성 된 0이 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setBytes 메서드 &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
