---
title: sp_browsesnapshotfolder (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: dcc7c4031253f83df49b45feae17449814af3fc3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768976"
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시에 대해 가장 최근에 생성된 스냅샷의 전체 경로를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`아티클이 포함 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|스냅샷 디렉터리의 전체 경로입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_browsesnapshotfolder** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 *구독자* 및 *subscriber_db* 필드가 NULL로 남아 있는 경우 저장 프로시저는 게시에 대해 찾을 수 있는 가장 최근 스냅숏의 스냅숏 폴더를 반환 합니다. *구독자* 및 *subscriber_db* 필드가 지정 된 경우 저장 프로시저는 지정 된 구독에 대 한 스냅숏 폴더를 반환 합니다. 스냅샷이 게시에 생성되지 않은 경우 빈 결과 집합이 반환됩니다.  
  
 게시가 스냅샷 파일을 생성할 수 있도록 게시자 작업 디렉터리 및 게시자 스냅샷 폴더에 설정되어 있는 경우 결과 집합은 두 행을 포함합니다. 첫 번째 행은 게시 스냅샷 폴더를 포함하며 두 번째 행은 게시자 작업 디렉터리를 포함합니다. **sp_browsesnapshotfolder** 는 스냅숏 파일이 생성 되는 디렉터리를 결정 하는 데 유용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_browsesnapshotfolder**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
