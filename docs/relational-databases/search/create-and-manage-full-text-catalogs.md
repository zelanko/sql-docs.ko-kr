---
description: 전체 텍스트 카탈로그 만들기 및 관리
title: 전체 텍스트 카탈로그 만들기 및 관리 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f95811113261f10701e0fcfc41c70e348891f6a9
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868092"
---
# <a name="create-and-manage-full-text-catalogs"></a>전체 텍스트 카탈로그 만들기 및 관리
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
전체 텍스트 카탈로그는 전체 텍스트 인덱스 그룹에 대한 논리적 컨테이너입니다. 전체 텍스트 인덱스를 만들려면 먼저 전체 텍스트 카탈로그를 만들어야 합니다.

전체 텍스트 카탈로그는 어떠한 파일 그룹에도 속하지 않는 가상 개체입니다.
  
##  <a name="create-a-full-text-catalog"></a><a name="creating"></a> 전체 텍스트 카탈로그 만들기  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Transact-SQL을 사용하여 전체 텍스트 카탈로그 만들기
[CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)를 사용합니다. 예를 들면 다음과 같습니다.

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Management Studio를 사용하여 전체 텍스트 카탈로그 만들기
1.  개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 전체 텍스트 카탈로그를 만들려는 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **새 전체 텍스트 카탈로그**를 선택합니다.  
  
4.  **새 전체 텍스트 카탈로그** 대화 상자에서 다시 만들려는 카탈로그에 대한 정보를 지정합니다. 자세한 내용은 [새 전체 텍스트 카탈로그&#40;일반 페이지&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)를 참조하세요.  
  
    > [!NOTE]  
    >  전체 텍스트 카탈로그 ID는 00005부터 시작하고 카탈로그를 새로 만들 때마다 1씩 증가합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

##  <a name="get-the-properties-of-a-full-text-catalog"></a><a name="props"></a> 전체 텍스트 카탈로그의 속성 가져오기  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 함수인 **FULLTEXTCATALOGPROPERTY**를 사용하여 전체 텍스트 카탈로그와 관련된 다양한 속성 값을 가져올 수 있습니다. 자세한 내용은 [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)를 참조하세요.

예를 들어 다음 쿼리를 실행하여 전체 텍스트 카탈로그 `Catalog1`의 인덱스 개수를 가져옵니다.

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
다음 표에서는 전체 텍스트 카탈로그에 관련된 속성을 나열합니다. 이 정보는 전체 텍스트 검색을 관리하고 이러한 검색에서 발생하는 문제를 해결하는 데 유용할 수 있습니다. 
  
|속성|Description|  
|--------------|-----------------|  
|**AccentSensitivity**|악센트 구분 설정입니다.|
|**ImportStatus**|전체 텍스트 카탈로그를 가져올지 여부를 나타냅니다.|  
|**IndexSize**|전체 텍스트 카탈로그의 크기(MB)입니다.| 
|**ItemCount**|현재 전체 텍스트 카탈로그에 있는 전체 텍스트 인덱싱된 항목 수입니다.|  
|**MergeStatus**|마스터 병합의 진행 여부를 나타냅니다.| 
|**PopulateCompletionAge**|마지막 전체 텍스트 인덱스 채우기가 완료된 시간과 01/01/1990 00:00:00 사이의 차이(초)입니다.| 
|**PopulateStatus**|채우기 상태입니다.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|전체 텍스트 카탈로그에서 고유 키 번호입니다.| 

##  <a name="rebuild-a-full-text-catalog"></a><a name="rebuildone"></a> 전체 텍스트 카탈로그 다시 작성  

Transact-SQL 문 [ALTER FULLTEXT CATALOG ... REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)를 실행하거나 SSMS(SQL Server Management Studio)에서 다음 작업을 수행합니다.

1.  SSMS의 개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 다시 작성할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 확장합니다.  
  
3.  다시 작성하려는 전체 텍스트 카탈로그의 이름을 마우스 오른쪽 단추로 클릭하고 **다시 작성**을 선택합니다.  
  
4.  **전체 텍스트 카탈로그를 삭제하고 다시 작성하시겠습니까?** 라는 질문에 **확인**을 클릭합니다.  
  
5.  **전체 텍스트 카탈로그 다시 작성** 대화 상자에서 **닫기**를 클릭합니다.  
   
##  <a name="rebuild-all-full-text-catalogs-for-a-database"></a><a name="rebuildall"></a> 데이터베이스의 전체 텍스트 카탈로그 모두 다시 작성  

1.  SSMS의 개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 다시 작성할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **모두 다시 작성**을 선택합니다.  
  
4.  **전체 텍스트 카탈로그를 모두 삭제하고 다시 작성하시겠습니까?** 라고 질문에 **확인**을 클릭합니다.  
  
5.  **전체 텍스트 카탈로그 모두 다시 작성** 대화 상자에서 **닫기**를 클릭합니다.  
  
  
  
##  <a name="remove-a-full-text-catalog-from-a-database"></a><a name="removing"></a> 데이터베이스에서 전체 텍스트 카탈로그 제거  

Transact-SQL 문 [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)를 실행하거나 SSMS(SQL Server Management Studio)에서 다음 작업을 수행합니다.

1.  SSMS의 개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 제거할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 확장합니다.  
  
3.  제거할 전체 텍스트 카탈로그를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 선택합니다.  
  
4.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  

## <a name="next-step"></a>다음 단계
[전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)