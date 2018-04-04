---
title: MDAC에서 SQL Server 용 OLE DB 드라이버로 응용 프로그램 업데이트 | Microsoft Docs
description: MDAC에서 SQL Server 용 OLE DB Driver로 응용 프로그램 업데이트
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b0581e1423cd2731b1edb0dbdc0f26523f445a7
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>MDAC에서 SQL Server 용 OLE DB 드라이버로 응용 프로그램 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server와 MDAC Microsoft Data Access Components (); 차이점의 여러 가지 Windows Vista 이상에서는 데이터 액세스 구성 요소는 이제 Windows Data Access Components (또는 Windows DAC) 이라고 합니다. 둘 다에 대 한 네이티브 데이터 액세스를 제공 하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스, OLE DB 드라이버의 새로운 기능을 노출 하도록 특별히 고안 된 SQL Server에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 이전 버전과 호환성을 유지 관리 하는 동시에 있는 동안 합니다.   

 또한 MDAC OLE DB, ODBC 및 ADO ActiveX Data Objects ()를 사용 하 여에 대 한 구성 요소를 포함 되어 있지만 OLE DB Driver for SQL Server 구현 OLE DB (ADO SQL Server 용 OLE DB Driver의 기능에 액세스할 수 있습니다) 하지만 합니다.  

 OLE DB Driver for SQL Server 및 MDAC는 다음 영역에서 다릅니다.  

-   ADO는 OLE DB Driver for SQL Server 액세스를 사용 하는 사용자는 SQL OLE DB 공급자에 액세스할 때 보다 적은 필터링 기능을 찾을 수 있습니다.  

-   ADO 응용 프로그램이 SQL Server 용 OLE DB 드라이버를 사용 하 여 하는 계산된 열을 업데이트 하려고 하는 경우 오류가 보고 됩니다. MDAC를 사용하면 업데이트가 허용되지만 무시되었습니다.  

-   OLE DB Driver for SQL Server 자체 포함 된 단일 동적 연결 라이브러리 (DLL) 파일입니다. 공개적으로 노출되는 인터페이스는 편리한 배포 및 보안 노출 제한을 위해 최소한으로 유지되었습니다.  

-   OLE DB 인터페이스만 지원 됩니다.  

-   Mdac를 사용할 경우 사용 되는 OLE DB 드라이버에서 SQL Server 이름이 서로 다릅니다.  

-   SQL Server 용 OLE DB 드라이버를 사용 하 여 MDAC 구성 요소에서 제공 하는 사용자를 액세스할 수 있는 기능이 표시 됩니다. 여기에는 연결 풀링, ADO 지원 및 클라이언트 커서 지원이 포함되지만 이에 제한되지 않습니다. 이러한 기능 중 하나를 사용 하면 OLE DB Driver for SQL Server에서 데이터베이스 연결만을 제공 합니다. MDAC는 추적, 관리 컨트롤 및 성능 카운터와 같은 기능을 제공합니다.  

-   응용 프로그램이 SQL Server 용 OLE DB 드라이버와 OLE DB 핵심 서비스에 사용할 수 있지만 데이터 형식 호환성 옵션 커서 엔진이 새로운 지식이 없는 있기 때문에 발생할 수 있는 잠재적 문제를 방지 하기 위해 사용 해야 OLE DB 커서 엔진을 사용 하는 경우 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 데이터 형식입니다.  

-   OLE DB Driver for SQL Server 이전에 대 한 액세스를 지 원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스.  

-   OLE DB Driver for SQL Server XML 통합을 포함 되지 않습니다. OLE DB Driver for SQL Server 지원 선택... XML 쿼리, 하지만 다른 XML 기능은 지원 하지 않습니다. 그러나 OLE DB Driver for SQL Server는 지원의 **xml** 에 도입 된 데이터 형식 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다.  

-   OLE DB Driver for SQL Server 연결 문자열 특성을 사용 하 여 클라이언트 쪽 네트워크 라이브러리 구성 지원 합니다. 보다 완전한 네트워크 라이브러리 구성이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용해야 합니다.  

-   OLE DB Driver for SQL Server odbcbcp.dll와 호환 되지 않습니다. SQL Server 용 OLE DB 드라이버를 사용 하려면 msoledbsql.lib와 연결 하려면 응용 프로그램을 빌드해야 합니다.    

-   MDAC 연결 문자열을 부울 값을 사용 (**true**)에 대 한는 **Trusted_Connection** 키워드입니다. OLE DB Driver for SQL Server 연결 문자열을 사용 해야 **예** 또는 **없습니다**합니다.  

-   경고와 오류가 약간 변경되었습니다. 이제는 서버에서 반환한 오류 및 경고는 SQL Server 용 OLE DB 드라이버에 전달 될 때 동일한 심각도 유지 합니다. 특정 경고 및 오류 트래핑을 사용하는 경우 응용 프로그램을 완전히 테스트해야 합니다.  

-   OLE DB Driver for SQL Server OLE DB 사양을 엄격 하 게 준수 하지 않는 일부 응용 프로그램 다르게 동작할 수 있습니다는 MDAC 보다 엄격한 오류 검사에 있습니다. SQLOLEDB 공급자 매개 변수 이름으로 시작 해야 하는 규칙을 적용 하지 않은 예를 들어, ' @' 매개 변수가 있지만 OLE DB Driver for SQL Server가 결과 대 한 합니다.  

-   OLE DB Driver for SQL Server 연결 실패와 관련해 MDAC와 다르게 동작 합니다. 예를 들어 MDAC OLE DB Driver for SQL Server 호출 응용 프로그램에서 오류를 보고 하는 반면 연결 실패에 대 한 캐시 된 속성 값을 반환 합니다.  

-   OLE DB Driver for SQL Server는 Visual Studio Analyzer 이벤트를 생성 하지 않는 하지만 대신 Windows 추적 이벤트를 생성 합니다.  

-   OLE DB Driver for SQL Server는 perfmon과 함께 사용할 수 없습니다. Perfmon은 Windows에 포함된 MDAC SQLODBC 드라이버를 사용하는 DSN에서만 사용할 수 있는 Windows 도구입니다.  

-   OLE DB Driver for SQL Server에 연결 되어 있을 때 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 이상 버전에서 서버 오류 16947이 SQL_ERROR로 반환 됩니다. 이 오류는 현재 위치 업데이트나 삭제 시 행이 업데이트 또는 삭제되지 않을 때 발생합니다. 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 MDAC를 사용할 경우 서버 오류 16947이 경고(SQL_SUCCESS_WITH_INFO)로 반환됩니다.  

-   OLE DB Driver for SQL Server를 구현 하는 **IDBDataSourceAdmin** 인터페이스에 이전에 구현 되지 않은 선택적 OLE DB 인터페이스인는 **CreateDataSource** 이 메서드 선택적 인터페이스 구현 됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   TABLES 및 TABLE_INFO에 동의어를 반환 하는 OLE DB 드라이버 SQL Server에 대 한 스키마 행 집합, table_type이 SYNONYM으로 설정 합니다.  

-   데이터 형식의 값을 반환할 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**, 다른 큰 개체 유형의 버전의 클라이언트에 반환 될 수 없습니다 또는 이전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. 반환 값으로 이러한 형식을 사용 하려는 경우 SQL Server 용 OLE DB 드라이버를 사용 해야 합니다.  

-   MDAC를 사용 하면 수동 및 암시적 트랜잭션 시작 시 실행 되도록 다음 문을 하지만 OLE DB Driver for SQL Server는 그렇지 않습니다. 자동 커밋 모드로 이러한 문을 실행해야 합니다.  

    -   모든 전체 텍스트 작업(인덱스 및 카탈로그 DDL)  

    -   모든 데이터베이스 작업(데이터베이스 만들기, 데이터베이스 변경, 데이터베이스 삭제)  

    -   다시 구성  

    -   시스템 종료  

    -   중지  

    -   백업  

-   MDAC 응용 프로그램이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하면 다음 그림과 같이 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 데이터 형식이 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 호환 데이터 형식으로 나타납니다.  

    |SQL Server 2005 형식|SQL Server 2000 유형|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     이 형식 매핑은 열 메타데이터에 대해 반환되는 값에 영향을 줍니다. 예를 들어 한 **텍스트** 열에 최대 크기가 2147483647, 있지만 OLE DB Driver for SQL Server의 최대 크기를 보고 **varchar (max)** 2,147,483,647 또는-1 플랫폼에 따라 열입니다.  

-   연결 문자열에서 모호성을 허용 하는 OLE DB Driver for SQL Server (예를 들어 일부 키워드를 두 번 이상 지정할 수 있습니다 및 위치나 우선 순위에 따라 해결 된 충돌 하는 키워드를 사용할 수 있습니다) 이전 버전과 호환성에 속하는 이유로 합니다. OLE DB Driver for SQL Server의 이후 릴리스에서 연결 문자열에서 모호성을 통합할 수 있습니다. OLE DB Driver for SQL Server를 사용 하 여 연결 문자열 모호성에 대 한 종속성을 제거 하려면 응용 프로그램을 수정 하는 경우에 것이 좋습니다.  

-   트랜잭션을 시작 하는 OLE DB 호출을 사용 하는 경우 차이가 있는 동작에 OLE DB Driver for SQL Server와 MDAC 사이 트랜잭션이 즉시 시작 OLE DB Driver for SQL Server 되지만 MDAC를 사용 하 여 첫 번째 데이터베이스 액세스 후 트랜잭션을 시작 합니다. 이 수에 영향을 줄 저장된 프로시저 및 일괄 처리의 동작 때문에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @ 필요@TRANCOUNT 일괄 처리 또는 저장된 프로시저 실행을 일괄 처리 또는 저장된 프로시저를 시작할 때 끝낸 후 동일 해야 합니다.  

-   OLE DB 드라이버와 SQL Server에 대 한 ITransactionLocal::BeginTransaction 인해 트랜잭션이 즉시 시작 됩니다. MDAC를 사용할 경우 응용 프로그램이 암시적 트랜잭션 모드의 트랜잭션이 필요한 문을 실행할 때까지 트랜잭션 시작이 지연되었습니다. 자세한 내용은 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)를 참조하세요.  


 두 OLE DB Driver for SQL Server 및 MDAC 지원 커밋된 읽기 트랜잭션 격리 행 버전 관리만 OLE DB 드라이버를 사용 하 여 SQL Server 지원 스냅숏 트랜잭션 격리에 대 한 합니다. 프로그래밍 측면에서 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  

## <a name="see-also"></a>관련 항목:  
 [SQL Server 용 OLE DB 드라이버 빌딩 응용 프로그램](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
