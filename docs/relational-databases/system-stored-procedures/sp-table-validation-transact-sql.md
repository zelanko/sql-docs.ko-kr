---
title: sp_table_validation (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e8695c847e6c5efce1869d55ec68e17bdee5800
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62683977"
---
# <a name="sptablevalidation-transact-sql"></a>sp_table_validation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  테이블 또는 인덱싱된 뷰에 관한 행 개수 또는 체크섬 정보를 반환하거나 제공된 행 개수 또는 체크섬 정보를 지정된 테이블 또는 인덱싱된 뷰와 비교합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다*합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @table = ] 'table'` 테이블의 이름이입니다. *테이블* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @expected_rowcount = ] expected_rowcountOUTPUT` 테이블의 예상된 행 개수를 반환할지 여부를 지정 합니다. *expected_rowcount* 됩니다 **int**, 기본값은 NULL입니다. NULL인 경우, 실제 행 개수가 출력 매개 변수로 반환됩니다. 값을 제공한 경우에는 해당 값을 실제 행 개수와 비교하여 차이를 확인합니다.  
  
`[ @expected_checksum = ] expected_checksumOUTPUT` 테이블에 대해 예상된 된 체크섬을 반환할 것인지를 지정 합니다. *expected_checksum* 됩니다 **숫자**, 기본값은 NULL입니다. NULL인 경우, 실제 체크섬이 출력 매개 변수로 반환됩니다. 값을 제공한 경우에는 해당 값을 실제 체크섬과 비교하여 차이를 확인합니다.  
  
`[ @rowcount_only = ] type_of_check_requested` 어떤 유형의 체크섬 또는 행 개수 수행할 작업을 지정 합니다. *type_of_check_requested* 됩니다 **smallint**, 기본값은 **1**합니다.  
  
 하는 경우 **0**를 수행할 행 개수와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬.  
  
 하는 경우 **1**, 행 개수 검사만 수행 합니다.  
  
 하는 경우 **2**, 행 개수 및 이진 체크섬을 수행 합니다.  
  
`[ @owner = ] 'owner'` 테이블 소유자의 이름이입니다. *소유자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @full_or_fast = ] full_or_fast` 행 개수를 계산 하려면 메서드가 사용 됩니다. *full_or_fast* 됩니다 **tinyint**, 기본값은 **2**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|빠른 계산 **sysindexes.rows**합니다. 사용한 행 계산은 **sysindexes** 실제 테이블의 행 계산 보다 훨씬 빠릅니다. 그러나 때문 **sysindexes** 는 느리게 업데이트 행 개수가 정확 하지 않을 합니다.|  
|**2** (기본값)|먼저 빠른 방법을 시도함으로써 조건부로 빠른 계산 방법을 수행합니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. 하는 경우 *expected_rowcount* 가 NULL이 저장된 프로시저 되 고 값을 가져오려면, 전체 그룹은 항상 사용 합니다.|  
  
`[ @shutdown_agent = ] shutdown_agent` 배포 에이전트가 실행 되는 경우 **sp_table_validation**에 있는지 여부를 배포 에이전트가 즉시 종료 되어야 유효성 검사 완료 시를 지정 합니다. *shutdown_agent* 됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **0**, 복제 에이전트가 종료 되지 않습니다. 하는 경우 **1**20578 오류가 발생 하 고 복제 에이전트가 종료 신호를 받는, 합니다. 이 매개 변수는 무시 하면 **sp_table_validation** 사용자가 직접 실행 됩니다.  
  
`[ @table_name = ] table_name` 출력 메시지에 사용 되는 뷰의 테이블 이름이입니다. *table_name* 됩니다 **sysname**, 기본값은 **@table**합니다.  
  
`[ @column_list = ] 'column_list'` Checksum 함수에서 사용 해야 하는 열의 목록이입니다. *column_list* 됩니다 **nvarchar(4000)**, 기본값은 NULL입니다. 계산 열 및 타임스탬프 열을 제외한 열 목록을 지정하려면 병합 아티클의 유효성 검사를 사용할 수 있도록 설정하십시오.  
  
## <a name="return-code-values"></a>반환 코드 값  
 테이블의 체크섬이 필요한 체크섬 및 체크섬 유효성 검사를 수행 하는 경우 **sp_table_validation** 테이블이 체크섬 유효성 검사를 통과 하는 메시지를 반환 합니다. 그렇지 않은 경우에는 테이블이 동기화되지 않았다는 메시지를 반환하며 예상 행 개수 및 실제 행 개수의 차이를 보고합니다.  
  
 테이블의 수와 같으면 행 개수 유효성 검사를 수행 하는 예상된 행 수가 **sp_table_validation** 테이블 행 개수 유효성 검사를 통과 하는 메시지를 반환 합니다. 그렇지 않은 경우에는 테이블이 동기화되지 않았다는 메시지를 반환하며 예상 행 개수 및 실제 행 개수의 차이를 보고합니다.  
  
## <a name="remarks"></a>Remarks  
 **sp_table_validation** 모든 유형의 복제에 사용 됩니다. **sp_table_validation** Oracle 게시자에 대해서는 지원 되지 않습니다.  
  
 체크섬은 페이지의 전체 행 이미지에 대한 32 비트 순환 중복 검사(CRC)를 계산합니다. 체크섬은 열을 선택적으로 검사하지 않으며 테이블의 뷰 또는 열 일부에 대해서는 계산할 수 없습니다. 또한 체크섬의 콘텐츠를 건너뜁니다 **텍스트** 하 고 **이미지** 열으로 (디자인).  
  
 체크섬을 계산할 때는 두 서버의 테이블 구조가 동일해야 합니다. 즉, 테이블에 같은 열이 같은 순서로 있어야 하며 데이터 형식, 길이가 같아야 하고 NULL 허용 여부가 같아야 합니다. 예를 들어 게시자가 CREATE TABLE 작업을 수행한 다음 열을 추가하기 위해 ALTER TABLE 작업을 수행하였으나 구독자에 적용되는 스크립트가 단순한 CREATE 테이블인 경우에는 구조가 일치하지 않습니다. 없는 경우 두 테이블의 구조와 동일한 지를 살펴봅니다 [syscolumns](../../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md) 하 고 각 테이블의 오프셋이 동일한 지 확인 합니다.  
  
 부동 소수점 값은 문자 모드 경우 서로 다른 체크섬을 생성 하는 일을 할 **bcp** 를 사용 하는 게시가 아닌 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다. 그 이유는 문자 모드에서, 또는 문자 모드로 변환을 수행할 때 사소하지만 피할 수 없는 전체 자릿수의 차이가 있기 때문입니다.  
  
## <a name="permissions"></a>사용 권한  
 실행할 **sp_table_validation**, 유효성 검사 중인 테이블에 대 한 SELECT 권한이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [체크섬 &#40;TRANSACT-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)   
 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_publication_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
