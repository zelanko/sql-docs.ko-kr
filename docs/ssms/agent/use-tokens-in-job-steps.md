---
title: "작업 단계에서 토큰 사용 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a4cef9cc3d5a72bba4b818c89acfe6e15878ebff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="use-tokens-in-job-steps"></a>작업 단계에서 토큰 사용
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 사용하면 [!INCLUDE[tsql](../../includes/tsql_md.md)] 작업 단계 스크립트에 토큰을 사용할 수 있습니다. 작업 단계를 작성할 때 토큰을 사용하면 소프트웨어 프로그램 작성 시 변수를 사용하는 것과 같은 유연성이 있습니다. 작업 단계 스크립트에 토큰을 삽입하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 하위 시스템에서 해당 작업 단계를 실행하기 전에 [!INCLUDE[tsql](../../includes/tsql_md.md)] 에이전트가 런타임 시 토큰을 바꿉니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 서비스 팩 1부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 단계의 토큰 구문이 변경되었습니다. 그러므로 작업 단계에서 사용되는 모든 토큰에 이스케이프 매크로를 사용해야 하며 그렇지 않으면 작업 단계가 실패합니다. 이스케이프 매크로 사용 및 토큰을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 단계 업데이트에 대해서는 다음에 나오는 "토큰 사용 이해", "[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 토큰 및 매크로" 및 "매크로를 사용하도록 작업 단계 업데이트" 섹션에서 설명합니다. 또한 대괄호를 사용하여 [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] 에이전트 작업 단계 토큰을 호출한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문(예: "`[DATE]`")이 변경되었습니다. 이제 토큰 이름을 괄호로 묶고 토큰 구문의 시작 부분에 달러 기호(`$`)를 사용해야 합니다. 예를 들어  
>   
> `$(ESCAPE_`*macro name*`(DATE))`  
  
## <a name="understanding-using-tokens"></a>토큰 사용 이해  
  
> [!IMPORTANT]  
> Windows 이벤트 로그에 대한 쓰기 권한이 있는 모든 Windows 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 경고 또는 WMI 경고로 활성화되는 작업 단계에 액세스할 수 있습니다. 이러한 보안상 위험을 방지하기 위해 경고로 활성화되는 작업에 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 토큰은 기본적으로 해제됩니다. 이러한 토큰에는 **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**및 **WMI(***property***)**가 있습니다. 이번 릴리스에서는 모든 경고에 토큰을 사용할 수 있습니다.  
>   
> 이러한 토큰을 사용해야 하는 경우 먼저 Administrators 그룹과 같은 트러스트된 Windows 보안 그룹의 멤버만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 설치된 컴퓨터의 이벤트 로그에 대한 쓰기 권한이 있는지 확인합니다. 그런 다음 개체 탐색기에서 **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택하고 **경고 시스템** 페이지에서 **경고에 대한 모든 응답 작업에 대해 토큰 바꾸기** 를 선택하여 이러한 토큰을 설정합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서는 토큰이 간단하고 효율적으로 바뀝니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 토큰을 해당하는 리터럴 문자열 값으로 바꿉니다. 모든 토큰은 대/소문자가 구분되며 작업 단계에서 이를 고려하여 사용하는 토큰을 따옴표로 올바르게 묶거나 교체 문자열을 올바른 데이터 형식으로 변환해야 합니다.  
  
예를 들어, 다음 문을 사용하여 작업 단계에서 데이터베이스 이름을 인쇄할 수 있습니다.  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
이 예에서 **ESCAPE_SQUOTE** 매크로는 **A-DBN** 토큰과 함께 삽입됩니다. 런타임 시 **A-DBN** 토큰은 해당 데이터베이스 이름으로 바뀝니다. 이스케이프 매크로는 토큰 교체 문자열에 실수로 전달될 수 있는 작은따옴표를 모두 이스케이프합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트는 최종 문자열에서 작은따옴표 하나를 작은따옴표 두 개로 바꿉니다.  
  
예를 들어, 토큰을 바꾸기 위해 전달된 문자열이 `AdventureWorks2012'SELECT @@VERSION --`이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 단계에서 실행되는 명령은 다음과 같습니다.  
  
`PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
이 경우 삽입된 `SELECT @@VERSION`문은 실행되지 않습니다. 대신 추가 작은따옴표로 인해 서버에서 삽입된 문을 문자열로 구문 분석합니다. 토큰 교체 문자열에 작은따옴표가 없으면 문자가 이스케이프되지 않으며 토큰이 포함된 작업 단계가 예상대로 실행됩니다.  
  
작업 단계에서의 토큰 사용을 디버깅하려면 `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` 과 같은 PRINT 문을 사용하고 작업 단계 출력을 파일이나 테이블에 저장합니다. **작업 단계 속성** 대화 상자의 **고급** 페이지에서 작업 단계 출력 파일이나 테이블을 지정할 수 있습니다.  
  
## <a name="sql-server-agent-tokens-and-macros"></a>SQL Server 에이전트 토큰 및 매크로  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 지원되는 토큰 및 매크로를 나열하고 설명합니다.  
  
### <a name="sql-server-agent-tokens"></a>SQL Server 에이전트 토큰  
  
|토큰|Description|  
|---------|---------------|  
|**(A-DBN)**|데이터베이스 이름입니다. 작업이 경고로 실행되면 이 토큰은 작업 단계에서 자동으로 데이터베이스 이름 값으로 대체됩니다.|  
|**(A-SVR)**|서버 이름입니다. 작업이 경고로 실행되면 이 토큰은 작업 단계에서 자동으로 서버 이름 값으로 대체됩니다.|  
|**(A-ERR)**|오류 번호입니다. 작업이 경고로 실행되면 이 토큰은 작업 단계에서 자동으로 오류 번호 값으로 대체됩니다.|  
|**(A-SEV)**|오류 심각도입니다. 작업이 경고로 실행되면 이 토큰은 작업 단계에서 자동으로 오류 심각도 값으로 대체됩니다.|  
|**(A-MSG)**|메시지 내용입니다. 작업이 경고로 실행되면 이 토큰은 작업 단계에서 자동으로 메시지 텍스트 값으로 대체됩니다.|  
|**(JOBNAME)**|작업의 이름입니다.|  
|**(STEPNAME)**|단계 이름입니다.|  
|**(DATE)**|현재 날짜(YYYYMMDD 형식)입니다.|  
|**(INST)**|인스턴스 이름입니다. 기본 인스턴스의 경우 이 토큰에는 기본 인스턴스 이름인 MSSQLSERVER를 가집니다.|  
|**(JOBID)**|작업 ID입니다.|  
|**(MACH)**|컴퓨터 이름입니다.|  
|**(MSSA)**|마스터 SQLServerAgent 서비스 이름입니다.|  
|**(OSCMD)**|**CmdExec** 작업 단계를 실행하는 데 사용되는 프로그램의 접두사입니다.|  
|**(SQLDIR)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 설치된 디렉터리입니다. 기본적으로 C:\Program Files\Microsoft SQL Server\MSSQL에 설치됩니다.|  
|**(SQLLOGDIR)**|SQL Server 오류 로그 폴더 경로의 대체 토큰입니다. 예를 들면 $(ESCAPE_SQUOTE(SQLLOGDIR))입니다.|  
|**(STEPCT)**|해당 단계가 실행된 횟수(다시 시도 제외)입니다. 단계 명령이 다중 단계 루프를 강제로 종료하기 위해 사용할 수 있습니다.|  
|**(STEPID)**|단계 ID입니다.|  
|**(SRVR)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 실행 중인 컴퓨터의 이름입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스가 명명된 인스턴스이면 이 이름에는 해당 인스턴스 이름이 포함됩니다.|  
|**(TIME)**|현재 시간(HHMMSS 형식)입니다.|  
|**(STRTTM)**|작업이 실행을 시작하는 시간(HHMMSS 형식)입니다.|  
|**(STRTDT)**|작업이 실행을 시작하는 날짜(YYYYMMDD 형식)입니다.|  
|**(WMI(***property***))**|WMI 경고에 대한 응답으로 실행되는 작업의 경우 *property*에 의해 지정되는 속성 값입니다. 예를 들어 `$(WMI(DatabaseName))` 는 경고를 실행시킨 WMI 이벤트에 대한 **DatabaseName** 속성 값을 제공합니다.|  
  
### <a name="sql-server-agent-escape-macros"></a>SQL Server 에이전트 이스케이프 매크로  
  
|이스케이프 매크로|Description|  
|-----------------|---------------|  
|**$(ESCAPE_SQUOTE(***token_name***))**|토큰 교체 문자열에서 작은따옴표(')를 이스케이프합니다. 작은따옴표 하나를 작은따옴표 두 개로 바꿉니다.|  
|**$(ESCAPE_DQUOTE(***token_name***))**|토큰 교체 문자열에서 큰따옴표(")를 이스케이프합니다. 큰따옴표 하나를 큰따옴표 두 개로 바꿉니다.|  
|**$(ESCAPE_RBRACKET(***token_name***))**|토큰 교체 문자열에서 오른쪽 대괄호(])를 이스케이프합니다. 오른쪽 대괄호 하나를 오른쪽 대괄호 두 개로 바꿉니다.|  
|**$(ESCAPE_NONE(***token_name***))**|문자열에서 아무 문자도 이스케이프하지 않고 토큰을 바꿉니다. 이 매크로는 신뢰할 수 있는 사용자만 토큰 교체 문자열을 제공할 수 있는 환경에서 이전 버전과의 호환성을 지원하기 위해 제공됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "매크로를 사용하도록 작업 단계 업데이트"를 참조하십시오.|  
  
## <a name="updating-job-steps-to-use-macros"></a>매크로를 사용하도록 작업 단계 업데이트  
[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 서비스 팩 1부터 이스케이프 매크로 없이 토큰이 포함된 작업 단계는 실패하고 작업을 실행하기 전에 매크로를 사용하여 작업 단계에 포함된 하나 이상의 토큰을 업데이트해야 한다는 오류 메시지가 반환됩니다.  
  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] 기술 자료 문서 915845: [토큰을 사용하는 SQL Server 에이전트 작업 단계가 SQL Server 2005 서비스 팩 1에서 실패합니다](http://support.microsoft.com/kb/915845). 이 스크립트를 통해 토큰을 사용하는 모든 작업 단계를 **ESCAPE_NONE** 매크로로 업데이트할 수 있습니다. 이 스크립트를 사용한 다음 토큰을 사용하는 작업 단계를 가능한 한 빨리 검토하여 **ESCAPE_NONE** 매크로를 작업 단계 컨텍스트에 맞는 이스케이프 매크로로 바꾸는 것이 좋습니다.  
  
다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 토큰 바꾸기를 처리하는 방법에 대해 설명합니다. 경고 토큰 바꾸기를 설정하거나 해제하려면 개체 탐색기에서 **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택하고 **경고 시스템** 페이지에서 **경고에 대한 모든 응답 작업에 대해 토큰 바꾸기** 확인란을 선택하거나 선택을 취소합니다.  
  
|토큰 구문|경고 토큰 바꾸기 설정|경고 토큰 바꾸기 해제|  
|----------------|------------------------------|-------------------------------|  
|ESCAPE 매크로가 사용됨|작업에 있는 모든 토큰이 성공적으로 바뀝니다.|경고로 활성화된 토큰이 바뀌지 않습니다. 이러한 토큰에는 **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**및 **WMI(***property***)**가 있습니다. 다른 정적 토큰은 성공적으로 바뀝니다.|  
|ESCAPE 매크로가 사용되지 않음|토큰이 포함된 모든 작업이 실패합니다.|토큰이 포함된 모든 작업이 실패합니다.|  
  
## <a name="token-syntax-update-examples"></a>토큰 구문 업데이트 예  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>1. 비중첩 문자열에 토큰 사용  
다음 예에서는 간단한 비중첩 스크립트를 적절한 이스케이프 매크로로 업데이트하는 방법을 보여 줍니다. 업데이트 스크립트를 실행하기 전에 다음 작업 단계 스크립트는 작업 단계 토큰을 사용하여 해당 데이터베이스 이름을 인쇄합니다.  
  
`PRINT N'Current database name is $(A-DBN)' ;`  
  
업데이트 스크립트를 실행하고 나면 `ESCAPE_NONE` 토큰 앞에 `A-DBN` 매크로가 삽입됩니다. 작은따옴표를 사용하여 인쇄 문자열을 구분하기 때문에 다음과 같이 `ESCAPE_SQUOTE` 매크로를 삽입하여 작업 단계를 업데이트해야 합니다.  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>2. 중첩 문자열에 토큰 사용  
중첩 문자열이나 문에 토큰이 사용되는 작업 단계 스크립트에서는 적절한 이스케이프 매크로를 삽입하기 전에 중첩 문을 여러 개의 문으로 다시 작성해야 합니다.  
  
예를 들어, `A-MSG` 토큰을 사용하며 이스케이프 매크로로 업데이트되지 않은 다음 작업 단계를 가정해 보십시오.  
  
`PRINT N'Print ''$(A-MSG)''' ;`  
  
업데이트 스크립트를 실행하고 나면 토큰과 함께 `ESCAPE_NONE` 매크로가 삽입됩니다. 그러나 이 경우 다음과 같이 중첩 없이 스크립트를 다시 작성한 다음 `ESCAPE_SQUOTE` 매크로를 삽입하여 토큰 교체 문자열에 전달될 수 있는 구분 기호를 올바르게 이스케이프해야 합니다.  
  
<pre>DECLARE @msgString nvarchar(max)  
SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'  
SET @msgString = QUOTENAME(@msgString,'''')  
PRINT N'Print ' + @msgString ;</pre>  
  
이 예에서 QUOTENAME 함수는 인용 문자도 설정합니다.  
  
### <a name="c-using-tokens-with-the-escapenone-macro"></a>3. 토큰에 ESCAPE_NONE 매크로 사용  
다음 예는 `job_id` 테이블에서 `sysjobs` 를 검색하고 `JOBID` 토큰을 사용하여 스크립트의 앞부분에서 binary 데이터 형식으로 선언된 `@JobID` 변수를 채우는 스크립트의 일부입니다. binary 데이터 형식에는 구분 기호가 필요하지 않으므로 `ESCAPE_NONE` 토큰에 `JOBID` 매크로가 사용됩니다. 이 작업 단계는 업데이트 스크립트를 실행한 후에 업데이트하지 않아도 됩니다.  
  
<pre>SELECT * FROM msdb.dbo.sysjobs  
WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;</pre>  
  
## <a name="see-also"></a>관련 항목:  
[작업 구현](../../ssms/agent/implement-jobs.md)  
[작업 단계 관리](../../ssms/agent/manage-job-steps.md)  
  
