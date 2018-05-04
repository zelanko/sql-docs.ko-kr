---
title: setCharacterStream 메서드 (java.lang.String, java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 88a8e89e-8817-4161-85b1-9a9a2fd01cdb
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b30af8cb6eef1b376d14bd612f67783be0b8d98d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-int"></a>setCharacterStream 메서드(java.lang.String, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문자 길이의 specifiedReader 개체를 지정된 된 매개 변수를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName,  
                              java.io.Reader value,  
                              int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *value*  
  
 유니코드 데이터를 포함 하는 판독기 개체입니다.  
  
 *length*  
  
 **int** 길이 문자 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setCharacterStream 메서드에 의해 지정 됩니다.  
  
 스트림의 길이에 지정 된 것과 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [setCharacterStream 메서드 (java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md) 응용 프로그램에서 길이 알 수 없는 스트림에서 열을 업데이트 하려는 경우.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
