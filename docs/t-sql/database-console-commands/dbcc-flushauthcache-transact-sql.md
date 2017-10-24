---
title: DBCC FLUSHAUTHCACHE (Transact SQL) | Microsoft Docs
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ba6a519ebcdbbc70bf19ec491539a3b07fb6c85
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

로그인 및 현재 사용자 데이터베이스에 대 한 방화벽 규칙에 대 한 정보가 포함 된 데이터베이스 인증 캐시를 비웁니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다. 이 문은 master 데이터베이스 로그인 및 방화벽 규칙에 대 한 정보에 대 한 물리적 저장소를 포함 하기 때문에 논리적 master 데이터베이스에 적용 되지 않습니다. 문을 실행 하는 사용자 및 현재 연결 된 다른 사용자가 연결 되어 있습니다. (DBCC FLUSHAUTHCACHE에 대 한 현재 지원 되지 않는 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)
 
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>인수  
없음
  
## <a name="remarks"></a>주의  
인증 캐시 로그인 및 master에 저장 되 고 사용자 데이터베이스에서 메모리에 배치 하는 서버 방화벽 규칙의 복사본을 만듭니다.  포함 된 데이터베이스 사용자에 대 한 정보는 사용자 데이터베이스에 이미 저장 되므로, 포함 된 데이터베이스 사용자가 인증 캐시의 일부 없습니다.
대 한 연속 활성 연결이 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 재인증 필요 (수행한는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]) 10 시간 이상 마다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 시도 재인증 제출 된 원래 암호와 사용자를 사용 하 여 입력이 필요 합니다. 성능상의 이유로 암호를 다시 설정 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 연결 풀링으로 인해 연결이 재설정 되더라도 연결이 다시 인증 되지 것입니다. 이 온-프레미스의 동작은 다릅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 연결이 초기 인증 후 암호가 변경 된 경우 연결을 종료 해야 하 고 새 암호를 사용 하 여 새 연결 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자에 대 한 연결을 명시적으로 종료할 수 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 를 사용 하 여는 [kill&#40; Transact SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md) 명령입니다.
  
## <a name="permissions"></a>Permissions  
필요는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정.
  
## <a name="example"></a>예제  
다음 문은 현재 데이터베이스에 대 한 인증 캐시를 지웁니다.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

