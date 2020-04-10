---
title: position 메서드(java.lang.String, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86fad8ed-375a-42e1-b40e-1fa085957a2c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 432ee4fccc21a57130e1bccad9c43b50e2b992ba
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914379"
---
# <a name="position-method-javalangstring-long"></a>position 메서드(java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 시작 위치에 따라 CLOB에서 지정된 부분 문자열이 있는 문자 위치를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long position(java.lang.String searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *searchstr*  
  
 검색할 부분 문자열입니다.  
  
 *start*  
  
 검색을 시작할 위치이며, 첫 번째 위치는 1입니다.  
  
## <a name="return-value"></a>Return Value  
 부분 문자열이 나타나는 위치이며, 부분 문자열이 없으면 -1입니다. 첫 번째 위치는 1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 position 메서드는 java.sql.Clob 인터페이스의 position 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [position 메서드&#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
