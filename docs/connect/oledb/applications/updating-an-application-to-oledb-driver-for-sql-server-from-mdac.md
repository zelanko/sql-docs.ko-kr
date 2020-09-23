---
title: MDAC에서 SQL Server용 OLE DB 드라이버로 애플리케이션 업데이트
description: 새 OLE DB Driver for SQL Server에서 변경된 내용과 새 드라이버를 업데이트하기 위해 알아야 할 사항을 살펴봅니다.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b531dbde34faab6995a3e4765156ccaa71f4324e
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860667"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>MDAC에서 SQL Server용 OLE DB 드라이버로 애플리케이션 업데이트
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버 및 MDAC(Microsoft Data Access Components) 사이에는 많은 차이점이 있습니다. Windows Vista부터 이제 데이터 액세스 구성 요소를 Windows Data Access Components 또는 Windows DAC라고 합니다. 양쪽 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 네이티브 데이터에 액세스하기 위한 것이지만, SQL Server용 OLE DB 드라이버는 특히 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 새 기능을 노출하도록 설계되었으며 동시에 이전 버전과의 호환성도 유지합니다.   

 또한 MDAC에는 OLE DB, ODBC 및 ADO(ActiveX Data Objects)를 사용하기 위한 구성 요소가 포함되어 있지만 OLE DB Driver for SQL Server는 OLE DB만 구현합니다(단, ADO는 OLE DB Driver for SQL Server의 기능에 액세스할 수 있음).  

 OLE DB Driver for SQL Server와 MDAC는 다음과 같은 영역이 다릅니다.  

-   ADO를 사용하여 OLE DB Driver for SQL Server에 액세스하는 사용자는 SQL OLE DB 공급자에 액세스할 때보다 필터링 기능이 적을 수 있습니다.  

-   ADO 애플리케이션이 OLE DB Driver for SQL Server를 사용하고 계산된 열을 업데이트하는 경우 오류가 보고됩니다. MDAC를 사용하면 업데이트가 허용되지만 무시되었습니다.  

-   OLE DB Driver for SQL Server는 단일 자체 포함 DLL(동적 연결 라이브러리) 파일입니다. 공개적으로 노출되는 인터페이스는 편리한 배포 및 보안 노출 제한을 위해 최소한으로 유지되었습니다.  

-   OLE DB 인터페이스만 지원됩니다.  

-   OLE DB Driver for SQL Server 이름은 MDAC에서 사용되는 이름과 다릅니다.  

-   OLE DB Driver for SQL Server를 사용하는 경우 MDAC 구성 요소에서 제공하는 사용자가 액세스할 수 있는 기능을 사용할 수 있습니다. 여기에는 연결 풀링, ADO 지원 및 클라이언트 커서 지원이 포함되지만 이에 제한되지 않습니다. 이러한 기능 중 하나를 사용하는 경우 OLE DB Driver for SQL Server는 데이터베이스 연결만 제공합니다. MDAC는 추적, 관리 컨트롤 및 성능 카운터와 같은 기능을 제공합니다.  

-   애플리케이션은 SQL Server용 OLE DB 드라이버와 함께 OLE DB 핵심 서비스를 사용할 수 있지만, OLE DB 커서 엔진을 사용하는 경우 커서 엔진이 새로운 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 데이터 형식을 모르기 때문에 발생할 수 있는 잠재적 문제를 방지하기 위해 데이터 형식 호환성 옵션을 사용해야 합니다.  

-   OLE DB Driver for SQL Server는 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 액세스를 지원합니다.  

-   OLE DB Driver for SQL Server에는 XML 통합이 포함되어 있지 않습니다. OLE DB Driver for SQL Server는 SELECT ... FOR XML 쿼리를 지원하지만 다른 XML 기능은 지원하지 않습니다. 그러나 OLE DB Driver for SQL Server는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 **xml** 데이터 형식을 지원합니다.  

-   SQL Server용 OLE DB 드라이버는 연결 문자열 특성만 사용하여 클라이언트 쪽 네트워크 라이브러리 구성을 지원합니다. 보다 완전한 네트워크 라이브러리 구성이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용해야 합니다.  

-   MDAC 연결 문자열은 **Trusted_Connection** 키워드에 부울 값(**true**)을 허용합니다. OLE DB Driver for SQL Server 연결 문자열은 **예** 또는 **아니요**를 사용해야 합니다.  

-   경고와 오류가 약간 변경되었습니다. 이제 서버에서 반환되는 경고와 오류가 SQL Server용 OLE DB 드라이버로 전달될 때 동일한 심각도를 유지합니다. 특정 경고 및 오류 트래핑을 사용하는 경우 애플리케이션을 완전히 테스트해야 합니다.  

-   SQL Server용 OLE DB 드라이버에는 MDAC보다 엄격한 오류 검사 기능이 있으므로 OLE DB 사양을 엄격하게 준수하지 않는 일부 애플리케이션이 다르게 동작할 수 있습니다. 예를 들어 SQLOLEDB 공급자는 결과 매개 변수의 경우 매개 변수 이름이 '\@'로 시작해야 한다는 규칙을 적용하지 않지만 SQL Server용 OLE DB 드라이버는 이 규칙을 적용합니다.  

-   OLE DB Driver for SQL Server는 실패한 연결에 대해 MDAC와 다르게 동작합니다. 예를 들어 MDAC는 실패한 연결에 대해 캐시된 속성 값을 반환하지만 SQL Server용 OLE DB 드라이버는 호출 애플리케이션에 오류를 보고합니다.  

-   SQL Server용 OLE DB 드라이버는 Visual Studio 분석기 이벤트를 생성하지 않고 대신 Windows 추적 이벤트를 생성합니다.  

-   OLE DB Driver for SQL Server는 perfmon과 함께 사용할 수 없습니다. Perfmon은 Windows에 포함된 MDAC SQLODBC 드라이버를 사용하는 DSN에서만 사용할 수 있는 Windows 도구입니다.  

-   OLE DB Driver for SQL Server가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에 연결된 경우 서버 오류 16947이 SQL_ERROR로 반환됩니다. 이 오류는 현재 위치 업데이트나 삭제 시 행이 업데이트 또는 삭제되지 않을 때 발생합니다. 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 MDAC를 사용할 경우 서버 오류 16947이 경고(SQL_SUCCESS_WITH_INFO)로 반환됩니다.  

-   SQL Server용 OLE DB 드라이버는 이전에 구현되지 않았던 선택적 OLE DB 인터페이스인 **IDBDataSourceAdmin** 인터페이스를 구현하지만 이 선택적 인터페이스의 **CreateDataSource** 메서드만 구현됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   SQL Server용 OLE DB 드라이버는 TABLE_TYPE이 SYNONYM으로 설정된 TABLES 및 TABLE_INFO 스키마 행 집합에 동의어를 반환합니다.  

-   [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전 버전의 클라이언트에는 데이터 형식 **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, **udt** 또는 다른 큰 개체 유형의 반환 값을 반환할 수 없습니다. 이러한 형식을 반환 값으로 사용하려는 경우에는 OLE DB Driver for SQL Server를 사용해야 합니다.  

-   MDAC를 사용하면 수동 및 암시적 트랜잭션을 시작할 때 다음 명령문을 실행할 수 있지만 SQL Server용 OLE DB 드라이버에서는 실행할 수 없습니다. 자동 커밋 모드로 이러한 문을 실행해야 합니다.  

    -   모든 전체 텍스트 작업(인덱스 및 카탈로그 DDL)  

    -   모든 데이터베이스 작업(데이터베이스 만들기, 데이터베이스 변경, 데이터베이스 삭제)  

    -   다시 구  

    -   Shutdown  

    -   종료  

    -   Backup  

-   MDAC 애플리케이션이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하면 다음 그림과 같이 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 데이터 형식이 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 호환 데이터 형식으로 나타납니다.  

    |SQL Server 2005 형식|SQL Server 2000 형식|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     이 형식 매핑은 열 메타데이터에 대해 반환되는 값에 영향을 줍니다. 예를 들어 **text** 열의 최대 크기는 2,147,483,647이지만 OLE DB Driver for SQL Server는 플랫폼에 따라 **varchar(max)** 열의 최대 크기를 2,147,483,647 또는 -1로 보고합니다.  

-   SQL Server용 OLE DB 드라이버는 이전 버전과의 호환성을 위해 연결 문자열에서 모호성을 허용합니다. 예를 들어 일부 키워드를 여러 번 지정할 수 있으며 위치나 우선 순위에 따라 충돌하는 키워드를 해결할 수 있습니다. 이후 릴리스의 OLE DB Driver for SQL Server에서는 연결 문자열의 모호성을 허용하지 않을 수 있습니다. SQL Server용 OLE DB 드라이버를 사용하도록 애플리케이션을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  

-   OLE DB 호출을 사용하여 트랜잭션을 시작하는 경우 OLE DB Driver for SQL Server와 MDAC 간에 동작 차이가 있습니다. OLE DB Driver for SQL Server를 사용하면 트랜잭션이 즉시 시작되지만 MDAC를 사용하면 첫 번째 데이터베이스 액세스 후에 트랜잭션이 시작됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 일괄 처리나 저장 프로시저의 실행이 완료된 후의 @@TRANCOUNT가 일괄 처리나 저장 프로시저를 시작할 때와 같아야 하기 때문에 이러한 동작 차이가 저장 프로시저와 일괄 처리의 동작에 영향을 줄 수 있습니다.  

-   OLE DB Driver for SQL Server에서는 ITransactionLocal::BeginTransaction을 사용하면 트랜잭션이 즉시 시작됩니다. MDAC를 사용할 경우 애플리케이션이 암시적 트랜잭션 모드의 트랜잭션이 필요한 문을 실행할 때까지 트랜잭션 시작이 지연되었습니다. 자세한 내용은 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)를 참조하세요.  


 OLE DB Driver for SQL Server와 MDAC는 모두 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 격리를 지원하지만 OLE DB Driver for SQL Server에서만 스냅샷 트랜잭션 격리를 지원합니다. 프로그래밍 측면에서 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
