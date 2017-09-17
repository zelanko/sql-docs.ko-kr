---
title: "updateNCharacterStream 메서드 문자열 판독기-긴) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db0a96a8-248f-4664-9c13-f480f309ab91
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3dc6bb87cb7539fb6060e2affbe0622a0d94cc6f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatencharacterstream-method-javalangstring-javaioreader-long"></a>updateNCharacterStream 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 바이트 수를 포함하는 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 A **문자열** 열 레이블이 들어 있는입니다.  
  
 *판독기*  
  
 판독기 개체입니다.  
  
 *length*  
  
 스트림의 길이입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateNCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 판독기 개체를 유니코드 문자를 전달 **nchar**, **nvarchar (max)**, **ntext**, 및 **xml** 열입니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
 스트림의 길이에 지정 된 것 보다 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [updateNCharacterStream 메서드 &#40;java.lang.String, java.io.Reader &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-java-lang-string-java-io-reader.md) 응용 프로그램에서 길이 스트림에서 열을 업데이트 하려고 할 때 알 수 없는 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateNCharacterStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
