---
title: truncate 메서드(SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.truncate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ef181e04-003a-442a-9b7e-0c508a7cc873
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddcb67b6a679cadaa33775d11987d90a735ca799
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80908465"
---
# <a name="truncate-method-sqlserverblob"></a>truncate 메서드(SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB을 지정된 길이로 자릅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *len*  
  
 BLOB의 새 길이입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>설명  
 이 truncate 메서드는 java.sql.Blob 인터페이스의 truncate 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
