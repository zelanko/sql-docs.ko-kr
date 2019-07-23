---
title: valueOf 메서드 (java. Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c13438851fdc543a3567abdc001af5b5b9e726fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001567"
---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 메서드(java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 java.sql.Timestamp 값과 분 단위 오프셋을 나타내는 값을 사용하여 GMT를 기준으로 특정 오프셋의 시점을 나타내는 **DateTimeOffset** 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timestamp*  
  
 java.sql.Timestamp값입니다.  
  
 *minutesOffset*  
  
 분 단위 오프셋입니다.  
  
## <a name="return-value"></a>반환 값  
 GMT에서 지정 된 오프셋 (분)에 표시 되는 특정 시점을 나타내는 DateTimeOffset 개체를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
