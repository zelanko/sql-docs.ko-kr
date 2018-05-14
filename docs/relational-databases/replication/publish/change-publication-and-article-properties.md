---
title: 게시 및 아티클 속성 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying article properties
- modifying publication properties
- administering replication, properties
- publications [SQL Server replication], changing properties
- articles [SQL Server replication], properties
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c79e19d6cd66cd25796d63d214b0234a659a9dc6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="change-publication-and-article-properties"></a>게시 및 아티클 속성 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  게시 생성 후 대부분의 게시 및 아티클 속성을 변경할 수 있지만 일부 속성을 변경하려면 스냅숏을 다시 생성하거나 구독을 다시 초기화해야 합니다. 이 항목에서는 변경 시 이러한 두 가지 동작 중 하나 또는 모두가 필요한 모든 속성에 대한 정보를 제공합니다.  
  
## <a name="publication-properties-for-snapshot-and-transactional-replication"></a>스냅숏 및 트랜잭션 복제에 대한 게시 속성  
  
|Description|저장 프로시저|속성|요구 사항|  
|-----------------|----------------------|----------------|------------------|  
|스냅숏 형식을 변경합니다.|**sp_changepublication**|**sync_method**|새 스냅숏|  
|스냅숏 위치를 변경합니다.|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|새 스냅숏|  
|스냅숏 위치를 변경합니다.|**sp_changedistpublisher**|**working_directory**|새 스냅숏|  
|스냅숏 압축을 변경합니다.|**sp_changepublication**|**compress_snapshot**|새 스냅숏|  
|모든 FTP(파일 전송 프로토콜) 스냅숏 옵션을 변경합니다.|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|새 스냅숏|  
|프리 스냅숏 스크립트 또는 포스트 스냅숏 스크립트의 위치를 변경합니다.|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|새 스냅숏(스크립트 내용을 변경한 경우에도 필요)<br /><br /> 구독자에 새 스크립트를 적용하기 위해 재초기화가 필요합니다.|  
|비-[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에 대한 지원을 설정 또는 해제합니다.|**sp_changepublication**|**is_enabled_for_het_sub**|새 스냅숏|  
|지연 업데이트 구독에 대한 충돌 보고를 변경합니다.|**sp_changepublication**|**centralized_conflicts**|활성 구독이 없을 때만 변경될 수 있습니다.|  
|지연 업데이트 구독에 대한 충돌 해결 정책을 변경합니다.|**sp_changepublication**|**conflict_policy**|활성 구독이 없을 때만 변경될 수 있습니다.|  
  
## <a name="article-properties-for-snapshot-and-transactional-replication"></a>스냅숏 및 트랜잭션 복제에 대한 아티클 속성  
  
|Description|저장 프로시저|속성|요구 사항|  
|-----------------|----------------------|----------------|------------------|  
|아티클을 삭제합니다.|**sp_droparticle**|모든 매개 변수|구독을 만들기 전에 아티클을 삭제할 수 있습니다. 저장 프로시저를 사용하면 아티클에 대한 구독을 삭제할 수 있고, [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]를 사용하면 전체 구독을 삭제하고 다시 만든 후 동기화해야 합니다. 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.|  
|열 필터를 변경합니다.|**sp_articlecolumn**|**@column**<br /><br /> **@operation**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|행 필터를 추가합니다.|**sp_articlefilter**|모든 매개 변수|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|행 필터를 삭제합니다.|**sp_articlefilter**|**@article**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|행 필터를 변경합니다.|**sp_articlefilter**|**@filter_clause**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|행 필터를 변경합니다.|**sp_changearticle**|**filter**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|스키마 옵션을 변경합니다.|**sp_changearticle**|**schema_option**|새 스냅숏|  
|스냅숏을 적용하기 전에 구독자에서 테이블이 처리되는 방식을 변경합니다.|**sp_changearticle**|**pre_creation_cmd**|새 스냅숏|  
|아티클 상태를 변경합니다.|**sp_changearticle**|**상태**|새 스냅숏|  
|INSERT, UPDATE 또는 DELETE 명령을 변경합니다.|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|대상 테이블 이름을 변경합니다.|**sp_changearticle**|**dest_table**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|대상 테이블 소유자(스키마)를 변경합니다.|**sp_changearticle**|**destination_owner**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|데이터 형식 매핑을 변경합니다. Oracle 게시에만 적용됩니다.|**sp_changearticlecolumndatatype**|**@type**<br /><br /> **@length**<br /><br /> **@precision**<br /><br /> **@scale**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
  
## <a name="publication-properties-for-merge-replication"></a>병합 복제에 대한 게시 속성  
  
|Description|저장 프로시저|속성|요구 사항|  
|-----------------|----------------------|----------------|------------------|  
|스냅숏 형식을 변경합니다.|**sp_changemergepublication**|**sync_mode**|새 스냅숏|  
|스냅숏 위치를 변경합니다.|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|새 스냅숏|  
|스냅숏 위치를 변경합니다.|**sp_changedistpublisher**|**working_directory**|새 스냅숏|  
|스냅숏 압축을 변경합니다.|**sp_changemergepublication**|**compress_snapshot**|새 스냅숏|  
|FTP 스냅숏 옵션을 변경합니다.|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|새 스냅숏|  
|프리 스냅숏 스크립트 또는 포스트 스냅숏 스크립트를 변경합니다.|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|새 스냅숏(스크립트 내용을 변경한 경우에도 필요)<br /><br /> 구독자에 새 스크립트를 적용하기 위해 재초기화가 필요합니다.|  
|조인 필터 또는 논리적 레코드를 추가합니다.|**sp_addmergefilter**|모든 매개 변수|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|조인 필터 또는 논리적 레코드를 삭제합니다.|**sp_dropmergefilter**|모든 매개 변수|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|조인 필터 또는 논리적 레코드를 변경합니다.|**sp_changemergefilter**|**@property**<br /><br /> **@value**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|매개 변수가 있는 필터의 사용을 해제합니다. 매개 변수가 있는 필터 사용 시 특별한 조치는 필요하지 않습니다.|**sp_changemergepublication**|**false** 에 대한 **false**값|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|사전 계산 파티션 사용을 설정 또는 해제합니다.|**sp_changemergepublication**|**use_partition_groups**|새 스냅숏|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 파티션 최적화를 설정 또는 해제합니다.|**sp_changemergepublication**|**keep_partition_changes**|구독을 다시 초기화합니다.|  
|구독자 파티션 유효성 검사를 설정 또는 해제합니다.|**sp_changemergepublication**|**validate_subscriber_info**|구독을 다시 초기화합니다.|  
|게시 호환성 수준을 80sp3 이하로 변경합니다.|**sp_changemergepublication**|**publication_compatibility_level**|새 스냅숏|  
  
## <a name="article-properties-for-merge-replication"></a>병합 복제에 대한 아티클 속성  
  
|Description|저장 프로시저|속성|요구 사항|  
|-----------------|----------------------|----------------|------------------|  
|매개 변수가 있는 필터가 게시의 마지막 필터인 아티클을 삭제합니다.|**sp_dropmergearticle**|모든 매개 변수|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|아티클이 조인 필터 또는 논리적 레코드에서 부모인 아티클을 삭제합니다. 조인을 삭제하면 의도하지 않는 결과가 발생할 수 있습니다.|**sp_dropmergearticle**|모든 매개 변수|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|다른 모든 경우의 아티클을 삭제합니다.|**sp_dropmergearticle**|모든 매개 변수|새 스냅숏|  
|이전에 게시되지 않은 열 필터를 포함합니다.|**sp_mergearticlecolumn**|**@column**<br /><br /> **@operation**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|행 필터를 추가, 삭제 또는 변경합니다.|**sp_changemergearticle**|**subset_filterclause**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.<br /><br /> 매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.<br /><br /> 아티클이 조인 필터에 포함되지 않은 경우 아티클을 삭제하고 이를 다른 행 필터로 다시 추가할 수 있습니다. 이 경우 전체 구독을 다시 초기화할 필요가 없습니다. 아티클을 추가 및 삭제하는 방법에 대한 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.|  
|스키마 옵션을 변경합니다.|**sp_changemergearticle**|**schema_option**|새 스냅숏|  
|열 수준 추적을 행 수준 추적을 변경합니다. 행 수준 추적에서 열 수준 추적으로 변경할 때는 특별한 조치가 필요하지 않습니다.|**sp_changemergearticle**|**false** 에 대한 **false**값|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|구독자에서 작성된 문이 게시자에 적용되기 전에 사용 권한을 확인할지 여부를 변경합니다.|**sp_changemergearticle**|**check_permissions**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
|다운로드 전용 구독을 설정 또는 해제합니다. 다른 업로드 옵션 간에 변경할 때는 특별한 조치가 필요하지 않습니다.|**sp_changemergearticle**|**2** 에 대한 값 **2**를 변경|구독을 다시 초기화합니다.|  
|대상 테이블 소유자를 변경합니다.|**sp_changemergearticle**|**destination_owner**|새 스냅숏<br /><br /> 구독을 다시 초기화합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [관리&#40;복제&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [스냅숏 만들기 및 적용](../../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_changearticlecolumndatatype&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_changemergefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_changemergepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_changepublication&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droparticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_dropmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_dropmergefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_mergearticlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)  
  
  
