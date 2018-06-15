---
title: setAsciiStream 메서드 입력 스트림을를 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39a2e810b8ae602f6d5a6a2da2f2927a2e83db7c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841778"
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
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *x*  
  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setAsciiStream 메서드는 java.sql.PreparedStatement 인터페이스의 setAsciiStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
