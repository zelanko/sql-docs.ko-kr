---
title: getCharacterStream 메서드 (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d875e82b4db5e1725f43307348d27a6701e2a88d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697791"
---
# <a name="getcharacterstream-method-long-long"></a>getCharacterStream 메서드(long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **Clob** 데이터를 지정된 위치 및 길이의 문자 스트림 또는 Reader 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 검색할 부분 값의 첫 번째 문자에 대한 오프셋을 나타내는 **long**입니다.  
  
 *length*  
  
 검색할 부분 값의 문자 길이를 나타내는 **long**입니다.  
  
## <a name="return-value"></a>반환 값  
 포함 된 판독기 개체를 **Clob** 데이터입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getCharacterStream 메서드는 java.sql.Clob 인터페이스의 getCharacterStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getCharacterStream 메서드(SQLServerClob)](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
