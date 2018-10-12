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
manager: craigg
ms.openlocfilehash: 990cb7cccd972ac926824ca3f8d99de3f0d6e305
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687741"
---
# <a name="tostring-method-datetimeoffset"></a>toString 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문자열 표현을 반환 합니다 **DateTimeOffset** 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public String toString()  
```  
  
## <a name="return-value"></a>반환 값  
 문자열 표현을 합니다 **DateTimeOffset** 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 문자열의 형식은 *YYYY*-*MM*-*DD * * hh*:*mm*:*의*[. *fffffff*] [+ |-]*hh*:*mm*합니다.  
  
 반환된 문자열의 소수 자릿수 초는 선언된 전체 자릿수까지 0으로 채워집니다. 예를 들어를 **datetimeoffset(6)** 값을 사용 하 여 "2010-03-10 12:34:56.78-08:00"으로 DateTimeOffset.toString 형식이 되도록 "2010-03-10 12:34:56.780000-08:00"입니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
