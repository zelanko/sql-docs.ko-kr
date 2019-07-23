---
title: updateBinaryStream 메서드(java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3c0fb5d-ca05-43f7-9f38-fba6cf3705c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4dd548fcd6342e4c69ea9acc1614d0bc899f7d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985327"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-long"></a>updateBinaryStream 메서드(java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 바이트 수를 포함하는 이진 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블을 포함하는 문자열입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
 *length*  
  
 스트림의 길이를 나타내는 **long**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateBinaryStream 메서드는 java. ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 InputStream 개체의 바이트를 binary, varbinary, varbinary(max), image, xml, udt와 같은 선택된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이진 열에 전달합니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 InputStream으로 업데이트하려면 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하는 경우에는 애플리케이션에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [updateBinaryStream 메서드&#40;java.lang.String, java.io.InputStream&#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
