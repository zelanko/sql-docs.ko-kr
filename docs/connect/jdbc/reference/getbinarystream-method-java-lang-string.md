---
title: "getBinaryStream 메서드 (java.lang.String) | Microsoft Docs"
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
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff004671c2e261d055b49e1a1de3b0643c1fc94b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-javalangstring"></a>getBinaryStream 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 해석 되지 않은 바이트의 이진 스트림으로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 getBinaryStream 메서드에 의해 지정 됩니다.  
  
 이 방법을 사용 하 여만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binary, varbinary, varbinary (max), 및 이미지의 데이터 형식. 다른 데이터 형식에 이 메서드를 사용하려고 하면 예외가 발생합니다.  
  
 이 메서드가 값을 스트림으로 가져온 후에는 스트림에서 해당 데이터를 청크로 읽을 수 있습니다. 이 메서드는 큰 LONGVARBINARY 값을 검색하는 데 특히 적합합니다.  
  
> [!NOTE]  
>  반환된 스트림의 모든 데이터는 다른 열의 값을 가져오기 전에 읽어야 합니다. 다음에 getter 메서드를 호출하면 스트림이 암시적으로 닫힙니다. 또한, 스트림을 반환할 수 있습니다 0 InputStream.available 메서드를 호출할 때 데이터가 있는지 사용 가능한 지 여부를 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getBinaryStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
