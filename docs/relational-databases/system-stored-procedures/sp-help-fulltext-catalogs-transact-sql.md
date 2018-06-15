---
title: sp_help_fulltext_catalogs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_TSQL
- sp_help_fulltext_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs
ms.assetid: 1b94f280-e095-423f-88bc-988c9349d44c
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5490c7e8d8658ddc8048e63d082d48ea92249c08
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33243396"
---
# <a name="sphelpfulltextcatalogs-transact-sql"></a>sp_help_fulltext_catalogs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 전체 텍스트 카탈로그에 대해 전체 텍스트 인덱싱된 테이블의 ID, 이름, 루트 디렉터리, 상태 및 번호를 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 카탈로그 뷰를 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_catalogs [ @fulltext_catalog_name = ] 'fulltext_catalog_name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@fulltext_catalog_name=**] **'***fulltext_catalog_name***'**  
 전체 텍스트 카탈로그의 이름입니다. *fulltext_catalog_name* 은 **sysname**합니다. 이 매개 변수를 생략하거나 그 값이 NULL인 경우에는 현재 데이터베이스와 연관된 모든 전체 텍스트 카탈로그에 대한 정보가 반환됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 **ftcatid**에 의해 정렬되는 결과 집합을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|전체 텍스트 카탈로그의 ID입니다.|  
|**이름**|**sysname**|전체 텍스트 카탈로그의 이름입니다.|  
|**PATH**|**nvarchar(260)**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 이 절은 아무 효과가 없습니다.|  
|**상태**|**int**|카탈로그의 전체 텍스트 인덱스 채우기 상태입니다.<br /><br /> 0 = 유휴 상태<br /><br /> 1 = 전체 채우기 진행 중<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 정체됨<br /><br /> 4 = 복구 중<br /><br /> 5 = 종료<br /><br /> 6 = 증분 채우기 진행 중<br /><br /> 7 = 인덱스 작성 중<br /><br /> 8 = 디스크가 꽉 참 일시 중지됨<br /><br /> 9 = 변경 내용 추적 중<br /><br /> NULL = 전체 텍스트 카탈로그에 대한 VIEW 권한이 사용자에게 없거나 데이터베이스에서 전체 텍스트를 사용하지 않거나 전체 텍스트 구성 요소가 설치되어 있지 않습니다.|  
|**NUMBER_FULLTEXT_TABLES**|**int**|카탈로그와 연관된 전체 텍스트 인덱싱된 테이블의 번호입니다.|  
  
## <a name="permissions"></a>Permissions  
 실행 권한은 기본적으로 **public** 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Cat_Desc` 전체 텍스트 카탈로그에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_catalogs 'Cat_Desc' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [FULLTEXTCATALOGPROPERTY & #40; Transact SQL & #41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
