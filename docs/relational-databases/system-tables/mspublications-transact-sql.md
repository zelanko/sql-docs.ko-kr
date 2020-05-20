---
title: MSpublications (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 31f7d9c3e5d297a39fd0278c51014793a4b8dbd0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829251"
---
# <a name="mspublications-transact-sql"></a>MSpublications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublications** 테이블은 게시자에 의해 복제 되는 각 게시 마다 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**publication_type**|**int**|게시의 유형입니다.<br /><br /> **0** = 트랜잭션<br /><br /> **1** = 스냅숏<br /><br /> **2** = 병합.|  
|**thirdparty_flag**|**bit**|게시가 데이터베이스 인지 여부를 나타냅니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> **1** = 이외의 데이터 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다.|  
|**independent_agent**|**bit**|이 게시에 대한 독립 실행형 배포 에이전트가 있는지 여부를 나타냅니다.|  
|**immediate_sync**|**bit**|스냅샷 에이전트가 실행될 때마다 동기화 파일을 만들거나 다시 만들지 여부를 나타냅니다.|  
|**allow_push**|**bit**|지정된 게시에 대해 밀어넣기 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**allow_pull**|**bit**|지정된 게시에 대해 끌어오기 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**allow_anonymous**|**bit**|지정된 게시에 대해 익명 구독을 만들 수 있는지 여부를 나타냅니다.|  
|**한**|**nvarchar(255)**|게시에 대한 설명입니다.|  
|**vendor_name**|**nvarchar (100)**|게시자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 아닌 경우의 공급업체 이름입니다.|  
|**보존**|**int**|게시 보존 기간(시간)입니다.|  
|**sync_method**|**int**|동기화 메서드<br /><br /> **0** = 네이티브 (모든 테이블의 기본 모드 대량 복사 출력 생성)<br /><br /> **1** = 문자 (모든 테이블의 문자 모드 대량 복사 출력을 생성)<br /><br /> **3** = 동시 (모든 테이블의 기본 모드 대량 복사 출력을 생성 하지만 스냅숏을 실행 하는 동안 테이블을 잠그지 않음)<br /><br /> **4** = Concurrent_c (모든 테이블의 문자 모드 대량 복사 출력을 생성 하지만 스냅숏을 실행 하는 동안 테이블을 잠그지 않음)<br /><br /> 값 **3** 과 **4** 는 트랜잭션 복제 및 병합 복제에 사용할 수 있지만 스냅숏 복제에 대해서는 사용할 수 없습니다.|  
|**allow_subscription_copy**|**bit**|이 게시를 구독하는 구독 데이터베이스를 복사하는 기능을 설정 또는 해제합니다. **0** 은 복사를 사용할 수 없음을 의미 하 고 **1** 은 사용 하도록 설정 되었음을 의미 합니다.|  
|**thirdparty_options**|**int**|의 복제 폴더에 있는 게시 표시를 표시 하지 않을 지 여부를 지정 합니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .<br /><br /> **0** = 유형이 다른 게시를의 복제 폴더에 표시 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 합니다.<br /><br /> **1** = 다른 유형의 게시를의 복제 폴더에 표시 하지 않습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .|  
|**allow_queued_tran**|**bit**|게시에 지연 업데이트가 허용되는지 여부를 지정합니다.<br /><br /> **0 =** 게시가 큐에 저장 되지 않았습니다.<br /><br /> **1** = 게시가 대기 중입니다.|  
|**options**|**int**|이 릴리스에서는 사용할 수 없는 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
