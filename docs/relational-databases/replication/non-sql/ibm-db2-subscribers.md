---
title: IBM DB2 구독자 | Microsoft 문서
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 091bc3b0ab56006e12064f6b873d419b4e0c5a7d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672382"
---
# <a name="ibm-db2-subscribers"></a>IBM DB2 Subscribers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration Server와 함께 제공되는 OLE DB 공급자를 통해 IBM DB2/AS 400, DB2/MVS 및 DB2/Universal Database에 대한 밀어넣기 구독을 지원합니다.  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>IBM DB2 구독자 구성  
 IBM DB2 구독자를 구성하려면 다음 단계를 따르십시오.  
  
1.  배포자에 최신 버전의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for DB2를 설치합니다.  
  
    -   [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition을 사용하는 경우 [SQL Server 다운로드](https://go.microsoft.com/fwlink/?LinkId=149256) 웹 페이지의 **관련 다운로드** 섹션에서 Microsoft SQL Server Feature Pack의 최신 버전에 대한 링크를 클릭합니다. **Microsoft SQL Server Feature Pack** 웹 페이지에서 **Microsoft OLE DB Provider for DB2**를 검색합니다.  
  
    -   [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Standard Edition을 사용하는 경우 해당 공급자가 포함된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] HIS(Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]) 서버의 최신 버전을 설치합니다.  
  
     공급자 설치 외에 다음 단계에서 사용되는 데이터 액세스 도구도 설치하는 것이 좋습니다. 이 도구는 [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition 다운로드 시 기본적으로 설치됩니다. 데이터 액세스 도구 설치 및 사용 방법은 공급자 설명서나 HIS 설명서를 참조하십시오.  
  
2.  구독자에 대한 연결 문자열을 만듭니다. 연결 문자열은 일반적인 텍스트 편집기로 만들 수 있지만 데이터 액세스 도구를 사용하는 것이 좋습니다. 데이터 액세스 도구에서 문자열을 만들려면 다음 작업을 수행하십시오.  
  
    1.  **시작**, **프로그램**, **Microsoft OLE DB Provider for DB2**를 클릭한 다음 **데이터 액세스 도구**를 클릭합니다.  
  
    2.  **데이터 액세스 도구**의 단계에 따라 DB2 서버에 대한 정보를 제공합니다. 도구의 단계를 모두 완료하면 관련 연결 문자열을 사용하여 유니버설 데이터 링크(UDL)가 생성됩니다. 실제로 복제에서는 UDL이 아닌 연결 문자열을 사용합니다.  
  
    3.  연결 문자열에 액세스합니다. 데이터 액세스 도구에서 UDL을 마우스 오른쪽 단추로 클릭하고 **연결 문자열 표시**를 선택합니다.  
  
     다음은 연결 문자열의 예입니다. 이 예에서는 읽기 쉽도록 줄 바꿈을 넣었습니다.  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Derive Parameters=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     이 문자열의 옵션 대부분은 구성 중인 DB2 서버와만 관련이 있지만 `Process Binary as Character` 및 `Derive Parameters` 옵션은 항상 `False`로 설정해야 합니다. 구독 데이터베이스를 식별하려면 `Initial Catalog` 옵션 값을 지정해야 합니다. 연결 문자열은 구독을 만들 때 새 구독 마법사에서 입력합니다.  
  
3.  스냅숏 또는 트랜잭션 게시를 만든 후[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자에 대해 설정한 다음 구독자에 대한 밀어넣기 구독을 만듭니다. 자세한 내용은 [SQL Server 이외 구독자에 대한 구독 만들기](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)을 참조하세요.  
  
4.  필요에 따라 하나 이상의 아티클에 대해 사용자 지정 생성 스크립트를 지정할 수 있습니다. 테이블이 게시되면 해당 테이블에 대한 `CREATE TABLE` 스크립트가 생성됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자의 경우 이 스크립트는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 언어로 생성된 다음 구독자에서 적용되기 전에 배포 에이전트에서 보다 일반적인 SQL 언어로 번역됩니다. 사용자 지정 생성 스크립트를 지정하려면 기존 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정하거나 DB2 SQL 언어를 사용하는 완전한 스크립트를 만듭니다. DB2 스크립트를 만드는 경우에는 **bypass_translation** 지시어를 사용하여 배포 에이전트가 구독자에서 번역 과정 없이 스크립트를 적용하도록 합니다.  
  
     여러 가지 이유로 스크립트를 수정할 수 있지만 가장 일반적인 이유는 데이터 형식 매핑을 변경하기 위해 수정합니다. 자세한 내용은 이 항목의 "데이터 형식 매핑 고려 사항" 섹션을 참조하십시오. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 수정하는 경우에는 데이터 형식 매핑 변경 시에만 스크립트를 변경해야 합니다. 그리고 스크립트에 주석이 포함되어서는 안 됩니다. 더 많은 변경이 필요하면 DB2 스크립트를 만듭니다.  
  
     **아티클 스크립트를 수정하고 사용자 지정 생성 스크립트로 제공하려면**  
  
    1.  게시에 대해 스냅숏을 생성한 후 게시에 대한 스냅숏 폴더로 이동합니다.  
  
    2.  `MyArticle.sch` 등 아티클과 같은 이름의 `.sch` 파일을 찾습니다.  
  
    3.  메모장 또는 다른 텍스트 편집기를 사용하여 이 파일을 엽니다.  
  
    4.  파일을 수정하고 다른 디렉터리에 저장합니다.  
  
    5.  *creation_script* 속성에 파일 경로 및 이름을 지정하여 `sp_changearticle`을 실행합니다. 자세한 내용은 [sp_changearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)을 참조하세요.  
  
     **아티클 스크립트를 만들어서 사용자 지정 생성 스크립트로 제공하려면**  
  
    1.  DB2 SQL 언어를 사용하여 아티클 스크립트를 만듭니다. 파일의 첫 줄에는 **bypass_translation**만 있어야 합니다.  
  
    2.  *creation_script* 속성에 파일 경로 및 이름을 지정하여 sp_changearticle을 실행합니다.  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>IBM DB2 구독자에 대한 고려 사항  
 DB2 구독자로 복제할 때 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)항목에서 다룬 고려 사항은 물론 다음 사항도 고려해야 합니다.  
  
-   복제된 각 테이블의 데이터 및 인덱스는 DB2 테이블스페이스에 할당됩니다. DB2 테이블스페이스의 페이지 크기는 테이블스페이스에 속하는 테이블의 최대 열 개수와 최대 행 크기를 제어합니다. 복제된 테이블과 연결된 테이블스페이스가 복제된 열의 개수 및 테이블의 최대 행 크기에 따라 적절한지 확인합니다.  
  
-   테이블에 있는 하나 이상의 기본 키 열이 DECIMAL(32-38, 0-38) 또는 NUMERIC(32-38, 0-38) 데이터 형식이면 트랜잭션 복제를 사용하여 테이블을 DB2 구독자로 게시해서는 안 됩니다. 트랜잭션 복제에서는 기본 키를 사용하여 행을 식별하는데 이 데이터 형식은 구독자에서 VARCHAR(41)로 매핑되므로 오류가 발생할 수 있습니다. 기본 키에서 이러한 데이터 형식을 사용하는 테이블은 스냅숏 복제를 사용하여 게시할 수 있습니다.  
  
-   복제에서 테이블을 만드는 대신 구독자에서 테이블을 미리 만들려면 replication support only 옵션을 사용합니다. 자세한 내용은 [스냅숏 없이 트랜잭션 구독 초기화](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)에서 수동으로 구독을 초기화하는 방법에 대해 설명합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 DB2에서 지원되는 길이보다 긴 테이블 이름과 열 이름을 사용할 수 있습니다.  
  
    -   게시 데이터베이스에 있는 테이블의 이름이 DB2 구독자에서 지원되는 이름보다 긴 경우에는 destination_table 아티클 속성에 대체 이름을 지정합니다. 게시 생성 시 속성을 설정하는 방법은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.  
  
    -   대체 열 이름은 지정할 수 없습니다. DB2 구독자에서 지원되는 이름의 길이보다 긴 이름의 열이 게시된 테이블에 포함되어 있는지 확인해야 합니다.  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>SQL Server에서 IBM DB2로 데이터 형식 매핑  
 다음 표에서는 IBM DB2를 실행하는 구독자로 데이터를 복제할 때 사용되는 데이터 형식 매핑을 보여 줍니다.  
  
|SQL Server 데이터 형식|IBM DB2 데이터 형식|  
|--------------------------|-----------------------|  
|**bigint**|DECIMAL(19,0)|  
|**binary(1-254)**|CHAR(1-254) FOR BIT DATA|  
|**binary(255-8000)**|VARCHAR(255-8000) FOR BIT DATA|  
|**bit**|SMALLINT|  
|**char(1-254)**|CHAR(1-254)|  
|**char(255-8000)**|VARCHAR(255-8000)|  
|**date**|DATE|  
|**datetime**|timestamp|  
|**datetime2(0-7)**|VARCHAR(27)|  
|**datetimeoffset(0-7)**|VARCHAR(34)|  
|**decimal(1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**decimal(32-38, 0-38)**|VARCHAR(41)|  
|**float(53)**|DOUBLE|  
|**float**|FLOAT|  
|**geography**|IMAGE|  
|**geometry**|IMAGE|  
|**hierarchyid**|IMAGE|  
|**image**|VARCHAR(0) FOR BIT DATA*|  
|**into**|INT|  
|**money**|DECIMAL(19,4)|  
|**nchar(1-4000)**|VARCHAR(1-4000)|  
|**ntext**|VARCHAR(0)*|  
|**numeric(1-31, 0-31)**|DECIMAL(1-31,0-31)|  
|**numeric(32-38, 0-38)**|VARCHAR(41)|  
|**nvarchar(1-4000)**|VARCHAR(1-4000)|  
|**nvarchar(max)**|VARCHAR(0)*|  
|**real**|real|  
|**smalldatetime**|timestamp|  
|**smallint**|SMALLINT|  
|**smallmoney**|DECIMAL(10,4)|  
|**sql_variant**|해당 사항 없음|  
|**sysname**|VARCHAR(128)|  
|**text**|VARCHAR(0)*|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|CHAR(8) FOR BIT DATA|  
|**tinyint**|SMALLINT|  
|**uniqueidentifier**|CHAR (38)|  
|**varbinary(1-8000)**|VARCHAR(1-8000) FOR BIT DATA|  
|**varchar(1-8000)**|VARCHAR(1-8000)|  
|**varbinary(max)**|VARCHAR(0) FOR BIT DATA*|  
|**varchar(max)**|VARCHAR(0)*|  
|**xml**|VARCHAR(0)*|  
  
* VARCHAR(0)로의 매핑에 대한 자세한 내용은 다음 섹션을 참조하세요.  
  
### <a name="data-type-mapping-considerations"></a>데이터 형식 매핑 고려 사항  
 DB2 구독자로 복제 시 데이터 형식 매핑과 관련된 다음 사항을 고려해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 **char**, **varchar**, **binary** 및 **varbinary**를 각각 DB2의 CHAR, VARCHAR, CHAR FOR BIT DATA 및 VARCHAR FOR BIT DATA에 매핑하면 복제에서 DB2 데이터 형식의 길이를 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식의 길이와 같게 설정합니다.  
  
     이렇게 하면 DB2의 페이지 크기를 최대 행 크기를 수용할 수 있을 정도로 늘릴 수 있는 한 생성된 테이블을 구독자에서 성공적으로 만들 수 있습니다. DB2 데이터베이스에 액세스하는 데 사용되는 로그인은 테이블을 DB2로 복제할 수 있는 충분한 크기의 테이블 공간에 액세스할 수 있어야 합니다.  
  
-   DB2는 최대 32KB의 VARCHAR 열을 지원할 수 있으므로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 일부 큰 개체 열을 DB2 VARCHAR 열로 적절하게 매핑할 수 있습니다. 그러나 복제에서 사용하는 DB2용 OLE DB 공급자에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 큰 개체를 DB2의 큰 개체로 매핑할 수 없습니다. 따라서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **text**, **varchar(max)**, **ntext**및 **nvarchar(max)** 열은 생성된 생성 스크립트에서 VARCHAR(0)에 매핑됩니다. 길이 값 0은 스크립트를 구독자에 적용하기 전에 적절한 값으로 바꾸어야 합니다. 데이터 형식의 길이를 변경하지 않으면 DB2 구독자에서 테이블을 만들려고 할 때 DB2에서 오류 604가 발생합니다. 오류 604는 데이터 형식의 전체 자릿수나 길이 특성이 유효하지 않음을 나타냅니다.  
  
     복제하는 원본 테이블에 대한 지식을 바탕으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 큰 개체를 가변 길이의 DB2 항목에 매핑하는 것이 적절한지 결정하고 사용자 지정 생성 스크립트에 적절한 최대 길이를 지정합니다. 사용자 지정 생성 스크립트 지정 방법은 이 항목의 "IBM DB2 구독자 구성" 섹션에서 5단계를 참조하십시오.  
  
    > [!NOTE]  
    >  DB2 형식에 지정한 길이와 다른 열 길이를 더한 값은 테이블 데이터가 할당되는 DB2 테이블 공간을 기준으로 설정되는 최대 행 크기를 초과할 수 없습니다.  
  
     큰 개체 열에 대한 적절한 매핑이 없으면 열이 복제되지 않도록 아티클에 대해 열 필터링을 사용해 보십시오. 자세한 내용은 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 **nchar** 및 **nvarchar**를 DB2의 CHAR 및 VARCHAR로 복제하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 형식과 DB2 형식에 같은 길이 지정자가 사용됩니다. 그러나 데이터 형식의 길이가 생성된 DB2 테이블에 비해 너무 작을 수도 있습니다.  
  
     일부 DB2 환경에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char** 데이터 항목의 문자가 싱글바이트로 제한되지는 않으므로 CHAR 또는 VARCHAR 항목의 길이를 정할 때 이를 고려해야 합니다. 또한 필요한 경우 *시프트 인* 및 *시프트 아웃* 문자를 사용해 볼 수 있습니다. **nchar** 열과 **nvarchar** 열이 있는 테이블을 복제하는 경우 사용자 지정 생성 스크립트로 해당 데이터 형식에 보다 큰 최대 길이를 지정할 수도 있습니다. 사용자 지정 생성 스크립트 지정 방법은 이 항목의 "IBM DB2 구독자 구성" 섹션에서 5단계를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
