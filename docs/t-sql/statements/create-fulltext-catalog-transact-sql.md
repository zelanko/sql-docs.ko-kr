---
title: CREATE FULLTEXT CATALOG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CATALOG_TSQL
- CREATE_FULLTEXT_TSQL
- FULLTEXT_TSQL
- FULLTEXT CATALOG
- CREATE FULLTEXT CATALOG
- CREATE_FULLTEXT_CATALOG_TSQL
- CATALOG
- FULLTEXT_CATALOG_TSQL
- CREATE FULLTEXT
- FULLTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- CREATE FULLTEXT CATALOG statement
ms.assetid: d7a8bd93-e2d7-4a40-82ef-39069e65523b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e8fa047a65663f918bfcce4a92692f1c443f77a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73064658"
---
# <a name="create-fulltext-catalog-transact-sql"></a>CREATE FULLTEXT CATALOG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스에 대한 전체 텍스트 카탈로그를 만듭니다. 전체 텍스트 카탈로그 하나에 전체 텍스트 인덱스는 여러 개 있을 수 있지만 각 전체 텍스트 인덱스는 전체 텍스트 카탈로그 하나에만 속할 수 있습니다. 각 데이터베이스에는 전체 텍스트 카탈로그가 없거나 하나 이상 포함될 수 있습니다.  
  
 **master**, **model** 또는 **tempdb** 데이터베이스에서는 전체 텍스트 카탈로그를 만들 수 없습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 전체 텍스트 카탈로그가 가상 개체이며 어떠한 파일 그룹에도 속하지 않습니다. 전체 텍스트 카탈로그는 전체 텍스트 인덱스 그룹을 나타내는 논리적 개념입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE FULLTEXT CATALOG catalog_name  
     [ON FILEGROUP filegroup ]  
     [IN PATH 'rootpath']  
     [WITH <catalog_option>]  
     [AS DEFAULT]  
     [AUTHORIZATION owner_name ]  
  
<catalog_option>::=  
     ACCENT_SENSITIVITY = {ON|OFF}  
  
```  
  
## <a name="arguments"></a>인수  
 *catalog_name*  
 새 카탈로그의 이름입니다. 카탈로그 이름은 현재 데이터베이스에 있는 모든 카탈로그 이름 중에서 고유해야 합니다. 또한 전체 텍스트 카탈로그(ON FILEGROUP 참조)에 해당하는 파일의 이름은 데이터베이스에 있는 모든 파일 이름과 중복되지 않는 고유 이름이어야 합니다. 카탈로그 이름이 데이터베이스의 다른 카탈로그에 이미 사용되었으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다.  
  
 카탈로그 이름은 120자를 초과할 수 없습니다.  
  
 ON FILEGROUP *filegroup*  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 이 절은 아무 효과가 없습니다.  
  
 IN PATH **'** _rootpath_ **'**  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 이 절은 아무 효과가 없습니다.  
  
 ACCENT_SENSITIVITY = {ON|OFF}  
 전체 텍스트 인덱싱에 대해 카탈로그의 악센트 구분 여부를 지정합니다. 이 속성이 변경되면 인덱스를 다시 만들어야 합니다. 기본값은 데이터베이스 데이터 정렬에 지정된 악센트 구분을 사용하는 것입니다. 데이터베이스 데이터 정렬을 표시하려면 **sys.databases** 카탈로그 뷰를 사용합니다.  
  
 전체 텍스트 카탈로그의 현재 악센트 구분 속성 설정을 확인하려면 *catalog_name*에 대해 **accentsensitivity** 속성 값을 가진 FULLTEXTCATALOGPROPERTY 함수를 사용합니다. 반환된 값이 '1'인 경우 전체 텍스트 카탈로그는 악센트를 구분하며 반환된 값이 '0'인 경우 카탈로그는 악센트를 구분하지 않습니다.  
  
 AS DEFAULT  
 카탈로그를 기본 카탈로그로 지정합니다. 전체 텍스트 카탈로그를 명시적으로 지정하지 않고 전체 텍스트 인덱스를 만든 경우 기본 카탈로그가 사용됩니다. 이미 AS DEFAULT로 표시된 기존의 전체 텍스트 카탈로그가 있을 경우 새 카탈로그를 AS DEFAULT로 설정하면 이 카탈로그가 기본 전체 텍스트 카탈로그가 됩니다.  
  
 AUTHORIZATION *owner_name*  
 전체 텍스트 카탈로그의 소유자를 데이터베이스 사용자 또는 역할의 이름으로 설정합니다. *owner_name*이 역할인 경우 이 역할은 현재 사용자가 속해 있는 역할의 이름이어야 합니다. 그렇지 않으면 문을 실행하는 사용자가 데이터베이스 소유자 또는 시스템 관리자여야 합니다.  
  
 *owner_name*이 사용자 이름인 경우 사용자 이름은 다음 중 하나여야 합니다.  
  
-   문을 실행하는 사용자의 이름이어야 합니다.  
  
-   명령을 실행하는 사용자가 가장 권한을 가지고 있는 사용자의 이름이어야 합니다.  
  
-   그렇지 않으면 명령을 실행하는 사용자가 데이터베이스 소유자 또는 시스템 관리자여야 합니다.  
  
 또한 *owner_name*에는 지정한 전체 텍스트 카탈로그에 대한 TAKE OWNERSHIP 권한이 있어야 합니다.  
  
## <a name="remarks"></a>설명  
 전체 텍스트 카탈로그 ID는 00005부터 시작하고 카탈로그를 새로 만들 때마다 1씩 증가합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 데이터베이스에 대한 CREATE FULLTEXT CATALOG 권한이 있거나 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 전체 텍스트 카탈로그와 전체 텍스트 인덱스를 만듭니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume) KEY INDEX PK_JobCandidate_JobCandidateID;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 
  
  
