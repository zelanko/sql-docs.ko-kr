---
title: setCharacterStream 메서드 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 43acac5b-5a8a-4685-bee6-7194d2d03a52
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 185d42ca1c9ded260ffe59b7f225ded72edb2984
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32841408"
---
# <a name="setcharacterstream-method-javalangstring-javaioreader"></a>setCharacterStream 메서드(java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 Reader 개체를 지정된 된 매개 변수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName,  
                                             java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *판독기*  
  
 유니코드 데이터를 포함 하는 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 setCharacterStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
