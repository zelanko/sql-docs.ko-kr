---
title: SQLServerException 생성자 (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daa4981f2ebb51c40725c1dd6e08935167b91914
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException 생성자 (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  새 인스턴스를 초기화는 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 지정 되 면 클래스는 **개체**, **문자열** 개체는 **문자열** 개체, 한 **int**, 및 **부울**합니다.

## <a name="syntax"></a>구문  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>매개 변수  
 *obj*  
  
 예외를 생성 하는 IO 버퍼입니다.

 *errText*  
  
 오류 텍스트를 포함 하는 문자열입니다.
  
 *sqlState*  
  
 SQL 상태를 포함 하는 열거형 개체입니다.
 
 *errNum*  
  
 예외에 대 한 오류 코드가 들어 있는 int입니다.
 
 *bStack*  
  
 스택 추적을 생성할지 여부를 나타내는 부울 값입니다.
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerException 생성자](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 클래스](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
