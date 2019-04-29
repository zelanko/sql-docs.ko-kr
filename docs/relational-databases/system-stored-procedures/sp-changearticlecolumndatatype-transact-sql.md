---
title: sp_changearticlecolumndatatype (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords:
- sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31895afacaee167bccf5144f1ab94e344a36be5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997110"
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Oracle 게시를 위한 아티클 열의 데이터 형식 매핑을 변경합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
> [!NOTE]  
>  지원되는 게시자 유형 간의 데이터 형식 매핑이 기본적으로 제공됩니다. 사용 하 여 **sp_changearticlecolumndatatype** 이러한 기본 설정을 재정의 하는 경우에 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changearticlecolumndatatype [ @publication= ] 'publication'  
    [ @article = ] 'article'   
    [ @column = ] 'column'  
    [ , [ @type = ] 'type' ]  
    [ , [ @length = ] length ]  
    [ , [ @precision = ] precision ]  
    [ , [ @scale = ] scale ]  
    [ , [ @publisher = ] 'publisher'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` Oracle 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @column = ] 'column'` 데이터 형식을 변경 하려는 열의 이름을 매핑하는 것입니다. *열* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @type = ] 'type'` 이름인 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 열의 데이터 형식입니다. *형식* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
`[ @length = ] length` 길이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 열의 데이터 형식입니다. *길이* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
`[ @precision = ] precision` 전체 자릿수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 열의 데이터 형식입니다. *전체 자릿수* 됩니다 **bigint**, 기본값은 NULL입니다.  
  
`[ @publisher = ] 'publisher'` 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **Sp_changearticlecolumndatatype** 지원 되는 게시자 유형 간의 기본 데이터 형식 매핑을 재정의 하는 데 사용 됩니다 (Oracle 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). 이러한 기본 데이터 형식 매핑을 보려면 실행 [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)합니다.  
  
 **sp_changearticlecolumndatatype** Oracle 게시자에 대해서만 지원 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시에 대해 이 저장 프로시저를 실행하면 오류가 발생합니다.  
  
 **sp_changearticlecolumndatatype** 변경 해야 하는 각 아티클 열 매핑에 대 한 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_changearticlecolumndatatype**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Oracle 게시자에 대한 데이터 형식 매핑](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
