---
title: getResponseBuffering 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf5a9ee4d4aa001103840ba8768ba338baa42db8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980406"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 응답 버퍼링 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Return Value  
 소문자 **full** 또는 **adaptive**가 들어 있는 **문자열**입니다.  
  
## <a name="remarks"></a>설명  
 **adaptive**는 필요할 때 가능한 최소한의 데이터를 버퍼링하도록 지정합니다.  
  
 **full**은 런타임에 서버의 전체 결과를 읽도록 지정합니다.  
  
 JDBC 드라이버 버전 2.0과 3.0에서는 **adaptive**가 기본값입니다. JDBC 드라이버 버전 2.0 이전에는 **full**이 기본값이었습니다.  
  
 응답 버퍼링 모드 사용에 대한 자세한 내용은 [적응 버퍼링 사용](../../../connect/jdbc/using-adaptive-buffering.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [setResponseBuffering 메서드(SQLServerStatement)](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
