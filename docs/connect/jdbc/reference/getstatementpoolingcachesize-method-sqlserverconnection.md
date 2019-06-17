---
title: getStatementPoolingCacheSize 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 773b5bc08affdc513e7ee5897fbd4b0f3c24993e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773897"
---
# <a name="getstatementpoolingcachesize-method-sqlserverconnection"></a>getStatementPoolingCacheSize 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 이 연결에 대 한 준비 된 문 캐시의 크기를 반환합니다. '0' 캐싱을 사용 하도록 설정 하지 것을 의미 합니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getStatementPoolingCacheSize()  
```  

## <a name="return-value"></a>반환 값
 **int** 의 값이 포함 된 **statementPoolingCacheSize** 연결 속성입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
