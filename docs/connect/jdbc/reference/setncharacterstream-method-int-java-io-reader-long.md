---
title: "setNCharacterStream 메서드를 java.io.Reader 개체-긴 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36396dc9-f109-4da0-bd64-726704046bbf
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1659f34537ae65aabb505ff01fa9796ec558a3de
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setncharacterstream-method-int-javaioreader-long"></a>setNCharacterStream 메서드(int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 Reader 개체를 지정된 된 매개 변수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                  java.io.Reader value,  
                                                                long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
 *value*  
  
 매개 변수 값을 포함 하는 판독기 개체입니다.  
  
 *length*  
  
 A **긴** 매개 변수 값의 문자 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNCharacterStream 메서드는 java.sql.PreparedStatement 인터페이스의 setNCharacterStream 메서드에 의해 지정 됩니다.  
  
 에 대 한이 메서드를 사용 해야 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 데이터 형식입니다.  
  
 스트림의 길이에 지정 된 것 보다 다른 경우는 *길이* 매개 변수를 JDBC 드라이버는 경우 예외를 throw 행이 업데이트 되거나 삽입 합니다.  
  
 스트림의 길이 알 수 없으면는 *길이* 드라이버의 길이 상관 없이 스트림을 수락 해야 함을 나타내려면 매개 변수를-1로 설정할 수 있습니다. Sqljdbc4.jar을 JDBC 4.0 메서드를 사용 하면 권장 [setNCharacterStream 방법 &#40; int, java.io.Reader &#41;](../../../connect/jdbc/reference/setncharacterstream-method-int-java-io-reader.md) 응용 프로그램에서 길이 알 수 없는 스트림에서 열을 업데이트 하려는 경우.  
  
## <a name="see-also"></a>관련 항목:  
 [setNCharacterStream 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

