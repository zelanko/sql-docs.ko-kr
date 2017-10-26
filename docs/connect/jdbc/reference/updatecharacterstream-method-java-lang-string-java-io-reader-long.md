---
title: "updateCharacterStream 메서드 (java.io.Reader, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e5e177c-7ed7-4d0c-8fa8-0e13daf46f4b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e54276942275e70bd2940dcf2d055bfb7cce2de3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatecharacterstream-method-javalangstring-javaioreader-long"></a>updateCharacterStream 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 문자 수를 포함하는 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateCharacterStream(java.lang.String columnLabel,  
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
 이 updateCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 선택한 텍스트 및 이진 열에 판독기 개체에서 유니코드 문자를 전달합니다. 여기에는 모든 텍스트 열과 binary, varbinary, varbinary(max), image 및 XML 열이 포함되지만 UDT 열은 포함되지 않습니다.  
  
 스트림의 길이에 지정 된 것 보다 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [updateCharacterStream 메서드 &#40;java.lang.String, java.io.Reader &#41;](../../../connect/jdbc/reference/updatecharacterstream-method-java-lang-string-java-io-reader.md) 응용 프로그램에서 길이 스트림에서 열을 업데이트 하려고 할 때 알 수 없는 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateCharacterStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

