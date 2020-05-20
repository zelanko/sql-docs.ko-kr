---
title: sp_help_fulltext_catalogs_cursor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 741b1311aee361e83c0d4ba2465ec9b80e1c217f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827717"
---
# <a name="sp_help_fulltext_catalogs_cursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  커서를 사용하여 지정된 전체 텍스트 카탈로그에 대해 전체 텍스트 인덱싱된 테이블의 ID, 이름, 루트 디렉터리, 상태 및 번호를 반환할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) 카탈로그 뷰를 사용 하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>인수  
`[ @cursor_return = ] @cursor_variable OUTPUT`**Cursor**유형의 출력 변수입니다. 커서는 읽기 전용의 스크롤할 수 있는 동적 커서입니다.  
  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`전체 텍스트 카탈로그의 이름입니다. *fulltext_catalog_name* 는 **sysname**입니다. 매개 변수를 생략하거나 그 값이 NULL인 경우에는 현재 데이터베이스와 연결된 모든 전체 텍스트 카탈로그에 대한 정보가 반환됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|전체 텍스트 카탈로그의 ID입니다.|  
|**이름**|**sysname**|전체 텍스트 카탈로그의 이름입니다.|  
|**PATH**|**nvarchar(260)**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 이 절은 아무 효과가 없습니다.|  
|**상태**|**int**|카탈로그의 전체 텍스트 인덱스 채우기 상태입니다.<br /><br /> 0 = 유휴 상태<br /><br /> 1 = 전체 채우기 진행 중<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 정체됨<br /><br /> 4 = 복구 중<br /><br /> 5 = 종료<br /><br /> 6 = 증분 채우기 진행 중<br /><br /> 7 = 인덱스 작성 중<br /><br /> 8 = 디스크가 꽉 참. 일시 중지됨<br /><br /> 9 = 변경 내용 추적 중|  
|**NUMBER_FULLTEXT_TABLES**|**int**|카탈로그와 연결된 전체 텍스트 인덱싱된 테이블의 번호입니다.|  
  
## <a name="permissions"></a>권한  
 실행 권한은 기본적으로 **public** 역할로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Cat_Desc` 전체 텍스트 카탈로그에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>참고 항목  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [Transact-sql&#41;sp_fulltext_catalog &#40;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [Transact-sql&#41;sp_help_fulltext_catalogs &#40;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
