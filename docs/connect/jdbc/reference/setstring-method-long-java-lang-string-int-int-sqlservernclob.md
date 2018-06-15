---
title: setString 메서드 (long, java.lang.String, int, int)-NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2d5e9f50-15b2-4c76-8bfc-3b5be49c2781
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d38e6265e5516f92155b4e69d7e7b2c61b8f2bd0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32844048"
---
# <a name="setstring-method-long-javalangstring-int-int-sqlservernclob"></a>setString 메서드(long, java.lang.String, int, int)(SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 오프셋 및 길이에 따라 지정된 된 위치에서 시작 NCLOB에 지정된 된 문자열을 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int setString(long pos,  
              java.lang.String str,  
              int offset,  
              int len)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 에 쓰기 시작할 위치는 **NCLOB**; 첫 번째 위치는 1입니다.  
  
 *str*  
  
 에 쓸 문자열은 **NCLOB**합니다.  
  
 *offset*  
  
 에 대 한 오프셋 *str* 를 쓸 문자 읽기를 시작 합니다.  
  
 *len*  
  
 쓸 문자 수입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 SetString 메서드가 java.sql.NClob 인터페이스의 setString 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerNClob 메서드](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 멤버](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 클래스](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
