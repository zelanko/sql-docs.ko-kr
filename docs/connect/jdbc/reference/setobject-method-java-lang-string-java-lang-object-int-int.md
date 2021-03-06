---
description: setObject 메서드(java.lang.String, java.lang.Object, int, int)
title: setObject 메서드(java.lang.String, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject (java.lang.String, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16f5f09a-51b5-423a-b52d-8c2eaa04e9ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92610692addf37ef83f9906453b398f43c53278d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458546"
---
# <a name="setobject-method-javalangstring-javalangobject-int-int"></a>setObject 메서드(java.lang.String, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 개체, 대상 형식 및 소수 자릿수를 사용하여 지정된 매개 변수의 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o,  
                      int n,  
                      int m)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *o*  
  
 **Object** 값입니다.  
  
 *n*  
  
 java.sql.Types에 정의된 대상 형식을 나타내는 **int**입니다.  
  
 *m*  
  
 소수점 이하의 자릿수를 나타내는 **int**입니다. NUMERIC 및 DECIMAL을 제외한 모든 형식의 경우에는 이 매개 변수가 무시됩니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setObject 메서드는 java.sql.CallableStatement 인터페이스의 setObject 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터 이 메서드의 동작은 **sendTimeAsDatetime** 연결 속성([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)에 의해 수정됩니다.  
  
 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setObject 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
