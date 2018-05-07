---
title: SQLServerCallableStatement 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3813574070c53f16cd04ff262d7134c87d4ea85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  입력 및 출력 매개 변수와 함께 호출할 저장 프로시저 이름을 지정할 수 있도록 합니다. 이 클래스는 ? = call( ?, ..) 구문을 사용하여 반환 상태 값을 검색하는 기능도 제공합니다.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **구현:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **확장:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>주의  
 SQLServerCallableStatement 입력 및 출력 매개 변수와 함께 호출할 저장된 프로시저 이름을 지정할 수 있습니다. SQLServerCallableStatement와 반환 상태 값을 검색 하는 기능도 제공는 `? = call( ?, ..)` 구문입니다.  
  
 이 클래스는 SQLServerCallableStatement 클래스, ISQLServerCallableStatement 인터페이스, java.sql.CallableStatement 인터페이스 및 클래스와 인터페이스에 대 한 SQLServerPreparedStatement에서 지 원하는에 대 한 래핑 해제를 지원 합니다. 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
 지정 된 형식과 충돌을 입력 하는 경우에 형식에 대 한 호출 됩니다 set SQLServerCallableStatement 중 하나는 메서드 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), 마지막 SQLServerCallableStatement set 메서드에 의해 지정 된 형식이 사용 됩니다. 그러나 이로 인해 호환되지 않는 데이터 유형 변환 오류가 발생할 수 있습니다. SQLServerCallableStatement 설정 메서드를 호출 하지 않으면 첫 번째 지정 된 형식의 [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 호출이 사용 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0은 결과 집합 JDBC 4.0 권장 사항을 준수 및 OUT 매개 변수를 검색 하기 전에 업데이트 횟수를 검색 해야 합니다. 결과 집합 및 업데이트 횟수를 완전히 처리하기 전에 OUT 매개 변수가 검색된 경우 처리되지 않은 결과 집합 및 업데이트 횟수는 손실됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
