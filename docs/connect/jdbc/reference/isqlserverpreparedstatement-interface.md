---
title: ISQLServerPreparedStatement 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf87892e-5c34-4ac6-8258-c2a81e117b26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05fda4ea42c1819f3cbb4f16fcc7f02da2a06b8e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977428"
---
# <a name="isqlserverpreparedstatement-interface"></a>ISQLServerPreparedStatement 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다. 이 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.sql.PreparedStatement, [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public interface ISQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>설명  
 이 인터페이스는 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)에 의해 구현됩니다.  
  
 이 인터페이스는 다음 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드를 노출합니다.  
  
|방법|자세한 내용은 다음을 참조하세요.|  
|------------|-------------------------------|  
|public void setDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
