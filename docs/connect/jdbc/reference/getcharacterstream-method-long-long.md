---
title: "getCharacterStream 메서드 (long, long) | Microsoft Docs"
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
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba910c36ff82209a668ef6d96987330705703080
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-long-long"></a>getCharacterStream 메서드(long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  반환 된 **Clob** 데이터 판독기 개체 또는 지정 된 위치 및 길이 문자 스트림으로 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 A **긴** 검색할 부분 값의 첫 번째 문자를 오프셋을 나타내는입니다.  
  
 *length*  
  
 A **긴** 검색할 부분 값의 문자 길이 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 포함 하는 판독기 개체는 **Clob** 데이터입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getCharacterStream 메서드는 java.sql.Clob 인터페이스의 getCharacterStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getCharacterStream 메서드 &#40; SQLServerClob &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  

