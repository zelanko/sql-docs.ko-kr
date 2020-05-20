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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3e9873045fd7e4fb11ad19bbbce953a086512df9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824374"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 적합한 Oracle 테이블을 나열할 때 제외되는 스키마에 대한 정보를 수정 및 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`이외 게시자의 이름입니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @schema = ] 'schema'`스키마의 이름입니다. *schema* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @operation = ] 'operation'`이 스키마에 대해 수행할 작업입니다. *연산은* **nvarchar (4)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**추가**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에 추가합니다.|  
|**그림자**|지정된 스키마를 게시에 적합하지 않은 스키마 목록에서 삭제합니다.|  
|**help**|게시에 적합하지 않은 스키마 목록을 반환합니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|게시에 적합하지 않은 스키마의 이름입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_schemafilter** 은 유형이 다른 게시자에만 사용 해야 합니다.  
  
## <a name="permissions"></a>권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_schemafilter**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
