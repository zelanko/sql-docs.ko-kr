---
title: "sqlmaint 유틸리티 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database maintenance plans [SQL Server]
- sqlmaint utility
- maintaining databases [SQL Server]
- backups [SQL Server], sqlmaint utility
- command prompt utilities [SQL Server], sqlmaint
- maintenance plans [SQL Server], command prompt
- backing up [SQL Server], sqlmaint utility
ms.assetid: 937a9932-4aed-464b-b97a-a5acfe6a50de
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fbc02b1b8d89972cfd25739f4055842e303450c1
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="sqlmaint-utility"></a>sqlmaint 유틸리티
  **sqlmaint** 유틸리티는 하나 이상의 데이터베이스에서 지정한 유지 관리 작업을 수행합니다. **sqlmaint** 를 사용하여 DBCC 검사를 실행하고 데이터베이스 및 트랜잭션 로그를 백업하고 통계를 업데이트하고 인덱스를 다시 만들 수 있습니다. 모든 데이터베이스 유지 관리 작업은 지정된 텍스트 파일, HTML 파일 또는 전자 메일 계정으로 보낼 수 있는 보고서를 만듭니다. **sqlmaint** 는 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 만든 데이터베이스 유지 관리 계획을 실행합니다. 명령 프롬프트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유지 관리 계획을 실행하려면 [dtexec 유틸리티](../integration-services/packages/dtexec-utility.md)를 사용합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../includes/ssnotedepnextavoid-md.md)] 대신 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유지 관리 계획 기능을 사용합니다. 유지 관리 계획에 대한 자세한 내용은 [유지 관리 계획](../relational-databases/maintenance-plans/maintenance-plans.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlmaint   
[-?] |  
[  
     [-S server_name[\instance_name]]  
     [-U login_ID [-P password]]  
     {  
          [-D database_name | -PlanName name | -PlanID guid ]  
          [-Rpt text_file]  
          [-To operator_name]  
          [-HtmlRpt html_file [-DelHtmlRpt <time_period>] ]  
          [-RmUnusedSpace threshold_percentfree_percent]  
          [-CkDB | -CkDBNoIdx]  
          [-CkAl | -CkAlNoIdx]  
          [-CkCat]  
          [-UpdOptiStats sample_percent]  
          [-RebldIdx free_space]  
          [-SupportComputedColumn]  
          [-WriteHistory]  
          [  
               {-BkUpDB [backup_path] | -BkUpLog [backup_path] }  
               {-BkUpMedia  
                    {DISK [  
                           [-DelBkUps <time_period>]   
                           [-CrBkSubDir ]   
                           [-UseDefDir ]   
                          ]  
                     | TAPE   
                    }  
               }  
               [-BkUpOnlyIfClean]  
               [-VrfyBackup]  
          ]  
     }  
]  
<time_period> ::=  
number[minutes | hours | days | weeks | months]  
```  
  
## <a name="arguments"></a>인수  
 매개 변수 및 해당 값은 공백으로 구분해야 합니다. 예를 들어 **-S** 와 *server_name*사이에 공백이 있어야 합니다.  
  
 **-?**  
 **sqlmaint** 에 대한 구문 다이어그램이 반환되도록 지정합니다. 이 매개 변수는 단독으로 사용해야 합니다.  
  
 **-S** *server_name*[ **\\***instance_name*]  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 대상 인스턴스를 지정합니다. 해당 서버 컴퓨터에 있는 기본 *인스턴스에 연결하려면* server_name [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 *인스턴스에 연결하려면***\\***server_name* instance_name [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 지정합니다. 서버를 지정하지 않으면 **sqlmaint** 가 로컬 컴퓨터에 있는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 기본 인스턴스에 연결됩니다.  
  
 **-U** *login_ID*  
 서버에 연결할 때 사용할 로그인 ID를 지정합니다. 이 인수를 제공하지 않으면 **sqlmaint** 에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 인증을 사용합니다. *login_ID* 에 특수 문자가 포함된 경우 큰따옴표(")로 묶어야 합니다. 그렇지 않은 경우 큰따옴표는 선택 사항입니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요.  
  
 **-P** *password*  
 로그인 ID의 암호를 지정합니다. **-U** 매개 변수도 제공한 경우에만 유효합니다. *password* 에 특수 문자가 포함된 경우 큰따옴표(")로 묶어야 합니다. 그렇지 않은 경우 큰따옴표는 선택 사항입니다.  
  
> [!IMPORTANT]  
>  암호는 마스킹되지 않습니다. 가능하면 Windows 인증을 사용하세요.  
  
 **-D** *database_name*  
 유지 관리 작업을 수행할 데이터베이스의 이름을 지정합니다. *database_name* 에 특수 문자가 포함된 경우 큰따옴표(")로 묶어야 합니다. 그렇지 않은 경우 큰따옴표는 선택 사항입니다.  
  
 **-PlanName** *name*  
 데이터베이스 유지 관리 계획 마법사를 사용하여 정의한 데이터베이스 유지 관리 계획의 이름을 지정합니다. **sqlmaint** 가 계획에서 사용하는 유일한 정보는 계획에 있는 데이터베이스 목록입니다. 다른 **sqlmaint** 매개 변수에서 지정한 모든 유지 관리 작업이 이 데이터베이스 목록에 적용됩니다.  
  
 **-PlanID** *guid*  
 데이터베이스 유지 관리 계획 마법사를 사용하여 정의한 데이터베이스 유지 관리 계획의 GUID(Globally Unique Identifier)를 지정합니다. **sqlmaint** 가 계획에서 사용하는 유일한 정보는 계획에 있는 데이터베이스 목록입니다. 다른 **sqlmaint** 매개 변수에서 지정한 모든 유지 관리 작업이 이 데이터베이스 목록에 적용됩니다. 이 인수는 msdb.dbo.sysdbmaintplans의 plan_id 값과 일치해야 합니다.  
  
 **-Rpt** *text_file*  
 보고서를 생성할 파일의 전체 경로와 이름을 지정합니다. 이 보고서는 화면에도 생성됩니다. 보고서에서는 파일 이름에 날짜를 추가하여 버전 정보를 유지 관리합니다. 날짜는 _*yyyyMMddhhmm*형식으로 파일 이름 끝의 마침표 앞에 생성됩니다. *yyyy* = 연도, *MM* = 월, *dd* = 일, *hh* = 시, *mm* = 분입니다.  
  
 1996년 12월 1일 오전 10시 23분에 유틸리티를 실행하는 경우 *text_file* 값은 다음과 같습니다.  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.rpt  
```  
  
 생성되는 파일 이름은 다음과 같습니다.  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint_199612011023.rpt  
```  
  
 *sqlmaint* 에서 원격 서버에 액세스할 때 **text_file** 에는 전체 UNC(범용 명명 규칙) 파일 이름이 필요합니다.  
  
 **-To**  *operator_name*  
 SQL 메일을 통해 생성된 보고서를 받는 운영자를 지정합니다.  
  
 **-HtmlRpt** *html_file*  
 HTML 보고서를 생성할 파일의 전체 경로와 이름을 지정합니다. **sqlmaint** 에서는*-Rpt* 매개 변수와 마찬가지로 _ **yyyyMMddhhmm** 형식의 문자열을 파일 이름에 더하여 파일 이름을 생성합니다.  
  
 *sqlmaint* 에서 원격 서버에 액세스할 때 **html_file** 에는 전체 UNC 파일 이름이 필요합니다.  
  
 **-DelHtmlRpt** \<*time_period*>  
 보고서 파일을 만든 후 시간 간격이 초과 하는 경우 보고서 디렉터리에 있는 HTML 보고서를 삭제 하도록 지정 \< *time_period*> 합니다. **-DelHtmlRpt** 는 *html_file* 매개 변수에서 생성된 패턴과 이름이 맞는 파일을 찾습니다. 경우 *html_file* 이 c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.htm 인 다음 **-DelHtmlRpt** 하면 **sqlmaint** C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint 패턴 일치 하는 파일을 삭제 하려면\*.htm에 있고 지정 된 다음 보다 오래 된 \< *time_period*> 합니다.  
  
 **-RmUnusedSpace** *threshold_percent free_percent*  
 **-D**에 지정된 데이터베이스에서 사용하지 않는 공간을 제거하도록 지정합니다. 이 옵션은 자동으로 증가하도록 정의된 데이터베이스에서만 유용합니다. *Threshold_percent* 는 데이터베이스 크기가 몇 MB에 도달하면 **sqlmaint** 가 사용하지 않는 데이터 공간을 제거할지를 지정합니다. 데이터베이스가 *threshold_percent*보다 작으면 동작이 수행되지 않습니다. *Free_percent* 는 사용하지 않는 공간 중 데이터베이스에 유지해야 할 공간을 최종 데이터베이스 크기의 백분율로 지정합니다. 예를 들어 200MB의 데이터베이스에 100MB 데이터가 포함된 경우 *free_percent* 에 10을 지정하면 최종 데이터베이스 크기는 110MB가 됩니다. 데이터베이스가 *free_percent* 와 데이터베이스의 데이터 양을 더한 크기보다 작으면 데이터베이스가 확장되지 않습니다. 예를 들어 108MB의 데이터베이스에 100MB 데이터가 포함된 경우 *free_percent* 에 10을 지정하면 데이터베이스가 110MB로 확장되지 않고 108MB로 유지됩니다.  
  
 **-CkDB** | **-CkDBNoIdx**  
 **-D**에 지정된 데이터베이스에서 NOINDEX 옵션으로 DBCC CHECKDB 문 또는 DBCC CHECKDB 문을 실행하도록 지정합니다. 자세한 내용은 DBCC CHECKDB를 참조하십시오.  
  
 *sqlmaint* 를 실행할 때 데이터베이스가 사용 중인 경우 **text_file** 에 경고가 기록됩니다.  
  
 **-CkAl** | **-CkAlNoIdx**  
 **-D**에 지정된 데이터베이스에서 NOINDEX 옵션으로 DBCC CHECKALLOC 문을 실행하도록 지정합니다. 자세한 내용은 [DBCC CHECKALLOC&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)를 참조하세요.  
  
 **-CkCat**  
 **-D**에 지정된 데이터베이스에서 DBCC CHECKCATALOG(Transact-SQL) 문을 실행하도록 지정합니다. 자세한 내용은 [DBCC CHECKCATALOG&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)를 참조하세요.  
  
 **-UpdOptiStats** *sample_percent*  
 데이터베이스의 각 테이블에서 다음 문을 실행하도록 지정합니다.  
  
```  
UPDATE STATISTICS table WITH SAMPLE sample_percent PERCENT;  
```  
  
 테이블에 계산 열이 포함된 경우에는 **-UpdOptiStats** 를 사용할 때 **-SupportedComputedColumn**인수도 지정해야 합니다.  
  
 자세한 내용은 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)로 만든 데이터베이스 유지 관리 계획을 실행합니다.  
  
 **-RebldIdx** *free_space*  
 채우기 비율과 반대로 *free_space* 백분율 값을 사용하여 대상 데이터베이스에서 테이블의 인덱스를 다시 만들도록 지정합니다. 예를 들어 *free_space* 백분율이 30인 경우 사용되는 채우기 비율은 70입니다. *free_space* 백분율 값으로 100을 지정하면 원래 채우기 비율 값으로 인덱스가 다시 작성됩니다.  
  
 인덱스가 계산 열에 있을 경우 **-RebldIdx** 를 사용할 때 **-SupportComputedColumn**인수도 지정해야 합니다.  
  
 **-RebldIdx**  
 계산 열에서 **sqlmaint** 를 사용하여 DBCC 유지 관리 명령을 실행하려면 반드시 지정해야 합니다.  
  
 **-WriteHistory**  
 **sqlmaint**에서 수행되는 각 유지 관리 동작에 대한 항목을 msdb.dbo.sysdbmaintplan_history에 만들도록 지정합니다. **-PlanName** 또는 **-PlanID** 를 지정할 경우 sysdbmaintplan_history의 항목은 지정된 계획의 ID를 사용합니다. **-D** 를 지정할 경우 sysdbmaintplan_history의 항목은 계획 ID에 0을 사용하여 생성됩니다.  
  
 **-BkUpDB** [ *backup_path*] |  **-BkUpLog** [ *backup_path* ]  
 백업 동작을 지정합니다. **-BkUpDb** 는 전체 데이터베이스를 백업합니다. **-BkUpLog** 는 트랜잭션 로그만 백업합니다.  
  
 *backup_path* 는 백업 디렉터리를 지정합니다. *-UseDefDir* 도 지정한 경우 **backup_path** 는 필요하지 않으며 둘 다 지정하는 경우에는 **-UseDefDir** 값이 우선 적용됩니다. 디렉터리나 \\\\.\TAPE0과 같은 테이프 장치 주소에 백업을 보관할 수 있습니다. 데이터베이스 백업 파일 이름은 다음과 같이 자동으로 생성됩니다.  
  
```  
dbname_db_yyyyMMddhhmm.BAK  
  
```  
  
 여기서  
  
-   *dbname* 은 백업하는 데이터베이스의 이름입니다.  
  
-   *yyyyMMddhhmm* 은 백업 작업의 시간이며 *yyyy* = 연도, *MM* = 월, *dd* = 일, *hh* = 시, 그리고 *mm* = 분을 나타냅니다.  
  
 트랜잭션 백업 파일 이름은 이와 비슷한 형식으로 자동 생성됩니다.  
  
```  
dbname_log_yyyymmddhhmm.BAK  
  
```  
  
 **-BkUpDB** 매개 변수를 사용하는 경우 **-BkUpMedia** 매개 변수를 사용하여 미디어도 지정해야 합니다.  
  
 **-BkUpMedia**  
 백업 미디어 유형을 DISK 또는 TAPE 중 하나로 지정합니다.  
  
 **DISK**  
 백업 미디어로 디스크를 사용하도록 지정합니다.  
  
 **-DelBkUps**< *time_period* >  
 디스크 백업의 경우 백업 만든 후 시간 간격이 초과 하는 경우 백업 디렉터리에 백업 파일은 모두 삭제 수를 지정 된 \< *time_period*> 합니다.  
  
 **-CrBkSubDir**  
 디스크 백업의 경우*-UseDefDir*도 지정했으면 [ **backup_path** ] 디렉터리나 기본 백업 디렉터리에 하위 디렉터리를 만들도록 지정합니다. 하위 디렉터리의 이름은 **-D**에 지정된 데이터베이스 이름을 사용하여 생성됩니다. **-CrBkSubDir** 을 사용하면 *backup_path* 매개 변수를 변경할 필요 없이 다른 데이터베이스의 모든 백업을 별도의 하위 디렉터리에 쉽게 넣을 수 있습니다.  
  
 **backup_path**  
 디스크 백업의 경우 기본 백업 디렉터리에 백업 파일을 만들도록 지정합니다. 둘 다 지정한 경우**UseDefDir** 이 *backup_path* 보다 우선 적용됩니다. 기본 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설정을 사용하는 경우 기본 백업 디렉터리는 C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Backup입니다.  
  
 **TAPE**  
 백업 미디어로 테이프를 사용하도록 지정합니다.  
  
 **-BkUpOnlyIfClean**  
 지정된 **-Ck** 검사를 통해 데이터에 문제가 발견되지 않을 경우에만 백업이 수행되도록 지정합니다. 유지 관리 동작은 명령 프롬프트에 표시되는 것과 같은 순서로 실행됩니다. **-BkUpOnlyIfClean**을 지정할 계획인 경우 **-BkUpDB**-BkUpLog **매개 변수 전에 매개 변수**-CkDB **,**-CkDBNoIdx **,**-CkAl **,** -CkAlNoIdx **,**/**-CkTxtAl** 또는 **-CkCat**를 지정합니다. 이 매개 변수를 지정하지 않으면 검사 보고서 문제가 있는지 여부에 상관없이 백업이 수행됩니다.  
  
 **-VrfyBackup**  
 백업이 완료되면 백업에서 RESTORE VERIFYONLY를 실행하도록 지정합니다.  
  
 *number*[**minutes**| **hours**| **day**| **weeks**| **months**]  
 보고서 또는 백업 파일을 삭제할 기준이 되는 시간 간격을 지정합니다. *number* 는 정수와 시간 단위로 공백 없이 구성됩니다. 올바른 예는 다음과 같습니다.  
  
-   **12weeks**  
  
-   **3months**  
  
-   **15days**  
  
 *number* 만 지정하면 기본적으로 날짜 부분에 **weeks**가 사용됩니다.  
  
## <a name="remarks"></a>주의  
 **sqlmaint** 유틸리티는 하나 이상의 데이터베이스에서 유지 관리 작업을 수행합니다. **-D** 를 지정할 경우 지정한 데이터베이스에서만 나머지 스위치에 지정된 작업이 수행됩니다. **-PlanName** 또는 **-PlanID** 를 지정할 경우 **sqlmaint** 가 지정된 유지 관리 작업에서 정보를 검색하면 계획에 있는 데이터베이스 목록만 검색됩니다. 나머지 **sqlmaint** 매개 변수에 지정된 모든 작업은 계획에서 가져온 목록의 각 데이터베이스에 대해 적용됩니다. **sqlmaint** 유틸리티는 계획 자체에 정의된 유지 관리 작업을 적용하지는 않습니다.  
  
 **sqlmaint** 유틸리티가 성공적으로 실행되면 0을 반환하고 실패하면 1을 반환합니다. 실패는 보고됩니다.  
  
-   유지 관리 동작이 실패할 경우  
  
-   **-CkDB**, **-CkDBNoIdx**, **-CkAl**, **-CkAlNoIdx**, **-CkTxtAl**또는 **-CkCat** 검사에서 데이터 관련 문제를 발견합니다.  
  
-   일반 오류가 발생한 경우  
  
## <a name="permissions"></a>사용 권한  
 **sqlmaint** 유틸리티는 **에 대한** 읽기 및 실행 `sqlmaint.exe`권한이 있는 Windows 사용자라면 누구나 실행할 수 있습니다. 이 파일은 기본적으로 `x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER1\MSSQL\Binn` 폴더에 저장되어 있습니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -login_ID **로 지정된** 로그인에는 지정된 동작을 수행하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용 권한이 있어야 합니다. Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결하는 경우 인증된 Windows 사용자에 매핑된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인에는 지정된 동작을 수행하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용 권한이 있어야 합니다.  
  
 예를 들어 **-BkUpDB** 를 사용하려면 BACKUP 문을 실행할 수 있는 권한이 있어야 합니다. 또한 **-UpdOptiStats** 인수를 사용하려면 UPDATE STATISTICS 문을 실행할 수 있는 권한이 있어야 합니다. 자세한 내용은 온라인 설명서에서 해당 항목의 "사용 권한" 섹션을 참조하십시오.  
  
## <a name="examples"></a>예  
  
### <a name="a-performing-dbcc-checks-on-a-database"></a>1. 데이터베이스에서 DBCC 검사를 수행합니다.  
  
```  
sqlmaint -S MyServer -D AdventureWorks2012 -CkDB -CkAl -CkCat -Rpt C:\MyReports\AdvWks_chk.rpt  
```  
  
### <a name="b-updating-statistics-using-a-15-sample-in-all-databases-in-a-plan-also-shrink-any-of-the-database-that-have-reached-110-mb-to-having-only-10-free-space"></a>2. 계획의 모든 데이터베이스에서 15% 샘플을 사용하여 통계를 업데이트합니다. 또한 110MB에 도달한 데이터베이스를 축소하여 빈 공간이 10%가 되도록 합니다.  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -UpdOptiStats 15 -RmUnusedSpace 110 10  
```  
  
### <a name="c-backing-up-all-the-databases-in-a-plan-to-their-individual-subdirectories-in-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory-also-delete-any-backups-older-than-2-weeks"></a>3. 계획의 모든 데이터베이스를 기본 x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup 디렉터리에 있는 개별 하위 디렉터리에 백업합니다. 또한 2주가 지난 백업을 삭제합니다.  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -BkUpDB -BkUpMedia DISK -UseDefDir -CrBkSubDir -DelBkUps 2weeks  
```  
  
### <a name="d-backing-up-a-database-to-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory"></a>4. 데이터베이스를 기본 x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup 디렉터리에 백업합니다.  
  
```  
sqlmaint -S MyServer -BkUpDB -BkUpMedia DISK -UseDefDir  
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)  
  
  

