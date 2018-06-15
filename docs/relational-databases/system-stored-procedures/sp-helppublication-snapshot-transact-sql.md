---
title: sp_helppublication_snapshot (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 166ddc44f6543a5c95ee2650504dcd3f71d45236
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33002720"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 게시에 대한 스냅숏 에이전트의 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher =** ] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자를 지정합니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에 아티클을 추가할 때 사용할 수 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|스냅숏 에이전트의 ID입니다.|  
|**name**|**nvarchar(100)**|스냅숏 에이전트의 이름입니다.|  
|**publisher_security_mode**|**smallint**|에이전트가 게시자에 연결할 때 사용하는 보안 모드로서 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증입니다.|  
|**publisher_login**|**sysname**|게시자에 연결할 때 사용하는 로그인입니다.|  
|**publisher_password**|**nvarchar (524)**|보안상의 이유로 값 **\* \* \* \* \* \* \* \* \* \*** 는 항상 반환 됩니다.|  
|**job_id**|**uniqueidentifier**|에이전트 작업의 고유한 ID입니다.|  
|**job_login**|**nvarchar(512)**|스냅숏 에이전트가 실행 되는, 형식으로 반환 되는 Windows 계정이 며 *도메인*\\*username*합니다.|  
|**job_password**|**sysname**|보안상의 이유로 값 **\* \* \* \* \* \* \* \* \* \*** 는 항상 반환 됩니다.|  
|**schedule_name**|**sysname**|이 에이전트 작업에 사용된 일정의 이름입니다.|  
|**frequency_type**|**int**|에이전트 실행이 예약되는 빈도로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 한 번<br /><br /> **2** = 요청 시<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월 상대적<br /><br /> **64** = 자동 시작<br /><br /> **128** = 되풀이|  
|**frequency_interval**|**int**|에이전트가 실행되는 요일로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**frequency_subday_type**|**int**|얼마나 자주 에이전트가 실행 되는 경우 정의 하는 형식이 *frequency_type* 은 **4** (매일), 다음이 값 중 하나일 수 있습니다.<br /><br /> **1** = 지정 된 시간<br /><br /> **2** = 초<br /><br /> **4** = 분<br /><br /> **8** = 시간|  
|**frequency_subday_interval**|**int**|간격의 수 *frequency_subday_type* 에이전트 예약된 실행 간에 발생 하는 합니다.|  
|**frequency_relative_interval**|**int**|지정된 된 월에서 에이전트가 실행 되는 주로 때 *frequency_type* 은 **32** (매월 상대적) 이며 다음이 값 중 하나일 수 있습니다.<br /><br /> **1** = 첫 번째<br /><br /> **2** = 초<br /><br /> **4** = 세 번째<br /><br /> **8** = 네 번째<br /><br /> **16** = 마지막|  
|**frequency_recurrence_factor**|**int**|에이전트 예약 실행 간의 주 수 또는 월 수입니다.|  
|**active_start_date**|**int**|에이전트의 실행이 음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_end_date**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_start_time**|**int**|에이전트의 실행이 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
|**active_end_time**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_help_publication_snapshot** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할의 멤버나 게시자는 **db_owner** 게시 데이터베이스의 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_help_publication_snapshot** .  
  
## <a name="see-also"></a>관련 항목:  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
