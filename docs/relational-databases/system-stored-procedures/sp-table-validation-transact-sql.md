---
title: sp_table_validation (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_table_validation_TSQL
- sp_table_validation
helpviewer_keywords:
- sp_table_validation
ms.assetid: 31b25f9b-9b62-496e-a97e-441d5fd6e767
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c63e6e535aed72684e56d5f578e52e065f8190d2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834228"
---
# <a name="sp_table_validation-transact-sql"></a>sp_table_validation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  테이블 또는 인덱싱된 뷰에 관한 행 개수 또는 체크섬 정보를 반환하거나 제공된 행 개수 또는 체크섬 정보를 지정된 테이블 또는 인덱싱된 뷰와 비교합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_table_validation [ @table = ] 'table'  
    [ , [ @expected_rowcount = ] type_of_check_requested OUTPUT]  
    [ , [ @expected_checksum = ] expected_checksum OUTPUT]  
    [ , [ @rowcount_only = ] rowcount_only ]  
    [ , [ @owner = ] 'owner' ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @table_name = ] table_name ]  
    [ , [ @column_list = ] 'column_list' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @table = ] 'table'`테이블의 이름입니다. *테이블* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT`테이블의 예상 행 수를 반환할지 여부를 지정 합니다. *expected_rowcount* 은 **int**이며 기본값은 NULL입니다. NULL인 경우, 실제 행 개수가 출력 매개 변수로 반환됩니다. 값을 제공한 경우에는 해당 값을 실제 행 개수와 비교하여 차이를 확인합니다.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT`테이블에 대해 예상 되는 체크섬을 반환할지 여부를 지정 합니다. *expected_checksum* 은 **숫자**이며 기본값은 NULL입니다. NULL인 경우, 실제 체크섬이 출력 매개 변수로 반환됩니다. 값을 제공한 경우에는 해당 값을 실제 체크섬과 비교하여 차이를 확인합니다.  
  
`[ @rowcount_only = ] type_of_check_requested`수행할 체크섬 또는 행 개수 유형을 지정 합니다. *type_of_check_requested* 은 **smallint**이며 기본값은 **1**입니다.  
  
 **0**인 경우 rowcount 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬을 수행 합니다.  
  
 **1**인 경우에는 rowcount 검사만 수행 합니다.  
  
 **2**인 경우 행 개수와 이진 체크섬을 수행 합니다.  
  
`[ @owner = ] 'owner'`테이블 소유자의 이름입니다. *owner* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @full_or_fast = ] full_or_fast`행 개수를 계산 하는 데 사용 되는 방법입니다. *full_or_fast* 은 **tinyint**이며 기본값은 **2**이 고 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|는 **sysindexes 행**에서 빠르게 계산 합니다. **Sysindexes** 에서 행을 계산 하는 것은 실제 테이블의 행 수를 계산 하는 것 보다 훨씬 빠릅니다. 그러나 **sysindexes** 는 지연 업데이트 되므로 행 개수가 정확 하지 않을 수 있습니다.|  
|**2** (기본값)|먼저 빠른 방법을 시도함으로써 조건부로 빠른 계산 방법을 수행합니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. *Expected_rowcount* 가 NULL이 고 저장 프로시저를 사용 하 여 값을 가져오는 경우에는 항상 전체 개수 (*)가 사용 됩니다.|  
  
`[ @shutdown_agent = ] shutdown_agent`배포 에이전트에서 **sp_table_validation**를 실행 하는 경우 배포 에이전트 유효성 검사가 완료 되 면 즉시 종료 해야 하는지 여부를 지정 합니다. *shutdown_agent* 은 **bit**이며 기본값은 **0**입니다. **0**인 경우 복제 에이전트가 종료 되지 않습니다. **1**인 경우 오류 20578가 발생 하 고 복제 에이전트가 종료 될 수 있습니다. 사용자가 **sp_table_validation** 를 직접 실행 하는 경우이 매개 변수는 무시 됩니다.  
  
`[ @table_name = ] table_name`출력 메시지에 사용 되는 뷰의 테이블 이름입니다. *table_name* 는 **sysname**이며 기본값은 ** \@ table**입니다.  
  
`[ @column_list = ] 'column_list'`Checksum 함수에서 사용 해야 하는 열 목록입니다. *column_list* 은 **nvarchar (4000)** 이며 기본값은 NULL입니다. 계산 열 및 타임스탬프 열을 제외한 열 목록을 지정하려면 병합 아티클의 유효성 검사를 사용할 수 있도록 설정하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 체크섬 유효성 검사를 수행 하는 경우 예상 체크섬이 테이블의 체크섬과 같으면 테이블에서 체크섬 유효성 검사를 통과 한 메시지를 **sp_table_validation** 반환 합니다. 그렇지 않은 경우에는 테이블이 동기화되지 않았다는 메시지를 반환하며 예상 행 개수 및 실제 행 개수의 차이를 보고합니다.  
  
 행 개수 유효성 검사를 수행 하는 경우 예상 행 수가 테이블의 수와 일치 하면 **sp_table_validation** 테이블에서 행 개수 유효성 검사를 통과 한 메시지를 반환 합니다. 그렇지 않은 경우에는 테이블이 동기화되지 않았다는 메시지를 반환하며 예상 행 개수 및 실제 행 개수의 차이를 보고합니다.  
  
## <a name="remarks"></a>설명  
 **sp_table_validation** 은 모든 유형의 복제에 사용 됩니다. Oracle 게시자에 대해서는 **sp_table_validation** 지원 되지 않습니다.  
  
 체크섬은 페이지의 전체 행 이미지에 대한 32 비트 순환 중복 검사(CRC)를 계산합니다. 체크섬은 열을 선택적으로 검사하지 않으며 테이블의 뷰 또는 열 일부에 대해서는 계산할 수 없습니다. 또한 체크섬은 **텍스트** 및 **이미지** 열의 내용을 의도적으로 건너뜁니다.  
  
 체크섬을 계산할 때는 두 서버의 테이블 구조가 동일해야 합니다. 즉, 테이블에 같은 열이 같은 순서로 있어야 하며 데이터 형식, 길이가 같아야 하고 NULL 허용 여부가 같아야 합니다. 예를 들어 게시자가 CREATE TABLE 작업을 수행한 다음 열을 추가하기 위해 ALTER TABLE 작업을 수행하였으나 구독자에 적용되는 스크립트가 단순한 CREATE 테이블인 경우에는 구조가 일치하지 않습니다. 두 테이블의 구조가 동일한 것이 확실 하지 않은 경우 [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) 를 확인 하 고 각 테이블의 오프셋이 동일한 지 확인 합니다.  
  
 문자 모드 **bcp** 를 사용 하는 경우 부동 소수점 값은 체크섬 차이를 생성할 수 있습니다 .이 경우 게시에 이외 구독자가 있는 경우입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 그 이유는 문자 모드에서, 또는 문자 모드로 변환을 수행할 때 사소하지만 피할 수 없는 전체 자릿수의 차이가 있기 때문입니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sp_table_validation**를 실행 하려면 유효성 검사 중인 테이블에 대 한 SELECT 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CHECKSUM &#40;Transact-sql&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [Transact-sql&#41;sp_article_validation &#40;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [Transact-sql&#41;sp_publication_validation &#40;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
