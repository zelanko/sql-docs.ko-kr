---
title: DBCC PROCCACHE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 97e617e7867c90bf1e66c5e64e37b9039087d463
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

프로시저 캐시에 대한 정보를 테이블 형식으로 표시합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 의 모든 멘션을  
 옵션을 지정할 수 있습니다.  
  
 NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>주의  
프로시저 캐시는 일괄 처리 실행 속도를 높이기 위해 컴파일된 계획 및 실행 계획을 캐시하는 데 사용합니다. 프로시저 캐시 내의 항목은 일괄 처리 수준으로 제어됩니다. 프로시저 캐시는 다음과 같은 항목을 포함합니다.
-   컴파일된 계획  
-   실행 계획  
-   Algebrizer 트리  
-   확장 프로시저  
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 결과 집합의 열에 대해 설명합니다.
  
|열 이름|Description|  
|-----------------|-----------------|  
|**num의 proc 마법 효과**|프로시저 캐시의 모든 항목에 사용되는 총 페이지 수입니다.|  
|**num proc 마법 효과 사용**|현재 사용 중인 모든 항목에 사용되는 총 페이지 수입니다.|  
|**활성 num proc 마법 효과**|이전 버전과의 호환성을 위해서만 지원됩니다. 현재 사용 중인 모든 항목에 사용되는 총 페이지 수입니다.|  
|**프로시저 캐시 크기**|프로시저 캐시의 총 항목 수입니다.|  
|**사용 되는 프로시저 캐시**|현재 사용 중인 총 항목 수입니다.|  
|**활성 proc 캐시**|이전 버전과의 호환성을 위해서만 지원됩니다. 현재 사용 중인 총 항목 수입니다.|  
  
## <a name="permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

