---
title: sysmergearticles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergearticles
- sysmergearticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticles system table
ms.assetid: e9b1648e-4660-4688-9f56-18b2baf7228c
author: stevestein
ms.author: sstein
ms.openlocfilehash: d712f462ebe504df20ded93d6a9730ce31e4d0db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72251943"
---
# <a name="sysmergearticles-transact-sql"></a>sysmergearticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 데이터베이스에 정의된 각 병합 아티클에 대해 한 행을 포함합니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|아티클의 이름입니다.|  
|**type**|**tinyint**|아티클 유형을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 테이블<br /><br /> **32** = 저장 프로시저 (스키마 전용)입니다.<br /><br /> **64** = 뷰 또는 인덱싱된 뷰 (스키마 전용)입니다.<br /><br /> **128** = 사용자 정의 함수 (스키마 전용)입니다.<br /><br /> **160** = 동의어 (스키마 전용)입니다.|  
|**objid**|**int**|개체 식별자입니다.|  
|**sync_objid**|**int**|동기화된 데이터 집합을 표시하는 뷰의 개체 ID입니다.|  
|**view_type**|**tinyint**|뷰의 유형:<br /><br /> **0** = 뷰가 아닙니다. 모든 기본 개체를 사용 합니다.<br /><br /> **1** = 영구 뷰입니다.<br /><br /> **2** = 임시 뷰|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**한**|**nvarchar(255)**|아티클에 대한 간단한 설명입니다.|  
|**pre_creation_command**|**tinyint**|아티클이 구독 데이터베이스에서 생성될 때 수행할 기본 동작입니다.<br /><br /> **0 =** None-구독자에 테이블이 이미 있는 경우 아무 동작도 수행 되지 않습니다.<br /><br /> **1** = Drop-테이블을 다시 만들기 전에 테이블을 삭제 합니다.<br /><br /> **2** = delete-하위 집합 필터의 where 절을 기반으로 삭제를 실행 합니다.<br /><br /> **3** = Truncate- **2**와 동일 하지만 행 대신 페이지를 삭제 합니다. 단, WHERE 절은 사용하지 않습니다.|  
|**pubid**|**uniqueidentifier**|현재 아티클이 속한 게시의 ID입니다.|  
|**애칭**|**int**|아티클 ID에 대한 애칭 매핑입니다.|  
|**column_tracking**|**int**|아티클에 대한 열 추적이 구현되는지 여부를 나타냅니다.|  
|**status**|**tinyint**|아티클의 상태를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 동기화 됨-테이블을 게시 하는 초기 처리 스크립트가 다음에 스냅숏 에이전트 실행 될 때 실행 됩니다.<br /><br /> **2** = 활성-테이블을 게시 하는 초기 처리 스크립트가 실행 되었습니다.<br /><br /> **5** = New_inactive를 추가 합니다.<br /><br /> **6** = New_active 추가할 수 있습니다.|  
|**conflict_table**|**sysname**|현재 아티클에 대한 충돌 기록이 들어 있는 로컬 테이블의 이름입니다. 이 테이블은 정보 제공의 목적으로만 제공되며 사용자 지정 충돌 해결 루틴에 의해서나 직접 관리자에 의해서 수정되거나 삭제될 수 있습니다.|  
|**creation_script**|**nvarchar(255)**|해당 아티클에 대한 생성 스크립트입니다.|  
|**conflict_script**|**nvarchar(255)**|해당 아티클에 대한 충돌 스크립트입니다.|  
|**article_resolver**|**nvarchar(255)**|해당 아티클에 대한 사용자 지정 행 수준 충돌 해결 프로그램입니다.|  
|**ins_conflict_proc**|**sysname**|**Conflict_table**에 대 한 충돌을 기록 하는 데 사용 되는 프로시저입니다.|  
|**insert_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 삽입하기 위해 사용하는 프로시저입니다.|  
|**update_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 업데이트하기 위해 사용하는 프로시저입니다.|  
|**select_proc**|**sysname**|병합 에이전트가 잠금을 수행하고 아티클에 대한 열 및 행을 찾기 위해 사용하는 자동 생성 저장 프로시저의 이름입니다.|  
|**metadata_select_proc**|**sysname**|병합 복제 시스템 테이블의 메타데이터에 액세스하기 위해 사용하는 자동 생성 저장 프로시저의 이름입니다.|  
|**delete_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 삭제하기 위해 사용하는 프로시저입니다.|  
|**schema_option**|**binary (8)**|*Schema_option*지원 되는 값은 [sp_addmergearticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)를 참조 하세요.|  
|**destination_object**|**sysname**|구독자에서 생성되는 테이블의 이름입니다.|  
|**destination_owner**|**sysname**|대상 개체의 소유자 이름입니다.|  
|**resolver_clsid**|**nvarchar(50)**|사용자 지정 충돌 해결 프로그램의 ID입니다.|  
|**subset_filterclause**|**nvarchar(1000)**|해당 아티클에 대한 필터 절입니다.|  
|**missing_col_count**|**int**|누락된 열의 수입니다.|  
|**missing_cols**|**varbinary(128)**|누락된 열의 비트맵입니다.|  
|**excluded_cols**|**varbinary(128)**|구독자로 보낼 때 아티클에서 제외되는 열의 비트맵입니다.|  
|**excluded_col_count**|**int**|제외되는 열 수입니다.|  
|**세로**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|원본 테이블에서 삭제된 열의 비트맵입니다.|  
|**resolver_info**|**nvarchar(255)**|사용자 지정 충돌 해결 프로그램에 필요한 추가 정보의 스토리지입니다.|  
|**view_sel_proc**|**nvarchar (가 나)**|병합 에이전트가 동적으로 필터링된 게시에 처음으로 아티클을 채우고 필터링된 모든 게시에 변경된 행을 열거하는 데 사용하는 저장 프로시저의 이름입니다.|  
|**gen_cur**|**int**|아티클의 기본 테이블에 대한 로컬 변경 사항의 생성 번호입니다.|  
|**vertical_partition**|**int**|테이블 아티클에 열 필터링 사용 여부를 지정합니다. **0** 은 세로 필터링이 없으며 모든 열을 게시 함을 나타냅니다.|  
|**identity_support**|**int**|자동 ID 범위 처리가 설정되었는지 여부를 지정합니다. **1** 은 id 범위 처리를 사용 하도록 설정 하 고 **0** 은 id 범위를 지원 하지 않음을 의미 합니다.|  
|**before_image_objid**|**int**|추적 테이블의 개체 ID입니다. * \@Keep_partition_changes* = **true**를 사용 하 여 게시를 만들 때 추적 테이블에 특정 키 열 값이 포함 됩니다.|  
|**before_view_objid**|**int**|뷰 테이블의 개체 ID입니다. 뷰는 행이 삭제 또는 업데이트되기 전에 특정 구독자에 속했는지를 추적하는 테이블에 있습니다. * \@Keep_partition_changes* = **true** 를 사용 하 여 게시를 만들 때만 적용 됩니다.|  
|**verify_resolver_signature**|**int**|해결 프로그램을 병합 복제에 사용하기 전에 디지털 서명을 확인할지 여부를 지정합니다.<br /><br /> **0** = 서명이 확인 되지 않습니다.<br /><br /> **1** = 서명을 확인 하 여 신뢰할 수 있는 원본에서 가져온 것인지 확인 합니다.|  
|**allow_interactive_resolver**|**bit**|아티클에 대화형 해결 프로그램을 사용할지 여부를 지정합니다. **1** 은 대화형 해결 프로그램을 아티클에서 사용 하도록 지정 합니다.|  
|**fast_multicol_updateproc**|**bit**|병합 에이전트를 사용하도록 설정하여 한 UPDATE 문에서 같은 행의 여러 열에 변경 사항을 적용했는지 여부를 지정합니다.<br /><br /> **0** = 변경 된 각 열에 대해 별도의 업데이트를 발급 합니다.<br /><br /> **1** = 한 문의 여러 열에 업데이트를 발생 시키는 UPDATE 문을 실행 합니다.|  
|**check_permissions**|**int**|병합 에이전트가 변경 사항을 게시자에 적용할 때 확인할 테이블 수준 권한의 비트맵입니다. *check_permissions* 는 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0x00 =** 사용 권한은 확인 되지 않습니다.<br /><br /> **0x10 =** 구독자에서 삽입 된 삽입 작업을 업로드 하기 전에 게시자에서 사용 권한을 확인 합니다.<br /><br /> **0x20 =** 구독자에서 수행 된 업데이트를 업로드 하기 전에 게시자에서 사용 권한을 확인 합니다.<br /><br /> **0x40 =** 구독자에서 수행 된 삭제 작업을 업로드 하기 전에 게시자에서 사용 권한을 확인 합니다.|  
|**maxversion_at_cleanup**|**int**|메타데이터가 정리되는 가장 높은 생성층입니다.|  
|**processing_order**|**int**|병합 게시에서 아티클의 처리 순서를 나타냅니다. 여기서 값 **0** 은 아티클이 정렬 되지 않은 것으로 표시 되 고 아티클은 가장 낮은 값에서 가장 높은 값으로 처리 됩니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 자세한 내용은 [병합 복제 속성 지정](../../relational-databases/replication/merge/specify-merge-replication-properties.md)을 참조하세요.|  
|**upload_options**|**tinyint**|클라이언트 구독이 있는 구독자에서 수행되는 업데이트에 대한 제한을 정의하며 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 클라이언트 구독이 있는 구독자에서 수행 되는 업데이트에 대 한 제한은 없습니다. 모든 변경 내용이 게시자로 업로드 됩니다.<br /><br /> **1** = 클라이언트 구독이 있는 구독자에서 변경이 허용 되지만 게시자로 업로드 되지 않습니다.<br /><br /> **2** = 클라이언트 구독이 있는 구독자에서 변경이 허용 되지 않습니다.<br /><br /> 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.|  
|**published_in_tran_pub**|**bit**|병합 게시의 아티클이 트랜잭션 게시에도 게시됨을 나타냅니다.<br /><br /> **0** = 아티클이 트랜잭션 아티클에서 게시 되지 않습니다.<br /><br /> **1** = 아티클이 트랜잭션 문서에도 게시 됩니다.|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|추가될 예정입니다.|  
|**delete_tracking**|**bit**|삭제 내용을 복제하는지 여부를 나타냅니다.<br /><br /> **0** = 삭제가 복제 되지 않습니다.<br /><br /> **1** = 병합 복제에 대 한 기본 동작인 삭제가 복제 됩니다.<br /><br /> *Delete_tracking* 값이 **0**이면 구독자에서 삭제 된 행을 게시자에서 수동으로 제거 하 고 게시자에서 삭제 된 행을 구독자에서 수동으로 제거 해야 합니다.<br /><br /> 참고: 값 **0** 은 일치 하지 않습니다.|  
|**compensate_for_errors**|**bit**|동기화 중에 오류가 발생할 경우 보정 동작을 수행하는지 여부를 나타냅니다.<br /><br /> **0** = 보정 동작을 사용할 수 없습니다.<br /><br /> **1** = 구독자 또는 게시자에서 적용할 수 없는 변경 내용은 항상 보정 동작을 수행 하 여 병합 복제의 기본 동작을 실행 취소 합니다.<br /><br /> 참고: 값 **0** 은 일치 하지 않습니다.|  
|**pub_range**|**bigint**|게시자 ID의 범위 크기입니다.|  
|**벗어납니다**|**bigint**|조정 시 구독자에게 할당되는 연속 ID 값의 크기입니다.|  
|**고대비**|**int**|ID 범위 임계값 비율입니다.|  
|**stream_blob_columns**|**bit**|BLOB(Binary Large Object) 열을 복제할 때 데이터 스트림 최적화를 사용할지 여부를 지정합니다. **1** 은 최적화가 시도 됨을 의미 합니다.|  
|**preserve_rowguidcol**|**bit**|복제에 기존 rowguid 열이 사용되는지 여부를 나타냅니다. 값 **1** 은 기존 ROWGUIDCOL 열이 사용 됨을 의미 합니다. **0** 은 복제가 ROWGUIDCOL 열을 추가 했음을 의미 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;복제 뷰](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Transact-sql&#41;sp_addmergearticle &#40;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [Transact-sql&#41;sp_changemergearticle &#40;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)  
  
  
