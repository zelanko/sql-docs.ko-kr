---
title: getBinaryStream 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c68917aefc39cce459a2de12f09ac75a35cf04b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920534"
---
# <a name="getbinarystream-method-int"></a>getBinaryStream 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 해석되지 않은 바이트의 이진 스트림으로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getBinaryStream 메서드는 java.sql.ResultSet 인터페이스의 getBinaryStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 binary, varbinary, varbinary(max) 및 image에만 사용할 수 있습니다. 다른 데이터 형식에 이 메서드를 사용하려고 하면 예외가 발생합니다.  
  
 이 메서드가 값을 스트림으로 가져온 후에는 스트림에서 해당 데이터를 청크로 읽을 수 있습니다. 이 메서드는 큰 LONGVARBINARY 값을 검색하는 데 특히 적합합니다.  
  
> [!NOTE]  
>  반환된 스트림의 모든 데이터는 다른 열의 값을 가져오기 전에 읽어야 합니다. 다음에 getter 메서드를 호출하면 스트림이 암시적으로 닫힙니다. 또한 InputStream.available 메서드가 호출되면 사용 가능한 데이터가 있는지 여부에 관계없이 스트림이 0을 반환할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getBinaryStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
