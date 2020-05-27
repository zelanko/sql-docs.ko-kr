---
title: CREATE WORKLOAD 분류자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 67f844ff5955f51b0c878f2a3161cc4762834f74
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79112256"
---
# <a name="create-workload-classifier-transact-sql"></a>워크로드 분류자 만들기(Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

워크로드 관리에 사용할 분류자 개체를 만듭니다.  분류자는 분류자 문 정의에 지정된 매개 변수에 따라 들어오는 요청을 워크로드 그룹에 할당합니다.  분류자는 제출된 모든 요청마다 평가됩니다.  요청이 분류자와 일치하지 않으면 기본 작업 그룹에 할당됩니다.  기본 작업 그룹은 smallrc 리소스 클래스입니다.

> [!NOTE]
> 워크로드 분류자는 sp_addrolemember 리소스 클래스 할당 대신 사용됩니다.  워크로드 분류자를 만든 후 sp_droprolemember를 실행하여 중복된 리소스 클래스 매핑을 모두 제거합니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    (   WORKLOAD_GROUP = 'name'  
    ,   MEMBERNAME = 'security_account' 
[ [ , ] WLM_LABEL = 'label' ]  
[ [ , ] WLM_CONTEXT = 'context' ]  
[ [ , ] START_TIME = 'HH:MM' ]  
[ [ , ] END_TIME = 'HH:MM' ]  
  
[ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]) 
[;]
```

## <a name="arguments"></a>인수

 *classifier_name*  
 워크로드 분류자를 식별하는 이름을 지정합니다.  classifier_name은 sysname입니다.  최대 128자까지 가능하며 인스턴스 내에서 고유해야 합니다.

 *WORKLOAD_GROUP* =  *'name'*    
 조건이 분류자 규칙으로 충족되면 이름은 요청을 작업 그룹에 매핑합니다.  이름은 sysname입니다.  최대 128자까지 가능하며 분류자 생성 시 유효한 작업 그룹 이름이어야 합니다.

 사용 가능한 워크로드 그룹은 [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) 카탈로그 뷰에서 찾을 수 있습니다.

 *MEMBERNAME* =  *‘security_account’*     
 분류하는 데 사용되는 보안 계정입니다.  Security_account는 sysname이며 기본값은 없습니다. Security_account는 데이터베이스 사용자, 데이터베이스 역할, Azure Active Directory 로그인 또는 Azure Active Directory 그룹일 수 있습니다.
 
 *WLM_LABEL*   
 요청을 분류하는 데 사용할 수 있는 레이블 값을 지정합니다.  Label은 nvarchar(255) 형식의 선택적 매개 변수입니다.  요청에 [OPTION (LABEL)](/azure/sql-data-warehouse/sql-data-warehouse-develop-label)을 사용하여 분류자 구성과 일치시킵니다.

예제:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'  
 ,WLM_LABEL      = 'dimension_loads' )

SELECT COUNT(*) 
  FROM DimCustomer
  OPTION (LABEL = 'dimension_loads')
```

*WLM_CONTEXT*  
요청을 분류할 수 있는 세션 컨텍스트 값을 지정합니다.  context는 nvarchar(255) 형식의 선택적 매개 변수입니다.  세션 컨텍스트 설정 요청을 제출하기 전에 `wlm_context` 변수와 동일한 변수 이름을 가진 [sp_set_session_context](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md?view=azure-sqldw-latest)를 사용합니다.

예제:

```sql
CREATE WORKLOAD CLASSIFIER wcDataLoad WITH  
( WORKLOAD_GROUP = 'wgDataLoad'
 ,MEMBERNAME     = 'ELTRole'
 ,WLM_CONTEXT    = 'dim_load' )
 
--set session context
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = 'dim_load'

--run multiple statements using the wlm_context setting
SELECT COUNT(*) FROM stg.daily_customer_load
SELECT COUNT(*) FROM stg.daily_sales_load

--turn off the wlm_context session setting
EXEC sys.sp_set_session_context @key = 'wlm_context', @value = null
```

*START_TIME* 및 *END_TIME*  
요청을 분류하는 데 사용할 수 있는 start_time 및 end_time을 지정합니다.  start_time 및 end_time은 UTC 표준 시간대로 HH:MM 형식입니다.  start_time과 end_time을 함께 지정해야 합니다.

예제:

```sql
CREATE WORKLOAD CLASSIFIER wcELTLoads WITH  
( WORKLOAD_GROUP = 'wgDataLoads'
 ,MEMBERNAME     = 'ELTRole'  
 ,START_TIME     = '22:00'
 ,END_TIME       = '02:00' )
```

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }  
요청의 상대적 중요도를 지정합니다.  중요도는 다음 값 중 하나입니다.

- LOW
- BELOW_NORMAL
- NORMAL(기본값)
- ABOVE_NORMAL
- HIGH  

중요도를 지정하지 않으면 워크로드 그룹의 중요도 설정이 사용됩니다.  기본 워크로드 그룹 중요도는 정상입니다.  중요도는 요청이 예약된 순서에 영향을 미치므로 리소스 및 잠금에 첫 번째 액세스 권한을 부여합니다.

## <a name="classification-parameter-weighting"></a>분류 매개 변수 가중치

요청을 여러 분류자와 일치시킬 수 있습니다.  분류자 매개 변수에는 가중치가 있습니다.  가중치가 높은 일치 분류자는 작업 그룹 및 중요도를 할당하는 데 사용됩니다.  가중치는 다음과 같습니다.

|분류자 매개 변수 |무게   |
|---------------------|---------|
|USER                 |64       |
|ROLE                 |32       |
|WLM_LABEL            |16       |
|WLM_CONTEXT          |8        |
|START_TIME/END_TIME  |4        |

다음 분류자 구성을 고려하세요.

```sql
CREATE WORKLOAD CLASSIFIER classifierA WITH  
( WORKLOAD_GROUP = 'wgDashboards'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = HIGH
 ,WLM_LABEL      = 'salereport' )

CREATE WORKLOAD CLASSIFIER classifierB WITH  
( WORKLOAD_GROUP = 'wgUserQueries'  
 ,MEMBERNAME     = 'userloginA'
 ,IMPORTANCE     = LOW
 ,START_TIME     = '18:00'
 ,END_TIME       = '07:00' )
```

사용자 `userloginA`는 두 분류자에 대해 구성됩니다.  userloginA가 UTC 오후 6시에서 오전 7시 사이에 `salesreport`와 동일한 레이블을 사용하여 쿼리를 실행하는 경우 요청은 HIGH 중요도의 wgDashboards 워크로드 그룹으로 분류됩니다.  휴가 보고에서 요청을 LOW 중요도의 wgUserQueries로 분류할 수 있지만 WLM_LABEL의 가중치는 START_TIME/END_TIME보다 높습니다.  classifierA의 가중치는 80입니다(사용자 64와 WLM_LABEL 16의 합계).  ClassifierB의 가중치는 68입니다(사용자 64와 START_TIME/END_TIME 4의 합계).  이 경우 classifierB에 WLM_LABEL을 추가할 수 있습니다.

 자세한 내용은 [워크로드 가중치](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-weighting)를 참조하세요.

## <a name="permissions"></a>사용 권한

 CONTROL DATABASE 권한이 필요합니다.  
  
## <a name="examples"></a>예

 다음 예제에서는 `wgcELTRole`라는 작업 분류자를 만드는 방법을 보여줍니다. staticrc20 작업 그룹, `ELTRole` 사용자를 사용하고 중요도를 `above_normal`로 설정합니다.

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>참고 항목

[SQL Data Warehouse 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)</br>
[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
[sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)</br>
[sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)

