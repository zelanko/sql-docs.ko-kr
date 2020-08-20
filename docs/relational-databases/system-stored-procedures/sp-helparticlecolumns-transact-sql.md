---
description: sp_helparticlecolumns(Transact-SQL)
title: sp_helparticlecolumns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: eed4538f2ffe43faf6ef83685ba3b5984198663c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474183"
---
# <a name="sp_helparticlecolumns-transact-sql"></a>sp_helparticlecolumns(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  기본 테이블의 모든 열을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. Oracle 게시자의 경우 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 아티클이 포함 된 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'` 열이 반환 된 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자가 요청한 아티클을 게시할 때 *게시자* 를 지정 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (게시 되지 않은 열) 또는 **1** (게시 된 열)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**열 id**|**int**|열의 식별자입니다.|  
|**column**|**sysname**|열의 이름입니다.|  
|**게시할지**|**bit**|열이 게시되는지 여부입니다.<br /><br /> **0** = 아니요<br /><br /> **1** = 예|  
|**게시자 유형**|**sysname**|게시자에 있는 열의 데이터 형식입니다.|  
|**구독자 유형**|**sysname**|구독자에 있는 열의 데이터 형식입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_helparticlecolumns** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_helparticlecolumns** 는 수직 분할을 확인 하는 데 유용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버, **db_owner** 고정 데이터베이스 역할 또는 현재 게시에 대 한 게시 액세스 목록의 멤버만 **sp_helparticlecolumns**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [열 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Transact-sql&#41;sp_articlecolumn &#40;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [Transact-sql&#41;sp_changearticle &#40;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [Transact-sql&#41;sp_droparticle &#40;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Transact-sql&#41;sp_droppublication &#40;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
