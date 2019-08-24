---
title: 데이터베이스의 주요 변경 내용은 엔진 SQL Server 2014의에서 기능 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d7b5bf6ff2324c8e63b030d03e36794faf0ec9d4
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419033"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 데이터베이스 엔진 기능의 주요 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 및 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 호환성이 손상되는 변경에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 애플리케이션, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
##  <a name="SQL14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]의 주요 변경 내용  
 새로운 문제가 없습니다.  
  
##  <a name="Denali"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]의 주요 변경 내용  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|기능|Description|  
|-------------|-----------------|  
|NEXT라는 테이블 또는 열에서 선택|시퀀스는 ANSI 표준 NEXT VALUE FOR 함수를 사용합니다. 테이블 또는 열 이름이 NEXT이 고 테이블 또는 열 별칭이 VALUE는 및 ANSI 표준 AS가 생략 된 경우 결과 문에서 오류가 발생할 수 있습니다. 이 문제를 해결하려면 ANSI 표준 AS 키워드를 포함합니다. 예를 들어 `SELECT NEXT VALUE FROM Table` 은 `SELECT NEXT AS VALUE FROM Table` 로 다시 작성하고, `SELECT Col1 FROM NEXT VALUE` 는 `SELECT Col1 FROM NEXT AS VALUE`로 다시 작성합니다.|  
|PIVOT 연산자|데이터베이스 호환성 수준이 110으로 설정되어 있는 경우 재귀 CTE(공통 테이블 식) 쿼리에 PIVOT 연산자를 사용할 수 없습니다. 쿼리를 다시 작성하거나 호환성 수준을 100 이하로 변경해야 합니다. 그룹화당 두 개 이상의 행이 있는 경우 재귀 CTE 쿼리에 PIVOT을 사용하면 잘못된 결과가 생성됩니다.|  
|sp_setapprole 및 sp_unsetapprole|현재 `OUTPUT`에 대한 쿠키 `sp_setapprole` 매개 변수는 정확한 최대 길이인 `varbinary(8000)`로 정의되어 있습니다. 그러나 현재 구현은 `varbinary(50)`입니다. 애플리케이션은 계속해서 `varbinary(8000)`를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다. 자세한 내용은 [sp_setapprole&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)을 참조하세요.|  
|EXECUTE AS|현재 EXECUTE AS에 대한 쿠키 OUTPUT 매개 변수는 정확한 최대 길이인 `varbinary(8000)`로 정의되어 있습니다. 그러나 현재 구현은 `varbinary(100)`입니다. 애플리케이션은 계속해서 `varbinary(8000)`를 예약하여 후속 릴리스에서 쿠키 반환 크기가 늘어날 경우에도 애플리케이션이 제대로 작동할 수 있도록 해야 합니다. 자세한 내용은 [EXECUTE AS&#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql)를 참조하세요.|  
|sys.fn_get_audit_file 함수|사용자 정의 감사 이벤트를 지원할 수 있도록 두 개의 열(**user_defined_event_id** 및 **user_defined_information**)이 추가되었습니다. 이름으로 열을 선택하지 않는 애플리케이션에서는 예상보다 많은 열이 반환될 수 있습니다. 이름으로 열을 선택하거나, 이러한 추가 열을 허용하도록 애플리케이션을 조정해야 합니다.|  
|WITHIN 예약 키워드|WITHIN은 이제 예약 키워드입니다. 따라서 이름이 'within'인 개체 또는 열에 대한 참조는 실패합니다. 개체 또는 열의 이름을 바꾸거나 대괄호 또는 따옴표를 사용하여 이름을 구분합니다.  `SELECT * FROM [within]`) 을 입력합니다.|  
|`time` 또는 `datetime2` 형식의 계산 열에 대한 CAST 및 CONVERT 연산|이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 `time` 및 `datetime2` 데이터 형식 중 하나가 계산 열 식에서 사용되는 경우를 제외하고 이러한 데이터 형식에 대한 CAST 및 CONVERT 연산의 기본 스타일이 121입니다. 계산 열의 경우 기본 스타일은 0입니다. 이 동작은 자동 매개 변수화와 관련된 쿼리에서 이러한 연산이 만들어지고 사용될 때 또는 제약 조건 정의에 사용될 때 계산 열에 영향을 줍니다.<br /><br /> 호환성 수준 110에서 `time` 및 `datetime2` 데이터 형식의 CAST 및 CONVERT 연산에 대한 기본 스타일은 항상 121입니다. 쿼리에 이전 동작이 적용되는 경우 110보다 낮은 호환성 수준을 사용하거나, 해당 쿼리에서 스타일 0을 명시적으로 지정해야 합니다.<br /><br /> 데이터베이스를 호환성 수준 110으로 업그레이드할 경우 디스크에 저장된 사용자 데이터는 변경되지 않습니다. 수동으로 이 데이터를 적절하게 수정해야 합니다. 예를 들어 SELECT INTO를 사용하여 위에서 설명한 계산 열 식이 포함된 원본에서 테이블을 만든 경우 계산 열 정의 자체가 아니라 스타일 0을 사용하는 데이터가 저장됩니다. 스타일 121과 일치하도록 이 데이터를 수동으로 업데이트해야 합니다.|  
|ALTER TABLE|ALTER TABLE 문에는 두 부분(schema.object)으로 구성된 테이블 이름만 허용됩니다. 이제 다음 형식을 사용 하 여 테이블 이름을 지정 하는 컴파일 시 오류 117 실패 합니다.<br /><br /> server.database.schema.table<br /><br /> .database.schema.table<br /><br /> ..schema.table<br /><br /> 이전 버전에서는 server.database.schema.table 형식을 지정할 경우 오류 4902가 반환되었습니다. 그러나 .database.schema.table 또는 ..schema.table 형식을 지정하면 작업이 성공했습니다. 이 문제를 해결하려면 네 부분으로 구성된 접두사를 사용하지 않아야 합니다.|  
|메타데이터 찾아보기|이제 FOR BROWSE 또는 SET NO_BROWSETABLE ON을 사용하여 뷰를 쿼리하면 기본 개체의 메타데이터가 아니라 뷰의 메타데이터가 반환됩니다. 현재 이 동작은 메타데이터를 찾아보는 다른 방법과 일치합니다.|  
|SOUNDEX|데이터베이스 호환성 수준 110에서는 SOUNDEX 함수가 새 규칙을 구현하므로 이 함수에서 계산된 값과 이전 호환성 수준에서 계산된 값이 달라질 수 있습니다. 호환성 수준 110으로 업그레이드한 후 SOUNDEX 함수를 사용하는 인덱스, 힙 또는 CHECK 제약 조건을 다시 작성해야 할 수 있습니다. 자세한 내용은 [SOUNDEX&#40;Transact-SQL&#41;](/sql/t-sql/functions/soundex-transact-sql)를 참조하세요.
|실패한 DML 문에 대한 행 개수 메시지|[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 [!INCLUDE[ssDE](../includes/ssde-md.md)]는 DML 문이 실패할 경우 클라이언트에 RowCount가 0인 TDS DONE 토큰을 지속적으로 보냅니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 실패한 문이 TRY-CATCH 블록에 포함되어 있고 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 의해 자동으로 매개 변수가 지정되거나 TRY-CATCH 블록이 실패한 문과 동일한 수준에 있지 않은 경우 잘못된 값 -1이 클라이언트에 보내집니다. 예를 들어 TRY-CATCH 블록에서 저장 프로시저를 호출할 경우 프로시저의 DML 문이 실패하면 클라이언트는 잘못된 값 -1을 받게 됩니다.<br /><br /> 이 잘못된 동작이 적용되는 애플리케이션에서는 오류가 발생합니다.|  
|SERVERPROPERTY ('버전')|[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 인스턴스의 설치된 제품 버전입니다. 이 속성 값을 사용하여 설치된 제품에서 지원하는 기능 및 최대 CPU 수와 같은 제한을 확인합니다.<br /><br /> 설치 된 Enterprise 버전에 따라 반환할 수 있습니다 ' Enterprise Edition' 또는 ' Enterprise Edition: 코어 기반 라이선스 '. Enterprise 버전은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 단일 인스턴스별 최대 컴퓨팅 용량에 따라 다릅니다. 계산 용량 제한에 대 한 자세한 내용은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]를 참조 하세요 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)합니다.|  
|CREATE LOGIN|합니다 `CREATE LOGIN WITH PASSWORD = '` *암호* `' HASHED` 옵션에서 만든 해시와 함께 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7 또는 이전 버전입니다.|  
|`datetimeoffset`에 대한 CAST 및 CONVERT 연산|날짜 및 시간 형식에서 `datetimeoffset`으로 변환할 때 지원되는 유일한 스타일은 0 또는 1입니다. 다른 모든 변환 스타일은 오류 9809를 반환합니다. 예를 들어 다음 코드는 오류 9809를 반환합니다.<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>동적 관리 뷰  
  
|보기|Description|  
|----------|-----------------|  
|sys.dm_exec_requests|명령 열이 `nvarchar(16)`에서 `nvarchar(32)`로 변경됩니다.|  
|sys.dm_os_memory_cache_counters|다음과 같은 열 이름이 바뀌었습니다.<br /><br /> single_pages_kb이 되었습니다. <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           이제: pages_in_use_kb|  
|sys.dm_os_memory_cache_entries|Pages_allocated_count 열 이름이 바뀐된 pages_kb 되었습니다.|  
|sys.dm_os_memory_clerks|열 multi_pages_kb 제거 되었습니다.<br /><br /> Single_pages_kb 열 이름이 바뀐된 pages_kb 되었습니다.|  
|sys.dm_os_memory_nodes|다음과 같은 열 이름이 바뀌었습니다.<br /><br /> single_pages_kb이 되었습니다. <br />                            pages_kb<br /><br /> multi_pages_kb이 되었습니다. <br />                            foreign_committed_kb|  
|sys.dm_os_memory_objects|다음 열의 이름이 바뀌었습니다.<br /><br /> pages_allocated_count이 되었습니다.<br />                            pages_in_bytes<br /><br /> max_pages_allocated_count 되었습니다: max_pages_in_bytes|  
|sys.dm_os_sys_info|다음과 같은 열 이름이 바뀌었습니다.<br /><br /> physical_memory_in_bytes가 되었습니다. <br />                            physical_memory_kb<br /><br /> bpool_commit_target이 이제: <br />                            committed_target_kb<br /><br /> bpool_visible은 이제 됩니다. <br />                            visible_target_kb<br /><br /> virtual_memory_in_bytes가 되었습니다. <br />                            virtual_memory_kb<br /><br /> bpool_commited가 되었습니다.<br />                            committed_kb|  
|sys.dm_os_workers|로캘 열이 제거되었습니다.|  
  
### <a name="catalog-views"></a>카탈로그 뷰  
  
|보기|Description|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|새로운 열인 is_system이 sys.data_spaces 및 sys.partition_functions에 추가되었습니다. sys.partition_schemes 및 sys.filegroups는 sys.data_spaces의 열을 상속합니다.<br /><br /> 이 열의 값이 1이면 개체가 전체 텍스트 인덱스 조각에 사용됨을 나타냅니다.<br /><br /> sys.partition_functions, sys.partition_schemes 및 sys.filegroups에서 새 열은 마지막 열이 아닙니다. 따라서 이러한 카탈로그 뷰에서 반환된 열의 순서에 의존하는 기존 쿼리를 수정해야 합니다.|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>SQL CLR 데이터 형식(geometry, geography 및 hierarchyid)  
 공간 데이터 형식 및 hierarchyid 형식을 포함하는 **Microsoft.SqlServer.Types.dll**어셈블리가 버전 10.0에서 버전 11.0으로 업그레이드되었습니다. 이 어셈블리를 참조하는 사용자 지정 애플리케이션에서는 다음 조건에 해당될 때 오류가 발생할 수 있습니다.  
  
-   컴퓨터에서 사용자 지정 응용 프로그램을 이동 하는 경우 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 만 있는 컴퓨터에 설치 된 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 가 설치 된 응용 프로그램 실패로 인해의 참조 된 버전 10.0 합니다 **SqlTypes** 어셈블리 존재 하지 않습니다. `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`라는 오류 메시지가 나타날 수 있습니다.  
  
-   참조 하는 경우는 **SqlTypes** 어셈블리 버전 11.0 버전 10.0도 설치 되 고이 오류 메시지가 표시 될 수 있습니다. `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   .NET 3.5, 4 또는 4.5를 대상으로 하는 사용자 지정 애플리케이션에서 **SqlTypes** 어셈블리 버전 11.0을 참조하는 경우 SqlClient는 기본적으로 이 어셈블리의 버전 10.0을 로드하므로 애플리케이션 오류가 발생합니다. 이 오류는 애플리케이션이 다음 메서드 중 하나를 호출할 때 발생합니다.  
  
    -   `GetValue` 클래스의 `SqlDataReader` 메서드  
  
    -   `GetValues` 클래스의 `SqlDataReader` 메서드  
  
    -   `SqlDataReader` 클래스의 대괄호 인덱스 연산자 []  
  
    -   `ExecuteScalar` 클래스의 `SqlCommand` 메서드  
  
 다음 메서드 중 하나를 사용하여 이 문제를 해결할 수 있습니다.  
  
-   코드에서 위에 나열된 Get 메서드 대신 다음 예와 같이 CLR [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시스템 형식을 검색하는 `GetSqlBytes` 메서드를 호출하여 이 문제를 해결할 수 있습니다.  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   다음 예와 같이 애플리케이션 구성 파일에 어셈블리 리디렉션을 사용하여 이 문제를 해결할 수 있습니다.  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   SqlClient가 어셈블리의 버전 11.0을 로드하도록 연결 문자열에서 "Type System Version" 특성에 대해 "SQL Server 2012" 값을 지정하여 이 문제를 해결할 수 있습니다. 이 연결 문자열 특성은 .NET 4.5 이상에서만 사용할 수 있습니다.  
  
-   `assemblyBinding` 태그는 `runtime` 태그에 싸여 있어야 합니다.  
  
### <a name="support-for-awe"></a>AWE 지원  
 32비트 AWE(Address Windowing Extensions) 지원이 중단되었습니다. 이로 인해 32비트 운영 체제의 성능이 저하될 수 있습니다. 많은 양의 메모리를 사용하는 설치의 경우 64비트 운영 체제로 마이그레이션해야 합니다.  
  
### <a name="xquery-functions-are-surrogate-aware"></a>서로게이트 인식 XQuery 함수  
 W3C 권장 구성에 따라 XQuery 함수 및 연산자는 상위 범위의 유니코드 문자를 UTF-16 인코딩의 단일 문자 모양으로 나타내는 서로게이트 쌍을 계산할 수 있어야 합니다. 그러나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 문자열 함수가 서로게이트 쌍을 단일 문자로 인식하지 못했습니다. 문자열 길이 계산 및 부분 문자열 추출-와 같은 일부 문자열 작업-잘못 된 결과 반환 합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 이제 UTF-16을 완전하게 지원하여 서로게이트 쌍을 올바르게 처리할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 XML 데이터 형식은 올바른 형식의 서로게이트 쌍만 허용합니다. 그러나 XQuery 함수에 잘못된 서로게이트 쌍이나 부분 서로게이트 쌍이 문자열 값으로 전달될 수 있으므로 일부 경우 몇몇 함수에서는 여전히 정의되지 않거나 예기치 않은 결과가 반환될 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 XQuery를 사용하는 경우에는 문자열 값을 생성할 때 다음과 같은 방법을 사용하는 것이 좋습니다.  
  
-   상수 문자열 값을 이진 값으로 제공합니다. 이 방법을 사용하더라도 잘못된 서로게이트 쌍이나 부분 서로게이트 쌍은 여전히 전달될 수 있습니다.  
  
-   문자 엔터티를 지정하여 상수 문자열 값을 제공합니다. 이 방법을 사용하면 잘못된 서로게이트 쌍이 전달되지 않습니다. XQuery 함수에는 높은 수준의 문자에 대한 단일 문자 엔터티가 필요합니다. 이러한 함수는 서로게이트 쌍 문자에 대한 문자 엔터티가 제공될 경우 오류를 발생시킵니다.  
  
-   **sql:column** 또는 **sql:variable**을 사용하여 외부 값을 가져옵니다. 이러한 방법을 사용하더라도 잘못된 서로게이트 쌍이나 부분 서로게이트 쌍은 여전히 제공될 수 있습니다.  
  
#### <a name="affected-xquery-functions-and-operators"></a>영향을 받는 XQuery 함수 및 연산자  
 다음 XQuery 함수 및 연산자는 이제 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 UTF-16 서로게이트 쌍을 올바르게 처리합니다.  
  
-   **fn:string-length**. 그러나 잘못된 서로게이트 쌍이나 부분 서로게이트 쌍이 인수로 전달될 경우 **string-length** 의 동작은 정의되어 있지 않습니다.  
  
-   **fn:substring**  
  
-   **fn:contains** 그러나 부분 서로게이트 쌍이 값으로 전달될 경우 **contains** 는 올바른 형식의 서로게이트 쌍에 포함된 부분 서로게이트 쌍을 찾을 수 있으므로 예기치 않은 결과를 반환할 수 있습니다.  
  
-   **fn:concat** 그러나 부분 서로게이트 쌍이 값으로 전달될 경우 **concat** 는 잘못된 서로게이트 쌍이나 부분 서로게이트 쌍을 생성할 수 있습니다.  
  
-   비교 연산자 및 **order by** 절. 비교 연산자에는 +, \<, >, \<=, > =, `eq`를 `lt`를 `gt`를 `le`, 및 `ge`합니다.  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>시스템 프로시저에 대한 분산 쿼리 호출  
 `OPENQUERY`를 통한 일부 시스템 프로시저에 대한 분산 쿼리 호출은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 서버에서 다른 서버로 호출될 경우 실패합니다. 이는 [!INCLUDE[ssDE](../includes/ssde-md.md)]이 프로시저에 대한 메타데이터를 검색할 수 없는 경우에 발생합니다. `SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')`) 을 입력합니다.  
  
#### <a name="isolation-level-and-sp_reset_connection"></a>격리 수준 및 sp_reset_connection  
 연결의 격리 수준은 클라이언트 드라이버에 의해 다음과 같은 방식으로 처리됩니다.  
  
-   모든 기본 드라이버(SNAC, MDAC, ODBC)는 sp_reset_connection 때 격리 수준(앱 설정을 기반으로 함)을 설정합니다.  
  
-   ADO.NET의 경우 기본적으로 풀에서 가져오는 연결에 따라(및 애플리케이션이 다른 격리 수준을 사용하는 경우) 임의 격리 수준이 적용됩니다. ADO.NET 풀은 내부적으로 투명하게 연결을 재활용할 수 있으므로 풀에서 어떤 항목이 나올지 예측할 수 없습니다.  
  
-   JDBC 드라이버의 경우 ADO.NET과 동일한 동작이 적용됩니다.  
  
     애플리케이션은 원하는 항목을 가져오기 위해 연결을 연 후에 항상 명시적으로 격리 수준을 설정해야 합니다.  
  
     JDBC 연결을 풀링할 수 있으므로 애플리케이션은 임의 격리 수준을 적용받아 이러한 격리 수준에 대해 모를 수도 있습니다.  
  
 이전 버전과의 호환성을 유지하기 위해 이 새로운 동작은 TDS 7.4부터 최신 클라이언트에만 적용됩니다.  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **호환성 수준에 따라 새 동작**  
  
 다음 함수 및 연산자는 호환성 수준이 110 이상인 경우에만 위에 설명된 새 동작을 보여 줍니다.  
  
-   **fn:contains**  
  
-   **fn:concat**  
  
-   비교 연산자 및 **order by** 절  
  
 **새 동작 함수에 대 한 기본 네임 스페이스 URI에 따라 다릅니다.**  
  
 새 동작을 설명한 경우에만 위에 기본 네임 스페이스 URI에 해당 하는 최종 권장 구성의 네임 스페이스, 다음 함수를 보여 [ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions)합니다. 호환성 수준이 110 이상인 경우 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서는 기본적으로 이 네임스페이스에 기본 함수 네임스페이스를 바인딩합니다. 그러나 이러한 함수는 호환성 수준에 상관없이 이 네임스페이스가 사용되는 경우 새 동작을 보여 줍니다.  
  
-   **fn:string-length**  
  
-   **fn:substring**  
  
##  <a name="KJKatmai"></a> 에서 주요 변경 내용 SQL Server 2008/s q L Server 2008 r2  
 이 섹션에는 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에 도입된 주요 변경 내용이 포함되어 있습니다. [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]에 도입된 변경 내용은 없습니다.  
  
### <a name="collations"></a>데이터 정렬  
  
|기능|Description|  
|-------------|-----------------|  
|새로운 데이터 정렬|Windows Server 2008에서 제공하는 것과 똑같은 데이터 정렬이 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에 도입되었습니다. 이러한 80개의 새로운 데이터 정렬은 언어 정확도가 향상되었으며 *_100 버전 참조로 표시되어 있습니다. 서버 또는 데이터베이스에서 새 데이터 정렬을 사용하도록 선택할 경우 이전 클라이언트 드라이버가 설치된 클라이언트에서 이러한 데이터 정렬을 인식하지 못할 수 있으므로 주의해야 합니다. 데이터 정렬이 인식되지 못할 경우 애플리케이션이 오류를 반환하고 실패할 수 있습니다. 다음과 같은 해결 방법을 고려해 보십시오.<br /><br /> 클라이언트 운영 체제를 업그레이드하여 기본 시스템 데이터 정렬을 업데이트합니다.<br /><br /> 클라이언트에 데이터베이스 클라이언트 소프트웨어가 설치되어 있는 경우에는 해당 데이터베이스 클라이언트 소프트웨어에 서비스 업데이트를 적용하는 것이 좋습니다.<br /><br /> 클라이언트의 코드 페이지에 매핑되는 기존 데이터 정렬을 선택합니다.|  
  
### <a name="common-language-runtime-clr"></a>CLR(공용 언어 런타임)  
  
|기능|Description|  
|-------------|-----------------|  
|CLR 어셈블리|데이터베이스를 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]로 업그레이드하면 새로운 데이터 형식을 지원하는 `Microsoft.SqlServer.Types` 어셈블리가 자동으로 설치됩니다. 업그레이드 관리자 규칙에서는 이름이 충돌하는 사용자 형식이나 어셈블리를 검색합니다. 업그레이드 관리자는 충돌하는 어셈블리의 이름을 바꾸고 충돌하는 형식의 이름을 바꾸거나 코드에서 두 부분으로 된 이름을 사용하여 기존 사용자 형식을 참조하도록 알려 줍니다.<br /><br /> 데이터베이스 업그레이드에서 이름이 충돌하는 사용자 어셈블리가 발견되면 해당 어셈블리의 이름이 자동으로 바뀌고 데이터베이스가 주의 대상 모드로 설정됩니다.<br /><br /> 업그레이드 중에 이름이 충돌하는 사용자 형식이 발견된 경우에는 특별한 조치가 취해지지 않습니다. 업그레이드 후에는 기존 사용자 형식과 새 시스템 형식이 모두 존재하게 됩니다. 사용자 형식은 두 부분으로 된 이름을 통해서만 사용할 수 있습니다.|  
|CLR 어셈블리|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]은 GAC(전역 어셈블리 캐시)의 라이브러리를 업데이트하는 .NET Framework 3.5 SP1을 설치합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 지원되지 않는 라이브러리가 등록되어 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 업그레이드하면 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 응용 프로그램이 작동을 중지할 수 있습니다. 이는 GAC의 라이브러리를 제공하거나 업그레이드해도 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 내부의 어셈블리는 업데이트되지 않기 때문입니다. 어셈블리가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스와 GAC에 모두 포함되어 있는 경우 해당 어셈블리의 두 복사본이 정확하게 일치해야 합니다. 일치하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] CLR 통합에서 해당 어셈블리를 사용할 때 오류가 발생합니다. 자세한 내용은 [Supported .NET Framework Libraries](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)을 참조하세요.<br /><br /> 데이터베이스를 업그레이드한 후 ALTER ASSEMBLY 문을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 내부의 어셈블리 복사본을 제공하거나 업그레이드합니다. 자세한 내용은 [기술 자료 문서 949080](https://go.microsoft.com/fwlink/?LinkId=154563)을 참조하십시오.<br /><br /> 애플리케이션에서 사용 중인 .NET Framework 라이브러리가 지원되는지 여부를 확인하려면 데이터베이스에서 다음 쿼리를 실행합니다.<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|CLR 루틴|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]로 업그레이드한 후 CLR 사용자 정의 함수, 사용자 정의 집계 또는 UDT(사용자 정의 형식) 내에 가장을 사용하면 응용 프로그램이 오류 6522와 함께 실패할 수 있습니다. 다음 시나리오는 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서는 성공하지만 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 실패합니다. 해결 방법은 각 시나리오별로 설명되어 있습니다.<br /><br /> CLR 사용자 정의 함수, 사용자 정의 집계 또는 UDT 메서드의 가장을 사용 하는 형식의 매개 변수가 `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text`, `image`, 또는 큰 UDT 합니다 없는 **DataAccessKind.Read** 특성입니다. 이 문제를 해결하려면 메서드에 **DataAccessKind.Read** 특성을 추가하고 어셈블리를 다시 컴파일한 후 루틴 및 어셈블리를 다시 배포하십시오.<br /><br /> 가장을 수행하는 **Init** 메서드가 있는 CLR 테이블 반환 함수 이 문제를 해결하려면 메서드에 **DataAccessKind.Read** 특성을 추가하고 어셈블리를 다시 컴파일한 후 루틴 및 어셈블리를 다시 배포하십시오.<br /><br /> 가장을 수행하는 **FillRow** 메서드가 있는 CLR 테이블 반환 함수 이 문제를 해결하려면 **FillRow** 메서드에서 가장을 제거하십시오. **FillRow** 메서드를 사용하여 외부 리소스에 액세스해서는 안 됩니다. 대신 **Init** 메서드를 사용해서 외부 리소스에 액세스하십시오.|  
  
### <a name="dynamic-management-views"></a>동적 관리 뷰  
  
|보기|Description|  
|----------|-----------------|  
|sys.dm_os_sys_info|cpu_ticks_in_ms 및 sqlserver_start_time_cpu_ticks 열은 제거되었습니다.|  
|sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|resource_semaphore_id 열은 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 고유한 ID가 아닙니다. 이러한 변경 내용은 쿼리 실행 문제를 해결하는 데 영향을 줄 수 있습니다. 자세한 내용은 [sys.dm_exec_query_resource_semaphores &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql)합니다.|  
  
### <a name="errors-and-events"></a>오류 및 이벤트  
  
|기능|Description|  
|-------------|-----------------|  
|로그인 오류|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서 SQL 로그인을 사용하여 Windows 인증만 사용하도록 구성된 서버에 연결하면 오류 18452가 반환됩니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 대신 오류 18456이 반환됩니다.|  
  
### <a name="showplan"></a>실행 계획  
  
|기능|Description|  
|-------------|-----------------|  
|실행 계획 XML 스키마|새 **SeekPredicateNew** Showplan XML 스키마 고 바깥쪽 xsd 시퀀스에 요소가 추가 됩니다 (**SqlPredicatesType**)로 변환 되는  **\<xsd: choice >** 항목입니다. 이제 실행 계획 XML에 하나 이상의 **SeekPredicate** 요소 대신 하나 이상의 **SeekPredicateNew** 요소가 표시될 수 있습니다. 이러한 두 요소는 함께 사용할 수 없습니다. **SeekPredicate** 는 이전 버전과의 호환성을 위해 실행 계획 XML 스키마에 유지되지만 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 에서 생성된 쿼리 계획에는 **SeekPredicateNew** 요소가 포함될 수 있습니다. **SeekPredicate** 요소가 없을 경우 ShowPlanXML/BatchSequence/Batch/Statements/StmtSimple/QueryPlan/RelOp/IndexScan/SeekPredicates 노드에서 **SeekPredicate** 자식만 검색해야 하는 응용 프로그램은 실패할 수 있습니다. 이 노드에서 **SeekPredicate** 또는 **SeekPredicateNew** 요소를 사용하도록 애플리케이션을 다시 작성하십시오. 자세한 내용은|  
|실행 계획 XML 스키마|실행 계획 XML 스키마의 **ObjectType** 복합 유형에 새로운 **IndexKind** 특성이 추가되었습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스키마에 대해 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 계획의 유효성을 엄격하게 검사하는 응용 프로그램은 실패합니다.|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|기능|Description|  
|-------------|-----------------|  
|ALTER_AUTHORIZATION_DATABASE DDL 이벤트|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서 DDL 이벤트 ALTER_AUTHORIZATION_DATABASE가 실행되면 DDL(데이터 정의 언어) 작업에서 보안 개체의 엔터티 유형이 개체인 경우 EVENTDATA xml의 **ObjectType** 요소에 값 'object'가 반환됩니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 실제 유형(예: 'table' 또는 'function')이 반환됩니다.|  
|CONVERT|CONVERT 함수에 잘못된 스타일이 전달되는 경우 변환 유형이 이진에서 문자 또는 문자에서 이진이면 오류가 반환됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 잘못된 스타일이 이진에서 문자 및 문자에서 이진 변환의 기본 스타일로 설정됩니다.|  
|어셈블리에 대한 GRANT/DENY/REVOKE EXECUTE|어셈블리에 대해 EXECUTE 권한을 부여, 거부 또는 취소할 수 없습니다. 이 권한은 아무런 효과가 없으며 이제 이 권한을 사용하면 오류가 발생합니다. 대신 어셈블리 메서드를 참조하는 저장 프로시저 또는 함수에 대해 EXECUTE 권한을 부여, 거부 또는 취소하십시오.|  
|시스템 형식에 대한 사용 권한 GRANT/DENY/REVOKE|시스템에 형식에 대해 사용 권한을 부여, 거부 또는 취소할 수 없습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 이러한 문은 성공하지만 아무런 영향을 주지 않습니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 오류가 반환됩니다.|  
|GROUP BY|GROUP BY 절은 GROUP BY 목록에 사용되는 식에서 하위 쿼리를 포함할 수 없습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이전 버전에서 허용됩니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 144 오류가 반환됩니다.<br /><br /> 예를 들어 다음 코드는 SQL Server 2005에서는 성공하고 SQL Server 2008에서는 실패합니다.<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|OUTPUT 절|비결정적 동작을 방지하기 위해 OUTPUT 절은 뷰 또는 인라인 테이블 반환 함수의 열이 다음 중 한 가지 방법으로 정의된 경우 이러한 열을 참조할 수 없습니다.<br /><br /> 하위 쿼리<br /><br /> 사용자 또는 시스템 데이터 액세스를 수행하거나 이러한 액세스를 수행하는 것으로 간주되는 사용자 정의 함수<br /><br /> 해당 정의에서 사용자 또는 시스템 데이터 액세스를 수행하는 사용자 정의 함수가 포함된 계산 열<br /><br /> <br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 OUTPUT 절에서 이러한 열을 감지하면 4186 오류가 발생합니다. 자세한 내용은 [MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md)을 참조하세요.|  
|OUTPUT INTO 절|OUTPUT INTO 절의 대상 테이블에 대해서는 트리거가 활성화될 수 없습니다.|  
|순위 사전 계산 서버 수준 옵션|이 옵션은 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 지원되지 않습니다. 현재 이 기능을 사용하는 애플리케이션을 가능한 한 빨리 수정하십시오.|  
|READPAST 테이블 힌트|스냅샷 격리에서 READPAST 힌트를 지정할 수 없습니다.<br /><br /> READ_COMMITED_SNAPSHOT 및 ALLOW_SNAPSHOT_ISOLATION 데이터베이스 옵션 중 하나라도 ON으로 설정된 경우 READPAST 힌트는 무시됩니다. 하지만 READPAST 힌트에 READCOMMITTEDLOCK을 결합하면 READPAST 동작이 차단 READCOMMITTED 힌트와 같아집니다.|  
|sp_helpuser|Sp_helpuser 저장 프로시저의 결과 집합에 반환 되는 다음과 같은 열 이름이 변경 되었습니다.<br /><br /> GroupName 되었습니다.<br />                            RoleName<br /><br /> Group_name은 이제:<br />                            Role_name<br /><br /> Group_id 되었습니다.<br />                            Role_id<br /><br /> Users_in_group 되었습니다.<br />                            Users_in_role|  
|Transparent Data Encryption|TDE(투명한 데이터 암호화)는 I/O 수준에서 수행됩니다. 따라서 페이지 구조는 메모리에서 암호화되지 않으며 페이지가 디스크에 기록될 때만 암호화됩니다. 데이터베이스 파일과 로그 파일은 모두 암호화됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 일반 페이지 액세스 메커니즘(예: 데이터 또는 로그 파일 직접 검사)을 사용하지 않는 타사 응용 프로그램은 데이터가 파일에 암호화되어 있기 때문에 데이터베이스에서 TDE를 사용할 경우 오류가 발생합니다. 이러한 응용 프로그램은 Window 암호화 API를 활용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 외부에서 데이터를 해독하는 솔루션을 개발할 수 있습니다.|  
  
### <a name="xquery"></a>XQuery  
  
|기능|Description|  
|-------------|-----------------|  
|날짜/시간 지원|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서 `xs:time`, `xs:date` 및 `xs:dateTime` 데이터 형식에는 표준 시간대가 지원되지 않았습니다. 표준 시간대 데이터는 UTC 표준 시간대에 매핑됩니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 표준 준수 동작을 제공함에 따라 다음과 같은 사항이 변경되었습니다.<br /><br /> 표준 시간대가 없는 값은 유효성이 검사됩니다.<br /><br /> 제공된 표준 시간대 또는 표준 시간대가 없는 상태가 유지됩니다.<br /><br /> 내부 스토리지 표현이 수정되었습니다.<br /><br /> 저장된 값 분석 기능이 개선되었습니다.<br /><br /> 음수 연도 표기가 허용되지 않습니다.<br /><br /> <br /><br /> 참고: 새로운 형식 값에 따라 응용 프로그램 및 XQuery 식을 수정하십시오.|  
|XQuery 및 Xpath 식|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]에서는 XQuery 또는 XPath 식 내에 콜론(':')으로 시작하는 단계를 사용할 수 있습니다. 예를 들어 다음 문의 경로 식 내에는 콜론으로 시작하는 이름 테스트(`CTR02)` 가 포함되어 있습니다.<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> 이러한 사용법은 XML 표준에 맞지 않으므로 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서는 이와 같이 사용할 수 없습니다. 오류 9341이 반환됩니다. (n$/CTR02)와 같이 앞에 오는 콜론을 제거하거나 (n$/p1:CTR02)와 같이 이름 테스트에 접두사를 지정하십시오.|  
  
### <a name="connecting"></a>Connecting  
  
|기능|Description|  
|-------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client에서 SSL을 사용하여 연결|이전에는 완화된 유효성 검사로 인해 해당 제목이 FQDN(정규화된 도메인 이름)을 지정하는 인증서와 함께 "SERVER=shortname; FORCE ENCRYPTION=true"를 사용하는 애플리케이션인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client를 통해서도 연결할 수 있었습니다. SQL Server 2008 R2에서는 인증서에 FQDN 제목을 적용하여 보안을 강화합니다. 완화된 유효성 검사를 사용하는 애플리케이션에서는 다음 조치 중 하나를 취해야 합니다.<br /><br /> 연결 문자열에 FQDN 사용<br /><br /> -이 옵션은 연결 문자열의 SERVER 키워드가 응용 프로그램 외부에서 구성 된 경우 응용 프로그램을 다시 컴파일하지 않아도 됩니다.<br /><br /> -이 옵션은 해당 연결 문자열이 하드 코딩 된 응용 프로그램에 대해 작동 하지 않습니다.<br /><br /> -이 옵션은 단순한 이름 갖는 미러된 서버 응답 이후 데이터베이스 미러링을 사용 하는 응용 프로그램에 대 한 작동 하지 않습니다.|  
||짧은 이름에 대해 FQDN에 매핑할 별칭 추가<br /><br /> -이 옵션은 해당 연결 문자열이 하드 코딩 된 응용 프로그램에 대해서도 작동 합니다.<br /><br /> -이 옵션은 공급자 받은 장애 조치 파트너 이름에 대 한 별칭을 조회 하지 하므로 데이터베이스 미러링을 사용 하는 응용 프로그램에 대 한 작동 하지 않습니다.|  
||짧은 이름에 대해 인증서 발급<br /><br /> -이 옵션은 모든 응용 프로그램에 대 한 작동합니다.|  

## <a name="Yukon"></a> SQL Server 2005의에서 주요 변경 내용  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>관련 항목  
 [SQL Server 2014에서에서 사용 되지 않는 데이터베이스 엔진 기능](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)   
 [SQL server 2014 데이터베이스 엔진 기능의 동작 변경 내용](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md?view=sql-server-2014)   
 [SQL Server 2014에서에서 지원 되지 않는 데이터베이스 엔진 기능](discontinued-database-engine-functionality-in-sql-server-2016.md?view=sql-server-2014)   
 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
 [SQL Server 2014에서 관리 도구 기능의 주요 변경 내용](breaking-changes-to-management-tools-features-in-sql-server-2014.md?view=sql-server-2014)  
  
