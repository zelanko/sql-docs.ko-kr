---
title: position 메서드(java.sql.Blob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fd642677405adf98cce23826775a0cab45221a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923185"
---
# <a name="position-method-javasqlblob-long"></a>position 메서드(java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 패턴과 시작 인덱스에 따라 BLOB에서 지정된 패턴이 있는 위치를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pattern*  
  
 검색할 패턴입니다.  
  
 *start*  
  
 검색할 시작 인덱스입니다.  
  
## <a name="return-value"></a>Return Value  
 패턴을 찾은 위치를 나타내는 **long** 값이거나, 패턴을 찾지 못한 경우 -1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 position 메서드는 java.sql.Blob 인터페이스의 position 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [position 메서드&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob 메서드](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 멤버](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 클래스](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
