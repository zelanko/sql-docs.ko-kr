---
title: sp_getmergedeletetype (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00a7499fb3050a5ab13fa3e9b454b4335200f55a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731662"
---
# <a name="sp_getmergedeletetype-transact-sql"></a>sp_getmergedeletetype(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  병합 삭제 유형을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자 또는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>인수  
`[ @source_object = ] 'source_object'`원본 개체의 이름입니다. *source_object* 은 **nvarchar (386)** 이며 기본값은 없습니다.  
  
`[ @rowguid = ] 'rowguid'`삭제 유형에 대 한 행 식별자입니다. *rowguid* 는 **uniqueidentifier**이며 기본값은 없습니다.  
  
`[ @delete_type = ] delete_type OUTPUT`삭제 유형을 나타내는 코드입니다. *delete_type* 는 **int**이며 기본값은 없습니다. 또한 *delete_type* 는 출력 매개 변수 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|사용자 삭제|  
|**5**|부분 삭제|  
|**6**|시스템 삭제|  
  
## <a name="remarks"></a>설명  
 **sp_getmergedeletetype** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_getmergedeletetype**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
