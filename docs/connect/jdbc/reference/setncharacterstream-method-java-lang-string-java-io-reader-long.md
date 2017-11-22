---
title: "setNCharacterStream 메서드 긴 판독기 개체 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: af9a1ba8-7980-43fa-88e5-14f6cc5e897c
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 291c94f63ebc86869682e769ef93b93c86f60ffc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setncharacterstream-method-javalangstring-javaioreader-long"></a>setNCharacterStream 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 문자 길이의 지정 된 판독기 개체에 지정된 된 매개 변수를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                     java.io.Reader value,  
                     long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름을 나타내는입니다.  
  
 *value*  
  
 판독기 개체입니다.  
  
 *length*  
  
 A **긴** 스트림의 문자 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setNCharacterStream 메서드에 의해 지정 됩니다.  
  
 에 대 한이 메서드를 사용 해야 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 데이터 형식입니다.  
  
 스트림의 길이에 지정 된 것 보다 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [setNCharacterStream 메서드 &#40;java.lang.String, java.io.Reader &#41;](../../../connect/jdbc/reference/setncharacterstream-method-java-lang-string-java-io-reader.md) 응용 프로그램에서 길이 스트림에서 열을 업데이트 하려고 할 때 알 수 없는 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setNCharacterStream 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
