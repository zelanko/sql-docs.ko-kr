---
title: sp_schemafilter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3018d23247a8f4d127d09878cb20c5f48f76c4ff
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206952"
---
# <a name="spschemafilter-transact-sql"></a>sp_schemafilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 적합한 Oracle 테이블을 나열할 때 제외되는 스키마에 대한 정보를 수정 및 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>인수  
 [**@publisher** =] **'***게시자***'**  
 비-의 이름인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@schema** =] **'***스키마***'**  
 스키마 이름입니다. *스키마* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [**@operation** =] **'***작업***'**  
 이 스키마에 수행할 동작입니다. *작업이* 됩니다 **nvarchar(4)**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**add**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에 추가합니다.|  
|**drop**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에서 삭제합니다.|  
|**도움말**|게시에 적합하지 않은 스키마 목록을 반환합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|게시에 적합하지 않은 스키마의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_schemafilter** 유형이 다른 게시자에 대해서만 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할의 배포자에서 실행할 수 있습니다 **sp_schemafilter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
