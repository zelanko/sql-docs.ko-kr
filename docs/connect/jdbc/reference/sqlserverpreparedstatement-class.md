---
title: SQLServerPreparedStatement 클래스 | Microsoft Docs
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
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cffeadf5a5e7085e81349516dd8eb9393c937c81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** SQLServerStatement  
  
 **구현:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>주의  
 SQLServerPreparedStatement 네이티브 Java 형식 및 여러 Java 개체 형식으로 매개 변수를 제공할 수 있는 메서드를 제공 합니다. SQLServerPreparedStatement를 사용 하 여 문을 준비는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **sp_prepare** 저장된 프로시저 및 각 후속 실행 일반적으로 사용 하 여 문의 다른 반환 된 문 핸들 다시 사용 사용자가 제공한 매개 변수입니다.  
  
 SQLServerPreparedStatement 일괄 처리를 지원은 준비 된 문의 집합으로에서 실행 되는 단일 데이터베이스 왕복 런타임 성능을 향상 시킵니다.  
  
 이 클래스는 SQLServerPreparedStatement 클래스, ISQLServerPreparedStatement 인터페이스, java.sql.PreparedStatement 인터페이스 및 클래스와 인터페이스에 대 한 SQLServerStatement에서 지 원하는에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
