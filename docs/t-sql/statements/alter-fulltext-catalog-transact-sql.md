---
title: ALTER FULLTEXT CATALOG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_FULLEXT_CATALOG_TSQL
- ALTER FULLEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- modifying full-text catalogs
- full-text catalogs [SQL Server], rebuilding
- accent sensitivity
- ALTER FULLTEXT CATALOG statement
- full-text catalogs [SQL Server], modifying
- full-text catalogs [SQL Server], reorganizing
ms.assetid: 31a47aaf-6c7f-48a4-a86a-d57aec66c9cb
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b79d00b02f06395a083ee93a2916a7d3aa5f0233
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712011"
---
# <a name="alter-fulltext-catalog-transact-sql"></a>ALTER FULLTEXT CATALOG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 카탈로그의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER FULLTEXT CATALOG catalog_name   
{ REBUILD [ WITH ACCENT_SENSITIVITY = { ON | OFF } ]  
| REORGANIZE  
| AS DEFAULT   
}  
```  
  
## <a name="arguments"></a>인수  
 *catalog_name*  
 수정할 카탈로그의 이름을 지정합니다. 지정된 이름의 카탈로그가 없을 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환하고 ALTER 작업을 수행하지 않습니다.  
  
 REBUILD  
 전체 카탈로그를 다시 작성하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 알려 줍니다. 카탈로그를 다시 작성하면 기존 카탈로그가 삭제되고 새 카탈로그가 해당 위치에 만들어집니다. 전체 텍스트 인덱싱 참조가 있는 모든 테이블은 새 카탈로그와 연결됩니다. 카탈로그를 다시 작성하면 데이터베이스 시스템 테이블의 전체 텍스트 메타데이터가 설정됩니다.  
  
 WITH ACCENT_SENSITIVITY = {ON|OFF}  
 변경할 카탈로그의 전체 텍스트 인덱싱 및 쿼리에 대한 악센트 구분 여부를 지정합니다.  
  
 전체 텍스트 카탈로그의 현재 악센트 구분 속성 설정을 확인하려면 *catalog_name*에 대해 **accentsensitivity** 속성 값을 가진 FULLTEXTCATALOGPROPERTY 함수를 사용합니다. 함수가 '1'을 반환하면 전체 텍스트 카탈로그가 악센트를 구분하고, '0'을 반환하면 악센트를 구분하지 않습니다.  
  
 카탈로그와 데이터베이스의 악센트 구분 기본값은 동일합니다.  
  
 REORGANIZE  
 인덱싱 과정에서 만들어진 작은 인덱스를 하나의 큰 인덱스로 병합하는 *master merge*을 수행하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 알려줍니다. 전체 텍스트 인덱스 조각을 병합하면 성능이 향상되고 디스크 및 메모리 리소스를 확보할 수 있습니다. 전체 텍스트 카탈로그를 자주 변경하는 경우에는 이 명령을 주기적으로 사용하여 전체 텍스트 카탈로그를 다시 구성할 수 있습니다.  
  
 REORGANIZE는 내부 인덱스 및 카탈로그 구조도 최적화합니다.  
  
 인덱싱된 데이터 양에 따라 마스터 병합을 완료하는 데 많은 시간이 걸릴 수 있습니다. 많은 양의 데이터를 마스터 병합하면 장기 실행 트랜잭션이 생성될 수 있으며 이로 인해 검사점이 사용되는 동안 트랜잭션 로그의 잘림이 지연될 수 있습니다. 이 경우 전체 복구 모델에서 트랜잭션 로그의 크기가 대폭 증가할 수 있습니다. 전체 복구 모델이 사용되는 데이터베이스에서 큰 전체 텍스트 인덱스를 다시 구성하기 전에 장기 실행 트랜잭션에 대비하여 트랜잭션 로그에 충분한 공간을 확보하는 것이 가장 좋은 방법입니다. 자세한 내용은 [트랜잭션 로그 파일의 크기 관리](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)를 참조하세요.  
  
 AS DEFAULT  
 이 카탈로그를 기본 카탈로그로 지정합니다. 카탈로그를 지정하지 않고 전체 텍스트 인덱스를 만들면 기본 카탈로그가 사용됩니다. 기본 전체 텍스트 카탈로그가 이미 있는 경우 이 카탈로그를 AS DEFAULT로 설정하면 기존 기본값보다 우선 적용됩니다.  
  
## <a name="permissions"></a>Permissions  
 사용자는 전체 텍스트 카탈로그에 대해 ALTER 권한이 있거나 **db_owner**, **db_ddladmin** 고정 데이터베이스 역할 또는 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  ALTER FULLTEXT CATALOG AS DEFAULT를 사용하려면 사용자에게 전체 텍스트 카탈로그에 대한 ALTER 권한과 데이터베이스에 대한 CREATE FULLTEXT CATALOG 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 악센트가 구분되는 기본 전체 텍스트 카탈로그 `accentsensitivity`의 `ftCatalog` 속성을 변경합니다.  
  
```  
--Change to accent insensitive  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog   
REBUILD WITH ACCENT_SENSITIVITY=OFF;  
GO  
-- Check Accentsensitivity  
SELECT FULLTEXTCATALOGPROPERTY('ftCatalog', 'accentsensitivity');  
GO  
--Returned 0, which means the catalog is not accent sensitive.  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
