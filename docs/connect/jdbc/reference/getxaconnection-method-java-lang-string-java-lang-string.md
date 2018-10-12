---
title: getXAConnection 메서드(java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276e0093-3d42-4f73-acc4-2b5b98245b40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75d79c0cb211a2d0da7b5e0f026d9ec2171d75d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694431"
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
  
 사용자 이름을 포함하는 **문자열**입니다.  
  
 *password*  
  
 암호가 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 XAConnection 개체입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 getXAConnection 메서드는 javax.sql.XADataSource 인터페이스의 getXAConnection 메서드에 의해 지정 됩니다.  
  
> [!NOTE]  
>  이 메서드는 일반적으로 XA 연결 풀 구현에서 호출되며 일반적인 JDBC 응용 프로그램 코드에서는 호출되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getXAConnection 메서드(SQLServerXADataSource)](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource 메서드](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 멤버](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 클래스](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
