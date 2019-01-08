---
title: MSpublications (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb939681cb97b80a7bd0498a2e0c1fa30202c404
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791545"
---
# <a name="mspublications-transact-sql"></a>MSpublications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSpublications** 게시자에 의해 복제 되는 각 게시에 대해 하나의 행을 포함 하는 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**publication_type**|**int**|게시의 유형입니다.<br /><br /> **0** = 트랜잭션.<br /><br /> **1** = 스냅숏.<br /><br /> **2** = 병합 합니다.|  
|**thirdparty_flag**|**bit**|게시 되는지 여부를 나타냅니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1** 이외의 데이터 원본 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**immediate_sync**|**bit**|스냅숏 에이전트가 실행될 때마다 동기화 파일을 만들거나 다시 만들지 여부를 나타냅니다.|  
|**allow_push**|**bit**|지정된 게시에 대해 밀어넣기 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**allow_pull**|**bit**|지정된 게시에 대해 끌어오기 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**allow_anonymous**|**bit**|지정된 게시에 대해 익명 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**description**|**nvarchar(255)**|게시에 대한 설명입니다.|  
|**vendor_name**|**nvarchar(100)**|게시자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 아닌 경우의 공급업체 이름입니다.|  
|**retention**|**int**|게시 보존 기간(시간)입니다.|  
|**sync_method**|**int**|동기화 메서드<br /><br /> **0** = 기본 (모든 테이블의 네이티브 모드 대량 복사 출력을 생성).<br /><br /> **1** = 문자 (모든 테이블의 문자 모드 대량 복사 출력을 생성).<br /><br /> **3** = concurrent (테이블의 모든 네이티브 모드 대량 복사 출력을 만들지만 스냅샷 중 테이블을 잠그지 않습니다).<br /><br /> **4** = Concurrent_c (테이블의 모든 문자 모드 대량 복사 출력을 만들지만 스냅샷 중 테이블을 잠그지 않습니다)<br /><br /> 값 **3** 하 고 **4** 사용할 수 있는 트랜잭션 복제 및 병합 복제 되지만 스냅숏 복제 합니다.|  
|**allow_subscription_copy**|**bit**|이 게시를 구독하는 구독 데이터베이스를 복사하는 기능을 설정 또는 해제합니다. **0** 는 복사 하지 않으면 의미 하 고 **1** 사용 하는 것을 의미 합니다.|  
|**thirdparty_options**|**int**|지정 여부의 복제 폴더에 있는 게시 표시를 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 표시 되지 않습니다.<br /><br /> **0** = 유형이 다른 게시의 복제 폴더에 표시할 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.<br /><br /> **1** 표시를 = 유형이 다른 게시의 복제 폴더에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.|  
|**allow_queued_tran**|**bit**|게시에 지연 업데이트가 허용되는지 여부를 지정합니다.<br /><br /> **0 =** 게시 지연 되지 않습니다.<br /><br /> **1** = 게시가 지연 됩니다.|  
|**options**|**int**|이 릴리스에서는 사용할 수 없는 정보입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
