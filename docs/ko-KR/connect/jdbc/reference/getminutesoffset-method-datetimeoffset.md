---
title: getMinutesOffset 메서드 (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6c768d1be182091db5306100c0b6ec239c4adc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 DateTimeOffset 개체의 gmt 기준 분 단위에서 오프셋을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>반환 값  
 분 단위 오프셋입니다.  
  
## <a name="remarks"></a>주의  
 2010 년 3 월 8 나타내는 DateTimeOffset 개체에 대 한 11시 35분: 48-0800을 getMinutesOffset 값 480을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
