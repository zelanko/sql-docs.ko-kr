---
title: SQLServerPreparedStatement 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96d2e01d4ca8d38b79906ee31cc5b50df0d8cb25
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970765"
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** SQLServerStatement  
  
 **구현:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>설명  
 SQLServerPreparedStatement는 매개 변수를 네이티브 Java 형식 및 많은 Java 개체 형식으로 제공하는 데 사용할 수 있는 메서드를 제공합니다. SQLServerPreparedStatement는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** 저장 프로시저를 사용하여 문을 준비한 다음, 이후에 이 문을 실행할 때마다 반환된 문 핸들을 다시 사용합니다. 이때 일반적으로 사용자가 제공하는 서로 다른 매개 변수를 사용합니다.  
  
 SQLServerPreparedStatement는 여러 개의 준비된 문이 단일 데이터베이스 왕복으로 실행되는 일괄 처리를 지원하여 런타임 성능을 향상시킵니다.  
  
 이 클래스는 SQLServerPreparedStatement 클래스, ISQLServerPreparedStatement 인터페이스, java.sql.PreparedStatement 인터페이스 및 래핑 해제용 SQLServerStatement에서 지원되는 클래스와 인터페이스에 대한 래핑 해제를 지원합니다. 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
