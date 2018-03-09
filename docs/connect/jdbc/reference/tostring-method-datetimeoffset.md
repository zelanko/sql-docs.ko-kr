---
title: "toString 메서드 (DateTimeOffset) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c6dd16bfddfa331fd2647bd8fd191ac91941e71
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="tostring-method-datetimeoffset"></a>toString 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문자열 표현을 반환 된 **DateTimeOffset** 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>반환 값  
 문자열 표현을 **DateTimeOffset** 개체입니다.  
  
## <a name="remarks"></a>주의  
 문자열의 형식은 *YYYY*-*MM*-*DD**hh*:*mm*: *ss*[. *fffffff*] [+ |-]*hh*:*mm*합니다.  
  
 반환된 문자열의 소수 자릿수 초는 선언된 전체 자릿수까지 0으로 채워집니다. 예를 들어는 **datetimeoffset(6)** 값이 "2010-03-10 12:34:56.78-08:00" DateTimeOffset.toString으로 형식이 지정 됩니다 "2010-03-10 12:34:56.780000-08:00"입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
