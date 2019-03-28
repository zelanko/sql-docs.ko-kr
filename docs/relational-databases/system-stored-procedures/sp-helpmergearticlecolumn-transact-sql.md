---
title: sp_helpmergearticlecolumn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticlecolumn
- sp_helpmergearticlecolumn_TSQL
helpviewer_keywords:
- sp_helpmergearticlecolumn
ms.assetid: 651c017b-9e9a-48f2-a0bd-6fc896eab334
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2221762934011c2268a40d0162bde7e62dbcf256
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528225"
---
# <a name="sphelpmergearticlecolumn-transact-sql"></a>p_helpmergearticlecolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 대한 지정된 테이블 또는 뷰 아티클의 열 목록을 반환합니다. 저장 프로시저에는 열이 없으므로 저장 프로시저를 아티클로 지정한 경우에는 오류를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergearticlecolumn [ @publication = ] 'publication' ]  
        , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *발행물* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 문서에서 정보를 검색 하는 뷰나 테이블의 이름이입니다. *아티클* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**sysname**|열을 식별합니다.|  
|**column_name**|**sysname**|테이블 또는 뷰의 열 이름입니다.|  
|**published**|**bit**|열 이름이 게시되는지 여부를 나타냅니다.<br /><br /> **1** 열이 게시를 지정 합니다.<br /><br /> **0** 게시 되지 않습니다 지정 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergearticlecolumn** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **replmonitor** 고정된 데이터베이스 역할 또는 배포 데이터베이스의 게시에 대 한 게시 액세스 목록에서 실행할 수 있습니다 **sp_helpmergearticlecolumn**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
