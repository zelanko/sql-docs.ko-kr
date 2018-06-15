---
title: getXAConnection 메서드 (java.lang.String, java.lang.String) | Microsoft Docs
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
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aec959822b00c79031226aaccbaf0085f68f79d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839328"
---
# <a name="getxaconnection-method-javalangstring-javalangstring"></a>getXAConnection 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 사용자 이름과 암호를 사용하여 실제 데이터베이스 연결을 설정하려고 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.sql.XAConnection getXAConnection(java.lang.String user,  
                                              java.lang.String password)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *user*  
  
 A **문자열** 사용자 이름이 들어 있는입니다.  
  
 *password*  
  
 A **문자열** 암호가 포함 된 합니다.  
  
## <a name="return-value"></a>반환 값  
 XAConnection 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 getXAConnection 메서드는 javax.sql.XADataSource 인터페이스의 getXAConnection 메서드에 의해 지정 됩니다.  
  
> [!NOTE]  
>  이 메서드는 일반적으로 XA 연결 풀 구현에서 호출되며 일반적인 JDBC 응용 프로그램 코드에서는 호출되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getXAConnection 메서드 &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource 메서드](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 멤버](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 클래스](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
