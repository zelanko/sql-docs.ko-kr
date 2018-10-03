---
title: sp_fulltext_catalog (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ab482a70374c9a11256719811db02dd4eb1586e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663241"
---
# <a name="spfulltextcatalog-transact-sql"></a>sp_fulltext_catalog(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 카탈로그를 만들고 삭제하며, 해당 카탈로그에 대한 인덱싱 동작을 시작하고 중지합니다. 각 데이터베이스에 여러 개의 전체 텍스트 카탈로그를 만들 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)하십시오 [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md), 및 [DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@ftcat=**] **'***fulltext_catalog_name***'**  
 전체 텍스트 카탈로그의 이름입니다. 카탈로그 이름은 각 데이터베이스에 대해 고유해야 합니다. *fulltext_catalog_name* 됩니다 **sysname**합니다.  
  
 [  **@action=**] **'***동작***'**  
 수행할 동작입니다. *동작* 됩니다 **varchar(20)"**, 이며 다음이 값 중 하나일 수 있습니다.  
  
> [!NOTE]  
>  필요에 따라 전체 텍스트 카탈로그를 만들고 삭제하고 수정할 수 있습니다. 그러나 동시에 여러 카탈로그에서 스키마를 변경하지 마십시오. 사용 하 여 이러한 작업을 수행할 수 있습니다 합니다 **sp_fulltext_table** 저장 프로시저는 것이 좋습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**만들기**|파일 시스템에 빈 새 전체 텍스트 카탈로그를 만들고 연결된 된 행을 추가 **sysfulltextcatalogs** 사용 하 여 합니다 *fulltext_catalog_name* 하 고 *root_directory*, 있는 경우에 값입니다. *fulltext_catalog_name* 데이터베이스 내에서 고유 해야 합니다.|  
|**Drop**|삭제 *fulltext_catalog_name* 파일 시스템에서 제거한에서 연결된 된 행을 삭제 하 여 **sysfulltextcatalogs**합니다. 해당 카탈로그에 한 개 이상의 테이블에 대한 인덱스가 있는 경우에는 이 동작이 실패합니다. **sp_fulltext_table** '*table_name*', 'drop' 카탈로그에서 테이블을 삭제 하려면 실행 해야 합니다.<br /><br /> 카탈로그가 없을 경우에는 오류가 표시됩니다.|  
|**start_incremental**|에 대 한 증분 채우기를 시작 *fulltext_catalog_name*합니다. 카탈로그가 없을 경우에는 오류가 표시됩니다. 전체 텍스트 인덱스 채우기가 이미 활성화된 경우에는 경고가 표시되고 채우기 동작은 수행되지 않습니다. 증분 채우기를 사용 하 여 변경 된 행만 검색 됩니다 전체 텍스트 인덱싱에 대해 있는 경우는 **타임 스탬프** 열은 테이블에 전체 텍스트 인덱싱되 합니다.|  
|**start_full**|에 대 한 전체 채우기를 시작 *fulltext_catalog_name*합니다. 전체 텍스트 인덱싱에 대해 전체 텍스트 카탈로그와 연결된 모든 테이블의 모든 행 및 이미 인덱스를 만든 행까지도 검색합니다.|  
|**중지**|에 대 한 인덱스 채우기를 중지 *fulltext_catalog_name*합니다. 카탈로그가 없을 경우에는 오류가 표시됩니다. 채우기가 이미 중단된 경우에는 경고가 표시되지 않습니다.|  
|**Rebuild**|다시 작성 *fulltext_catalog_name*합니다. 카탈로그를 다시 작성하면 기존 카탈로그가 삭제되고 새 카탈로그가 해당 위치에 만들어집니다. 전체 텍스트 인덱싱 참조가 있는 모든 테이블은 새 카탈로그와 연결됩니다. 카탈로그를 다시 작성하면 데이터베이스 시스템 테이블의 전체 텍스트 메타데이터가 설정됩니다.<br /><br /> 변경 추적이 해제되어 있으면 새로 만들어진 전체 텍스트 카탈로그가 다시 채워지지도 않습니다. 이 경우 다시 채우려면 실행 **sp_fulltext_catalog** 사용 하 여는 **start_full** 하거나 **start_incremental** 작업 합니다.|  
  
 [ **@path=**] **'***root_directory***'**  
 루트 디렉터리 (없습니다 전체 물리적 경로)에 대 한는 **만들** 작업 합니다. *root_directory* 됩니다 **nvarchar(100)** 있고 기본값은 NULL 이며이 설치 시 지정한 기본 위치를 사용 합니다. 이 Mssql 디렉터리의 Ftdata 하위 디렉터리 예를 들어, C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\FTData 합니다. 지정된 루트 디렉터리는 반드시 같은 컴퓨터의 드라이브에 있어야 하며 드라이브 문자 및 다른 문자로 구성되어야 하고 상대 경로가 될 수 없습니다. 네트워크 드라이브, 이동식 드라이브, 플로피 디스크 및 UNC 경로는 지원하지 않습니다. 전체 텍스트 카탈로그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 로컬 하드 드라이브에 만들어야 합니다.  
  
 **@path** 유효한 경우에 *동작* 됩니다 **만들기**합니다. 이외의 작업에 대 한 **만듭니다** (**중지**를 **다시 작성**등), **@path** 생략 하거나 NULL 이어야 합니다.  
  
 클러스터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 가상 서버인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스가 의존하는 공유 디스크 드라이브에 있는 카탈로그 디렉터리를 지정해야 합니다. 경우 @path 지정 하지 않으면 기본 카탈로그 디렉터리의 위치는 공유 디스크 드라이브, 가상 서버를 설치할 때 지정 된 디렉터리에 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 합니다 **start_full** 작업에서 전체 텍스트 데이터의 전체 스냅숏을 만드는 데 사용 됩니다 *fulltext_catalog_name*합니다. 합니다 **start_incremental** 작업은 데이터베이스에서 변경된 된 행만 다시 인덱스를 사용 합니다. 증분 채우기는 테이블 형식의 열에 있는 경우에 적용할 수 있습니다 **타임 스탬프**합니다. 전체 텍스트 카탈로그에 테이블 형식의 열이 없으면 **타임 스탬프**, 테이블은 full 채우기를 수행 합니다.  
  
 전체 텍스트 카탈로그 및 인덱스 데이터는 전체 텍스트 카탈로그 디렉터리에서 만들어진 파일에 저장됩니다. 전체 텍스트 카탈로그 디렉터리에서 지정 된 디렉터리의 하위 디렉터리로 만들어집니다 **@path** 또는 서버 기본 전체 텍스트 카탈로그 디렉터리에 있는 경우 **@path** 아닙니다 지정 합니다. 전체 텍스트 카탈로그 디렉터리의 이름은 해당 서버에서 고유한 이름이 되도록 생성됩니다. 따라서 서버의 모든 전체 텍스트 카탈로그 디렉터리는 같은 경로를 공유할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 호출자의 멤버 여야 필요 합니다 **db_owner** 역할입니다. 요청 된 동작에 따라 호출자에 게 거부 되어서는 안 ALTER 또는 CONTROL 권한 (입니다 **db_owner** 에) 대상 전체 텍스트 카탈로그에 대해 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-create-a-full-text-catalog"></a>1. 전체 텍스트 카탈로그 만들기  
 이 예제에서는 빈 전체 텍스트 카탈로그를 만듭니다 **Cat_Desc**를 **AdventureWorks2012** 데이터베이스입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>2. 전체 텍스트 카탈로그를 다시 작성하려면  
 이 예제에서는 기존 전체 텍스트 카탈로그를 다시 작성 **Cat_Desc**를 **AdventureWorks2012** 데이터베이스입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>3. 전체 텍스트 카탈로그의 채우기 시작  
 전체 채우기를 시작 하는이 예제는 **Cat_Desc** 카탈로그입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>4. 전체 텍스트 카탈로그의 채우기 중지  
 이 예에서는 채우기를 중지 합니다 **Cat_Desc** 카탈로그입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>5. 전체 텍스트 카탈로그 제거  
 이 예제를 제거 합니다 **Cat_Desc** 카탈로그입니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
