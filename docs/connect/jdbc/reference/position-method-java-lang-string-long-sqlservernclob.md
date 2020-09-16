---
description: position 메서드(java.lang.String, long)(SQLServerNClob)
title: position 메서드(java.lang.String, long)(SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 46d4beec-831a-449f-98b6-322a80cc499a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a16db92eb2181cfe6db2ee9e6b1c3039acb6df93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433055"
---
# <a name="position-method-javalangstring-long-sqlservernclob"></a>position 메서드(java.lang.String, long)(SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 하위 문자열 *searchstr*이 이 **NClob** 개체에 의해 표현되는 **NCLOB** 값에 나타나는 문자 위치를 검색합니다.  
  
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
  
## <a name="return-value"></a>반환 값  
 부분 문자열이 나타나는 위치이며, 부분 문자열이 없으면 -1입니다. 첫 번째 위치는 1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 position 메서드는 java.sql.NClob 인터페이스의 position 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [position 메서드&#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 메서드](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 멤버](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 클래스](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
