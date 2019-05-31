---
title: OPENROWSET(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 3a6e2d51b9a2926f6d542ce3da5fc1c916881918
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944809"
---
# <a name="openrowset-transact-sql"></a>OPENROWSET(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  OLE DB 데이터 원본에서 원격 데이터를 액세스하는 데 필요한 모든 연결 정보를 포함합니다. 이 방법은 OLE DB를 사용하여 원격 데이터에 연결하고 액세스하는 일회성의 임시 방법이며 연결된 서버에서 테이블을 액세스하는 방법의 대안입니다. OLE DB 데이터 원본을 자주 참조하려면 연결된 서버를 사용합니다. 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요. `OPENROWSET` 함수는 쿼리의 FROM 절에서 테이블 이름인 것처럼 참조될 수 있습니다. `OPENROWSET` 함수는 OLE DB 공급자의 기능에 따라 `INSERT`, `UPDATE` 또는 `DELETE` 문의 대상 테이블로 참조될 수도 있습니다. 쿼리는 여러 결과 집합을 반환할 수 있지만 `OPENROWSET`은 첫 번째 결과 집합만 반환할 수 있습니다.  
  
 `OPENROWSET`은 파일의 데이터를 읽어서 행 집합으로 반환할 수 있는 기본 제공 BULK 공급자를 통해 대량 작업을 지원합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>인수  
 '*provider_name*'  
 레지스트리에 지정된 OLE DB 공급자의 이름(또는 PROGID)을 나타내는 문자열입니다. *provider_name*에는 기본값이 없습니다.  
  
 '*datasource*'  
 특정 OLE DB 데이터 원본에 해당되는 문자열 상수입니다. *datasource*는 공급자의 IDBProperties 인터페이스에 전달되어 공급자를 초기화하는 DBPROP_INIT_DATASOURCE 속성입니다. 일반적으로 이 문자열에는 데이터베이스 파일의 이름, 데이터베이스 서버의 이름 또는 공급자가 데이터베이스의 위치를 알 수 있는 이름이 포함됩니다.  
  
 '*user_id*'  
 지정한 OLE DB 공급자에게 전달되는 사용자 이름을 나타내는 문자열 상수입니다. *user_id*는 연결의 보안 컨텍스트를 지정하고 DBPROP_AUTH_USERID 속성으로 전달되어 공급자를 초기화합니다. *user_id*는 Microsoft Windows 로그인 이름일 수 없습니다.  
  
 '*password*'  
 OLE DB 공급자에게 전달되는 사용자 암호를 나타내는 문자열 상수입니다. *password*는 공급자를 초기화할 때 DBPROP_AUTH_PASSWORD 속성으로 전달됩니다. *password*는 Microsoft Windows 암호일 수 없습니다.  
  
 '*provider_string*'  
 DBPROP_INIT_PROVIDERSTRING 속성으로 전달되어 OLE DB 공급자를 초기화하는 공급자별 연결 문자열입니다. *provider_string*은 일반적으로 공급자를 초기화하는 데 필요한 모든 연결 정보를 캡슐화합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 인식하는 키워드 목록은 [초기화 및 권한 부여 속성](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요.  
  
 *catalog*  
 지정한 개체가 있는 카탈로그 또는 데이터베이스의 이름입니다.  
  
 *schema*  
 지정한 개체에 대한 스키마 또는 개체 소유자의 이름입니다.  
  
 *object*  
 작업할 개체를 고유하게 식별하는 개체 이름입니다.  
  
 '*query*'  
 공급자에게 전달되어 공급자에 의해 실행되는 문자열 상수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스는 이 쿼리를 처리하지 않지만 공급자에 의해 반환되는 쿼리 결과(통과 쿼리)는 처리합니다. 통과 쿼리는 테이블 형식의 데이터를 테이블 이름을 통해서는 사용할 수 없고 명령 언어를 통해서만 사용할 수 있는 공급자에 대해 사용할 경우 유용합니다. 쿼리 공급자가 OLE DB 명령 개체와 해당 필수 인터페이스를 지원하는 경우에는 원격 서버에서 통과 쿼리를 사용할 수 있습니다. 자세한 내용은 [SQL Server Native Client&#40;OLE DB&#41; 참조](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)를 참조하세요.  
  
 BULK  
 OPENROWSET의 BULK 행 집합 공급자를 사용하여 파일에서 데이터를 읽습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 OPENROWSET은 데이터를 대상 테이블에 로드하지 않고 데이터 파일에서 읽을 수 있습니다. 이를 통해 간단한 SELECT 문과 함께 OPENROWSET을 사용할 수 있습니다.  

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.
  
 BULK 옵션의 인수를 사용하면 데이터 읽기의 시작 및 끝 위치, 오류 처리 방법 및 데이터 해석 방법을 효과적으로 제어할 수 있습니다. 예를 들어 **varbinary**, **varchar** 또는 **nvarchar** 형식의 단일 행 및 단일 열로 된 행 집합으로 데이터 파일을 읽도록 지정할 수 있습니다. 기본 동작에 대한 설명은 그 다음에 나오는 인수 설명을 따릅니다.  
  
 BULK 옵션 사용법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오. BULK 옵션에 필요한 사용 권한에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "사용 권한"을 참조하십시오.  
  
> [!NOTE]  
> 전체 복구 모델로 데이터를 가져올 때 OPENROWSET(BULK ...)을 사용하면 로깅이 최적화되지 않습니다.  
  
 대량 가져오기를 위한 데이터 준비 방법은 [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.  
  
 '*data_file*'  
 대상 테이블에 복사할 데이터가 있는 데이터 파일의 전체 경로입니다.   
 **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1.   
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 data_file은 Azure Blob Storage에 있을 수 있습니다. 예제는 [Azure Blob Storage의 데이터에 대량 액세스 예제](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요.

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.
  
 \<bulk_options>  
 BULK 옵션에 대한 하나 이상의 인수를 지정합니다.  
  
 CODEPAGE = { 'ACP'| 'OEM'| 'RAW'| '*code_page*' }  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다. CODEPAGE는 문자 값이 127보다 크거나 32보다 작은 **char**, **varchar** 또는 **text** 열이 데이터에 포함된 경우에만 적합합니다.  

> [!IMPORTANT]
> CODEPAGE는 Linux에서 지원되는 옵션이 아닙니다.

> [!NOTE]  
> 데이터 정렬/코드 페이지 사양보다 65001 옵션에 더 높은 우선 순위를 두려는 경우를 제외하고는 서식 파일의 각 열에 대한 데이터 정렬 이름을 지정하는 것이 좋습니다.  
  
|CODEPAGE 값|설명|  
|--------------------|-----------------|  
|ACP|**char**, **varchar** 또는 **text** 데이터 형식의 열을 ANSI/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 코드 페이지(ISO 1252)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지로 변환합니다.|  
|OEM(기본값)|**char**, **varchar** 또는 **text** 데이터 형식의 열을 시스템 OEM 코드 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지로 변환합니다.|  
|RAW|코드 페이지 간 변환이 일어나지 않습니다. 가장 빠른 옵션입니다.|  
|*code_page*|데이터 파일의 문자 데이터가 인코딩된 원본 코드 페이지(예: 850)를 나타냅니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이전 버전은 코드 페이지 65001(UTF-8 인코딩)을 지원하지 않습니다.|  
  
 ERRORFILE ='*file_name*'  
 형식 오류가 있어 OLE DB 행 집합으로 변환할 수 없는 행을 수집하는 데 사용되는 파일을 지정합니다. 이러한 행은 데이터 파일에서 "있는 그대로" 이 오류 파일에 복사됩니다.  
  
 오류 파일은 명령이 실행될 때 생성됩니다. 파일이 이미 있으면 오류가 발생합니다. 또한 확장명이 .ERROR.txt인 제어 파일이 생성됩니다. 이 파일은 오류 파일의 각 행을 참조하여 오류를 진단합니다. 오류를 해결한 후에는 데이터를 로드할 수 있습니다.  
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]부터 `error_file_path`는 Azure Blob Storage에 있을 수 있습니다. 

'errorfile_data_source_name'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
가져오는 동안 발견된 오류를 포함할 오류 파일의 Azure Blob 스토리지 위치를 가리키는 명명된 외부 데이터 원본입니다. 외부 데이터 원본은 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1에서 추가된 `TYPE = BLOB_STORAGE` 옵션을 사용하여 만들어야 합니다. 자세한 내용은 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 참조하세요.
  
 FIRSTROW =*first_row*  
 로드할 첫 번째 행의 번호를 지정합니다. 기본값은 1입니다. 지정한 데이터 파일의 첫 번째 행을 나타냅니다. 행 번호는 행 종결자를 계산하여 결정됩니다. FIRSTROW는 1부터 시작합니다.  
  
 LASTROW =*last_row*  
 로드할 마지막 행의 번호를 지정합니다. 기본값은 0입니다. 지정한 데이터 파일의 마지막 행을 나타냅니다.  
  
 MAXERRORS =*maximum_errors*  
 OPENROWSET에서 예외가 발생하기 전에 나타날 수 있는 구문 오류 또는 서식 파일의 정의와 일치하지 않는 행의 최대 수를 지정합니다. MAXERRORS에 도달할 때까지 OPENROWSET은 각각의 잘못된 행을 로드하지 않고 무시하며 잘못된 행을 오류로 간주하여 계산합니다.  
  
 *maximum_errors*의 기본값은 10입니다.  
  
> [!NOTE]  
> MAX_ERRORS는 CHECK 제약 조건이나 **money** 및 **bigint** 데이터 형식 변환에 적용되지 않습니다.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 데이터 파일에 있는 대략적인 데이터 행 수를 지정합니다. 이 값은 실제 행 수와 순서가 같아야 합니다.  
  
 OPENROWSET은 데이터 파일을 항상 단일 일괄 처리로 가져옵니다. 그러나 0보다 큰 값으로 *rows_per_batch*를 지정하면 쿼리 프로세서가 *rows_per_batch*의 값을 힌트로 사용하여 리소스를 쿼리 계획에 할당합니다.  
  
 기본적으로 ROWS_PER_BATCH는 알 수 없습니다. ROWS_PER_BATCH = 0을 지정하는 것은 ROWS_PER_BATCH를 생략하는 것과 같습니다.  
  
 ORDER ( { *column* [ ASC | DESC ] } [ ,... *n* ] [ UNIQUE ] )  
 데이터 파일에 있는 데이터의 정렬 방식을 지정하는 선택적 힌트입니다. 기본적으로 대량 작업은 데이터 파일이 정렬되지 않았음을 전제로 합니다. 쿼리 최적화 프로그램에서 지정된 순서를 사용하여 보다 효율적인 쿼리 계획을 생성할 수 있다면 성능이 향상될 수 있습니다. 정렬을 지정하는 것이 유용한 예는 다음과 같습니다.  
  
-   클러스터형 인덱스를 포함하는 테이블에 행을 삽입하는 경우. 이 경우 행 집합 데이터가 클러스터형 인덱스 키에 따라 정렬됩니다.  
  
-   다른 테이블과 행 집합을 조인하는 경우. 이 경우 정렬 열과 조인 열이 일치합니다.  
  
-   정렬 열에 따라 행 집합 데이터를 집계하는 경우  
  
-   쿼리의 FROM 절에서 행 집합을 원본 테이블로 사용하는 경우. 이 경우 정렬 열과 조인 열이 일치합니다.  
  
 UNIQUE는 데이터 파일에 중복 항목이 포함되지 않도록 지정합니다.  
  
 데이터 파일의 실제 행이 지정된 순서에 따라 정렬되지 않거나 UNIQUE 힌트를 지정했는데 중복된 키가 있는 경우 오류가 반환됩니다.  
  
 ORDER를 사용하는 경우 열 별칭이 필요합니다. 열 별칭 목록은 BULK 절에서 액세스되는 파생 테이블을 참조해야 합니다. ORDER 절에 지정된 열 이름은 이 열 별칭 목록을 참조합니다. 큰 값 유형(**varchar(max)** , **nvarchar(max)** , **varbinary(max)** 및 **xml**) 및 LOB(Large Object) 형식(**text**, **ntext** 및 **image**) 열은 지정할 수 없습니다.  
  
 SINGLE_BLOB  
 *data_file*의 내용을 **varbinary(max)** 형식의 단일 행 및 단일 열로 된 행 집합으로 반환합니다.  
  
> [!IMPORTANT]  
> SINGLE_BLOB만 모든 Windows 인코딩 변환을 지원하므로 SINGLE_CLOB 및 SINGLE_NCLOB가 아닌 SINGLE_BLOB 옵션만 사용하여 XML 데이터를 가져오는 것이 좋습니다.  
  
 SINGLE_CLOB  
 *data_file*을 ASCII로 읽은 후 현재 데이터베이스의 데이터 정렬을 사용하여 내용을 **varchar(max)** 형식의 단일 행 및 단일 열로 된 행 집합으로 반환합니다.  
  
 SINGLE_NCLOB  
 *data_file*을 UNICODE로 읽은 후 현재 데이터베이스의 데이터 정렬을 사용하여 내용을 **nvarchar(max)** 형식의 단일 행 및 단일 열로 된 행 집합으로 반환합니다.  

### <a name="input-file-format-options"></a>입력 파일 형식 옵션
  
FORMAT **=** 'CSV'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
[RFC 4180](https://tools.ietf.org/html/rfc4180) 표준을 준수하는 쉼표로 구분된 값 파일을 지정합니다.

 FORMATFILE ='*format_file_path*'  
 서식 파일의 전체 경로를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 두 가지 유형의 형식 파일을 지원합니다. XML 및 비 XML.  
  
 서식 파일은 결과 집합에서 열 유형을 정의하는 데 필요합니다. 단, SINGLE_CLOB, SINGLE_BLOB 또는 SINGLE_NCLOB를 지정한 경우에는 서식 파일이 필요하지 않습니다.  
  
 서식 파일에 대한 자세한 내용은 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.  

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 format_file_path는 Azure Blob Storage에 있을 수 있습니다. 예제는 [Azure Blob Storage의 데이터에 대량 액세스 예제](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요.

FIELDQUOTE **=** 'field_quote'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
CSV 파일에 따옴표 문자로 사용될 문자를 지정합니다. 지정하지 않으면 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준에 정의한 대로 따옴표 문자(")가 따옴표 문자로 사용됩니다.

  
## <a name="remarks"></a>Remarks  
 `OPENROWSET`는 지정된 공급자에 대해 명시적으로 **DisallowAdhocAccess** 레지스트리 옵션을 0으로 설정하고 Ad Hoc Distributed Queries 고급 구성 옵션을 설정할 때만 OLE DB 데이터 원본에서 원격 데이터에 액세스하는 데 사용할 수 있습니다. 이러한 옵션을 설정하지 않은 경우 기본적으로 임시 액세스가 허용되지 않습니다.  
  
 원격 OLE DB 데이터 원본에 액세스할 때 트러스트된 연결의 로그인 ID는 클라이언트가 쿼리 중인 서버에 연결되어 있는 서버에서 자동으로 위임되지 않습니다. 이 경우 인증 위임을 구성해야 합니다.  
  
 OLE DB 공급자가 지정된 데이터 원본에서 여러 카탈로그와 스키마를 지원하는 경우에는 카탈로그 이름과 스키마 이름이 필요합니다. OLE DB 공급자가 카탈로그와 스키마를 지원하지 않는 경우에는 _catalog_ 및 _schema_에 대한 값을 생략할 수 있습니다. 공급자가 스키마 이름만 지원하는 경우에는 _schema_ **.** _object_형식의 두 부분으로 된 이름을 반드시 지정해야 합니다. 공급자가 카탈로그 이름만 지원하는 경우에는_catalog_ **.** _schema_ **.** _object_ 형식의 세 부분으로 된 이름을 반드시 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하는 통과 쿼리의 경우 세 부분으로 된 이름을 반드시 지정해야 합니다. 자세한 내용은 [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)을 참조하세요.  
  
 `OPENROWSET`는 변수를 인수로 받아들이지 않습니다.  
  
 `FROM` 절에서 `OPENDATASOURCE`, `OPENQUERY` 또는 `OPENROWSET`에 대한 모든 호출은 두 호출에 동일한 인수가 제공되는 경우에도 업데이트의 대상으로 사용되는 함수에 대한 호출과는 개별적이고 독립적으로 평가됩니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>BULK 옵션이 있는 OPENROWSET 사용  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 향상된 기능은 OPENROWSET(BULK...) 함수를 지원합니다.  
  
-   `SELECT`와 함께 사용되는 FROM 절에서는 전체 `SELECT` 기능을 사용하여 테이블 이름 대신 `OPENROWSET(BULK...)`을 호출할 수 있습니다.  
  
     `BULK` 옵션이 있는 `OPENROWSET`에는 `FROM` 절에 범위 변수 또는 별칭이라고도 하는 상관 관계 이름이 필요합니다. 열 별칭을 지정할 수 있습니다. 열 별칭 목록을 지정하지 않은 경우에는 서식 파일에 반드시 열 이름이 있어야 합니다. 열 별칭을 지정하면 서식 파일의 열 이름은 무시됩니다. 다음 예를 참조하십시오.  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
> [!IMPORTANT]  
> `AS <table_alias>`를 추가하지 않으면 오류가 발생합니다.    
> 메시지 491, 수준 16, 상태 1, 줄 20    
> FROM 절의 대량 행 집합에 대해 상관 관계 이름을 지정해야 합니다.    
  
-   `SELECT...FROM OPENROWSET(BULK...)` 문은 데이터를 테이블로 가져오지 않고 파일의 데이터를 직접 쿼리합니다. `SELECT...FROM OPENROWSET(BULK...)` 문도 서식 파일을 사용하여 대량 열 별칭을 나열하는 방법으로 열 이름 및 데이터 형식을 지정할 수 있습니다.  
  
-   `INSERT` 또는 `MERGE` 문에서 `OPENROWSET(BULK...)`을 원본 테이블로 사용하면 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 대량으로 가져올 수 있습니다. 자세한 내용은 [BULK INSERT 또는 OPENROWSET&#40;BULK...&#41;를 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)를 참조하세요.  
  
-   `OPENROWSET BULK` 옵션을 `INSERT` 문과 함께 사용하면 BULK 절에 테이블 힌트를 사용할 수 있습니다. 또한 `TABLOCK`과 같은 일반적인 테이블 힌트 외에도 `BULK` 절에는 `IGNORE_CONSTRAINTS`(`CHECK` 및 `FOREIGN KEY` 제약 조건만 무시), `IGNORE_TRIGGERS`, `KEEPDEFAULTS` 및 `KEEPIDENTITY`와 같은 특수 테이블 힌트가 허용됩니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 `INSERT...SELECT * FROM OPENROWSET(BULK...)` 문을 사용하는 방법에 대한 자세한 내용은 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)를 참조하세요. 대량 가져오기로 수행된 행 삽입 작업이 트랜잭션 로그에 기록되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
> [!NOTE]  
> `OPENROWSET`을 사용할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가장을 처리하는 방법을 이해하는 것이 중요합니다. 보안 고려 사항에 대한 자세한 내용은 [BULK INSERT 또는 OPENROWSET&#40;BULK...&#41;를 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)를 참조하세요.  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>SQLCHAR, SQLNCHAR 또는 SQLBINARY 데이터 대량 가져오기  
 OPENROWSET(BULK...)은 지정되지 않은 경우 SQLCHAR, SQLNCHAR 또는 SQLBINARY 데이터의 최대 길이가 8000바이트를 초과하지 않는다고 가정합니다. 가져올 데이터가 8000바이트를 초과하는 **varchar(max)** , **nvarchar(max)** 또는 **varbinary(max)** 개체가 포함된 LOB 데이터 필드에 있는 경우 데이터 필드의 최대 길이를 정의하는 XML 서식 파일을 사용해야 합니다. 최대 길이를 지정하려면 서식 파일을 편집하고 MAX_LENGTH 특성을 선언합니다.  
  
> [!NOTE]  
> 자동으로 생성된 서식 파일은 LOB 필드의 길이 또는 최대 길이를 지정하지 않습니다. 그러나 직접 서식 파일을 편집하고 길이 또는 최대 길이를 지정할 수 있습니다.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기  
 SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.  
  
|데이터 형식|영향|  
|---------------|------------|  
|SQLCHAR 또는 SQLVARYCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다.|  
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다.|  
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 `OPENROWSET` 권한은 OLE DB 공급자에게 전달되는 사용자 이름의 사용 권한에 의해 결정됩니다. `BULK` 옵션을 사용하려면 `ADMINISTER BULK OPERATIONS` 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>1. SELECT 및 SQL Server Native Client OLE DB 공급자와 함께 OPENROWSET 사용  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 `Seattle1` 원격 서버에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `HumanResources.Department` 테이블에 액세스합니다. SQLNCLI를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자로 리디렉션됩니다. `SELECT` 문은 반환되는 행 집합을 정의하는 데 사용됩니다. 공급자 문자열에는 `Server` 및 `Trusted_Connection` 키워드가 포함됩니다. 이러한 키워드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 인식합니다.  
  
```sql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>2. Microsoft OLE DB Provider for Jet 사용  
 다음 예에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access `Customers` 데이터베이스의 `Northwind` 테이블에 액세스합니다.  
  
> [!NOTE]  
> 이 예에서는 Access가 설치되어 있다고 가정합니다. 이 예를 실행하려면 Northwind 데이터베이스를 설치해야 합니다.  
  
```sql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. INNER JOIN에서 OPENROWSET 및 다른 테이블 사용  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` 데이터베이스의 로컬 인스턴스에 있는 `Customers` 테이블과 해당 컴퓨터에 저장되어 있는 Access `Northwind` 데이터베이스의 `Orders` 테이블에서 모든 데이터를 선택합니다.  
  
> [!NOTE]  
> 이 예에서는 Access가 설치되어 있다고 가정합니다. 이 예를 실행하려면 Northwind 데이터베이스를 설치해야 합니다.  
  
```sql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.

  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. OPENROWSET를 사용하여 varbinary(max) 열에 파일 데이터 대량 삽입  
 다음 예에서는 데모용으로 작은 테이블을 만들고 `Text1.txt` 루트 디렉터리에 있는 `C:`라는 파일의 파일 데이터를 `varbinary(max)` 열에 삽입합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.
  

### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. OPENROWSET BULK 공급자를 서식 파일과 함께 사용하여 텍스트 파일의 행 검색  
 다음 예에서는 서식 파일을 사용하여 다음 데이터가 들어 있는 탭으로 분리된 텍스트 파일인 `values.txt`에서 행을 검색합니다.  
  
```sql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 서식 파일인 `values.fmt`는 `values.txt`의 열을 설명합니다.  
  
```sql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 다음은 해당 데이터를 검색하는 쿼리입니다.  
  
```sql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.
  

### <a name="f-specifying-a-format-file-and-code-page"></a>F. 서식 파일 및 코드 페이지 지정  
 다음 예제는 서식 파일과 코드 페이지 옵션을 동시에 사용하는 방법을 보여줍니다.  
  
```sql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. 서식 파일로 CSV 파일의 데이터에 액세스  
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1.   
```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.


### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. 서식 파일 없이 CSV 파일의 데이터에 액세스

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

> [!IMPORTANT]
> Microsoft Azure SQL Database는 Windows 파일에서 읽기를 지원하지 않습니다.


### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>9. Azure Blob 스토리지에 저장된 파일에서 데이터에 액세스   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.1.   
다음 예에서는 공유 액세스 서명을 위해 만든 데이터베이스 범위 자격 증명 및 Azure 스토리지 계정의 컨테이너를 가리키는 외부 데이터 원본을 사용합니다.     

```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
자격 증명 및 외부 데이터 원본의 구성을 포함하여 전체 `OPENROWSET` 예제는 [Azure Blob Storage의 데이터에 대한 대량 액세스 예제](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)를 참조하세요.
 
### <a name="additional-examples"></a>추가 예  
 `INSERT...SELECT * FROM OPENROWSET(BULK...)` 사용에 대한 추가 예는 다음 항목을 참조하세요.  
  
-   [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY&#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Rowset 함수&#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
