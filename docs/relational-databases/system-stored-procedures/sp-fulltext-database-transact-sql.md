---
title: sp_fulltext_database (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ee0918a0b190b7b058f38eac4152dfb952f214bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771065"
---
# <a name="sp_fulltext_database-transact-sql"></a>sp_fulltext_database(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않으며 이전 버전과의 호환성을 위해서만 지원됩니다. **sp_fulltext_database** 는 지정 된 데이터베이스에 대해 전체 텍스트 엔진을 사용 하지 않도록 설정 하지 않습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용자가 만든 모든 데이터베이스가 전체 텍스트 인덱스에 대해 항상 설정됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]을 대신 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>인수  
`[ @action = ] 'action'`수행할 동작입니다. **action** 은 **varchar (20)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**enable**|이전 버전과의 호환성을 위해서만 지원됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않습니다.|  
|**disable**|이전 버전과의 호환성을 위해서만 지원됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 전체 텍스트 인덱싱 기능을 해제할 수 없습니다. 전체 텍스트 인덱싱을 사용 하지 않도록 설정 해도 **sysfulltextcatalogs** 에서 행이 제거 되지 않으며 전체 텍스트를 사용 하도록 설정 된 테이블이 더 이상 전체 텍스트 인덱싱을 위해 표시 되지 않습니다. 모든 전체 텍스트 메타데이터 정의는 시스템 테이블 내에서 여전히 유효합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 및 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_fulltext_database**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DATABASEPROPERTYEX &#40;Transact-sql&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY 함수의 &#40;Transact-sql&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
