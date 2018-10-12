---
title: position 메서드 (byte, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3844d294c72539e752f944b604409b4967a8c166
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603935"
---
# <a name="position-method-byte-long"></a>position 메서드(byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 **byte** 배열 패턴과 시작 인덱스에 따라 BLOB에서 지정된 패턴이 있는 위치를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *bPattern*  
  
 검색할 패턴입니다.  
  
 *start*  
  
 검색할 시작 인덱스입니다.  
  
## <a name="return-value"></a>반환 값  
 패턴을 찾은 위치를 나타내는 **long** 값이거나, 패턴을 찾지 못한 경우 -1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 위치 메서드는 java.sql.Blob 인터페이스의 위치 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [position 메서드 &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
