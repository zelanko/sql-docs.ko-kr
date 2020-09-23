---
description: OBJECTPROPERTYEX(Transact-SQL)
title: OBJECTPROPERTYEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTYEX
- OBJECTPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTYEX function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: be36b3e3-3309-4332-bfb5-c7e9cf8dc8bd
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0d2e9cd5f22c0aea8b44c0e7db527be893c732f8
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116647"
---
# <a name="objectpropertyex-transact-sql"></a>OBJECTPROPERTYEX(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스의 스키마 범위 개체에 대한 정보를 반환합니다. 이러한 개체 목록에 대해서는 [sys.objects& #40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)을 참조하십시오. OBJECTPROPERTYEX는 DDL(데이터 정의 언어) 트리거와 이벤트 알림 같이 스키마 범위가 아닌 개체에 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
OBJECTPROPERTYEX ( id , property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *id*  
 현재 데이터베이스에 있는 개체의 ID를 나타내는 식입니다. *id*는 **int**이며 현재 데이터베이스 컨텍스트에서 스키마 범위 개체로 간주됩니다.  
  
 *property*  
 ID가 지정한 개체에 대해 반환되는 정보가 있는 식입니다. 반환 형식은 **sql_variant**입니다. 다음 표에서는 각 속성 값에 대한 기본 데이터 형식을 보여 줍니다.  
  
> [!NOTE]  
>  달리 언급하지 않는 한 *속성*이 유효한 속성 이름이 아니거나, *id*가 유효한 개체 ID가 아니거나, *id*가 지정된 *속성*에 대해 지원되지 않는 개체 유형이거나 또는 호출자가 개체의 메타데이터를 볼 수 있는 권한이 없는 경우에는 NULL이 반환됩니다.  
  
|속성 이름|개체 유형|설명 및 반환 값|  
|-------------------|-----------------|-------------------------------------|  
|BaseType|임의의 스키마 범위 개체|개체의 기본 유형을 확인합니다. 지정된 개체가 SYNONYM이면 기본 개체의 기본 유형이 반환됩니다.<br /><br /> Null이 아닌 경우 = 개체 형식<br /><br /> 기본 데이터 형식: **char(2)**|  
|CnstIsClustKey|제약 조건|클러스터형 인덱스가 있는 PRIMARY KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsColumn|제약 조건|단일 열에 대한 CHECK, DEFAULT 또는 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsDeleteCascade|제약 조건|ON DELETE CASCADE 옵션이 지정된 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsDisabled|제약 조건|비활성화된 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsNonclustKey|제약 조건|비클러스터형 인덱스가 있는 PRIMARY KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsNotRepl|제약 조건|NOT FOR REPLICATION 키워드를 사용하여 제약 조건을 정의합니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsNotTrusted|제약 조건|기존 행을 검사하지 않고 제약 조건이 설정되었습니다. 따라서 제약 조건이 모든 행에 적용되지 않을 수도 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|CnstIsUpdateCascade|제약 조건|ON UPDATE CASCADE 옵션이 지정된 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsAfterTrigger|트리거|AFTER 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|만드는 시점의 ANSI_NULLS 설정입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsDeleteTrigger|트리거|DELETE 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsFirstDeleteTrigger|트리거|테이블에 대해 DELETE가 실행될 때 처음 시작되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsFirstInsertTrigger|트리거|테이블에 대해 INSERT가 실행될 때 처음 시작되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsFirstUpdateTrigger|트리거|테이블에 대해 UPDATE가 실행될 때 처음 시작되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsInsertTrigger|트리거|INSERT 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsInsteadOfTrigger|트리거|INSTEAD OF 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsLastDeleteTrigger|트리거|테이블에 대해 DELETE가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsLastInsertTrigger|트리거|테이블에 대해 INSERT가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsLastUpdateTrigger|트리거|테이블에 대해 UPDATE가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|생성 시의 QUOTED_IDENTIFIER 설정입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsStartup|프로시저|시작 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsTriggerDisabled|트리거|비활성화된 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsTriggerNotForRepl|트리거|NOT FOR REPLICATION으로 정의된 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsUpdateTrigger|트리거|UPDATE 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|ExecIsWithNativeCompilation|[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 프로시저는 기본적으로 컴파일됩니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasAfterTrigger|테이블, 뷰|테이블이나 뷰에 AFTER 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasDeleteTrigger|테이블, 뷰|테이블이나 뷰에 DELETE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasInsertTrigger|테이블, 뷰|테이블이나 뷰에 INSERT 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasInsteadOfTrigger|테이블, 뷰|테이블이나 뷰에 INSTEAD OF 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasUpdateTrigger|테이블, 뷰|테이블이나 뷰에 UPDATE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|테이블에 대한 ANSI NULLS 옵션 설정을 ON으로 지정합니다. 즉 NULL 값에 대한 모든 비교가 UNKNOWN으로 평가됩니다. 이 설정은 테이블이 존재하는 한 계산 열과 제약 조건을 포함하여 테이블 정의 내의 모든 식에 적용됩니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsCheckCnst|임의의 스키마 범위 개체|CHECK 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsConstraint|임의의 스키마 범위 개체|제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsDefault|임의의 스키마 범위 개체|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 바운드 기본값입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsDefaultCnst|임의의 스키마 범위 개체|DEFAULT 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsDeterministic|스칼라 및 테이블 반환 함수, 뷰|함수 또는 뷰의 결정성 속성입니다.<br /><br /> 1 = 결정적<br /><br /> 0 = 비결정적<br /><br /> 기본 데이터 형식: **int**|  
|IsEncrypted|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|모듈 문의 원본 텍스트가 난독 처리된 형식으로 변환되었음을 나타냅니다. 난독 처리된 출력은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 카탈로그 뷰 어디에서도 직접 표시되지 않습니다. 시스템 테이블 또는 데이터베이스 파일에 대한 액세스 권한이 없는 사용자는 난독 처리된 텍스트를 검색할 수 없습니다. 그러나 [DAC 포트](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)를 통해 시스템 테이블에 액세스하거나 데이터베이스 파일에 직접 액세스할 수 있는 사용자는 난독 처리된 텍스트를 사용할 수 있습니다. 또한 디버거를 서버 프로세스에 연결할 수 있는 사용자는 런타임에 메모리에서 원래 프로시저를 검색할 수 있습니다.<br /><br /> 1 = 암호화됨<br /><br /> 0 = 암호화되지 않음<br /><br /> 기본 데이터 형식: **int**|  
|IsExecuted|임의의 스키마 범위 개체|이 개체가 실행되도록 지정합니다(뷰, 프로시저, 함수 또는 트리거).<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsExtendedProc|임의의 스키마 범위 개체|확장 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsForeignKey|임의의 스키마 범위 개체|FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsIndexed|테이블, 뷰|인덱스가 있는 테이블 또는 뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsIndexable|테이블, 뷰|인덱스를 만들 수 있는 테이블 또는 뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsInlineFunction|기능|인라인 함수입니다.<br /><br /> 1 = 인라인 함수<br /><br /> 0 = 비인라인 함수<br /><br /> 기본 데이터 형식: **int**|  
|IsMSShipped|임의의 스키마 범위 개체|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 만들어진 개체입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsPrecise|계산 열, 함수, 사용자 정의 형식, 뷰|개체에 부동 소수점 연산 같이 정확하지 않은 계산이 있는지를 나타냅니다.<br /><br /> 1 = 정확<br /><br /> 0 = 정확하지 않음<br /><br /> 기본 데이터 형식: **int**|  
|IsPrimaryKey|임의의 스키마 범위 개체|PRIMARY KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsProcedure|임의의 스키마 범위 개체|프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsQuotedIdentOn|CHECK 제약 조건, DEFAULT 정의, [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|개체에 따옴표 붙은 식별자 설정을 ON으로 지정합니다. 이것은 개체 정의에 포함된 모든 식의 큰따옴표 구분 식별자를 의미합니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsQueue|임의의 스키마 범위 개체|Service Broker 큐입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsReplProc|임의의 스키마 범위 개체|복제 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsRule|임의의 스키마 범위 개체|바운드 규칙입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsScalarFunction|기능|스칼라 반환 함수입니다.<br /><br /> 1 = 스칼라 반환 함수<br /><br /> 0 = 스칼라 반환 함수 아님<br /><br /> 기본 데이터 형식: **int**|  
|IsSchemaBound|함수, 프로시저, 뷰|SCHEMABINDING을 사용하여 만든 스키마 바운드 함수 또는 뷰입니다.<br /><br /> 1 = 스키마 바운드<br /><br /> 0 = 스키마 바운드 아님<br /><br /> 기본 데이터 형식: **int**|  
|IsSystemTable|테이블|시스템 테이블입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsSystemVerified|계산 열, 함수, 사용자 정의 형식, 뷰|개체의 전체 자릿수와 결정성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 확인할 수 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsTable|테이블|테이블.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsTableFunction|기능|테이블 반환 함수입니다.<br /><br /> 1 = 테이블 반환 함수<br /><br /> 0 = 테이블 반환 함수 아님<br /><br /> 기본 데이터 형식: **int**|  
|IsTrigger|임의의 스키마 범위 개체|트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsUniqueCnst|임의의 스키마 범위 개체|UNIQUE 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsUserTable|테이블|사용자 정의 테이블입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|IsView|View|뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|OwnerId|임의의 스키마 범위 개체|개체의 소유자입니다.<br /><br /> **참고:** 스키마 소유자가 개체 소유자일 필요는 없습니다. 예를 들어 자식 개체(*parent_object_id*가 Null이 아닌 개체)는 항상 부모 개체와 같은 소유자 ID를 반환합니다.<br /><br /> Null이 아닌 경우 = 개체 소유자의 데이터베이스 사용자 ID입니다.<br /><br /> NULL = 지원되지 않는 개체 형식이거나 개체 ID가 잘못되었습니다.<br /><br /> 기본 데이터 형식: **int**|  
|SchemaId|임의의 스키마 범위 개체|개체와 관련된 스키마의 ID입니다.<br /><br /> Null이 아닌 경우 = 개체의 스키마 ID입니다.<br /><br /> 기본 데이터 형식: **int**|  
|SystemDataAccess|함수, 뷰|개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에서 시스템 데이터, 시스템 카탈로그 또는 가상 시스템 테이블에 액세스합니다.<br /><br /> 0 = 없음<br /><br /> 1 = 읽기<br /><br /> 기본 데이터 형식: **int**|  
|TableDeleteTrigger|테이블|테이블에 DELETE 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.<br /><br /> 기본 데이터 형식: **int**|  
|TableDeleteTriggerCount|테이블|테이블에 지정된 개수의 DELETE 트리거가 있습니다.<br /><br /> Null이 아닌 경우 = DELETE 트리거 수<br /><br /> 기본 데이터 형식: **int**|  
|TableFullTextMergeStatus|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 테이블에 현재 병합 중인 전체 텍스트 인덱스가 있는지를 나타냅니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없거나 병합 중인 전체 텍스트 인덱스가 없습니다.<br /><br /> 1 = 전체 텍스트 인덱스가 병합 중입니다.|  
|TableFullTextBackgroundUpdateIndexOn|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 테이블의 전체 텍스트 백그라운드 업데이트 인덱스(변경 내용 자동 추적)가 활성화되었습니다.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextCatalogId|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 테이블의 전체 텍스트 인덱스 데이터가 있는 전체 텍스트 카탈로그 ID입니다.<br /><br /> 0이 아닌 값 = 전체 텍스트 인덱싱된 테이블의 행을 식별하는 고유 인덱스와 연결된 전체 텍스트 카탈로그 ID입니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFullTextChangeTrackingOn|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 테이블의 전체 텍스트 변경 내용 추적이 활성화되었습니다.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextDocsProcessed|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 전체 텍스트 인덱싱이 시작된 이후에 처리된 행의 수입니다. 전체 텍스트 검색을 위해 인덱싱 중인 테이블에서 한 행의 모든 열은 인덱싱할 한 문서의 일부로 간주됩니다.<br /><br /> 0 = 활성 탐색 또는 전체 텍스트 인덱싱이 완료되지 않았습니다.<br /><br /> > 0 = 다음 중 하나(A 또는 B)입니다. A) 전체, 증분 또는 수동 변경 내용 추적 채우기를 시작한 이래 삽입 또는 업데이트 작업으로 처리된 문서의 수, B) 백그라운드 업데이트 인덱스 채우기를 사용한 변경 내용 추적이 활성화된 이래 삽입 또는 업데이트 작업으로 처리된 행의 수, 변경된 전체 텍스트 인덱스 스키마, 다시 작성된 전체 텍스트 카탈로그 또는 다시 시작된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 등.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**<br /><br /> **Note** 이 속성은 모니터링하지 않으며 삭제된 행을 세지 않습니다.|  
|TableFulltextFailCount|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 전체 텍스트 검색이 인덱싱되지 않은 행의 수입니다.<br /><br /> 0 = 채우기가 완료되었습니다.<br /><br /> >0 = 다음 중 하나(A 또는 B)입니다. A) 전체, 증분 및 수동 업데이트 변경 내용 추적 채우기를 시작한 이래 인덱싱되지 않은 문서의 수, B) 백그라운드 업데이트 인덱스를 사용한 변경 내용 추적의 경우 채우기를 시작하거나 채우기를 다시 시작한 이래 인덱싱되지 않은 행의 수. 이러한 결과는 스키마 변경, 카탈로그 다시 작성, 서버 다시 시작 등으로 인해 나타날 수 있습니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextItemCount|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> Null이 아닌 경우 = 전체 텍스트가 인덱싱된 행의 수입니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextKeyColumn|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 전체 텍스트 인덱스와 의미 체계 인덱스 정의의 일부인 단일 열의 고유 인덱스와 관련된 열의 ID입니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextPendingChanges|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 처리할 보류 중인 변경 내용 추적 항목의 수입니다.<br /><br /> 0 = 변경 내용 추적이 활성화되지 않았습니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFulltextPopulateStatus|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 0 = 유휴 상태<br /><br /> 1 = 전체 채우기가 진행 중입니다.<br /><br /> 2 = 증분 채우기가 진행 중입니다.<br /><br /> 3 = 추적된 변경 내용의 전파가 진행 중입니다.<br /><br /> 4 = 변경 내용 자동 추적과 같은 백그라운드 업데이트 인덱스가 진행 중입니다.<br /><br /> 5 = 전체 텍스트 인덱싱이 정체 또는 일시 중지되었습니다.<br /><br /> 6 = 오류가 발생했습니다. 자세한 내용은 크롤링 로그를 검사합니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)의 **전체 텍스트 채우기의 오류 문제 해결(탐색)** 섹션을 참조합니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableFullTextSemanticExtraction|테이블|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 테이블에 의미 체계 인덱싱이 사용하도록 설정되어 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasActiveFulltextIndex|테이블|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 테이블에 활성 전체 텍스트 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasCheckCnst|테이블|테이블에 CHECK 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasClustIndex|테이블|테이블에 클러스터형 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasDefaultCnst|테이블|테이블에 DEFAULT 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasDeleteTrigger|테이블|테이블에 DELETE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasForeignKey|테이블|테이블에 FOREIGN KEY 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasForeignRef|테이블|테이블이 FOREIGN KEY 제약 조건에 의해 참조됩니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasIdentity|테이블|테이블에 ID 열이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasIndex|테이블|테이블에 임의 유형의 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasInsertTrigger|테이블|개체에 INSERT 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasNonclustIndex|테이블|테이블에 비클러스터형 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasPrimaryKey|테이블|테이블에 기본 키가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasRowGuidCol|테이블|테이블은 **uniqueidentifier** 열에 대해 ROWGUIDCOL을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasTextImage|테이블|테이블은 **텍스트**, **ntext** 또는 **이미지** 열을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasTimestamp|테이블|테이블은 **timestamp** 열을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasUniqueCnst|테이블|테이블에 UNIQUE 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasUpdateTrigger|테이블|개체에 Update 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableHasVarDecimalStorageFormat|테이블|테이블을 **vardecimal** 스토리지 형식에 사용할 수 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|테이블|테이블에 INSERT 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.<br /><br /> 기본 데이터 형식: **int**|  
|TableInsertTriggerCount|테이블|테이블에 지정된 개수의 INSERT 트리거가 있습니다.<br /><br /> >0 = INSERT 트리거의 수.<br /><br /> 기본 데이터 형식: **int**|  
|TableIsFake|테이블|실제 테이블이 아닙니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 요청이 있을 때 내부적으로 구체화됩니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableIsLockedOnBulkLoad|테이블|**bcp** 또는 BULK INSERT 작업으로 인해 테이블이 잠겼습니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|TableIsMemoryOptimized|테이블|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 테이블이 메모리 액세스에 최적화된 테이블임<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**<br /><br /> 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.|  
|TableIsPinned|테이블|테이블이 데이터 캐시에 보유되도록 고정됩니다.<br /><br /> 0 = False<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 이 기능을 지원하지 않습니다.|  
|TableTextInRowLimit|테이블|테이블에 text in row 옵션이 설정되어 있습니다.<br /><br /> > 0 = 행의 텍스트에 허용되는 최대 바이트.<br /><br /> 0 = text in row 옵션이 설정되지 않았습니다.<br /><br /> 기본 데이터 형식: **int**|  
|TableUpdateTrigger|테이블|테이블에 UPDATE 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.<br /><br /> 기본 데이터 형식: **int**|  
|TableUpdateTriggerCount|테이블|테이블에 지정된 개수의 UPDATE 트리거가 있습니다.<br /><br /> > 0 = UPDATE 트리거의 수.<br /><br /> 기본 데이터 형식: **int**|  
|UserDataAccess|함수, 뷰|개체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에서 사용자 데이터 및 사용자 테이블에 액세스할 수 있음을 나타냅니다.<br /><br /> 1 = 읽기<br /><br /> 0 = 없음<br /><br /> 기본 데이터 형식: **int**|  
|TableHasColumnSet|테이블|테이블에 열 집합이 있습니다.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.|  
|카디널리티|테이블(시스템 또는 사용자 정의), 뷰 또는 인덱스|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 지정한 개체의 행 수입니다.|  
|TableTemporalType|테이블|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상<br /><br /> 테이블의 형식을 지정합니다.<br /><br /> 0 = 비임시 테이블<br /><br /> 1 = 시스템 버전 테이블에 대한 기록 테이블<br /><br /> 2 = 시스템 버전 임시 테이블|  
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECTPROPERTYEX와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 *object_id*가 현재 데이터베이스 컨텍스트에 있다고 가정합니다. 다른 데이터베이스의 *object_id*를 참조하는 쿼리는 NULL 또는 잘못된 결과를 반환합니다. 예를 들어 다음 쿼리에서 현재 데이터베이스 컨텍스트는 마스터 데이터베이스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 쿼리에서 지정된 데이터베이스 대신 현재 데이터베이스에서 지정된 *object_id*에 대한 속성 값을 반환하려고 합니다. 마스터 데이터베이스에는 `vEmployee` 뷰가 없으므로 이 쿼리는 잘못된 결과를 반환합니다.  
  
```sql  
USE master;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTYEX(*view_i*d, 'IsIndexable')는 IsIndexable 속성 평가에 뷰 정의의 구문 분석, 정규화 및 부분 최적화를 요구하므로 상당히 많은 컴퓨터 리소스를 사용할 수 있습니다. IsIndexable 속성은 인덱싱 가능한 테이블이나 뷰를 식별할 수 있지만 인덱스 키에 대한 특정한 요구가 만족되지 않으면 인덱스가 실제로 생성되지 않을 수 있습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
 OBJECTPROPERTYEX(*table_id*, 'TableHasActiveFulltextIndex')는 인덱싱을 위해 하나 이상의 테이블 열을 추가한 경우 값 1(true)을 반환합니다. 전체 텍스트 인덱싱은 첫 번째 열이 인덱싱용으로 추가되자마자 채우기용으로 활성화됩니다.  
  
 메타데이터 표시 유형에 대한 제한 사항이 결과 집합에 적용됩니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
  
### <a name="a-finding-the-base-type-of-an-object"></a>A. 기본 개체 형식 찾기  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `MyEmployeeTable` 테이블에 대한 SYNONYM `Employee`을 만든 다음 SYNONYM에 대한 기본 유형을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE SYNONYM MyEmployeeTable FOR HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX ( object_id(N'MyEmployeeTable'), N'BaseType')AS [Base Type];  
GO  
```  
  
 결과 집합은 기본 개체의 기본 유형인 `Employee` 테이블이 사용자 테이블임을 나타냅니다.  
  
 ```
Base Type 
--------  
U
```  
  
### <a name="b-returning-a-property-value"></a>B. 속성 값 반환  
 다음 예에서는 지정된 테이블의 UPDATE 트리거 수를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'HumanResources.Employee'), N'TABLEUPDATETRIGGERCOUNT');  
GO  
```  
  
### <a name="c-finding-tables-that-have-a-foreign-key-constraint"></a>C. FOREIGN KEY 제약 조건이 있는 테이블 찾기  
 다음 예에서는 `TableHasForeignKey` 속성을 사용하여 FOREIGN KEY 제약 조건이 있는 모든 테이블을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name, object_id, schema_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTYEX(object_id, N'TableHasForeignKey') = 1  
ORDER BY name;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-finding-the-base-type-of-an-object"></a>4. 기본 개체 형식 찾기  
 다음 예에서는 기본 `dbo.DimReseller` 개체 형식을 반환합니다.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT OBJECTPROPERTYEX ( object_id(N'dbo.DimReseller'), N'BaseType')AS BaseType;  
```  
  
 결과 집합은 기본 개체의 기본 유형인 `dbo.DimReseller` 테이블이 사용자 테이블임을 나타냅니다.  
  
```  
BaseType   
--------   
U   
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [OBJECT_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)  
  
  

