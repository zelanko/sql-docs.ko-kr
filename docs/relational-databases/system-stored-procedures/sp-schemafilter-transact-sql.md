---
title: sp_schemafilter (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 231796d1678a19106eb89f3039cd755e8385082c
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633012"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter(Transact-SQL)
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
`[ @publisher = ] 'publisher'`은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @schema = ] 'schema'`은 스키마의 이름입니다. *schema* 는 **sysname**이며 기본값은 NULL입니다.  
  
이 스키마에서 수행할 작업은 `[ @operation = ] 'operation'`입니다. *연산은* **nvarchar (4)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**add**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에 추가합니다.|  
|**그림자**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에서 삭제합니다.|  
|**help**|게시에 적합하지 않은 스키마 목록을 반환합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|게시에 적합하지 않은 스키마의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_schemafilter** 은 유형이 다른 게시자에만 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_schemafilter**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
