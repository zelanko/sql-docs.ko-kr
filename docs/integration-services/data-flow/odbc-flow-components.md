---
title: ODBC 흐름 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e59efeb278c7d5f1236a9943f03ad471491f354a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726655"
---
# <a name="odbc-flow-components"></a>ODBC 흐름 구성 요소

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 항목에서는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]용 Connector for ODBC(Open Database Connectivity)는 SSIS 개발자가 데이터를 ODBC 지원 데이터베이스로 로드하거나 해당 데이터베이스에서 언로드하는 패키지를 쉽게 만드는 데 도움이 됩니다.  
  
 ODBC Connector는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]의 컨텍스트에서 데이터를 ODBC 지원 데이터베이스로 로드하거나 해당 데이터베이스에서 언로드할 때 최적의 성능을 얻기 위해 디자인되었습니다.  
  
## <a name="benefits"></a>이점  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 용 ODBC 원본 및 ODBC 대상은 데이터를 ODBC 지원 데이터베이스로 로드하거나 해당 데이터베이스에서 언로드하는 프로젝트에서 SSIS를 위한 경쟁 우위를 제공합니다.  
  
 ODBC 원본과 ODBC 대상 모두 ODBC 사용 데이터베이스와의 고성능 데이터 통합을 가능하게 만듭니다. 두 구성 요소 모두 이 바인딩 모드를 지원하는 고기능 ODBC 공급자를 위해 행 단위 매개 변수 배열 바인딩과 함께 작동하도록 구성하고 저기능 ODBC 공급자를 위해 단일 행 매개 변수 바인딩과 함께 작동하도록 구성할 수 있습니다.  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>ODBC 원본 및 대상 시작  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]를 사용하는 패키지를 설정하려면 먼저 다음을 사용할 수 있는지 확인해야 합니다.  
  
-   [ODBC 원본](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 대상](../../integration-services/data-flow/odbc-destination.md)  
  
 ODBC 원본 및 ODBC 대상을 사용하면 쉽게 데이터를 로드 및 언로드하고 ODBC 지원 원본 데이터베이스에서 ODBC 지원 대상 데이터베이스로 데이터를 전송할 수 있습니다.  
  
 원본 또는 대상을 사용하여 데이터를 로드 또는 언로드하려면 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 새 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]프로젝트를 엽니다. 그런 다음 원본 또는 대상을 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 디자인 화면으로 끌어 옵니다.  
  
-   ODBC 원본 구성 요소는 원본 ODBC 지원 데이터베이스에서 데이터를 읽습니다.  
  
 ODBC 원본을 임의의 대상에 연결하거나 SSIS가 지원하는 구성 요소를 변환할 수 있습니다.  
  
 **참고 항목:**  
  
 ODBC 원본  
  
 ODBC 원본 편집기(연결 관리자 페이지)  
  
 ODBC 원본 편집기(오류 출력 페이지)  
  
-   ODBC 대상은 ODBC 지원 데이터베이스로 데이터를 로드합니다. 대상을 임의의 원본에 연결하거나 SSIS가 지원하는 구성 요소를 변환합니다.  
  
 **참고 항목:**  
  
 ODBC 대상  
  
 ODBC 대상 편집기(연결 관리자 페이지)  
  
 ODBC 대상 편집기(오류 출력 페이지)  
  
## <a name="operating-scenarios"></a>운영 시나리오  
 이 섹션에서는 ODBC 원본 및 대상 구성 요소의 주된 용도 중 일부를 설명합니다.  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>SQL Server 테이블에서 임의의 ODBC 지원 데이터베이스 테이블로 데이터 대량 복사  
 구성 요소를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 단일 ODBC 지원 데이터베이스 테이블로 데이터를 대량 복사할 수 있습니다.  
  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 데이터를 추출하여 DB2 테이블로 로드하는 SSIS 데이터 흐름 태스크를 만드는 방법을 보여 줍니다.  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]프로젝트를 만듭니다.  
  
-   복사할 데이터가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 OLE DB 연결 관리자를 만듭니다.  
  
-   로컬 또는 원격 DB2 데이터베이스를 가리키는 DSN이 지정된 로컬에 설치된 DB2 ODBC 드라이버를 사용하는 ODBC 연결 관리자를 만듭니다. 이 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터가 로드되는 위치입니다.  
  
-   OLE DB 원본을 디자인 화면으로 끌어 온 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 추출할 데이터가 포함된 테이블에서 데이터를 가져오도록 원본을 구성합니다. 이전에 만든 OLE DB 연결 관리자를 사용합니다.  
  
-   ODBC 대상을 디자인 화면으로 끌어 오고 원본 출력을 ODBC 대상에 연결한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 추출한 데이터가 포함된 DB2 테이블로 데이터를 로드하도록 대상을 구성합니다. 이전에 만든 ODBC 연결 관리자를 사용합니다.  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>SQL 지원 데이터베이스 테이블에서 임의의 SQL Server 테이블로 데이터 대량 복사  
 구성 요소를 사용하여 하나 이상의 ODBC 지원 데이터베이스 테이블에서 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 테이블로 데이터를 대량 복사할 수 있습니다.  
  
 다음 예에서는 Sybase 데이터베이스 테이블에서 데이터를 추출하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 테이블로 로드하는 SSIS 데이터 흐름 태스크를 만드는 방법을 보여 줍니다.  
  
-   다음에서 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 프로젝트를 만듭니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   로컬 또는 원격 Sybase 데이터베이스를 가리키는 DSN이 지정된 로컬에 설치된 Sybase ODBC 드라이버를 사용하는 ODBC 연결 관리자를 만듭니다. 이 데이터베이스는 데이터가 추출되는 위치입니다.  
  
-   데이터를 로드할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 OLE DB 연결 관리자를 만듭니다.  
  
-   ODBC 원본을 디자인 화면으로 끌어 온 다음 복사할 데이터가 포함된 Sybase 테이블에서 데이터를 가져오도록 원본을 구성합니다. 이전에 만든 ODBC 연결 관리자를 사용합니다.  
  
-   OLE DB 대상을 디자인 화면으로 끌어 오고 원본 출력을 OLE DB 대상에 연결한 다음 Sybase 데이터베이스에서 추출하는 데이터가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 데이터를 로드하도록 대상을 구성합니다. 이전에 만든 OLE DB 연결 관리자를 사용합니다.  
  
## <a name="supported-data-types"></a>지원되는 데이터 형식  
 ODBC 대량 SSIS 구성 요소는 큰 개체(CLOB 및 BLOB)에 대한 지원을 포함하여 모든 기본 제공 ODBC 데이터 형식에 대한 지원을 제공합니다.  
  
ODBC 3.8 사양에 설명된 대로 확장 가능한 C 형식에 대한 데이터 형식 지원은 없습니다. 다음 표에서는 각 ODBC SQL 형식에 사용되는 SSIS 데이터 형식을 설명합니다. SSIS 개발자는 필요한 데이터 변환 작업의 성능에 영향을 주지 않으면서 기본 매핑을 무시하고 입력/출력 열에 다른 SSIS 데이터 형식을 지정할 수 있습니다.  
  
|ODBC SQL 형식|SSIS 데이터 형식|주석|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|ODBC 드라이버가 해당 SQL 데이터 형식에 대해 UNSIGNED_ATTRIBUTE를 SQL_TRUE로 설정하면 SQL 데이터 형식이 SSIS 부호 없는 형식(DT_UI1, DT_UI2, DT_UI4, DT_UI8)에 매핑됩니다.|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|ODBC 드라이버가 해당 SQL 데이터 형식에 대해 UNSIGNED_ATTRIBUTE를 SQL_TRUE로 설정하면 SQL 데이터 형식이 SSIS 부호 없는 형식(DT_UI1, DT_UI2, DT_UI4, DT_UI8)에 매핑됩니다.|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|ODBC 드라이버가 해당 SQL 데이터 형식에 대해 UNSIGNED_ATTRIBUTE를 SQL_TRUE로 설정하면 SQL 데이터 형식이 SSIS 부호 없는 형식(DT_UI1, DT_UI2, DT_UI4, DT_UI8)에 매핑됩니다.|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|ODBC 드라이버가 해당 SQL 데이터 형식에 대해 UNSIGNED_ATTRIBUTE를 SQL_TRUE로 설정하면 SQL 데이터 형식이 SSIS 부호 없는 형식(DT_UI1, DT_UI2, DT_UI4, DT_UI8)에 매핑됩니다.|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC(p,s)|DT_NUMERIC(p,s)|P가 38보다 크거나 같고 S가 0보다 크거나 같으며 S가 P보다 작거나 같으면 숫자 데이터 형식이 DT_NUMERIC에 매핑됩니다.|  
||DT_R8|다음 중 하나 이상이 참이면 숫자 데이터 형식이 DT_R8에 매핑됩니다.<br /><br />전체 자릿수가 38보다 큼<br /><br />소수 자릿수가 0보다 작음<br /><br />소수 자릿수가 38보다 큼<br /><br />소수 자릿수가 전체 자릿수보다 큼|  
||DT_CY|숫자 데이터 형식이 money 데이터 형식으로 선언되면 숫자 데이터 형식이 DT_CY에 매핑됩니다.|  
|SQL_DECIMAL(p, s)|DT_NUMERIC(p,s)|P가 38보다 크거나 같고 S가 0보다 크거나 같으며 S가 P보다 작거나 같으면 decimal 데이터 형식이 DT_NUMERIC에 매핑됩니다.|  
||DT_R8|다음 중 하나 이상이 참이면 decimal 데이터 형식이 DT_R8에 매핑됩니다.<br /><br />전체 자릿수가 38보다 큼<br /><br />소수 자릿수가 0보다 작음<br /><br />소수 자릿수가 38보다 큼<br /><br />소수 자릿수가 전체 자릿수보다 큼|  
||DT_CY|decimal 데이터 형식이 money 데이터 형식으로 선언되면 decimal 데이터 형식이 DT_CY에 매핑됩니다.|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|소수 자릿수가 3보다 크면 SQL_TIMESTAMP 데이터 형식이 DT_DBTIMESTAMP2에 매핑됩니다. 다른 모든 경우에는 DT_DBTIMESTAMP에 매핑됩니다.|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|열 길이가 8000보다 작거나 같고 **ExposeStringsAsUnicode** 속성이 false이면 DT_STR이 사용됩니다.<br /><br />열 길이가 8000보다 작거나 같고 **ExposeStringsAsUnicode** 속성이 true이면 DT_WSTR이 사용됩니다.<br /><br />열 길이가 8000보다 크고 **ExposeStringsAsUnicode** 속성이 false이면 DT_TEXT가 사용됩니다.<br /><br />열 길이가 8000보다 크고 **ExposeStringsAsUnicode** 속성이 true이면 DT_NTEXT가 사용됩니다.|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|**ExposeStringsAsUnicode** 속성이 true이면 DT_NTEXT가 사용됩니다.|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|열 길이가 4000보다 작거나 같으면 DT_WSTR이 사용됩니다.<br /><br />열 길이가 4000보다 크면 DT_NTEXT가 사용됩니다.|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|열 길이가 8000보다 작거나 같으면 DT_BYTES가 사용됩니다.<br /><br />열 길이가 8000보다 크면 DT_IMAGE가 사용됩니다.|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|공급자별 데이터 형식|DT_BYTES<br /><br />DT_IMAGE|열 길이가 8000보다 작거나 같으면 DT_BYTES가 사용됩니다.<br /><br />열 길이가 0이거나 8000보다 크면 DT_IMAGE가 사용됩니다.|  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC 원본](../../integration-services/data-flow/odbc-source.md)  
  
-   [ODBC 대상](../../integration-services/data-flow/odbc-destination.md)  
  
 
