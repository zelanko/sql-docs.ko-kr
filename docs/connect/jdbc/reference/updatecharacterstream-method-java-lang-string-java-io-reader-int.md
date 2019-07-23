---
title: updateCharacterStream 메서드(java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (java.lang.String, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08cfc4e0-83f0-4f2f-ac55-b381f34fe67f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20249faca3338a5f085de0e0071b20206b13dee1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996747"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader-int"></a>updateCharacterStream 메서드(java.lang.String, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 문자 수를 포함하는 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateCharacterStream(java.lang.String columnName,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *readerValue*  
  
 판독기 개체입니다.  
  
 *length*  
  
 스트림의 길이를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateCharacterStream 메서드는 updateCharacterStream 인터페이스의 메서드에 의해 지정 됩니다.  
  
 이 메서드는 판독기 개체의 유니코드 문자를 선택된 텍스트 및 이진 열에 전달합니다. 여기에는 모든 텍스트 열과 **binary**, **varbinary**, **varbinary(max)** , **image** 및 **xml** 열이 포함되지만 **udt** 열은 포함되지 않습니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하면 애플리케이션에서 길이를 알 수 없는 스트림에서 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [updateCharacterStream 메서드&#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-java-lang-string-java-io-reader.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateCharacterStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
