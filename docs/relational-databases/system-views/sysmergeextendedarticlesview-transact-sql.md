---
title: sysmergeextendedarticlesview (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergeextendedarticlesview
- sysmergeextendedarticlesview_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmergeextendedarticlesview view
ms.assetid: bd5c8414-5292-41fd-80aa-b55a50ced7e2
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3902f8b0486928ea1b8601f9d4d225156d9874be
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmergeextendedarticlesview-transact-sql"></a>sysmergeextendedarticlesview(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **sysmergeextendedarticlesview** 뷰는 아티클 정보입니다. 이 뷰는 게시자의 게시 데이터베이스와 구독자의 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|아티클의 이름입니다.|  
|**유형**|**tinyint**|아티클 유형을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 테이블입니다.<br /><br /> **32** = 프로시저 스키마 전용입니다.<br /><br /> **64** = 뷰 스키마 전용 또는 인덱싱된 뷰 스키마 전용입니다.<br /><br /> **128** = 함수 스키마 전용입니다.<br /><br /> **160** = 동의어의 스키마 전용입니다.|  
|**objid**|**int**|게시자 개체에 대한 식별자입니다.|  
|**sync_objid**|**int**|동기화된 데이터 집합을 표시하는 뷰의 식별자입니다.|  
|**view_type**|**tinyint**|뷰의 유형:<br /><br /> **0** = 뷰가 아니며 모든 기준 개체를 사용 하십시오.<br /><br /> **1** = 영구 뷰.<br /><br /> **2** = 임시 뷰.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**설명**|**nvarchar(255)**|아티클에 대한 간단한 설명입니다.|  
|**pre_creation_command**|**tinyint**|아티클이 구독 데이터베이스에서 생성될 때 수행할 기본 동작입니다.<br /><br /> **0** = none-구독자에서 테이블이 이미 있는 경우 아무 작업도 수행 합니다.<br /><br /> **1** = drop-테이블을 다시 만들기 전에 삭제 합니다.<br /><br /> **2** = delete-하위 집합 필터의 WHERE 절을 기준으로 삭제 하는 문제입니다.<br /><br /> **3** = Truncate-2, 같지만 행 대신 페이지를 삭제 합니다. 단, WHERE 절은 사용하지 않습니다.|  
|**pubid**|**uniqueidentifier**|현재 아티클이 속한 게시의 ID입니다.|  
|**애칭**|**int**|아티클 ID에 대한 애칭 매핑입니다.|  
|**column_tracking**|**int**|아티클에 대한 열 추적이 구현되는지 표시합니다.|  
|**상태**|**tinyint**|아티클의 상태를 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **1** = Unsynced-테이블을 게시 하는 초기 처리 스크립트가 다음에 스냅숏 에이전트가 실행 될 때 실행 됩니다.<br /><br /> **2** = active-테이블을 게시 하는 초기 처리 스크립트가 실행 되었습니다.<br /><br /> **5** = New_inactive-추가 될 합니다.<br /><br /> **6** = New_active-추가 될 합니다.|  
|**conflict_table**|**sysname**|현재 아티클에 대한 충돌 기록이 들어 있는 로컬 테이블의 이름입니다. 이 테이블은 정보 제공의 목적으로만 제공되며 사용자 지정 충돌 해결 루틴에 의해서나 직접 관리자에 의해서 수정되거나 삭제될 수 있습니다.|  
|**creation_script**|**nvarchar(255)**|해당 아티클에 대한 생성 스크립트입니다.|  
|**conflict_script**|**nvarchar(255)**|해당 아티클에 대한 충돌 스크립트입니다.|  
|**article_resolver**|**nvarchar(255)**|해당 아티클에 대한 사용자 지정 행 수준 충돌 해결 프로그램입니다.|  
|**ins_conflict_proc**|**sysname**|뿐만 아니라 충돌을 작성 하는 데 필요한 절차 **conflict_table**합니다.|  
|**insert_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 삽입하기 위해 사용하는 프로시저입니다.|  
|**update_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 업데이트하기 위해 사용하는 프로시저입니다.|  
|**select_proc**|**sysname**|병합 에이전트가 잠금을 수행하고 아티클에 대한 열 및 행을 찾기 위해 사용하는 자동 생성 저장 프로시저의 이름입니다.|  
|**schema_option**|**binary (8)**|지원 되는 값에 대 한 *schema_option*, 참조 [sp_addmergearticle &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|구독자에서 생성되는 테이블의 이름입니다.|  
|**resolver_clsid**|**nvarchar(50)**|사용자 지정 충돌 해결 프로그램의 ID입니다.|  
|**subset_filterclause**|**nvarchar (1000)**|해당 아티클에 대한 필터 절입니다.|  
|**missing_col_count**|**int**|누락된 열의 수입니다.|  
|**missing_cols**|**varbinary(128)**|누락된 열의 비트맵입니다.|  
|**열**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resolver_info**|**nvarchar(255)**|사용자 지정 충돌 해결 프로그램에 필요한 추가 정보의 저장소입니다.|  
|**view_sel_proc**|**nvarchar(290)**|병합 에이전트가 동적으로 필터링된 게시에 처음으로 아티클을 채우고 필터링된 모든 게시에 변경된 행을 열거하는 데 사용하는 저장 프로시저의 이름입니다.|  
|**gen_cur**|**int**|아티클의 기본 테이블에 대한 로컬 변경 사항의 생성 번호입니다.|  
|**excluded_cols**|**varbinary(128)**|구독자로 보낼 때 아티클에서 제외되는 열의 비트맵입니다.|  
|**excluded_col_count**|**int**|제외되는 열 수입니다.|  
|**vertical_partition**|**int**|테이블 아티클에 열 필터링 사용 여부를 지정합니다. **0** 는 열 필터링을 나타내는 모든 열을 게시 합니다.|  
|**identity_support**|**int**|자동 ID 범위 처리가 설정되었는지 여부를 지정합니다. **1** id 범위 처리가 활성화 되어 있는지를 의미 하 고 **0** 의미는 없는 id 범위 처리를 지원 합니다.|  
|**destination_owner**|**sysname**|대상 개체의 소유자 이름입니다.|  
|**before_image_objid**|**int**|추적 테이블의 개체 ID입니다. 파티션 변경 최적화를 활성화하도록 게시를 구성하면 추적 테이블에 특정 키 열 값이 포함됩니다.|  
|**before_view_objid**|**int**|뷰 테이블의 개체 ID입니다. 뷰는 행이 삭제 또는 업데이트되기 전에 특정 구독자에 속했는지를 추적하는 테이블에 있습니다. 게시를으로 만든 경우에 적용 됩니다.  *@keep_partition_changes*   =  **true**합니다.|  
|**verify_resolver_signature**|**int**|해결 프로그램을 병합 복제에 사용하기 전에 디지털 서명을 확인할지 여부를 지정합니다.<br /><br /> **0** = 서명을 확인 하지 않습니다.<br /><br /> **1** = 서명을 확인 하는 출처를 신뢰할 수 있는지 여부를 확인 합니다.|  
|**allow_interactive_resolver**|**bit**|아티클에 대화형 해결 프로그램을 사용할지 여부를 지정합니다. **1** 아티클에서 대화형 해결 프로그램이 사용 되도록 지정 합니다.|  
|**fast_multicol_updateproc**|**bit**|병합 에이전트를 사용하도록 설정하여 한 UPDATE 문에서 같은 행의 여러 열에 변경 사항을 적용했는지 여부를 지정합니다.<br /><br /> **0** = 각 열에 대해 별도 업데이트로 변경 하는 문제입니다.<br /><br /> **1** = 하나의 문에서 여러 열에 대 한 업데이트는 UPDATE 문에서 대 한 발급 합니다.|  
|**check_permissions**|**int**|병합 에이전트가 변경 내용을 게시자에 적용할 때 확인할 테이블 수준 사용 권한의 비트맵입니다. *check_permissions* 다음이 값 중 하나일 수 있습니다.<br /><br /> **0x00** = 권한을 확인 하지 않습니다.<br /><br /> **0x10** 구독자에서 수행한 Insert를 업로드 하기 전에 = 게시자에서 사용 권한을 확인 합니다.<br /><br /> **0x20** 구독자에서 수행한 Update를 업로드 하기 전에 = 게시자에서 사용 권한을 확인 합니다.<br /><br /> **0x40** 구독자에서 수행한 업로드 하기 전에 = 게시자에서 사용 권한을 확인 합니다.|  
|**maxversion_at_cleanup**|**int**|메타데이터가 정리되는 가장 높은 생성층입니다.|  
|**processing_order**|**int**|병합 게시에서 아티클의 처리 순서를 나타냅니다. 여기서 값 **0** 은 아티클이 정렬 되지 최소값부터 최대값의 순서로 아티클이 처리 표시 합니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 자세한 내용은 [병합 아티클의 처리 순서 지정](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)을 참조하세요.|  
|**published_in_tran_pub**|**bit**|병합 게시의 아티클이 트랜잭션 게시에도 게시됨을 나타냅니다.<br /><br /> **0** = 아티클을 트랜잭션 아티클에도 게시 하지 않습니다.<br /><br /> **1** = 아티클을 트랜잭션 아티클에도 게시 합니다.|  
|**upload_options**|**tinyiny**|구독자에서 변경이 수행되거나 업로드될 수 있는지 여부를 정의하며 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 구독자에서 수행 되는 업데이트에 대 한 제한은 없습니다; 모든 변경 내용이 게시자로 업로드 됩니다.<br /><br /> **1** =는 허용 되지만 변경 내용이 구독자에서 게시자로 업로드 되지 않습니다.<br /><br /> **2** = 구독자에서 변경이 허용 되지 않습니다.|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**delete_proc**|**sysname**|동기화 동안 기본 충돌 해결 프로그램이 행을 삭제하기 위해 사용하는 프로시저입니다.|  
|**before_upd_view_objid**|**int**|업데이트하기 전 테이블 뷰의 ID입니다.|  
|**delete_tracking**|**bit**|삭제 내용을 복제할지 여부를 나타냅니다.<br /><br /> **0** = 삭제 내용을 복제 하지 않습니다.<br /><br /> **1** = 삭제 내용을 복제, 이것이 병합 복제에 대 한 기본 동작입니다.<br /><br /> 때의 값 *delete_tracking* 은 **0**구독자에서 삭제 된 행은 게시자에서 수동으로 제거 하 고 게시자에서 삭제 된 행은 구독자에서 수동으로 제거 해야 합니다.<br /><br /> 참고: 값 **0** 불일치가 발생 합니다.|  
|**compensate_for_errors**|**bit**|동기화 중에 오류가 발생할 경우 보정 동작이 수행될지 여부를 나타냅니다.<br /><br /> **0** = 보정 동작이 해제 합니다.<br /><br /> **1** = 적용할 수 없는 구독자 또는 게시자 인해 항상 보정 이것이 병합 복제에 대 한 기본 동작을 이러한 변경 내용을 실행 취소 하는 동작을 변경 합니다.<br /><br /> 참고: 값 **0** 불일치가 발생 합니다.|  
|**pub_range**|**bigint**|게시자 ID의 범위 크기입니다.|  
|**범위**|**bigint**|조정 시 구독자에게 할당되는 연속 ID 값의 크기입니다.|  
|**임계값**|**int**|ID 범위 임계값 비율입니다.|  
|**metadata_select_proc**|**sysname**|병합 복제 시스템 테이블의 메타데이터에 액세스하기 위해 사용하는 자동 생성 저장 프로시저의 이름입니다.|  
|**stream_blob_columns**|**bit**|이진 대용량 개체 열을 복제할 때 데이터 스트림 최적화를 사용할지 지정합니다. **1** 의미 하는 최적화를 시도 합니다.|  
|**preserve_rowguidcol**|**bit**|복제에 기존 rowguid 열이 사용될지 여부를 나타냅니다. 값이 **1** 기존 ROWGUIDCOL 열 사용 됨을 의미 합니다. **0** 복제가 ROWGUIDCOL 열을 추가 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sysmergearticles &#40; Transact SQL &#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)  
  
  
