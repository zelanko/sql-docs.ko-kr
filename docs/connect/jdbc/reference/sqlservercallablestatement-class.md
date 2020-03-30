---
title: SQLServerCallableStatement 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f47c034a720be5409d83868a7a61dd229ab70e24
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77600131"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  입력 및 출력 매개 변수와 함께 호출할 저장 프로시저 이름을 지정할 수 있도록 합니다. 이 클래스는 `? = call( ?, ..)` 구문으로 반환 상태 값을 검색하는 기능도 제공합니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **확장:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>설명  
 SQLServerCallableStatement를 사용하면 입력 및 출력 매개 변수와 함께 호출할 저장 프로시저 이름을 지정할 수 있습니다. SQLServerCallableStatement는 `? = call( ?, ..)` 구문으로 반환 상태 값을 검색하는 기능도 제공합니다.  
  
 이 클래스는 SQLServerCallableStatement 클래스, ISQLServerCallableStatement 인터페이스, java.sql.CallableStatement 인터페이스에 대한 래핑 해제와 SQLServerPreparedStatement에서 래핑 해제를 지원하는 클래스와 인터페이스를 지원합니다. 자세한 내용은 [래퍼와 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)를 참조하세요.  
  
 SQLServerCallableStatement 설정 메서드 중 하나가 형식에 대해 호출될 때 형식이 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)로 지정된 형식과 충돌할 경우, 최근 SQLServerCallableStatement 설정 메서드로 지정된 형식이 사용됩니다. 그러나 이로 인해 호환되지 않는 데이터 유형 변환 오류가 발생할 수 있습니다. SQLServerCallableStatement set 메서드가 호출되지 않은 경우 첫 번째 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 호출로 지정된 유형이 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0은 OUT 매개 변수를 검색하기 전에 결과 집합 및 업데이트 횟수를 검색해야 한다는 JDBC 4.0 권장 사항을 준수합니다. 결과 집합 및 업데이트 횟수를 완전히 처리하기 전에 OUT 매개 변수가 검색된 경우 처리되지 않은 결과 집합 및 업데이트 횟수는 손실됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
