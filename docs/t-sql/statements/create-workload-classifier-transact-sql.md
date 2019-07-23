---
title: CREATE WORKLOAD 분류자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
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
ms.openlocfilehash: 327d0b0929305561a7be55b38b9d6cb97299e088
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938874"
---
# <a name="create-workload-classifier-transact-sql"></a>워크로드 분류자 만들기(Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

워크로드 관리 분류자를 만듭니다.  분류자는 들어오는 요청을 작업 그룹에 할당하고 분류자 문 정의에 지정된 매개 변수에 따라 중요도를 할당합니다.  분류자는 제출된 모든 요청마다 평가됩니다.  요청이 분류자와 일치하지 않으면 기본 작업 그룹에 할당됩니다.  기본 작업 그룹은 smallrc 리소스 클래스입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL (default) | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>인수

 *classifier_name*  
 워크로드 분류자를 식별하는 이름을 지정합니다.  classifier_name은 sysname입니다.  최대 128자까지 가능하며 인스턴스 내에서 고유해야 합니다.

WORKLOAD_GROUP = *'name'* 조건이 분류자 규칙으로 충족되면 이름은 요청을 작업 그룹에 매핑합니다.  이름은 sysname입니다.  최대 128자까지 가능하며 분류자 생성 시 유효한 작업 그룹 이름이어야 합니다.

WORKLOAD_GROUP은 기존 리소스 클래스에 매핑해야 합니다.

|정적 리소스 클래스|동적 리소스 클래스|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = *'security_account'* 역할에 추가되는 보안 계정입니다.  Security_account는 sysname이며 기본값은 없습니다. Security_account는 데이터베이스 사용자, 데이터베이스 역할, Azure Active Directory 로그인 또는 Azure Active Directory 그룹일 수 있습니다.

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } 요청의 상대적 중요도를 지정합니다.  중요도는 다음 값 중 하나입니다.

- LOW
- BELOW_NORMAL
- NORMAL(기본값)
- ABOVE_NORMAL
- HIGH  

중요도는 요청이 예약된 순서에 영향을 미치므로 리소스 및 잠금에 첫 번째 액세스 권한을 부여합니다.

사용자가 여러 분류자에서 다른 리소스 클래스가 할당되거나 일치하는 여러 역할의 멤버인 경우, 사용자에게 가장 높은 리소스 클래스 할당이 제공됩니다. 자세한 내용은 [작업 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)를 참조하세요.

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

[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
카탈로그 뷰 [sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)</br>
카탈로그 뷰 [sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
[SQL Data Warehouse Classification](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
