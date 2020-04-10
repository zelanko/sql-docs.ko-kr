---
title: getMinutesOffset 메서드(DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 350a1f63eefa87eccbca7ba0a12c4381ab820854
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906164"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>getMinutesOffset 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  GMT를 기준으로 한 이 DateTimeOffset 개체의 오프셋(단위: 분)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Return Value  
 분 단위 오프셋입니다.  
  
## <a name="remarks"></a>설명  
 2010년 3월 8일, 11:35:48 -0800을 나타내는 DateTimeOffset 개체의 경우 getMinutesOffset은 값 480을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
