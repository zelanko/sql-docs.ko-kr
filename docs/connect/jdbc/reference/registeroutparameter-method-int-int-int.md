---
title: registerOutParameter 메서드 (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d902d4e0-881f-4182-814c-0ede9a8da7fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6948bf6b86160b1752a483b13f83abbfc467ef2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975947"
---
# <a name="registeroutparameter-method-int-int-int"></a>registerOutParameter 메서드(int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 서수 위치의 OUT 매개 변수를 지정된 JDBC 형식 및 소수 자릿수로 등록합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수의 서수 위치를 나타내는 **int**입니다.  
  
 *sqlType*  
  
 java.sql.Types에 정의된 JDBC 형식 코드입니다.  
  
 *scale*  
  
 소수점 이하의 자릿수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 registerOutParameter 메서드는 java. CallableStatement 인터페이스의 registerOutParameter 메서드에 의해 지정 됩니다.  
  
 JDBC driver 3.0부터 *sqlType* 가 **sendTimeAsDatetime** 형식일 때이 메서드의 동작은 connection 속성 ([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md))에 의해 수정 됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [ SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 자세한 내용은 [java. 시간 값을 서버로 보내는 방법 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [registerOutParameter 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
