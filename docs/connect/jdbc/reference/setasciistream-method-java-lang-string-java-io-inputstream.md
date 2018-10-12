---
title: setAsciiStream 메서드 스트림 입력 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45d76d8dc1123cf17d95a0e6587b79168bedefb0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643951"
---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>setAsciiStream 메서드(java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 입력 스트림으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setAsciiStream 메서드는 java.sql.PreparedStatement 인터페이스의 setAsciiStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setAsciiStream&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
