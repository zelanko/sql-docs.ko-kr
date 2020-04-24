---
title: DBCC FLUSHAUTHCACHE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 15b8116b0677ebfccece9c13a49480d6702c6c54
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631350"
---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE(Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 현재 사용자 데이터베이스에 대한 로그인 및 방화벽 규칙 정보가 포함된 데이터베이스 인증 캐시를 비웁니다. master 데이터베이스는 로그인 및 방화벽 규칙 정보에 대한 물리적 스토리지를 포함하기 때문에 이 명령문은 논리 master 데이터베이스에 적용되지 않습니다. 명령문을 실행하는 사용자 또는 현재 연결된 다른 사용자는 연결된 상태로 유지됩니다. (DBCC FLUSHAUTHCACHE는 현재 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]에 지원되지 않습니다.)
 
![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>인수  
없음
  
## <a name="remarks"></a>설명  
인증 캐시는 master에 저장되는 로그인 및 서버 방화벽 규칙의 복사본을 만들고 사용자 데이터베이스의 메모리에 배치합니다.  포함된 데이터베이스 사용자에 대한 정보는 이미 사용자 데이터베이스에 저장되어 있으므로 포함된 데이터베이스 사용자는 인증 캐시의 일부가 아닙니다.
[!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 활성 연결을 지속하기 위해서는 적어도 10시간 마다 다시 인증해야 합니다([!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 수행됨). [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 원래 제출된 암호를 사용하여 다시 인증을 시도하며, 사용자 입력은 필요하지 않습니다. 성능상의 이유로 암호를 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 재설정한 경우 연결 풀링으로 인해 연결이 재설정되더라도 연결은 다시 인증되지 않습니다. 이 동작은 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동작과 다릅니다. 초기에 연결을 인증한 후 암호를 변경하면 연결을 종료하고 새 암호를 사용하여 새 연결을 설정해야 합니다. KILL DATABASE CONNECTION 권한이 있는 사용자는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 연결을 [KILL&#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md) 명령을 사용하여 명시적으로 종료할 수 있습니다.
  
## <a name="permissions"></a>사용 권한  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 관리자 계정이 필요합니다.
  
## <a name="example"></a>예제  
다음 명령문은 현재 데이터베이스에 대한 인증 캐시를 지웁니다.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
