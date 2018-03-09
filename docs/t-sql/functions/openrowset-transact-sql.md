---
title: OPENROWSET (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 68db78ede26c3e7f8c60ced655d89d0fc9a615ac
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="openrowset-transact-sql"></a>OPENROWSET(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OLE DB 데이터 원본에서 원격 데이터를 액세스하는 데 필요한 모든 연결 정보를 포함합니다. 이 방법은 OLE DB를 사용하여 원격 데이터에 연결하고 액세스하는 일회성의 임시 방법이며 연결된 서버에서 테이블을 액세스하는 방법의 대안입니다. OLE DB 데이터 원본을 자주 참조하려면 연결된 서버를 사용합니다. 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요. `OPENROWSET` 테이블 이름 처럼 쿼리의 FROM 절에 함수를 참조할 수 있습니다. `OPENROWSET` 함수의 대상 테이블로 참조할 수도 있습니다는 `INSERT`, `UPDATE`, 또는 `DELETE` OLE DB 공급자의 기능에 따라 문입니다. 쿼리는 여러 결과 집합을 반환할 수 있지만 `OPENROWSET` 첫 번째 것만 반환 합니다.  
  
 `OPENROWSET`또한 읽고 행 집합으로 반환 된 파일의 데이터는 기본 제공 BULK 공급자를 이용한 대량 작업도 지원 합니다.  
  
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
 레지스트리에 지정된 OLE DB 공급자의 이름(또는 PROGID)을 나타내는 문자열입니다. *provider_name* 기본값은 없습니다.  
  
 '*datasource*'  
 특정 OLE DB 데이터 원본에 해당되는 문자열 상수입니다. *데이터 원본* 는 DBPROP_INIT_DATASOURCE 속성 공급자를 초기화 공급자의 IDBProperties 인터페이스를 전달 하도록 합니다. 일반적으로 이 문자열에는 데이터베이스 파일의 이름, 데이터베이스 서버의 이름 또는 공급자가 데이터베이스의 위치를 알 수 있는 이름이 포함됩니다.  
  
 '*user_id*'  
 지정한 OLE DB 공급자에게 전달되는 사용자 이름을 나타내는 문자열 상수입니다. *user_id* 연결에 대 한 보안 컨텍스트를 지정 하 고에서 공급자를 초기화 하 고 DBPROP_AUTH_USERID 속성으로 전달 됩니다. *user_id* Microsoft Windows 로그인 이름이 될 수 없습니다.  
  
 '*암호*'  
 OLE DB 공급자에게 전달되는 사용자 암호를 나타내는 문자열 상수입니다. *암호* 공급자를 초기화할 때 DBPROP_AUTH_PASSWORD 속성으로 전달 됩니다. *암호* Microsoft Windows 암호로 사용할 수 없습니다.  
  
 '*provider_string*'  
 DBPROP_INIT_PROVIDERSTRING 속성으로 전달되어 OLE DB 공급자를 초기화하는 공급자별 연결 문자열입니다. *provider_string* 일반적으로 공급자를 초기화 하는 데 필요한 모든 연결 정보를 캡슐화 합니다. 인식 되는 키워드 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 참조 [초기화 및 권한 부여 속성](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
  
 *카탈로그*  
 지정한 개체가 있는 카탈로그 또는 데이터베이스의 이름입니다.  
  
 *스키마*  
 지정한 개체에 대한 스키마 또는 개체 소유자의 이름입니다.  
  
 *개체*  
 작업할 개체를 고유하게 식별하는 개체 이름입니다.  
  
 '*쿼리*'  
 공급자에게 전달되어 공급자에 의해 실행되는 문자열 상수입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스는 이 쿼리를 처리하지 않지만 공급자에 의해 반환되는 쿼리 결과(통과 쿼리)는 처리합니다. 통과 쿼리는 테이블 형식의 데이터를 테이블 이름을 통해서는 사용할 수 없고 명령 언어를 통해서만 사용할 수 있는 공급자에 대해 사용할 경우 유용합니다. 통과 쿼리는 쿼리 공급자는 OLE DB 명령 개체와 해당 필수 인터페이스를 지 원하는 원격 서버에서 지원 됩니다. 자세한 내용은 참조 [SQL Server Native Client &#40; OLE db&#41; 참조](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)합니다.  
  
 BULK  
 OPENROWSET의 BULK 행 집합 공급자를 사용하여 파일에서 데이터를 읽습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 OPENROWSET은 데이터를 대상 테이블에 로드하지 않고 데이터 파일에서 읽을 수 있습니다. 이를 통해 간단한 SELECT 문과 함께 OPENROWSET을 사용할 수 있습니다.  
  
 BULK 옵션의 인수를 사용하면 데이터 읽기의 시작 및 끝 위치, 오류 처리 방법 및 데이터 해석 방법을 효과적으로 제어할 수 있습니다. 데이터 파일 형식의 단일 행, 단일 열 행 집합으로 읽을 수를 지정할 수는 예를 들어 **varbinary**, **varchar**, 또는 **nvarchar**합니다. 기본 동작에 대한 설명은 그 다음에 나오는 인수 설명을 따릅니다.  
  
 BULK 옵션 사용법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오. BULK 옵션에 필요한 사용 권한에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "사용 권한"을 참조하십시오.  
  
> [!NOTE]  
>  전체 복구 모델로 데이터를 가져올 때 OPENROWSET(BULK ...)을 사용하면 로깅이 최적화되지 않습니다.  
  
 대량 가져오기를 위한 데이터 준비에 대 한 정보를 참조 하세요. [대량 내보내기 또는 가져오기 &#40;에 대 한 데이터 준비 SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 대상 테이블에 복사할 데이터가 있는 데이터 파일의 전체 경로입니다.   
 **적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1는 data_file Azure 블로그 저장소에 있을 수 있습니다. 예제를 보려면 [예의 대량 데이터에에서 액세스를 Azure Blob 저장소](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)합니다.
  
 \<bulk_options >  
 BULK 옵션에 대한 하나 이상의 인수를 지정합니다.  
  
 코드 페이지 = {'ACP' | 'OEM' | '원시' | *code_page*'을 (를)  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다. 코드 페이지와 데이터를 포함 하는 경우에 관련 된 **char**, **varchar**, 또는 **텍스트** 127 보다 크거나 32 보다 작은 문자 값이 있는 열입니다.  
  
> [!NOTE]  
>  65001 옵션에는 데이터 정렬/코드 페이지 사양 보다 우선 순위가를 하려는 경우를 제외 하 고 서식 파일의 각 열에 대 한 데이터 정렬 이름의 지정 하는 것이 좋습니다.  
  
|CODEPAGE 값|Description|  
|--------------------|-----------------|  
|ACP|열을 변환 **char**, **varchar**, 또는 **텍스트** ANSI에서 데이터 형식을 /[!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 Windows 코드 페이지 (ISO 1252)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지입니다.|  
|OEM(기본값)|열을 변환 **char**, **varchar**, 또는 **텍스트** 를 시스템 OEM 코드 페이지에서 데이터 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드 페이지입니다.|  
|RAW|코드 페이지 간 변환이 일어나지 않습니다. 가장 빠른 옵션입니다.|  
|*code_page*|데이터 파일의 문자 데이터가 인코딩된 원본 코드 페이지(예: 850)를 나타냅니다.<br /><br /> **\*\*중요 한 \* \***  이전 버전을 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 코드 페이지 65001 (utf-8 인코딩)을 지원 하지 않습니다.|  
  
 ERRORFILE ='*file_name*'  
 형식 오류가 있어 OLE DB 행 집합으로 변환할 수 없는 행을 수집하는 데 사용되는 파일을 지정합니다. 이러한 행은 데이터 파일에서 "있는 그대로" 이 오류 파일에 복사됩니다.  
  
 오류 파일은 명령이 실행될 때 생성됩니다. 파일이 이미 있으면 오류가 발생합니다. 또한 확장명이 .ERROR.txt인 제어 파일이 생성됩니다. 이 파일은 오류 파일의 각 행을 참조하여 오류를 진단합니다. 오류를 해결한 후에는 데이터를 로드할 수 있습니다.  
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], `error_file_path` Azure 블로그 저장소에 있을 수 있습니다. 

' errorfile_data_source_name'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
명명 된 외부 데이터 소스는 가져오기 중 발견 된 오류가 포함 될 오류 파일의 Azure Blob 저장소 위치를 가리킵니다. 외부 데이터 원본을 사용 하 여 만들어야는 `TYPE = BLOB_STORAGE` 옵션에 추가 된 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. 자세한 내용은 참조 [외부 데이터 원본 만들기](../../t-sql/statements/create-external-data-source-transact-sql.md)합니다.
  
 FIRSTROW =*first_row*  
 로드할 첫 번째 행의 번호를 지정합니다. 기본값은 1입니다. 지정한 데이터 파일의 첫 번째 행을 나타냅니다. 행 번호는 행 종결자를 계산하여 결정됩니다. FIRSTROW는 1부터 시작합니다.  
  
 LASTROW =*last_row*  
 로드할 마지막 행의 번호를 지정합니다. 기본값은 0입니다. 지정한 데이터 파일의 마지막 행을 나타냅니다.  
  
 MAXERRORS =*maximum_errors*  
 OPENROWSET에서 예외가 발생하기 전에 나타날 수 있는 구문 오류 또는 서식 파일의 정의와 일치하지 않는 행의 최대 수를 지정합니다. MAXERRORS에 도달할 때까지 OPENROWSET은 각각의 잘못된 행을 로드하지 않고 무시하며 잘못된 행을 오류로 간주하여 계산합니다.  
  
 에 대 한 기본 *maximum_errors* 은 10입니다.  
  
> [!NOTE]  
>  MAX_ERRORS는 CHECK 제약 조건 또는 변환에 적용 되지 않습니다 **money** 및 **bigint** 데이터 형식입니다.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 데이터 파일에 있는 대략적인 데이터 행 수를 지정합니다. 이 값은 실제 행 수와 순서가 같아야 합니다.  
  
 OPENROWSET은 데이터 파일을 항상 단일 일괄 처리로 가져옵니다. 그러나 지정 하는 경우 *rows_per_batch* 값 > 0 인 쿼리 프로세서는 값을 *rows_per_batch* 쿼리 계획에 리소스를 할당 하기 위한 힌트로 합니다.  
  
 기본적으로 ROWS_PER_BATCH는 알 수 없습니다. ROWS_PER_BATCH = 0을 지정하는 것은 ROWS_PER_BATCH를 생략하는 것과 같습니다.  
  
 순서 ({ *열* [ASC | DESC]} [,...  *n*  ] [UNIQUE])  
 데이터 파일에 있는 데이터의 정렬 방식을 지정하는 선택적 힌트입니다. 기본적으로 대량 작업은 데이터 파일이 정렬되지 않았음을 전제로 합니다. 쿼리 최적화 프로그램에서 지정된 순서를 사용하여 보다 효율적인 쿼리 계획을 생성할 수 있다면 성능이 향상될 수 있습니다. 정렬을 지정하는 것이 유용한 예는 다음과 같습니다.  
  
-   클러스터형 인덱스를 포함하는 테이블에 행을 삽입하는 경우. 이 경우 행 집합 데이터가 클러스터형 인덱스 키에 따라 정렬됩니다.  
  
-   다른 테이블과 행 집합을 조인하는 경우. 이 경우 정렬 열과 조인 열이 일치합니다.  
  
-   정렬 열에 따라 행 집합 데이터를 집계하는 경우  
  
-   쿼리의 FROM 절에서 행 집합을 원본 테이블로 사용하는 경우. 이 경우 정렬 열과 조인 열이 일치합니다.  
  
 UNIQUE는 데이터 파일에 중복 항목이 포함되지 않도록 지정합니다.  
  
 데이터 파일의 실제 행이 지정된 순서에 따라 정렬되지 않거나 UNIQUE 힌트를 지정했는데 중복된 키가 있는 경우 오류가 반환됩니다.  
  
 ORDER를 사용하는 경우 열 별칭이 필요합니다. 열 별칭 목록은 BULK 절에서 액세스되는 파생 테이블을 참조해야 합니다. ORDER 절에 지정된 열 이름은 이 열 별칭 목록을 참조합니다. 큰 값 형식 (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 및 **xml**) 및 큰 개체 (LOB) 형식 (**텍스트**, **ntext**, 및 **이미지**) 열을 지정할 수 없습니다.  
  
 SINGLE_BLOB  
 내용을 반환 *data_file* 형식의 단일 행, 단일 열 행 집합으로 **varbinary (max)**합니다.  
  
> [!IMPORTANT]  
>  SINGLE_BLOB만 모든 Windows 인코딩 변환을 지원하므로 SINGLE_CLOB 및 SINGLE_NCLOB가 아닌 SINGLE_BLOB 옵션만 사용하여 XML 데이터를 가져오는 것이 좋습니다.  
  
 SINGLE_CLOB  
 읽어 *data_file* ASCII로 콘텐츠 형식의 단일 행, 단일 열 행 집합으로 반환 **varchar (max)**, 현재 데이터베이스의 데이터 정렬을 사용 하 여 합니다.  
  
 SINGLE_NCLOB  
 읽어 *data_file* 유니코드로 콘텐츠 형식의 단일 행, 단일 열 행 집합으로 반환 **nvarchar (max)**, 현재 데이터베이스의 데이터 정렬을 사용 하 여 합니다.  

### <a name="input-file-format-options"></a>입력된 파일 형식 옵션입니다.
  
형식  **=**  'CSV'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
쉼표로 구분 된 값 파일에 규정 지정는 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준입니다.

 FORMATFILE ='*format_file_path*'  
 서식 파일의 전체 경로를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]두 가지 유형의 서식 파일 지원: XML 및 비-XML입니다.  
  
 서식 파일은 결과 집합에서 열 유형을 정의하는 데 필요합니다. 단, SINGLE_CLOB, SINGLE_BLOB 또는 SINGLE_NCLOB를 지정한 경우에는 서식 파일이 필요하지 않습니다.  
  
 서식 파일에 대 한 정보를 참조 하세요. [서식 파일 데이터 대량 가져오기 &#40;을 사용 하 여 SQL Server &#41; ](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
부터는 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1는 format_file_path Azure 블로그 저장소에 있을 수 있습니다. 예제를 보려면 [예의 대량 데이터에에서 액세스를 Azure Blob 저장소](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)합니다.

FIELDQUOTE  **=**  'field_quote'   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
CSV 파일의 따옴표 문자로 사용 될 문자를 지정 합니다. 에 정의 된 대로 인용 문자 (") 따옴표 문자로 사용될지를 지정 하지는 [RFC 4180](https://tools.ietf.org/html/rfc4180) 표준입니다.

  
## <a name="remarks"></a>주의  
 `OPENROWSET`원격 데이터에 액세스 하는 데 사용 될 때만 데이터 원본에서 OLE DB는 **DisallowAdhocAccess** 레지스트리 옵션은 명시적으로 지정된 된 공급자에 대 한 0으로 설정 됩니다 이며 고급 구성 옵션 Ad Hoc Distributed Queries 사용할 수 있습니다. 이러한 옵션을 설정하지 않은 경우 기본적으로 임시 액세스가 허용되지 않습니다.  
  
 원격 OLE DB 데이터 원본에 액세스할 때 트러스트된 연결의 로그인 ID는 클라이언트가 쿼리 중인 서버에 연결되어 있는 서버에서 자동으로 위임되지 않습니다. 이 경우 인증 위임을 구성해야 합니다.  
  
 OLE DB 공급자가 지정된 데이터 원본에서 여러 카탈로그와 스키마를 지원하는 경우에는 카탈로그 이름과 스키마 이름이 필요합니다. 에 대 한 값 *카탈로그* 및 *스키마* OLE DB 공급자에서 지원 하지 않는 경우 생략할 수 있습니다. 공급자는 폼의 두 부분으로 된 이름을 스키마 이름만 지 원하는 경우 *스키마***.** *개체* 지정 해야 합니다. 공급자 형식의 세 부분으로 이루어진 이름을 카탈로그 이름만 지 원하는 경우 *카탈로그***.** *스키마***.** *개체* 지정 해야 합니다. 통과 쿼리의 세 부분으로 된 이름을 지정 해야 사용는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. 자세한 내용은 참조 [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`변수를 인수로 받아들이지 않습니다.  
  
 호출에 `OPENDATASOURCE`, `OPENQUERY`, 또는 `OPENROWSET` 에 `FROM` 절에서에서 평가 됩니다 별도로 고 독립적으로 업데이트를 대상으로 사용 되는 이러한 함수를 호출할 때와 동일한 인수가 두 호출에 제공 되는 경우에 합니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>BULK 옵션이 있는 OPENROWSET 사용  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 향상된 기능은 OPENROWSET(BULK...) 함수를 지원합니다.  
  
-   와 함께 사용 되는 FROM 절 `SELECT` 호출할 수 `OPENROWSET(BULK...)` 전체 테이블 이름 대신 `SELECT` 기능입니다.  
  
     `OPENROWSET`와 `BULK` 옵션에서 범위 변수 또는 별칭이 라고도 상관 관계 이름이 필요는 `FROM` 절. 열 별칭을 지정할 수 있습니다. 열 별칭 목록을 지정하지 않은 경우에는 서식 파일에 반드시 열 이름이 있어야 합니다. 열 별칭을 지정하면 서식 파일의 열 이름은 무시됩니다. 다음 예를 참조하십시오.  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    추가할 수는 `AS <table_alias>` 는 오류가 발생 합니다.    
>    메시지 491, 수준 16, 상태 1, 줄 20    
>    FROM 절의 대량 행 집합에 대해 상관 관계 이름을 지정해야 합니다.    
  
-   A `SELECT...FROM OPENROWSET(BULK...)` 문은 파일의 데이터를 직접 쿼리 데이터를 테이블로 가져오지 않고 합니다. `SELECT…FROM OPENROWSET(BULK...)`문은 열 이름 및 데이터 형식을 지정 하려면 서식 파일을 사용 하 여 대량 열 별칭을 나열할 수도 있습니다.  
  
-   사용 하 여 `OPENROWSET(BULK...)` 원본 테이블로 `INSERT` 또는 `MERGE` 문을 대량 데이터 파일에서 데이터를 가져오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 자세한 내용은 참조 [를 사용 하 여 BULK INSERT 또는 openrowset&#40; 하 여 데이터 대량 가져오기 대량... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   때는 `OPENROWSET BULK` 옵션은 함께 사용할 프로그램 `INSERT` 문, BULK 절은 테이블 힌트를 지원 합니다. 일반적인 외에도 테이블 힌트를 같은 `TABLOCK`, `BULK` 절에는 다음과 같은 특수 테이블 힌트도 사용할 수 있습니다: `IGNORE_CONSTRAINTS` (만 무시는 `CHECK` 및 `FOREIGN KEY` 제약 조건), `IGNORE_TRIGGERS`, `KEEPDEFAULTS`, 및 `KEEPIDENTITY`합니다. 자세한 내용은 [테이블 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)를 참조하세요.  
  
 사용 하는 방법에 대 한 내용은 `INSERT...SELECT * FROM OPENROWSET(BULK...)` 참조 [대량 가져오기 및 데이터의 내보내기 &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). 대량 가져오기로 수행된 행 삽입 작업이 트랜잭션 로그에 기록되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
> [!NOTE]  
>  사용 하는 경우 `OPENROWSET`를 이해 하는 방법을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 가장을 처리 합니다. 보안 고려 사항에 대 한 정보를 참조 하십시오. [를 사용 하 여 BULK INSERT 또는 openrowset&#40; 하 여 데이터 대량 가져오기 대량... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>SQLCHAR, SQLNCHAR 또는 SQLBINARY 데이터 대량 가져오기  
 OPENROWSET(BULK...)은 지정되지 않은 경우 SQLCHAR, SQLNCHAR 또는 SQLBINARY 데이터의 최대 길이가 8000바이트를 초과하지 않는다고 가정합니다. 가져올 데이터를 포함 하는 LOB 데이터 필드에 있으면 **varchar (max)**, **nvarchar (max)**, 또는 **varbinary (max)** 사용 해야 합니다를 8000 바이트를 초과 하는 개체는 데이터 필드에 대 한 최대 길이 정의 하는 XML 서식 파일 최대 길이를 지정하려면 서식 파일을 편집하고 MAX_LENGTH 특성을 선언합니다.  
  
> [!NOTE]  
>  자동으로 생성된 서식 파일은 LOB 필드의 길이 또는 최대 길이를 지정하지 않습니다. 그러나 직접 서식 파일을 편집하고 길이 또는 최대 길이를 지정할 수 있습니다.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기  
 SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.  
  
|데이터 형식|영향|  
|---------------|------------|  
|SQLCHAR 또는 SQLVARYCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다.|  
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다.|  
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|  
  
## <a name="permissions"></a>Permissions  
 `OPENROWSET`권한은 OLE DB 공급자에 전달 되는 사용자 이름의 사용 권한에 의해 결정 됩니다. 사용 하 여 `BULK` 옵션을 사용 하려면 `ADMINISTER BULK OPERATIONS` 권한.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>1. SELECT 및 SQL Server Native Client OLE DB 공급자와 함께 OPENROWSET 사용  
 다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 액세스 하는 `HumanResources.Department` 테이블에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 원격 서버의 데이터베이스 `Seattle1`합니다. SQLNCLI를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자로 리디렉션됩니다. `SELECT` 문은 반환되는 행 집합을 정의하는 데 사용됩니다. 공급자 문자열에는 `Server` 및 `Trusted_Connection` 키워드가 포함됩니다. 이러한 키워드에서 인식 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다.  
  
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
>  이 예에서는 Access가 설치되어 있다고 가정합니다. 이 예를 실행하려면 Northwind 데이터베이스를 설치해야 합니다.  
  
```sql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>3. INNER JOIN에서 OPENROWSET 및 다른 테이블 사용  
 다음 예제에서는 모든 데이터를 선택는 `Customers` 의 로컬 인스턴스에서 테이블 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` 데이터베이스와는 `Orders` 테이블 액세스에서 `Northwind` 동일한 컴퓨터에 저장 된 데이터베이스입니다.  
  
> [!NOTE]  
>  이 예에서는 Access가 설치되어 있다고 가정합니다. 이 예를 실행하려면 Northwind 데이터베이스를 설치해야 합니다.  
  
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
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>4. OPENROWSET를 사용하여 varbinary(max) 열에 파일 데이터 대량 삽입  
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
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>5. OPENROWSET BULK 공급자를 서식 파일과 함께 사용하여 텍스트 파일의 행 검색  
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
  
### <a name="f-specifying-a-format-file-and-code-page"></a>6. 서식 파일 및 코드 페이지 지정  
 다음 예제에서는 서식 파일 및 코드 페이지 옵션 모두 동시에 사용 하는 방법을 보여 줍니다.  
  
```sql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>7. 서식 파일을 사용 하는 CSV 파일에서 데이터에 액세스  
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>8. 서식 파일 없이 CSV 파일에서 데이터에 액세스

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>9. Azure Blob 저장소에 저장 된 파일에서 데이터에 액세스   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
다음 예제에서는 Azure 저장소 계정 및 공유 액세스 서명을 생성 하는 데이터베이스 범위 자격 증명에서 컨테이너를 가리키는 외부 데이터 원본을 사용 합니다.     

```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
에 대 한 완료 `OPENROWSET` 자격 증명 및 외부 데이터 원본을 구성 하는 등 예제 참조 [예의 대량 데이터에에서 액세스를 Azure Blob 저장소](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)합니다.
 
### <a name="additional-examples"></a>추가 예  
 사용 하 여 보여 주는 추가 예에 대 한 `INSERT...SELECT * FROM OPENROWSET(BULK...)`, 다음 항목을 참조 합니다.  
  
-   [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40; Transact SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [행 집합 함수 &#40; Transact SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
