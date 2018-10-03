---
title: sp_fulltext_database (TRANSACT-SQL) | Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 11f2886a261ebe760616dade945e652b620918a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841923"
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않으며 이전 버전과의 호환성을 위해서만 지원됩니다. **sp_fulltext_database** 지정된 된 데이터베이스에 대 한 전체 텍스트 엔진을 비활성화 하지 않습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용자가 만든 모든 데이터베이스가 전체 텍스트 인덱스에 대해 항상 설정됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]을 대신 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>인수  
 [  **@action=**] **'***동작***'**  
 수행할 동작입니다. **동작** 됩니다 **varchar(20)"**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**enable**|이전 버전과의 호환성을 위해서만 지원됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않습니다.|  
|**disable**|이전 버전과의 호환성을 위해서만 지원됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그에 영향을 미치지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 전체 텍스트 인덱싱 기능을 해제할 수 없습니다. 전체 텍스트 인덱싱을 사용 하지 않도록 설정에서 행을 제거 하지 않습니다 **sysfulltextcatalogs** 하며 전체 텍스트 인덱싱에 대 한 전체 텍스트 사용된 테이블을 더 이상 표시할는 나타내지 않습니다. 모든 전체 텍스트 메타데이터 정의는 시스템 테이블 내에서 여전히 유효합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_fulltext_database**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DATABASEPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
