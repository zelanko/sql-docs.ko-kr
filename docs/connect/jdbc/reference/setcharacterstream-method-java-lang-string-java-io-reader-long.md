---
title: setCharacterStream 메서드(java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 54fb2f13-f8d8-47b5-bec1-4a5af3e86a84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 304797651e93ea39269b9a68f810a3e98290eac8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929054"
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-long"></a>setCharacterStream 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 문자 길이의 지정된 java.io.Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *reader*  
  
 유니코드 데이터가 들어 있는 Reader 개체입니다.  
  
 *length*  
  
 스트림의 문자 수를 나타내는 **long**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setCharacterStream 메서드에 의해 지정됩니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하는 경우에는 애플리케이션에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [setCharacterStream 메서드(java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [setCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
