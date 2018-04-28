---
title: getResponseBuffering 메서드 (SQLServerStatement) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0946f0aba47904f8ceb0f02d84a741504fafc7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응답 버퍼링 모드를이 대 한 검색 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 포함 하는 소문자 **전체** 또는 **적응**합니다.  
  
## <a name="remarks"></a>주의  
 **적응** 필요할 때 최소 가능한 데이터를 버퍼링 하도록 지정 합니다.  
  
 **전체** 런타임 시 서버에서 전체 결과 읽도록 지정 합니다.  
  
 **적응** JDBC 드라이버 버전 2.0과 3.0의에서 기본값입니다. **전체** JDBC 드라이버 버전 2.0 이전이 기본값 이었습니다.  
  
 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setResponseBuffering 메서드 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
