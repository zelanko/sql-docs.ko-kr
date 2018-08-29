---
title: sp_copysubscription (TRANSACT-SQL) | Microsoft Docs
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
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b96c458f38dc43a7d35f00d88b4572a9ae95d5d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030324"
---
# <a name="spcopysubscription-transact-sql"></a>sp_copysubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  연결 가능한 구독 기능은 더 이상 사용되지 않으며 후속 릴리스에서 제거될 예정입니다. 새로운 개발 작업에서는 이 기능을 사용하면 안 됩니다. 매개 변수가 있는 필터를 사용하여 분할된 병합 게시의 경우 구독을 대량으로 초기화하는 작업을 간단하게 만들어 주는 분할된 스냅숏의 새 기능을 사용하는 것이 좋습니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요. 분할되지 않은 게시의 경우 백업을 사용하여 구독을 초기화할 수 있습니다. 자세한 내용은 [스냅숏 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
 끌어오기 구독만 있고 밀어넣기 구독이 없는 구독 데이터베이스를 복사합니다. 하나의 파일로 구성된 데이터베이스만 복사할 수 있습니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>인수  
 [ **@filename =**] **'***file_name***'**  
 파일 이름을 포함한 전체 경로를 지정하는 문자열이며 데이터 파일(.mdf)의 사본을 저장할 위치에 해당합니다. *파일 이름* 됩니다 **nvarchar(260)**, 기본값은 없습니다.  
  
 [  **@temp_dir=**] **'***temp_dir***'**  
 임시 파일이 포함된 디렉터리의 이름입니다. *temp_dir* 됩니다 **nvarchar(260)**, 기본값은 NULL입니다. NULL 인 경우는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 데이터 디렉터리가 사용 됩니다. 디렉터리에는 모든 구독자 데이터베이스 파일을 저장할 수 있는 충분한 공간이 있어야 합니다.  
  
 [  **@overwrite_existing_file=**] **'***overwrite_existing_file***'**  
 에 지정 된 동일한 이름의 기존 파일을 덮어쓸 것인지 여부를 지정 하는 선택적인 부울 플래그 **@filename**합니다. *overwrite_existing_file*됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **1**, 지정 된 파일을 덮어씁니다 **@filename**존재 하는 경우. 하는 경우 **0**, 파일이 존재 하는 경우 파일을 덮어쓰지 않습니다 저장된 프로시저가 실패 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_copysubscription** 모든 유형의 복제에 구독자에서 스냅숏을 적용 하는 대신 파일 구독 데이터베이스를 복사 하는 데 사용 됩니다. 데이터베이스는 반드시 끌어오기 구독만을 지원하도록 구성되어야 합니다. 적절한 권한을 가진 사용자는 구독 데이터베이스를 복사할 수 있으며, 그런 다음 구독 파일(.msf)을 다른 구독자가 구독으로 사용할 수 있게끔 전자 메일로 보내거나 복사하거나 전송할 수 있습니다.  
  
 복사할 구독 데이터베이스의 크기는 2GB 미만이어야 합니다.  
  
 **sp_copysubscription** 클라이언트 구독을 사용 하 여 데이터베이스에 대 한 에서만 지원 되며 데이터베이스에 서버 구독이 있는 경우에 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_copysubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [대체 스냅숏 폴더 위치](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
