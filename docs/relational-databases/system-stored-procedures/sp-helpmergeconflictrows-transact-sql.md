---
title: sp_helpmergeconflictrows (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: b72a821c56f35e1ea7f3542b5746c234012c2da0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68137767"
---
# <a name="sp_helpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 충돌 테이블의 행을 반환합니다. 이 저장 프로시저는 충돌 테이블이 저장된 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **%** 입니다. 게시가 지정된 경우에는 해당 게시에 대한 모든 충돌이 반환됩니다. 예를 들어 **MSmerge_conflict_Customers** 테이블에 **WA** 및 **CA** 게시에 대 한 충돌 행이 있는 경우 게시 이름 **ca** 를 전달 하면 **ca** 게시와 관련 된 충돌을 검색 합니다.  
  
`[ @conflict_table = ] 'conflict_table'`충돌 테이블의 이름입니다. *conflict_table* 는 **sysname**이며 기본값은 없습니다. 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 버전에서 충돌 테이블은 게시 된 각 아티클에 대해 하나의 테이블을 사용 하 여 **\_MSmerge_conflict 게시\_아티클의**형식 이름을 사용 하 여 지정 됩니다.  
  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @logical_record_conflicts = ] logical_record_conflicts`결과 집합에 논리 레코드 충돌 정보가 포함 되는지 여부를 나타냅니다. *logical_record_conflicts* 은 **int**이며 기본값은 0입니다. **1** 은 논리적 레코드 충돌 정보가 반환 됨을 의미 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_helpmergeconflictrows** 은 기본 테이블 구조와 이러한 추가 열로 구성 된 결과 집합을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar (255)**|충돌의 시작입니다.|  
|**conflict_type**|**int**|충돌 유형을 표시하는 코드입니다.<br /><br /> **1** = 업데이트 충돌: 행 수준에서 충돌을 감지 합니다.<br /><br /> **2** = 열 업데이트 충돌: 열 수준에서 충돌이 검색 되었습니다.<br /><br /> **3** = 업데이트 삭제 wins 충돌: 삭제는 충돌을 적용 합니다.<br /><br /> **4** = 업데이트 Wins 삭제 충돌: 충돌을 손실 하는 삭제 된 rowguid가이 테이블에 기록 됩니다.<br /><br /> **5** = 업로드 삽입 실패: 게시자에서 구독자의 삽입을 적용할 수 없습니다.<br /><br /> **6** = 다운로드 삽입 실패: 게시자에서의 삽입을 구독자에서 적용할 수 없습니다.<br /><br /> **7** = 업로드를 삭제 하지 못했습니다. 구독자에서 삭제를 게시자로 업로드할 수 없습니다.<br /><br /> **8** = 다운로드 삭제 실패: 게시자에서 삭제를 구독자에 다운로드할 수 없습니다.<br /><br /> **9** = 업로드 업데이트 실패: 게시자에서 구독자의 업데이트를 적용할 수 없습니다.<br /><br /> **10** = 다운로드 업데이트 실패: 게시자의 업데이트를 구독자에 적용할 수 없습니다.<br /><br /> **12** = 논리적 레코드 업데이트 Wins 삭제: 충돌을 잃은 삭제 된 논리적 레코드가이 테이블에 기록 됩니다.<br /><br /> **13** = 논리적 레코드 충돌 삽입 업데이트: 논리 레코드에 삽입이 업데이트와 충돌 합니다.<br /><br /> **14** = 논리적 레코드 삭제 Wins 업데이트 충돌: 충돌을 잃은 업데이트 된 논리적 레코드가이 테이블에 기록 됩니다.|  
|**reason_code**|**int**|상황에 맞는 오류 코드입니다.|  
|**reason_text**|**varchar (720)**|상황에 맞는 오류 설명입니다.|  
|**pubid**|**uniqueidentifier**|게시 식별자입니다.|  
|**MSrepl_create_time**|**datetime**|충돌 정보가 추가된 시간입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpmergeconflictrows** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 배포 데이터베이스의 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 및 **replmonitor** 역할의 멤버만 **sp_helpmergeconflictrows**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 Transact-sql 프로그래밍 &#40;병합 게시에 대 한 충돌 정보 보기&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
