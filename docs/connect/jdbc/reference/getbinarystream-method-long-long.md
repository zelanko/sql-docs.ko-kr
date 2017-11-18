---
title: "getBinaryStream 메서드 (long, long) | Microsoft Docs"
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
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d53bb0e01198d1c4ecb5c08068be4220a34b765c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-long-long"></a>getBinaryStream 메서드(long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 시작 위치와 길이를 사용하여 부분적 BLOB 값이 들어 있는 입력 스트림 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 검색할 부분 값의 첫 번째 바이트에 대한 오프셋입니다.  
  
 *length*  
  
 검색할 부분 값의 길이(바이트)입니다.  
  
## <a name="return-value"></a>반환 값  
 BLOB 데이터가 들어 있는 입력 스트림입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBinaryStream 메서드는 java.sql.Blob 인터페이스의 getBinaryStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

