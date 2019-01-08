---
title: sp_helpmergeconflictrows (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af247734b941a0d9fd7010d4699f9ddb296c890e
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589167"
---
# <a name="sphelpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 충돌 테이블의 행을 반환합니다. 이 저장 프로시저는 충돌 테이블이 저장된 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=**] **'**_게시_**'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 **%** 합니다. 게시가 지정된 경우에는 해당 게시에 대한 모든 충돌이 반환됩니다. 예를 들어 경우는 **MSmerge_conflict_Customers** 테이블에 대 한 충돌 행의 **WA** 및 **CA** 게시에 게시 이름을 **CA**  와 관련 된 충돌을 검색 합니다 **CA** 게시 합니다.  
  
 [  **@conflict_table=**] **'**_conflict_table_**'**  
 충돌 테이블의 이름입니다. *conflict_table* 됩니다 **sysname**, 기본값은 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 충돌 테이블 이름으로 형식 이름을 사용 하 여 **MSmerge_conflict\__게시\_문서_** 를 사용 하 여 게시 된 각 아티클당 한 테이블입니다.  
  
 [  **@publisher=**] **'**_게시자_**'**  
 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 게시자 데이터베이스의 이름이입니다. *publisher_db* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@logical_record_conflicts=** ] *logical_record_conflicts*  
 결과 집합에 논리 레코드 충돌 정보가 포함되는지 여부를 나타냅니다. *logical_record_conflicts* 됩니다 **int**을 기본값인 0 사용 하 여 합니다. **1** 논리 레코드 충돌 정보가 반환 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_helpmergeconflictrows** 결과 기본 테이블 구조 및 이러한 추가 열으로 구성 된 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|충돌의 시작입니다.|  
|**conflict_type**|**int**|충돌 유형을 표시하는 코드입니다.<br /><br /> **1** = 업데이트 충돌: 충돌이 행 수준에서 검색됩니다.<br /><br /> **2** = 열 업데이트 충돌: 충돌이 열 수준에서 검색됩니다.<br /><br /> **3** = 업데이트 / 삭제 충돌 합니다. 삭제가 충돌에서 적용됩니다.<br /><br /> **4** = 업데이트 / 삭제 충돌 합니다. 충돌에서 패한 삭제된 rowguid가 이 테이블에 기록됩니다.<br /><br /> **5** = 업로드 삽입 실패: 구독자에서의 삽입을 게시자에 적용할 수 없습니다.<br /><br /> **6** = 다운로드 삽입 실패: 게시자에서의 삽입을 구독자에 적용할 수 없습니다.<br /><br /> **7** = 업로드 삭제 실패: 구독자에서의 삭제를 게시자로 업로드할 수 없습니다.<br /><br /> **8** = 다운로드 삭제 실패: 게시자에서의 삭제를 구독자로 다운로드할 수 없습니다.<br /><br /> **9** = 업로드 업데이트 실패: 구독자에서의 업데이트를 게시자에 적용할 수 없습니다.<br /><br /> **10** = 다운로드 업데이트 실패: 게시자에서의 업데이트를 구독자에 적용할 수 없습니다.<br /><br /> **12** = 논리 레코드 업데이트/삭제 충돌 합니다. 충돌에서 적용하지 못한 삭제된 논리 레코드가 이 테이블에 기록됩니다.<br /><br /> **13** = 논리 레코드 삽입/업데이트 충돌: 논리 레코드 삽입이 업데이트와 충돌합니다.<br /><br /> **14** = 논리 레코드 삭제 / 업데이트 충돌: 충돌에서 적용하지 못한 업데이트된 논리 레코드가 이 테이블에 기록됩니다.|  
|**reason_code**|**int**|상황에 맞는 오류 코드입니다.|  
|**reason_text**|**varchar(720)**|상황에 맞는 오류 설명입니다.|  
|**pubid**|**uniqueidentifier**|게시 식별자입니다.|  
|**MSrepl_create_time**|**datetime**|충돌 정보가 추가된 시간입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergeconflictrows** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원만 합니다 **sysadmin** 고정 서버 역할을 **db_owner** 고정 데이터베이스 역할 및 **replmonitor** 배포 데이터베이스의 역할 실행할수있습니다**sp_helpmergeconflictrows**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 게시에 대 한 충돌 정보 보기 &#40;복제 TRANSACT-SQL 프로그래밍&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
