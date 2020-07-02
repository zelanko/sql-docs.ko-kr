---
title: sp_helpreplicationoption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationoption
- sp_helpreplicationoption_TSQL
helpviewer_keywords:
- sp_helpreplicationoption
ms.assetid: ef988dbc-dd0b-4132-80ab-81eebec1cffe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e04daaa5be757df60f07a8bd9205e1fd44f95502
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775743"
---
# <a name="sp_helpreplicationoption-transact-sql"></a>sp_helpreplicationoption(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  서버에 대해 사용할 수 있는 복제 옵션 유형을 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 모든 서버에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplicationoption [ [ @optname =] 'option_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @optname = ] 'option_name'`쿼리할 복제 옵션의 이름입니다. *option_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
|값|설명|  
|-----------|-----------------|  
|**트랜잭션과**|트랜잭션 복제를 사용하는 경우 반환되는 결과 집합입니다.|  
|**결합**|병합 복제를 사용하는 경우 반환되는 결과 집합입니다.|  
|NULL(기본값)|결합 집합이 반환되지 않습니다.|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|복제 옵션의 이름이며 다음 중 하나입니다.<br /><br /> **트랜잭션과**<br /><br /> **결합**|  
|**value**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**major_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**minor_version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**revision**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**install_failures**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpreplicationoption** 은 특정 서버에서 사용 하도록 설정 된 복제 옵션에 대 한 정보를 가져오는 데 사용 됩니다. 특정 데이터베이스에 대 한 정보를 가져오려면 **sp_helpreplicationdboption**를 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 실행 권한은 기본적으로 **public** 역할로 사용 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
