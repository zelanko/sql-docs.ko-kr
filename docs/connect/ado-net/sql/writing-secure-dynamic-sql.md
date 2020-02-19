---
title: SQL Server에서 보안 동적 SQL 작성
description: 저장 프로시저를 사용하여 보안 동적 SQL을 작성하는 기술에 대해 설명합니다.
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d64b260d8d700afc8ed354d87de730e8c3b21f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253371"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>SQL Server에서 보안 동적 SQL 작성

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL 삽입은 악의적인 사용자가 유효한 입력 대신 Transact-SQL 문을 입력하는 프로세스입니다. 입력이 유효성 검사를 거치지 않고 서버로 직접 전달되고 애플리케이션이 삽입된 코드를 실수로 실행하는 경우 공격으로 인해 데이터가 손상되거나 제거될 수 있습니다.  
  
SQL Server는 구문상 유효한 모든 수신 쿼리를 실행하므로 SQL 문을 생성하는 모든 프로시저에 삽입과 관련한 취약성이 있는지 확인해야 합니다. 매개 변수가 있는 데이터도 숙련된 전문 공격자에 의해 조작될 수 있습니다. 동적 SQL을 사용하는 경우 명령을 매개 변수화해야 하고 매개 변수 값을 쿼리 문자열에 직접 포함하지 않아야 합니다.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>SQL 삽입 공격 분석  
삽입 프로세스는 텍스트 문자열을 미리 종료하고 새 명령을 덧붙이는 방법으로 수행됩니다. 삽입된 명령에는 실행 전에 덧붙여진 추가 문자열이 있을 수 있으므로 공격자는 주입된 문자열을 주석 표시인 "--"으로 종료합니다. 실행 시 이후 텍스트는 무시됩니다. 세미콜론(;) 구분 기호를 사용하여 여러 명령을 삽입할 수 있습니다.  
  
삽입된 SQL 코드가 구문상 정확하기만 하면 프로그래밍 방식으로 변조를 감지할 수 없습니다. 따라서 모든 사용자 입력의 유효성을 검사하고 생성된 SQL 명령을 사용 중인 서버에서 실행하는 코드를 주의 깊게 검토해야 합니다. 유효성 검사를 수행하지 않은 사용자 입력을 연결하지 않습니다. 문자열 연결은 스크립트 삽입이 발생하는 주요 진입점입니다.  
  
다음은 몇 가지 유용한 지침입니다.  
  
- 사용자 입력에서 직접 Transact-SQL 문을 작성하지 마세요. 저장 프로시저를 사용하여 사용자 입력의 유효성을 검사합니다.  
  
- 형식, 길이, 서식 및 범위를 테스트하여 사용자 입력의 유효성을 검사합니다. Transact-SQL QUOTENAME() 함수를 사용하여 시스템 이름을 이스케이프하거나 REPLACE() 함수를 사용하여 문자열의 모든 문자를 이스케이프합니다.  
  
- 애플리케이션의 각 계층에서 다중 계층 유효성 검사를 구현합니다.  
  
- 입력의 크기 및 데이터 형식을 테스트하고 적합한 제한 조치를 수행합니다. 그러면 의도적인 버퍼 오버런을 방지할 수 있습니다.  
  
- 문자열 변수의 내용을 테스트하고 예상 값만 허용합니다. 이진 데이터, 이스케이프 시퀀스 및 주석 문자를 포함하는 항목은 거부합니다.  
  
- XML 문서 작업에서는 입력한 스키마에 대해 모든 데이터의 유효성을 검사합니다.  
  
- 다중 계층 환경에서는 신뢰할 수 있는 영역으로 들어가기 전에 모든 데이터의 유효성을 검사해야 합니다.  
  
- 파일 이름을 생성하는 데 사용될 수 있는 필드에는 AUX, CLOCK$, COM1~COM8, CON, CONFIG$, LPT1~LPT8, NUL, PRN과 같은 문자열을 허용하지 않습니다.  
  
- 저장 프로시저 및 명령과 함께 <xref:Microsoft.Data.SqlClient.SqlParameter> 개체를 사용하여 형식 검사 및 길이 유효성 검사를 제공합니다.  
  
- 클라이언트 코드에서 <xref:System.Text.RegularExpressions.Regex> 식을 사용하여 잘못된 문자를 필터링합니다.  
  
## <a name="dynamic-sql-strategies"></a>동적 SQL 전략  
프로시저 코드에서 동적으로 생성된 SQL 문을 실행하면 소유권 체인이 중단되고 이로 인해 SQL Server가 동적 SQL에서 액세스하는 개체에 대해 호출자의 권한을 확인하게 됩니다.  
  
SQL Server에는 동적 SQL을 실행하는 사용자 정의 함수 및 저장 프로시저를 사용하여 데이터에 액세스할 수 있는 권한을 사용자에게 부여하는 방법이 있습니다.  
  
- Transact-SQL EXECUTE AS 절을 통한 가장 사용  
  
- 인증서로 저장 프로시저 서명  
  
### <a name="execute-as"></a>EXECUTE AS  
EXECUTE AS 절은 호출자의 권한을 EXECUTE AS 절에 지정된 사용자의 권한으로 바꿉니다. 중첩된 저장 프로시저 또는 트리거는 프록시 사용자의 보안 컨텍스트에서 실행됩니다. 이는 행 수준 보안을 사용하거나 감사를 요구하는 애플리케이션을 중단시킬 수 있습니다. 사용자의 ID를 반환하는 일부 함수는 원래 호출자가 아니라 EXECUTE AS 절에 지정된 사용자를 반환합니다. 실행 컨텍스트는 프로시저 실행 후 또는 REVERT 문이 실행된 후에만 원래 호출자로 되돌아갑니다.  
  
### <a name="certificate-signing"></a>인증서 서명  
인증서로 서명된 저장 프로시저를 실행하면 인증서 사용자에게 부여된 권한이 해당 호출자의 권한과 병합됩니다. 실행 컨텍스트는 동일하게 유지됩니다. 인증서 사용자는 호출자를 가장하지 않습니다. 저장 프로시저에 서명하려면 여러 단계를 구현해야 합니다. 프로시저를 수정할 때마다 다시 서명해야 합니다.  
  
### <a name="cross-database-access"></a>데이터베이스 간 액세스  
동적으로 생성된 SQL 문을 실행하는 경우에는 데이터베이스 간 소유권 체인이 작동하지 않습니다. SQL Server에서는 다른 데이터베이스의 데이터에 액세스하는 저장 프로시저를 만들고 두 데이터베이스 모두에 존재하는 인증서로 프로시저에 서명하여 이 문제를 피할 수 있습니다. 이렇게 하면 사용자에게 데이터베이스 액세스 또는 권한을 부여하지 않고 사용자가 프로시저에서 사용하는 데이터베이스 리소스에 액세스할 수 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[저장 프로시저](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md) 및 [SQL 삽입](../../../relational-databases/security/sql-injection.md)(SQL Server 온라인 설명서)|이들 항목에서는 저장 프로시저를 만드는 방법과 SQL 삽입이 작동하는 방식을 설명합니다.|  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server의 애플리케이션 보안 시나리오](application-security-scenarios-sql-server.md)
