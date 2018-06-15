---
title: prepareCall 메서드 (java.lang.String, int, int) | Microsoft Docs
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
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b3eb39174f6164d76c4e60eada168987871abc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842168"
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall 메서드(java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 생성 하는 개체 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 지정 된 형식 및 동시성을 사용 하 여 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문을 포함 합니다.  
  
 *resultSetType*  
  
 **int** 결과 집합 유형을 나타내는입니다.  
  
 *resultSetConcurrency*  
  
 결과 집합 동시성 유형을 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 CallableStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 prepareCall 메서드는 java.sql.Connection 인터페이스의 prepareCall 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [prepareCall 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
