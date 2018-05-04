---
title: sp_syscollector_upload_collection_set (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0bb4ba04b346e6931a55d26172f0d34b27166950
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합이 활성화되어 있으면 컬렉션 집합 데이터의 업로드를 시작합니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 데이터 컬렉션 및 업로드가 캐시된 모드로 구성된 컬렉션 집합에만 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@collection_set_id =** ] *collection_set_id*  
 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 경우 값이 있어야 하 고 *이름* 은 NULL입니다.  
  
 [ **@name =** ] **'***name***'**  
 컬렉션 집합의 이름입니다. *이름* 은 **sysname** 경우 값이 있어야 하 고 *collection_set_id* 은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 어느 *collection_set_id* 또는 *이름* 해야 값 수 있으며 둘 다 NULL 일 수 없습니다.  
  
 이 프로시저는 실행 중인 컬렉션 집합에 대한 요청 시 업로드를 시작하는 데 사용될 수 있습니다. 또한 데이터 컬렉션 및 업로드가 캐시된 모드로 구성된 컬렉션 집합에만 사용할 수 있습니다. 이를 통해 사용자는 예약된 업로드를 기다리지 않고 분석에 사용할 데이터를 가져올 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **dc_operator** (EXECUTE 권한 있음)와이 프로시저를 실행 하는 고정된 데이터베이스 역할.  
  
## <a name="example"></a>예제  
 `Simple Collection Set`이라는 컬렉션 집합의 요청 시 업로드를 수행합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
