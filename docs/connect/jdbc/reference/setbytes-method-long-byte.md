---
title: setBytes 메서드 (long, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f0d47be46aac25807fd9f97bb3ee40cf96ffd4fd
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797643"
---
# <a name="setbytes-method-long-byte"></a>setBytes 메서드(long, byte)
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
  
 *bytes*  
  
 BLOB에 쓸 바이트의 배열입니다.  
  
## <a name="return-value"></a>반환 값  
 쓴 바이트 수를 지정하는 **long** 값입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 setBytes 메서드는 java.sql.Blob 인터페이스의 setBytes 메서드에 의해 지정됩니다.  
  
 데이터는 지정된 위치부터 덮어쓰여지며 BLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 바이트가 추가되고, 위치+2 이상(또는 0 이하)의 값을 전달하면 위치 오류가 발생합니다. 길이가 0인 **byte** 배열을 전달하면 작성된 바이트가 없으므로 0이 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setBytes 메서드 &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
