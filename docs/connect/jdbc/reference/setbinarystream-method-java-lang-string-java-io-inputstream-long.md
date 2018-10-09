---
title: setBinaryStream 메서드 입력 스트림을-장기를 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d59c7327-c9dc-4e4f-9dff-19e1a3c62eb2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36ba3cf5fec53024faf83a83d7e9a24116f143be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849581"
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream-long"></a>setBinaryStream 메서드(java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 바이트 수를 포함하는 지정된 입력 스트림으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x,  
                            long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수의 이름을 포함하는 **문자열**입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
 *length*  
  
 길이(바이트)를 나타내는 입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setBinaryStream 메서드는 java.sql.CallableStatement 인터페이스의 setBinaryStream 메서드에 의해 지정 됩니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하는 경우에는 응용 프로그램에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [setBinaryStream 메서드(java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [setBinaryStream&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
