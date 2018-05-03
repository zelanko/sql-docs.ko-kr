---
title: ISQLServerStatement 인터페이스 | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc5a8fb9479d5e66ae264c3327f78089a643eadc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isqlserverstatement-interface"></a>ISQLServerStatement 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 문 기능의 기본 구현을 나타냅니다. 이 인터페이스에 추가 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.sql.Statement  
  
## <a name="syntax"></a>구문  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>주의  
 이 인터페이스는 구현 하 여 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)합니다.  
  
 이 인터페이스를 노출 다음 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드:  
  
|메서드|자세한 내용은 다음을 참조하세요.|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
