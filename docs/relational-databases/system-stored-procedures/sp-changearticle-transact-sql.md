---
title: sp_changearticle (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
caps.latest.revision: 77
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1f68944355ce8af106d46ebba123e4c1fff05b04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  트랜잭션 또는 스냅숏 게시에 있는 아티클의 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 아티클을 포함하는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@article=**] **'***문서***'**  
 속성을 변경할 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@property=**] **'***속성***'**  
 변경할 아티클 속성입니다. *속성* 은 **nvarchar (100)** 합니다.  
  
 [  **@value=**] **'***값***'**  
 아티클 속성의 새 값입니다. *값* 은 **nvarchar (255)** 합니다.  
  
 다음 표에서는 아티클의 속성 및 해당 속성의 값을 설명합니다.  
  
|속성|값|Description|  
|--------------|------------|-----------------|  
|**creation_script**||대상 테이블을 만드는 데 사용하는 아티클 스키마 스크립트의 경로 및 이름입니다. 기본값은 NULL입니다.|  
|**del_cmd**||실행할 DELETE 문입니다. 그렇지 않은 경우에는 로그에서 만들어집니다.|  
|**설명**||아티클에 대한 새로운 설명 항목입니다.|  
|**dest_object**||이전 버전과의 호환성을 위해 제공됩니다. 사용 하 여 **dest_table**합니다.|  
|**dest_table**||새 대상 테이블입니다.|  
|**destination_owner**||대상 개체 소유자의 이름입니다.|  
|**filter**||테이블을 필터링(행 필터링)하는 데 사용할 새 저장 프로시저입니다. 기본값은 NULL입니다. 피어 투 피어 복제 내의 게시에 대해서는 변경할 수 없습니다.|  
|**fire_triggers_on_snapshot**|**true**|초기 스냅숏을 적용할 때 복제된 사용자 트리거를 실행합니다.<br /><br /> 참고: 복제 된 트리거에 대 한 비트 마스크 값 *schema_option* 는 값을 포함 해야 **0x100**합니다.|  
||**false**|초기 스냅숏을 적용할 때 복제된 사용자 트리거를 실행하지 않습니다.|  
|**identity_range**||구독자에 할당된 ID 범위의 크기를 제어합니다. 피어 투 피어 복제의 경우에는 지원되지 않습니다.|  
|**ins_cmd**||실행할 INSERT 문입니다. 그렇지 않은 경우에는 로그에서 만들어집니다.|  
|**pre_creation_cmd**||동기화를 적용하기 전에 대상 테이블을 제거, 삭제 또는 자를 수 있는 사전 작성 명령입니다.|  
||**없음**|명령을 사용하지 않습니다.|  
||**drop**|대상 테이블을 삭제합니다.|  
||**delete**|대상 테이블을 삭제합니다.|  
||**truncate**|대상 테이블을 자릅니다.|  
|**pub_identity_range**||구독자에 할당된 ID 범위의 크기를 제어합니다. 피어 투 피어 복제의 경우에는 지원되지 않습니다.|  
|**schema_option**||지정한 아티클에 대한 스키마 생성 옵션의 비트맵을 지정합니다. *schema_option* 은 **binary (8)** 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 주의 섹션을 참조하십시오.|  
||**0x00**|스냅숏 에이전트가 스크립팅을 사용하지 않습니다.|  
||**0x01**|개체를 만듭니다(CREATE TABLE, CREATE PROCEDURE 등).|  
||**0x02**|정의된 경우 아티클에 대한 변경 내용을 전파하는 저장 프로시저를 생성합니다.|  
||**0x04**|IDENTITY 속성을 사용하여 ID 열이 스크립팅됩니다.|  
||**0x08**|복제 **타임 스탬프** 열입니다. 그렇지 않은 경우 설정, **타임 스탬프** 열은로 복제 **이진**합니다.|  
||**0x10**|해당 클러스터형 인덱스를 생성합니다.|  
||**0x20**|사용자 정의 데이터 형식(UDT)을 구독자에서의 기본 데이터 형식으로 변환합니다. UDT 열에 CHECK 또는 DEFAULT 제약 조건이 있거나 UDT 열이 기본 키의 일부이거나 계산 열이 UDT 열을 참조하는 경우 이 옵션을 사용할 수 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**0x40**|해당 비클러스터형 인덱스를 생성합니다.|  
||**0x80**|기본 키에 대해 선언된 참조 무결성을 포함합니다.|  
||**0x100**|정의된 경우 테이블 아티클에 사용자 트리거를 복제합니다.|  
||**0x200**|FOREIGN KEY 제약 조건을 복제합니다. 참조되는 테이블이 게시의 일부가 아닌 경우 게시된 테이블의 모든 FOREIGN KEY 제약 조건은 복제되지 않습니다.|  
||**0x400**|CHECK 제약 조건을 복제합니다.|  
||**0 x 800**|기본값을 복제합니다.|  
||**0x1000**|열 수준 데이터 정렬을 복제합니다.|  
||**0x2000**|게시된 아티클 원본 개체와 연관된 확장 속성을 복제합니다.|  
||**0x4000**|테이블 아티클에 정의된 경우 고유 키를 복제합니다.|  
||**0x8000**|ALTER TABLE 문을 사용하여 테이블 아티클의 기본 키 및 고유 키를 제약 조건으로 복제합니다.<br /><br /> 참고:이 옵션 되지 않습니다. 사용 하 여 **0x80** 및 **0x4000** 대신 합니다.|  
||**0x10000**|동기화하는 동안 CHECK 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
||**0 x 20000**|동기화하는 동안 FOREIGN KEY 제약 조건이 강제 적용되지 않도록 해당 제약 조건을 NOT FOR REPLICATION으로 복제합니다.|  
||**0x40000**|분할된 테이블이나 인덱스와 연결된 파일 그룹을 복제합니다.|  
||**0x80000**|분할된 테이블에 대한 파티션 구성표를 복제합니다.|  
||**0x100000**|분할된 인덱스에 대한 파티션 구성표를 복제합니다.|  
||**0x200000**|테이블 통계를 복제합니다.|  
||**0x400000**|기본 바인딩|  
||**0x800000**|규칙 바인딩|  
||**0x1000000**|전체 텍스트 인덱스|  
||**0x2000000**|XML 스키마 컬렉션에 바인딩된 **xml** 열이 복제 되지 않습니다.|  
||**0x4000000**|인덱스를 복제 **xml** 열입니다.|  
||**0x8000000**|구독자에 없는 스키마를 만듭니다.|  
||**0x10000000**|변환 **xml** 열을 **ntext** 구독자에 있습니다.|  
||**0x20000000**|변환 큰 개체 데이터 형식 (**nvarchar (max)**, **varchar (max)**, 및 **varbinary (max)**)에서 도입 된 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 지원 되는 데이터 형식 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]합니다.|  
||**0x40000000**|사용 권한을 복제합니다.|  
||**0 x 80000000**|게시의 일부가 아닌 개체에 대한 종속성을 삭제합니다.|  
||**0x100000000**|로 지정 될 경우 FILESTREAM 특성을 복제 하려면이 옵션을 사용 하 여 **varbinary (max)** 열입니다. 테이블을 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 구독자에 복제할 경우에는 이 옵션을 지정하지 마십시오. 테이블에 FILESTREAM 열이 있는 복제 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 이 스키마 옵션이 어떻게 설정 되었는지에 관계 없이 구독자가 지원 되지 않습니다.<br /><br /> 관련된 옵션 참조 **0x800000000**합니다.|  
||**0x200000000**|날짜 및 시간 데이터 형식으로 변환 (**날짜**, **시간**, **datetimeoffset**, 및 **datetime2**)에서 도입 된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전 버전에서 지원 되는 데이터 형식에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
||**0x400000000**|데이터 및 인덱스에 대한 압축 옵션을 복제합니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.|  
||**0x800000000**|FILESTREAM 데이터를 구독자에서 고유한 파일 그룹에 저장하려면 이 옵션을 설정합니다. 이 옵션을 설정하지 않으면 FILESTREAM 데이터는 기본 파일 그룹에 저장됩니다. 복제 기능에서는 파일 그룹을 만들지 않으므로 이 옵션을 설정할 경우 구독자에서 스냅숏을 적용하기 전에 파일 그룹을 만들어야 합니다. 스냅숏을 적용 하기 전에 개체를 만드는 방법에 대 한 자세한 내용은 참조 [실행 스크립트 전과 후의 스냅숏 적용](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)합니다.<br /><br /> 관련된 옵션 참조 **0x100000000**합니다.|  
||**0x1000000000**|공용 언어 런타임 (CLR) 사용자 정의 형식 (Udt)에 8000 바이트 보다 큰 변환 **varbinary (max)** 형식의 열을 실행 하는 구독자에 복제할 수 있도록 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.|  
||**0 x 2000000000**|변환는 **hierarchyid** 데이터 형식을 **varbinary (max)** 있도록 형식의 열 **hierarchyid** 실행 하는 구독자에 복제할 수 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. 사용 하는 방법에 대 한 자세한 내용은 **hierarchyid** 복제 된 테이블의 열 참조 [hierarchyid &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)합니다.|  
||**0x4000000000**|테이블의 필터링된 인덱스를 복제합니다. 필터링 된 인덱스에 대 한 자세한 내용은 참조 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)합니다.|  
||**0x8000000000**|변환 된 **geography** 및 **기 하 도형** 데이터 형식을 **varbinary (max)** 를실행하는구독자에이러한형식의열을복제할수있도록[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|형식의 열에 인덱스를 복제 **geography** 및 **geometry**합니다.|  
||**0x20000000000**|열에 대한 SPARSE 특성을 복제합니다. 이 특성에 대 한 자세한 내용은 참조 [스파스 열을 사용 하 여](../../relational-databases/tables/use-sparse-columns.md)합니다.|  
||**0x40000000000**|구독자에서 메모리 액세스에 최적화 된 테이블을 만들려고 스냅숏 에이전트가 스크립팅을 사용 하도록 설정 합니다.|  
||**0x80000000000**|메모리 액세스에 최적화 된 아티클에 대 한 비클러스터형된 인덱스에 클러스터형된 인덱스를 변환 합니다.|  
|**상태**||속성의 새 상태를 지정합니다.|  
||**dts 수평 분할**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**열 이름 포함**|복제된 INSERT 문에 열 이름이 포함됩니다.|  
||**열 이름 없음**|복제된 INSERT 문에 열 이름이 포함되지 않습니다.|  
||**dts horizontal p 없음**|아티클에 대한 수평 분할이 변환 가능한 구독에 의해 정의되지 않습니다.|  
||**없음**|에 상태 옵션을 모두 해제는 [sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) 테이블 및 해당 아티클을 비활성으로 표시 합니다.|  
||**parameters**|매개 변수가 있는 명령을 사용하여 변경 내용을 구독자에게 전파합니다. 이것은 새 아티클에 대한 기본 설정입니다.|  
||**문자열 리터럴**|문자열 리터럴 값을 사용하여 변경 내용을 구독자에게 전파합니다.|  
|**sync_object**||동기화 출력 파일 생성에 사용하는 테이블 또는 뷰의 이름입니다. 기본값은 NULL입니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**테이블 스페이스**||Oracle 데이터베이스에서 게시된 아티클에 대한 로깅 테이블에서 사용되는 테이블스페이스를 식별합니다. 자세한 내용은 [Oracle 테이블스페이스 관리](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)를 참조하세요.|  
|**threshold**||배포 에이전트가 새 ID 범위를 할당하는 시점을 제어하는 비율 값입니다. 피어 투 피어 복제의 경우에는 지원되지 않습니다.|  
|**type**||Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**logbased**|로그 기반 아티클입니다.|  
||**logbased manualboth**|수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 및 *필터* 속성도 설정 해야 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**logbased manualfilter**|수동 필터가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 및 *필터* 속성도 설정 해야 합니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**logbased manualview**|수동 뷰가 있는 로그 기반 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 속성을 설정할 수도 있습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**인덱싱된 viewlogbased**|로그 기반의 인덱싱된 뷰 아티클입니다. Oracle 게시자에 대해서는 지원되지 않습니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다.|  
||**인덱싱된 viewlogbased manualboth**|수동 필터 및 수동 뷰가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 및 *필터* 속성도 설정 해야 합니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**인덱싱된 viewlogbased manualfilter**|수동 필터가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 및 *필터* 속성도 설정 해야 합니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
||**인덱싱된 viewlogbased manualview**|수동 뷰가 있는 로그 기반의 인덱싱된 뷰 아티클입니다. 이 옵션을 사용 하려면는 *sync_object* 속성을 설정할 수도 있습니다. 이 유형의 아티클은 기본 테이블을 별도로 게시할 필요가 없습니다. Oracle 게시자에 대해서는 지원되지 않습니다.|  
|**upd_cmd**||실행할 UPDATE 문입니다. 그렇지 않은 경우에는 로그에서 만들어집니다.|  
|NULL|NULL|변경될 수 있는 아티클 속성의 목록을 반환합니다.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 는 **비트**, 기본값은 **0**합니다.  
  
 **0** 은 아티클의 변경이 스냅숏을 무효화 인해 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅숏을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 는 아티클에 대 한 변경 유효 하려면 스냅숏을 무효화를 의미 하며 새 스냅숏이 필요한 기존 구독이 있는 경우에 사용 되지 않는 것으로 표시 될 기존 스냅숏과 새 스냅숏을 생성할 권한을 부여 하도록 지정 합니다.  
  
 변경 시 새 스냅숏의 생성을 필요로 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
 [**@force_reinit_subscription=] * * * force_reinit_subscription*  
 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화해야 할 수도 있습니다. *force_reinit_subscription* 는 **비트** 기본값인 **0**합니다.  
  
 **0** 문서에 대 한 변경으로 인해 구독이 다시 초기화 해야 하지 않도록 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 아티클의 변경이 아티클에 기존 구독이 다시 초기화 해야 할 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
 변경 시 기존의 모든 구독을 다시 초기화해야 하는 속성에 대해서는 주의 섹션을 참조하십시오.  
  
 [ **@publisher**=] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자를 지정합니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에서 아티클 속성을 변경 하는 경우 사용할 수 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_changearticle** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 아티클을 피어 투 피어 트랜잭션 복제를 지 원하는 게시에 속한 경우만 변경할 수 있습니다는 **설명**, **ins_cmd**, **upd_cmd**, 및 **del_cmd** 속성입니다.  
  
 다음 속성을 변경 하려면 새 스냅숏을 생성 해야 하 고 값을 지정 해야 **1** 에 대 한는 *force_invalidate_snapshot* 매개 변수:  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 다음과 같은 속성을 변경 하려면 해당 기존 초기화할 수의 값을 지정 해야 **1** 에 대 한는 *force_reinit_subscription* 매개 변수입니다.  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **filter**  
  
-   **ins_cmd**  
  
-   **상태**  
  
-   **upd_cmd**  
  
 기존 게시에서 사용할 수 있습니다 **sp_changearticle** 아티클을 삭제 하 고 전체 게시를 다시 만들 필요 없이 변경할 수 있습니다.  
  
> [!NOTE]  
>  값을 변경할 때 *schema_option*, 시스템 비트 단위 업데이트를 수행 하지 않습니다. 즉, 설정한 *schema_option* 를 사용 하 여 **sp_changearticle**기존 비트 설정이 해제 될 수 있습니다. 기존 설정을 유지 하려면 수행 해야 [| (비트 OR) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 설정 하는 값과의 현재 값 사이 *schema_option*를 실행 하 여 얻는 [sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)합니다.  
  
## <a name="valid-schema-options"></a>유효한 스키마 옵션  
 다음 표에서 설명의 사용 가능한 값 *schema_option* (위쪽에 표시)는 복제 유형 및 아티클 유형 (첫 번째 열에 표시)에 기반 합니다.  
  
|아티클 유형|복제 유형||  
|------------------|----------------------|------|  
||트랜잭션|스냅숏|  
|**logbased**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**logbased manualfilter**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**logbased manualview**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**인덱싱된 뷰 logbased**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**logbased manualfilter 인덱싱된 뷰**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**logbased manualview 인덱싱된 뷰**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**인덱싱된 뷰 logbase manualboth**|모든 옵션|모든 옵션이 있지만 **0x02**|  
|**proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|  
|**serializable proc exec**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|  
|**프로시저 스키마 전용**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|  
|**뷰 스키마 전용**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000입니다**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000입니다**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, 및 **0x80000000**|  
|**func 스키마 전용**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x20**, **0x2000**, **0x400000입니다**, **0x800000**, **0x2000000**, **0x8000000**, **0x10000000**, **0x20000000**, **0x40000000**, 및 **0x80000000**|  
|**인덱싱된 뷰 스키마 전용**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000입니다**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, 및 **0x80000000**|**0x01**, **0x010**, **0x020**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x100000**, **0x200000**, **0x400000입니다**, **0x800000**,  **0x2000000**, **0x8000000**, **0x40000000**, 및 **0x80000000**|  
  
> [!NOTE]  
>  지연 업데이트 게시의 *schema_option* 값 **0x80** 활성화 해야 합니다. 지원 되는 *schema_option* 에 대 한 값 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시는: **0x01**, **0x02**, **0x10**,  **0x40**, **0x80**, **0x1000** 및 **0x4000**합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_changearticle**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [아티클 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
