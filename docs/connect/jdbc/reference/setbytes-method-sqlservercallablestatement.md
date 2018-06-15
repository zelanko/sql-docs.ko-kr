---
title: setBytes 메서드 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f264f1a6-ee35-4eaf-81d8-ecf99f03b35d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5990743ccdf751bbfab7afe80aa4927846c0380d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842048"
---
# <a name="setbytes-method-sqlservercallablestatement"></a>setBytes 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 배열에 지정된 된 매개 변수를 설정 **바이트** 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setBytes(java.lang.String sCol,  
                     byte[] b)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *B*  
  
 배열을 **바이트** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이전 버전의 드라이버에서 바이트 배열 간에 값을 변환할 SQLServerCallableStatement.setBytes를 사용할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식 **날짜**, **시간**, **datetime2** , 또는 **datetimeoffset**합니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
 이 setBytes 메서드는 java.sql.CallableStatement 인터페이스의 setBytes 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
