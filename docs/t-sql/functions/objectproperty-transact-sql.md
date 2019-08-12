---
title: OBJECTPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTY
- OBJECTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTY function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: 27569888-f8b5-4cec-a79f-6ea6d692b4ae
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8865d5c4331fc9414d4621f98d6b21f85561f15f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702759"
---
# <a name="objectproperty-transact-sql"></a>OBJECTPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 스키마 범위 개체에 대한 정보를 반환합니다. 스키마 범위 개체 목록에 대해서는 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조하십시오. DDL(데이터 정의 언어) 트리거 및 이벤트 알림과 같이 스키마 범위가 아닌 개체에 대해서는 이 함수를 사용할 수 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OBJECTPROPERTY ( id , property )   
```  
  
## <a name="arguments"></a>인수  
 *id*  
 현재 데이터베이스에 있는 개체의 ID를 나타내는 식입니다. *id*는 **int**이며 현재 데이터베이스 컨텍스트에서 스키마 범위 개체로 간주됩니다.  
  
 *property*  
 *id*로 지정한 개체에 대해 반환될 정보를 나타내는 식입니다. *property*는 다음 값 중 하나일 수 있습니다.  
  
> [!NOTE]  
>  달리 언급하지 않는 한 *속성*이 유효한 속성 이름이 아니거나, *id*가 유효한 개체 ID가 아니거나, *id*가 지정된 *속성*에 대해 지원되지 않는 개체 유형이거나 또는 호출자가 개체의 메타데이터를 볼 수 있는 권한이 없는 경우에는 NULL이 반환됩니다.  
  
|속성 이름|개체 유형|설명 및 반환 값|  
|-------------------|-----------------|-------------------------------------|  
|CnstIsClustKey|제약 조건|클러스터형 인덱스가 있는 PRIMARY KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsColumn|제약 조건|단일 열에 대한 CHECK, DEFAULT 또는 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDeleteCascade|제약 조건|ON DELETE CASCADE 옵션이 지정된 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDisabled|제약 조건|비활성화된 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNonclustKey|제약 조건|비클러스터형 인덱스가 있는 PRIMARY KEY 또는 UNIQUE 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotRepl|제약 조건|NOT FOR REPLICATION 키워드를 사용하여 제약 조건을 정의합니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotTrusted|제약 조건|기존 행을 검사하지 않고 제약 조건을 사용했으므로 제약 조건이 모든 행에 적용되지 않을 수도 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsUpdateCascade|제약 조건|ON UPDATE CASCADE 옵션이 지정된 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAfterTrigger|트리거|AFTER 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|만든 시간의 ANSI_NULLS 설정입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsDeleteTrigger|트리거|DELETE 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstDeleteTrigger|트리거|테이블에 대해 DELETE가 실행될 때 처음으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstInsertTrigger|트리거|테이블에 대해 INSERT가 실행될 때 처음으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstUpdateTrigger|트리거|테이블에 대해 UPDATE가 실행될 때 처음으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsertTrigger|트리거|INSERT 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsteadOfTrigger|트리거|INSTEAD OF 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastDeleteTrigger|트리거|테이블에 대해 DELETE가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastInsertTrigger|트리거|테이블에 대해 INSERT가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastUpdateTrigger|트리거|테이블에 대해 UPDATE가 실행될 때 마지막으로 실행되는 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|생성 시의 QUOTED_IDENTIFIER 설정입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsStartup|절차|시작 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerDisabled|트리거|비활성화된 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerNotForRepl|트리거|NOT FOR REPLICATION으로 정의된 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsUpdateTrigger|트리거|UPDATE 트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsWithNativeCompilation|[!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 프로시저는 기본적으로 컴파일됩니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**|  
|HasAfterTrigger|테이블, 뷰|테이블이나 뷰에 AFTER 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasDeleteTrigger|테이블, 뷰|테이블이나 뷰에 DELETE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsertTrigger|테이블, 뷰|테이블이나 뷰에 INSERT 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsteadOfTrigger|테이블, 뷰|테이블이나 뷰에 INSTEAD OF 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasUpdateTrigger|테이블, 뷰|테이블이나 뷰에 UPDATE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsAnsiNullsOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|테이블에 대한 ANSI NULLS 옵션 설정을 ON으로 지정합니다. 이는 Null 값에 대한 모든 비교가 UNKNOWN으로 계산된다는 의미입니다. 이 설정은 테이블이 존재하는 한 계산 열과 제약 조건을 포함하여 테이블 정의 내의 모든 식에 적용됩니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsCheckCnst|임의의 스키마 범위 개체|CHECK 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsConstraint|임의의 스키마 범위 개체|열 또는 테이블에 대한 단일 열 CHECK, DEFAULT 또는 FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefault|임의의 스키마 범위 개체|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 바운드 기본값입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefaultCnst|임의의 스키마 범위 개체|DEFAULT 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDeterministic|함수, 뷰|함수 또는 뷰의 결정성 속성입니다.<br /><br /> 1 = 결정적<br /><br /> 0 = 비결정적|  
|IsEncrypted|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰|모듈 문의 원본 텍스트가 난독 처리된 형식으로 변환되었음을 나타냅니다. 난독 처리된 출력은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 카탈로그 뷰 어디에서도 직접 표시되지 않습니다. 시스템 테이블 또는 데이터베이스 파일에 대한 액세스 권한이 없는 사용자는 난독 처리된 텍스트를 검색할 수 없습니다. 그러나 [DAC 포트](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)를 통해 시스템 테이블에 액세스하거나 데이터베이스 파일에 직접 액세스할 수 있는 사용자는 난독 처리된 텍스트를 사용할 수 있습니다. 또한 디버거를 서버 프로세스에 연결할 수 있는 사용자는 런타임에 메모리에서 원래 프로시저를 검색할 수 있습니다.<br /><br /> 1 = 암호화됨<br /><br /> 0 = 암호화되지 않음<br /><br /> 기본 데이터 형식: **int**|  
|IsExecuted|임의의 스키마 범위 개체|개체를 실행할 수 있습니다(뷰, 프로시저, 함수 또는 트리거).<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsExtendedProc|임의의 스키마 범위 개체|확장 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsForeignKey|임의의 스키마 범위 개체|FOREIGN KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexed|테이블, 뷰|인덱스가 있는 테이블 또는 뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexable|테이블, 뷰|인덱스를 만들 수 있는 테이블 또는 뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsInlineFunction|함수|인라인 함수입니다.<br /><br /> 1 = 인라인 함수<br /><br /> 0 = 비인라인 함수|  
|IsMSShipped|임의의 스키마 범위 개체|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 동안 만들어진 개체입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsPrimaryKey|임의의 스키마 범위 개체|PRIMARY KEY 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> NULL = 함수가 아니거나 개체 ID가 유효하지 않습니다.|  
|IsProcedure|임의의 스키마 범위 개체|프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsQuotedIdentOn|[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수, [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로시저, 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거, 뷰, CHECK 제약 조건, DEFAULT 정의|개체에 대해 따옴표 붙은 식별자 설정을 ON으로 지정합니다. 이는 개체 정의에 관련된 모든 식에서 큰따옴표가 식별자를 구분함을 의미합니다.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|IsQueue|임의의 스키마 범위 개체|Service Broker 큐입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsReplProc|임의의 스키마 범위 개체|복제 프로시저입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsRule|임의의 스키마 범위 개체|바운드 규칙입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsScalarFunction|함수|스칼라 반환 함수입니다.<br /><br /> 1 = 스칼라 반환 함수<br /><br /> 0 = 스칼라 반환 함수 아님|  
|IsSchemaBound|함수, 뷰|SCHEMABINDING을 사용하여 만든 스키마 바운드 함수 또는 뷰입니다.<br /><br /> 1 = 스키마 바운드<br /><br /> 0 = 스키마 바운드가 아닙니다.|  
|IsSystemTable|Table|시스템 테이블입니다.<br /><br /> 1 = True<br /><br /> 0 = False| 
|IsSystemVerified|Object|SQL Server에서 개체의 결정성과 정확성 속성을 확인할 수 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False| 
|IsTable|Table|테이블.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTableFunction|함수|테이블 반환 함수입니다.<br /><br /> 1 = 테이블 반환 함수<br /><br /> 0 = 테이블 반환 함수 아님|  
|IsTrigger|임의의 스키마 범위 개체|트리거입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUniqueCnst|임의의 스키마 범위 개체|UNIQUE 제약 조건입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUserTable|Table|사용자 정의 테이블입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsView|보기|뷰입니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|OwnerId|임의의 스키마 범위 개체|개체의 소유자입니다.<br /><br /> **참고:**  스키마 소유자가 개체 소유자일 필요는 없습니다. 예를 들어 자식 개체(*parent_object_id*가 Null이 아닌 개체)는 항상 부모 개체와 같은 소유자 ID를 반환합니다.<br /><br /> Null이 아닌 경우 = 개체 소유자의 데이터베이스 사용자 ID입니다.|  
|SchemaId|임의의 스키마 범위 개체| 개체가 속한 스키마의 스키마 ID입니다.| 
|TableDeleteTrigger|Table|테이블에 DELETE 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.|  
|TableDeleteTriggerCount|Table|테이블에 지정된 개수의 DELETE 트리거가 있습니다.<br /><br /> >0 = DELETE 트리거의 수입니다.|  
|TableFullTextMergeStatus|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블에 현재 병합 중인 전체 텍스트 인덱스가 있는지를 나타냅니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없거나 병합 중인 전체 텍스트 인덱스가 없습니다.<br /><br /> 1 = 전체 텍스트 인덱스가 병합 중입니다.|  
|TableFullTextBackgroundUpdateIndexOn|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블이 활성화된 전체 텍스트 백그라운드 업데이트 인덱스(자동 변경 추적)를 가집니다.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextCatalogId|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블의 전체 텍스트 인덱스 데이터가 있는 전체 텍스트 카탈로그 ID입니다.<br /><br /> 0이 아닌 값 = 전체 텍스트 인덱싱된 테이블의 행을 식별하는 고유 인덱스와 연결된 전체 텍스트 카탈로그 ID입니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없습니다.|  
|TableFulltextChangeTrackingOn|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블의 전체 텍스트 변경 내용 추적이 활성화되었습니다.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextDocsProcessed|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 전체 텍스트 인덱싱이 시작된 이후에 처리된 행의 수입니다. 전체 텍스트 검색을 위해 인덱싱 중인 테이블에서 한 행의 모든 열은 인덱싱할 한 문서의 일부로 간주됩니다.<br /><br /> 0 = 활성 탐색 또는 전체 텍스트 인덱싱이 완료되지 않았습니다.<br /><br /> >0 = 다음 중 하나(A 또는 B): A) 전체, 증분 또는 수동 변경 내용 추적 채우기가 시작된 이후에 삽입 또는 업데이트 작업으로 처리된 문서의 수입니다. B) 백그라운드 업데이트 인덱스 채우기로 변경 내용 추적이 활성화되고 전체 텍스트 인덱스 스키마가 변경되고 전체 텍스트 카탈로그 다시 작성되고 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 다시 시작된 이후에 삽입 또는 업데이트 작업에 의해 처리된 행의 수입니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.<br /><br /> 이 속성은 삭제된 행을 모니터링하거나 세지 않습니다.|  
|TableFulltextFailCount|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 전체 텍스트 검색이 인덱싱하지 않은 행의 수입니다.<br /><br /> 0 = 채우기가 완료되었습니다.<br /><br /> >0 = 다음 중 하나(A 또는 B): A) 전체, 증분 및 수동 업데이트 변경 내용 추적 채우기가 시작된 이후에 인덱싱되지 않은 문서의 수입니다. B) 백그라운드 업데이트 인덱스가 지정된 변경 내용 추적에서 채우기가 시작 또는 다시 시작된 이후에 인덱싱되지 않은 행의 수입니다. 그 원인은 스키마 변경, 카탈로그 다시 작성, 서버 다시 시작 등이 될 수 있습니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.|  
|TableFulltextItemCount|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 성공적으로 전체 텍스트 인덱싱된 행의 수입니다.|  
|TableFulltextKeyColumn|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 전체 텍스트 인덱스 정의에 사용되는 단일 열의 고유 인덱스와 관련된 열의 ID입니다.<br /><br /> 0 = 테이블에 전체 텍스트 인덱스가 없습니다.|  
|TableFulltextPendingChanges|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 처리할 보류 중인 변경 내용 추적 항목의 수입니다.<br /><br /> 0 = 변경 내용 추적이 활성화되지 않았습니다.<br /><br /> NULL = 테이블에 전체 텍스트 인덱스가 없습니다.|  
|TableFulltextPopulateStatus|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 0 = 유휴 상태<br /><br /> 1 = 전체 채우기가 진행 중입니다.<br /><br /> 2 = 증분 채우기가 진행 중입니다.<br /><br /> 3 = 추적된 변경 내용의 전파가 진행 중입니다.<br /><br /> 4 = 변경 내용 자동 추적과 같은 백그라운드 업데이트 인덱스가 진행 중입니다.<br /><br /> 5 = 전체 텍스트 인덱싱이 정체 또는 일시 중지되었습니다.|  
|TableHasActiveFulltextIndex|Table|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블에 활성 전체 텍스트 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasCheckCnst|Table|테이블에 CHECK 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasClustIndex|Table|테이블에 클러스터형 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDefaultCnst|Table|테이블에 DEFAULT 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDeleteTrigger|Table|테이블에 DELETE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignKey|Table|테이블에 FOREIGN KEY 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignRef|Table|테이블이 FOREIGN KEY 제약 조건에 의해 참조됩니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIdentity|Table|테이블에 ID 열이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIndex|Table|테이블에 임의 유형의 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasInsertTrigger|Table|개체에 INSERT 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasNonclustIndex|Table|테이블에 비클러스터형 인덱스가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasPrimaryKey|Table|테이블에 기본 키가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasRowGuidCol|Table|테이블은 **uniqueidentifier** 열에 대해 ROWGUIDCOL을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTextImage|Table|테이블은 **텍스트**, **ntext** 또는 **이미지** 열을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTimestamp|Table|테이블은 **timestamp** 열을 갖습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUniqueCnst|Table|테이블에 UNIQUE 제약 조건이 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUpdateTrigger|Table|개체에 UPDATE 트리거가 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasVarDecimalStorageFormat|Table|테이블을 **vardecimal** 스토리지 형식에 사용할 수 있습니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Table|테이블에 INSERT 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.|  
|TableInsertTriggerCount|Table|테이블에 지정된 개수의 INSERT 트리거가 있습니다.<br /><br /> >0 = INSERT 트리거의 수.|  
|TableIsFake|Table|실제 테이블이 아닙니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 요청이 있을 때 내부적으로 구체화됩니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsLockedOnBulkLoad|Table|**bcp** 또는 BULK INSERT 작업으로 인해 테이블이 잠깁니다.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsMemoryOptimized|Table|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블이 메모리 액세스에 최적화된 테이블임<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> 기본 데이터 형식: **int**<br /><br /> 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.|  
|TableIsPinned|Table|테이블이 데이터 캐시에 보유되도록 고정됩니다.<br /><br /> 0 = False<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서는 이 기능이 지원되지 않습니다.|  
|TableTextInRowLimit|Table|text in row에 최대 바이트가 허용됩니다.<br /><br /> text in row 옵션을 설정하지 않으면 0입니다.|  
|TableUpdateTrigger|Table|테이블에 UPDATE 트리거가 있습니다.<br /><br /> >1 = 지정된 유형의 첫 번째 트리거 ID.|  
|TableUpdateTriggerCount|Table|테이블에 지정된 개수의 UPDATE 트리거가 있습니다.<br /><br /> > 0 = UPDATE 트리거의 수.|  
|TableHasColumnSet|Table|테이블에 열 집합이 있습니다.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.|  
|TableTemporalType|Table|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 테이블의 형식을 지정합니다.<br /><br /> 0 = 비임시 테이블<br /><br /> 1 = 시스템 버전 테이블에 대한 기록 테이블<br /><br /> 2 = 시스템 버전 임시 테이블|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 OBJECTPROPERTY와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 *object_id*가 현재 데이터베이스 컨텍스트에 있다고 가정합니다. 다른 데이터베이스의 *object_id*를 참조하는 쿼리는 NULL 또는 잘못된 결과를 반환합니다. 예를 들어 다음 쿼리에서 현재 데이터베이스 컨텍스트는 마스터 데이터베이스입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]는 쿼리에서 지정된 데이터베이스 대신 현재 데이터베이스에서 지정된 *object_id*에 대한 속성 값을 반환하려고 합니다. 마스터 데이터베이스에는 `vEmployee` 뷰가 없으므로 이 쿼리는 잘못된 결과를 반환합니다.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTY(*view_i*d, 'IsIndexable')는 IsIndexable 속성 평가에 뷰 정의의 구문 분석, 정규화 및 부분 최적화를 요구하므로 상당히 많은 컴퓨터 리소스를 사용할 수 있습니다. IsIndexable 속성은 인덱싱 가능한 테이블이나 뷰를 식별할 수 있지만 인덱스 키에 대한 특정한 요구가 만족되지 않으면 인덱스가 실제로 생성되지 않을 수 있습니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
 OBJECTPROPERTY(*table_id*, 'TableHasActiveFulltextIndex')는 인덱싱을 위해 하나 이상의 테이블 열을 추가한 경우 값 1(true)을 반환합니다. 전체 텍스트 인덱싱은 첫 번째 열이 인덱싱용으로 추가되자마자 채우기용으로 활성화됩니다.  
  
 테이블이 생성될 때 QUOTED IDENTIFIER 옵션이 OFF로 설정된 경우에도 해당 테이블의 메타데이터에는 항상 ON으로 저장됩니다. 따라서 OBJECTPROPERTY(*table_id*, 'IsQuotedIdentOn')는 항상 값 1(true)을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-verifying-that-an-object-is-a-table"></a>1\. 개체가 테이블인지 확인  
 다음 예에서는 `UnitMeasure`가 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 테이블인지 테스트하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 1  
   PRINT 'UnitMeasure is a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 0  
   PRINT 'UnitMeasure is not a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') IS NULL  
   PRINT 'ERROR: UnitMeasure is not a valid object.';  
GO  
  
```  
  
### <a name="b-verifying-that-a-scalar-valued-user-defined-function-is-deterministic"></a>2\. 스칼라 반환 사용자 정의 함수가 결정적인지 확인  
 다음 예에서는 **money** 값을 반환하는 사용자 정의 스칼라 반환 함수 `ufnGetProductDealerPrice`가 결정적인지 여부를 테스트하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID('dbo.ufnGetProductDealerPrice'), 'IsDeterministic');  
GO  
```  
  
 결과 집합은 `ufnGetProductDealerPrice`가 결정적 함수가 아님을 보여 줍니다.  
  
 ```
-----  
0
```  
  
### <a name="c-finding-the-tables-that-belong-to-a-specific-schema"></a>C: 특정 스키마에 속하는 테이블 찾기  
 다음 예에서는 dbo 스키마에 있는 모든 테이블을 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT name, object_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTY(object_id, N'SchemaId') = SCHEMA_ID(N'dbo')  
ORDER BY type_desc, name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-verifying-that-an-object-is-a-table"></a>D: 개체가 테이블인지 확인  
 다음 예에서는 `dbo.DimReseller`가 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 데이터베이스에 있는 테이블인지 테스트하는 방법을 보여 줍니다.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECTPROPERTY (OBJECT_ID(N'dbo.DimReseller'),'ISTABLE') = 1  
   SELECT 'DimReseller is a table.'  
ELSE   
   SELECT 'DimReseller is not a table.';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

