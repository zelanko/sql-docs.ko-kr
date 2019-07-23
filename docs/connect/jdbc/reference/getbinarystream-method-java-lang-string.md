---
title: getBinaryStream 메서드 (java. lang) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0ee14b90dd8aaffb178c81ea46e5ec914752e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953693"
---
# <a name="getbinarystream-method-javalangstring"></a>getBinaryStream 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 이름의 값을 해석되지 않은 바이트의 이진 스트림으로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getBinaryStream 메서드는 java. ResultSet 인터페이스의 getBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 binary, varbinary, varbinary(max) 및 image에만 사용할 수 있습니다. 다른 데이터 형식에 이 메서드를 사용하려고 하면 예외가 발생합니다.  
  
 이 메서드가 값을 스트림으로 가져온 후에는 스트림에서 해당 데이터를 청크로 읽을 수 있습니다. 이 메서드는 큰 LONGVARBINARY 값을 검색하는 데 특히 적합합니다.  
  
> [!NOTE]  
>  반환된 스트림의 모든 데이터는 다른 열의 값을 가져오기 전에 읽어야 합니다. 다음에 getter 메서드를 호출하면 스트림이 암시적으로 닫힙니다. 또한 InputStream.available 메서드가 호출되면 사용 가능한 데이터가 있는지 여부에 관계없이 스트림이 0을 반환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
