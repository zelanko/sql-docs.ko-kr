---
title: SQLServerException 생성자(java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1cc42a09e455fa42d3f89b05903a22afc945424
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971127"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException 생성자(java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [개체](../../../connect/jdbc/reference/sqlserverexception-class.md), **문자열** 개체, **문자열** 개체, **StreamError** 개체 및 **부울**이 주어진 경우 **SQLServerException** 클래스의 새 인스턴스를 초기화합니다.

## <a name="syntax"></a>구문  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>매개 변수  
 *obj*  
  
 예외를 생성한 IO 버퍼입니다.

 *errText*  
  
 오류 문자를 포함하는 문자열입니다.
  
 *sqlState*  
  
 SQL 상태가 포함된 열거형 개체입니다.
 
 *streamError*  
  
 오류에 대한 정보를 포함하는 StreamError 개체입니다.
 
 *bStack*  
  
 스택 추적을 생성해야 하는지 여부를 나타내는 부울입니다.
  
## <a name="see-also"></a>참고 항목  
 [SQLServerException 생성자](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 클래스](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
