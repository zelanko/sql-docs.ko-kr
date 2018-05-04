---
title: setNClob 메서드 (int, java.io.Reader, long) | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 11071f8f-0e9b-45f0-b600-aaef7e2815d8
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01c0ac7d15616dff3113826808154e405e2cf75d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setnclob-method-int-javaioreader-long"></a>setNClob 메서드(int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 문자 길이의 지정 된 판독기 개체에 지정된 된 매개 변수를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNClob(int parameterIndex,  
                    java.io.Reader reader,  
                    long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
 *판독기*  
  
 매개 변수 값을 나타내는 판독기 개체입니다.  
  
 *length*  
  
 **긴** 매개 변수 값의 문자 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNClob 메서드는 java.sql.PreparedStatement 인터페이스의 setNClob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setNClob 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
