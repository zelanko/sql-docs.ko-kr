---
title: toString 메서드(DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e77b9be3-1a02-4769-8acf-ac71d48d6a76
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3acffe6a922084fd63e38a8e212b5cf86d6b278
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "71096904"
---
# <a name="tostring-method-datetimeoffset"></a>toString 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **DateTimeOffset** 개체의 문자열 표현을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>Return Value  
 **DateTimeOffset** 개체의 문자열 표현입니다.  
  
## <a name="remarks"></a>설명  
 문자열의 형식은 다음과 같습니다. `YYYY-MM-DD HH:mm:ss[.fffffff] [+|-]HH:mm`  
  
 반환된 문자열의 소수 자릿수 초는 선언된 전체 자릿수까지 0으로 채워집니다. 예를 들어 값이 “2010-03-10 12:34:56.78 -08:00”인 **datetimeoffset(6)** 은 DateTimeOffset.toString에 의해 “2010-03-10 12:34:56.780000 -08:00”으로 형식이 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
