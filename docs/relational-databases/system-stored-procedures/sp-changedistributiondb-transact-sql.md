---
title: sp_changedistributiondb (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributiondb_TSQL
- sp_changedistributiondb
helpviewer_keywords:
- sp_changedistributiondb
ms.assetid: 66f73185-ea9e-43f9-86ed-9dd933cee2f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b9bd4367a4af33195ffdb3e233980f46205ca39a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760208"
---
# <a name="sp_changedistributiondb-transact-sql"></a>sp_changedistributiondb(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  배포 데이터베이스의 속성을 변경합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changedistributiondb [ @database= ] 'database'   
    [ , [ @property= ] 'property' ]   
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @database = ] 'database'`배포 데이터베이스의 이름입니다. *데이터베이스* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`지정 된 데이터베이스에 대해 변경할 속성입니다. *속성* 은 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**history_retention**|기록 테이블의 보존 기간입니다.|  
|**max_distretention**|최대 배포 보존 기간입니다.|  
|**min_distretention**|최소 배포 보존 기간입니다.|  
|NULL(기본값)|사용 가능한 모든 *속성* 값이 출력 됩니다.|  
  
`[ @value = ] 'value'`지정 된 속성의 새 값입니다. *value* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changedistributiondb** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/sp-changedistributiondb-_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changedistributiondb**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Transact-sql&#41;sp_adddistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistributiondb &#40;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
