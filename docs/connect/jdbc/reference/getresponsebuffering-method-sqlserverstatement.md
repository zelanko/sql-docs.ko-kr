---
title: getResponseBuffering 메서드 (SQLServerStatement) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c682e28244bf85ce761ab6f8d0b54d5f5f054679
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680411"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 응답 버퍼링 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 소문자를 포함 하는 **전체** 하거나 **적응**합니다.  
  
## <a name="remarks"></a>Remarks  
 **adaptive**는 필요할 때 가능한 최소한의 데이터를 버퍼링하도록 지정합니다.  
  
 **full**은 런타임에 서버의 전체 결과를 읽도록 지정합니다.  
  
 **적응** JDBC 드라이버 버전 2.0과 3.0의에서 기본값입니다. **전체** JDBC 드라이버 버전 2.0 이전이 기본값 이었습니다.  
  
 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 선택 버퍼링](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setResponseBuffering 메서드(SQLServerStatement)](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
