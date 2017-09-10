---
title: "작업 그룹 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 46dce7ed81cdce215cfbff8f5fcce0900a9309a0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  리소스 관리자 작업 그룹을 만든 후 이 작업 그룹을 리소스 관리자 리소스 풀에 연결합니다. 리소스 관리자의 일부 버전에서 사용할 수 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE WORKLOAD GROUP group_name  
[ WITH  
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING {   
    [ pool_name | "default" ]    
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]   
    } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *o u p _*  
 작업 그룹에 대한 사용자 정의 이름입니다. *group_name* 은 영숫자로 최대 128 자를 사용할 수의 인스턴스 내에서 고유 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대 한 규칙을 준수 해야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 중요도 = {LOW | **보통** | 높은}  
 작업 그룹에 있는 요청의 상대적 중요도를 지정합니다. 중요도는 다음 중 하나이며 MEDIUM이 기본값이 됩니다.  
  
-   LOW  
  
-   MEDIUM  
  
-   HIGH  
  
> [!NOTE]  
>  내부적으로 각 중요도 설정은 계산에 사용된 멤버로 저장됩니다.  
  
 IMPORTANCE는 리소스 풀에 대해 로컬입니다. 같은 리소스 풀 내에 있는 다른 중요도의 작업 그룹은 서로 영향을 주지만 다른 리소스 풀의 작업 그룹에는 영향을 주지 않습니다.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*값*  
 단일 요청이 풀에서 사용할 수 있는 최대 메모리 양을 지정합니다. 이 비율은 MAX_MEMORY_PERCENT에서 지정한 리소스 풀 크기에 따라 바뀝니다.  
  
> [!NOTE]  
>  지정된 양은 쿼리 실행 부여 메모리만 참조합니다.  
  
 *값* 0 또는 양의 정수 여야 합니다. 허용된 범위 *값* 은 0에서 100 까지입니다. 에 대 한 기본 설정은 *값* 은 25입니다.  
  
 다음에 유의하세요.  
  
-   설정 *값* 0은 차단 쿼리와 사용자 정의 작업 그룹에 SORT 및 HASH JOIN 연산 함께 실행에서 합니다.  
  
-   설정을 권장 하지는 않습니다 *값* 서버 수 다른 동시 쿼리를 실행 중인 경우 가능한 메모리를 충분히 따로 설정 수 없기 때문에 70 보다 큽니다. 71 이상의 값으로 설정하면 쿼리 시간 초과 오류 8645가 발생할 수 있습니다.  
  
> [!NOTE]  
>  쿼리 메모리 요구 사항이 이 매개 변수에 지정된 제한을 초과하는 경우 서버는 다음을 수행합니다.  
>   
>  사용자 정의 작업 그룹의 경우 서버는 메모리 요구 사항이 제한 수준 아래로 낮아지거나 병렬 처리 수준이 1이 될 때까지 쿼리 병렬 처리 수준을 줄이려고 합니다. 그래도 쿼리 메모리 요구 사항이 제한보다 클 경우 오류 8657이 발생합니다.  
>   
>  내부 및 기본 작업 그룹의 경우 서버는 쿼리가 필요한 메모리를 가져오도록 허용합니다.  
>   
>  두 경우 모두 서버에 실제 메모리가 부족하면 시간 초과 오류 8645가 발생할 수 있습니다.  
  
 REQUEST_MAX_CPU_TIME_SEC =*값*  
 요청이 사용할 수 있는 최대 CPU 시간(초)을 지정합니다. *값* 0 또는 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값* 0은 무제한을 의미 합니다.  
  
> [!NOTE]  
>  최대 시간이 초과하는 경우 리소스 관리자가 요청을 종료하지는 않지만 이벤트가 생성됩니다. 자세한 내용은 참조 [CPU 임계값을 초과 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)합니다.  
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*값*  
 메모리(작업 버퍼 메모리)가 부여될 때까지 쿼리가 대기할 수 있는 최대 시간(초)을 지정합니다.  
  
> [!NOTE]  
>  메모리 부여 제한 시간에 도달할 때마다 쿼리가 실패하지는 않습니다. 쿼리는 너무 많은 쿼리가 동시에 실행되는 경우에만 실패합니다. 그렇지 않을 경우 쿼리에 최소한의 메모리만 부여되어 쿼리 성능이 떨어질 수 있습니다.  
  
 *값* 0 또는 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값*, 0, 쿼리 비용에 따른 내부 계산을 사용 하 여 최대 시간을 결정 합니다.  
  
 MAX_DOP =*값*  
 병렬 요청의 최대 DOP(병렬 처리 수준)를 지정합니다. *값* 0 또는 양의 정수 여야 합니다. 허용된 범위 *값* 은 0에서 64 까지입니다. 에 대 한 기본 설정은 *값*, 0, 글로벌 설정을 사용 합니다. MAX_DOP는 다음과 같이 처리합니다.  
  
-   MAX_DOP는 작업 그룹 MAX_DOP를 초과하지 않는 한 쿼리 힌트로 유효합니다. MAXDOP 쿼리 힌트 값이 리소스 관리자를 사용하여 구성된 값을 초과하는 경우 데이터베이스 엔진은 리소스 관리자 MAXDOP 값을 사용합니다.  
  
-   MAX_DOP는 쿼리 힌트로서 항상 sp_configure 'max degree of parallelism'을 무시합니다.  
  
-   작업 그룹 MAX_DOP는 sp_configure 'max degree of parallelism'을 무시합니다.  
  
-   컴파일할 때 쿼리가 직렬로 표시되면 작업 그룹이나 sp_configure 설정에 관계없이 런타임에서 병렬로 다시 변경할 수 없습니다.  
  
-   DOP가 구성된 후에는 부여 메모리가 부족할 때만 낮아질 수 있습니다. 작업 그룹 재구성은 부여 메모리 큐에서 대기하는 동안 표시되지 않습니다.  
  
 GROUP_MAX_REQUESTS =*값*  
 작업 그룹에서 실행할 수 있는 최대 동시 요청 수를 지정합니다. *값* 는 0 또는 양의 정수 여야 합니다. 에 대 한 기본 설정은 *값*, 0, 무제한 요청을 허용 합니다. 최대 동시 요청에 도달한 경우 해당 그룹의 사용자가 로그인할 수 있지만 지정된 값 아래로 동시 요청 수가 떨어질 때까지 사용자가 대기 상태에 배치됩니다.  
  
 사용 하 여 { *pool_name 이라는* | **"default"** }  
 로 식별 되는 사용자 정의 리소스 풀과 작업 그룹을 연결 *pool_name 이라는*합니다. 그러면 실제로 리소스 풀에 작업 그룹을 넣습니다. 경우 *pool_name 이라는* 를 제공 하지 않으면 또는 USING 인수가 사용 되지 않으면 작업 그룹 미리 정의 된 리소스 관리자 기본 풀에 저장 됩니다.  
  
 "default"는 예약어이며 USING으로 사용될 경우 따옴표("") 또는 대괄호([])로 묶여야 합니다.  
  
> [!NOTE]  
>  미리 정의된 작업 그룹과 리소스 풀은 모두 "default"와 같은 소문자 이름을 사용합니다. 대/소문자 구분 데이터 정렬을 사용하는 서버의 경우 이러한 사항을 고려해야 합니다. 대/소문자 구분 데이터 정렬(예: SQL_Latin1_General_CP1_CI_AS)을 사용하는 서버는 "default"와 "Default"를 똑같이 처리합니다.  
  
 외부 external_pool_name | "default"  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 작업 그룹 외부 리소스 풀을 지정할 수 있습니다. 작업 그룹을 정의할 수 있고 2 풀과 연결 됩니다.  
  
-   에 대 한 리소스 풀 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 및 쿼리  
  
-   외부 프로세스에 대 한 외부 리소스 풀입니다. 자세한 내용은 참조 [sp_execute_external_script &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
## <a name="remarks"></a>주의  
 REQUEST_MEMORY_GRANT_PERCENT: 인덱스를 만드는 향상 된 성능을 위해 초기에 부여 된 보다 더 많은 작업 영역 메모리를 사용할 수 있습니다. 이러한 특별 처리는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 리소스 관리자에서 지원됩니다. 그러나 초기 부여 및 추가 메모리 부여는 리소스 풀 및 작업 그룹 설정으로 제한됩니다.  
  
 **분할된 된 테이블에서 인덱스 생성**  
  
 정렬되지 않은 분할된 테이블에서 인덱스 생성에 사용되는 메모리는 관련된 파티션 수에 비례합니다. 필요한 총 메모리가 리소스 관리자 작업 그룹 설정에서 지정한 쿼리당 제한(REQUEST_MAX_MEMORY_GRANT_PERCENT)을 초과하면 이 인덱스 생성이 실행되지 않을 수 있습니다. "default" 작업 그룹에서는 쿼리가 필요한 최소 메모리를 포함하는 쿼리당 제한을 초과하게 되므로 "default" 리소스 풀에 이러한 쿼리를 실행할 수 있는 총 메모리가 구성되어 있는 경우 사용자가 "default" 작업 그룹에서 같은 인덱스 생성을 실행할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `newReports`라는 작업 그룹을 만드는 방법을 보여 줍니다. 리소스 관리자 기본 설정을 사용하고 리소스 관리자 기본 풀에 있습니다. 예에서는 `default` 풀을 지정하지만 이 작업을 반드시 수행할 필요는 없습니다.  
  
```  
CREATE WORKLOAD GROUP newReports  
    USING "default" ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  


