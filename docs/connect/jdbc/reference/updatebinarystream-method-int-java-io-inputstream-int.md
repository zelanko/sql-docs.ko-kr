---
title: updateBinaryStream 메서드(int, java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBinaryStream (int, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c8e55377-aaea-4415-8159-938fab1b2a93
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d511ac17f9afa4b387f62d5a8bf22d9a90a44dbd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925535"
---
# <a name="updatebinarystream-method-int-javaioinputstream-int"></a>updateBinaryStream 메서드(int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 지정된 바이트 수를 포함하는 이진 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
 *length*  
  
 스트림의 길이를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 updateBinaryStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 InputStream 개체의 바이트를 binary, varbinary, varbinary(max), image, xml, udt와 같은 선택된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이진 열에 전달합니다. 이 메서드를 사용하여 문자 열을 업데이트할 수는 없습니다. 문자 열을 InputStream으로 업데이트하려면 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
 스트림의 길이가 *length* 매개 변수에 지정된 길이와 다르면 행이 업데이트되거나 삽입될 때 JDBC 드라이버에서 예외가 발생합니다.  
  
 스트림의 길이를 알 수 없으면 *length* 매개 변수는 드라이버에서 스트림의 길이에 상관없이 스트림을 허용해야 함을 나타내는 -1로 설정될 수 있습니다. sqljdbc4.jar을 사용하면 길이를 알 수 없는 스트림에서 애플리케이션이 열을 업데이트하려고 할 때 JDBC 4.0 메서드 [updateBinaryStream 메서드&#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updatebinarystream-method-int-java-io-inputstream.md)를 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
