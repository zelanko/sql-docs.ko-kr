---
title: "updateBinaryStream 메서드 (int, java.io.InputStream) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.updateBinaryStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9be246a7-85fa-49fc-ad79-aabe97f5b280
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1199bdd667e4b24c39f987a37f48f841176ae05
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-int"></a>updateBinaryStream 메서드(java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 바이트 수를 포함하는 이진 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 AStringthat 열 레이블이 포함 되어 있습니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
 *length*  
  
 **int** 스트림의 길이 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 메서드를 선택 InputStream 개체에서 바이트 전달 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binary, varbinary, varbinary (max), 이미지, xml 및 udt 등의 이진 열입니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 프로그램 InputStream를 업데이트 하려면 사용 하 여는 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드.  
  
 스트림의 길이에 지정 된 것과 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [updateBinaryStream 메서드 &#40;java.lang.String, java.io.InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md) 응용 프로그램에서 길이 스트림에서 열을 업데이트 하려고 할 때 알 수 없는 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateBinaryStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
