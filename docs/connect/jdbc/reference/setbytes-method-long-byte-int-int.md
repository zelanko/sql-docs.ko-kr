---
title: setBytes 메서드(long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee4ab641ede4d4ec614a306f9c0e08c9f16aa5ee
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974944"
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes 메서드(long, byte, int, int)
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
  
 *bytes*  
  
 BLOB에 쓸 바이트의 배열입니다.  
  
 *offset*  
  
 **byte** 배열에서 데이터를 읽기 시작할 위치의 오프셋입니다.  
  
 *len*  
  
 바이트 배열에서 BLOB으로 읽어 올 바이트 수입니다.  
  
## <a name="return-value"></a>Return Value  
 작성한 바이트 수가 들어 있는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>설명  
 이 setBytes 메서드는 java.sql.Blob 인터페이스의 setBytes 메서드에 의해 지정됩니다.  
  
 데이터는 지정된 위치부터 덮어쓰여지며 CLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 바이트가 추가되고, 위치+2 이상(또는 0 이하)의 값을 전달하면 위치 오류가 발생합니다. 길이가 0인 **byte** 배열을 전달하면 작성된 바이트가 없으므로 0이 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setBytes 메서드&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
