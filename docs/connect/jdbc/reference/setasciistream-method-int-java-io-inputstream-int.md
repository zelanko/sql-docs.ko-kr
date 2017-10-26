---
title: "setAsciiStream 메서드 (int, java.io.InputStream, int) | Microsoft Docs"
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
- SQLServerPreparedStatement.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9436c39f-f1a1-484a-a75b-776a72ca70f4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aae3e7f9c249612d37b30c326d0a3fec2128295f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setasciistream-method-int-javaioinputstream-int"></a>setAsciiStream 메서드(int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 바이트 수를 지정 된 InputStream 개체에 지정 된 매개 변수 번호를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setAsciiStream(int n,  
                                 java.io.InputStream x,  
                                 int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 **int** 매개 변수 수를 나타내는입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
 *length*  
  
 바이트 수입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setAsciiStream 메서드는 java.sql.PreparedStatement 인터페이스의 setAsciiStream 메서드에 의해 지정 됩니다.  
  
 스트림의 길이에 지정 된 것과 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [setAsciiStream 메서드 &#40; int, java.io.InputStream &#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) 응용 프로그램에서 길이 알 수 없는 스트림에서 열을 업데이트 하려는 경우.  
  
## <a name="see-also"></a>관련 항목:  
 [setAsciiStream 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

