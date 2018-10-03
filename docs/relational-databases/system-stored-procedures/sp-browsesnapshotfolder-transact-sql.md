---
title: sp_browsesnapshotfolder (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6fffd6e0131c00194ae65fb425b202add18cd23f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785231"
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 대해 가장 최근에 생성된 스냅숏의 전체 경로를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 아티클을 포함하는 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber=**] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|스냅숏 디렉터리의 전체 경로입니다.|  
  
## <a name="remarks"></a>Remarks  
 **sp_browsesnapshotfolder** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 경우는 *구독자* 하 고 *subscriber_db* 필드는 NULL을 왼쪽, 저장된 프로시저 게시에서 찾을 수 있는 가장 최근 스냅숏의 스냅숏 폴더를 반환 합니다. 경우는 *구독자* 및 *subscriber_db* 필드가 지정 된, 저장된 프로시저는 지정된 된 구독에 대 한 스냅숏 폴더를 반환 합니다. 스냅숏이 게시에 생성되지 않은 경우 빈 결과 집합이 반환됩니다.  
  
 게시가 스냅숏 파일을 생성할 수 있도록 게시자 작업 디렉터리 및 게시자 스냅숏 폴더에 설정되어 있는 경우 결과 집합은 두 행을 포함합니다. 첫 번째 행은 게시 스냅숏 폴더를 포함하며 두 번째 행은 게시자 작업 디렉터리를 포함합니다. **sp_browsesnapshotfolder** 스냅숏 파일이 생성 되는 디렉터리를 결정 하는 데 유용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_browsesnapshotfolder**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
