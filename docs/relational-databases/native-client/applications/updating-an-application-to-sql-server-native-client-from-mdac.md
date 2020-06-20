---
title: MDAC에서 업데이트
description: Windows 데이터 액세스 구성 요소에서 SQL Server Native Client로 업그레이드 합니다 .이는 이전 버전과의 호환성을 통해 SQL Server 2005의 새로운 기능을 노출 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0c9902e15064ac6e80b15563289417dd82c0db5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84949619"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>MDAC에서 SQL Server Native Client로 애플리케이션 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 및 MDAC(Microsoft Data Access Components) 사이에는 많은 차이점이 있습니다. Windows Vista부터 이제 데이터 액세스 구성 요소를 Windows Data Access Components 또는 Windows DAC라고 합니다. 양쪽 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 네이티브 데이터에 액세스하기 위한 것이지만, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 특히 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 새 기능을 노출하도록 설계되었으며 동시에 이전 버전과의 호환성도 유지합니다.  
  
 이 항목의 정보는 MDAC(또는 Windows DAC) 애플리케이션을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 버전과 최신 상태로 업데이트하는 데 유용합니다. 에서 제공 하는 native Client 버전을 사용 하 여이 응용 프로그램을 최신 상태로 만들기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)를 참조 하세요.  
  
 또한 MDAC에는 OLE DB, ODBC 및 ADO(ActiveX Data Objects)를 사용하기 위한 구성 요소가 포함되어 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 OLE DB 및 ODBC만 구현합니다(단, ADO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 기능에 액세스할 수 있음).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 및 MDAC는 다음과 같은 영역에서 차이가 있습니다.  
  
-   ADO를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 공급자에 액세스하는 사용자는 SQL OLE DB 공급자에 액세스할 때보다 더 적은 필터링 기능을 사용할 수 있습니다.  
  
-   ADO 애플리케이션이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하고 계산된 열을 업데이트하는 경우 오류가 보고됩니다. MDAC를 사용하면 업데이트가 허용되지만 무시되었습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 자체 포함된 하나의 DLL(동적 연결 라이브러리) 파일입니다. 공개적으로 노출되는 인터페이스는 편리한 배포 및 보안 노출 제한을 위해 최소한으로 유지되었습니다.  
  
-   OLE DB 및 ODBC 인터페이스만 지원됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 ODBC 드라이버 이름은 MDAC에서 사용된 이름과 다릅니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하는 경우 MDAC 구성 요소에서 제공하는 사용자가 액세스할 수 있는 기능을 사용할 수 있습니다. 여기에는 연결 풀링, ADO 지원 및 클라이언트 커서 지원이 포함되지만 이에 제한되지 않습니다. 이러한 기능을 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 데이터베이스 연결만 제공합니다. MDAC는 추적, 관리 컨트롤 및 성능 카운터와 같은 기능을 제공합니다.  
  
-   애플리케이션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 OLE DB 핵심 서비스를 사용할 수 있지만, OLE DB 커서 엔진을 사용하는 경우 커서 엔진이 새로운 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 데이터 형식을 모르기 때문에 발생할 수 있는 잠재적 문제를 방지하기 위해 데이터 형식 호환성 옵션을 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 액세스를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 XML 통합이 포함되어 있지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client에서 SELECT ... XML 쿼리는 이지만 다른 XML 기능은 지원 하지 않습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는에서 도입 된 **xml** 데이터 형식을 지원 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결 문자열 특성만 사용하여 클라이언트 쪽 네트워크 라이브러리 구성을 지원합니다. 보다 완전한 네트워크 라이브러리 구성이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 odbcbcp.dll과 호환되지 않습니다. Native Client를 사용 하려면 ODBC 및 **bcp** api를 모두 사용 하는 응용 프로그램을 sqlncli11와 연결 하도록 다시 빌드해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 ODBC용 Microsoft OLE DB 공급자(MSDASQL)에서 지원되지 않습니다. MDAC SQLODBC 드라이버를 MSDASQL과 함께 사용하거나 MDAC SQLODBC 드라이버를 ADO와 함께 사용하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 OLE DB를 사용하십시오.  
  
-   MDAC 연결 문자열은 **Trusted_Connection** 키워드에 부울 값(**true**)을 허용합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 연결 문자열은 **yes** 또는 **no**를 사용 해야 합니다.  
  
-   경고와 오류가 약간 변경되었습니다. 이제 서버에서 반환되는 경고와 오류가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client로 전달될 때 동일한 심각도를 유지합니다. 특정 경고 및 오류 트래핑을 사용하는 경우 애플리케이션을 완전히 테스트해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 MDAC보다 엄격한 오류 검사 기능이 있으므로 ODBC 및 OLE DB 사양을 엄격하게 준수하지 않는 일부 애플리케이션이 다르게 동작할 수 있습니다. 예를 들어, SQLOLEDB 공급자는 결과 매개 변수의 경우 매개 변수 이름이 ' '로 시작 해야 하는 규칙을 적용 하지 \@ 않지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는이 규칙을 적용 하지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결 실패와 관련해서 MDAC와 다르게 동작합니다. 예를 들어 MDAC는 실패한 연결에 대해 캐시된 속성 값을 반환하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 호출 애플리케이션에 오류를 보고합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 Visual Studio Analyzer 이벤트를 생성하지 않고 대신 Windows 추적 이벤트를 생성합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 perfmon과 함께 사용할 수 없습니다. Perfmon은 Windows에 포함된 MDAC SQLODBC 드라이버를 사용하는 DSN에서만 사용할 수 있는 Windows 도구입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에 연결되어 있으면 서버 오류 16947이 SQL_ERROR로 반환됩니다. 이 오류는 현재 위치 업데이트나 삭제 시 행이 업데이트 또는 삭제되지 않을 때 발생합니다. 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 MDAC를 사용할 경우 서버 오류 16947이 경고(SQL_SUCCESS_WITH_INFO)로 반환됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client는 **IDBDataSourceAdmin** 인터페이스를 구현 합니다 .이 인터페이스는 이전에 구현 되지 않은 선택적 OLE DB 인터페이스 이지만이 선택적 인터페이스의 **createdatasource** 메서드만 구현 됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 TABLE_TYPE이 SYNONYM으로 설정된 TABLES 및 TABLE_INFO 스키마 행 집합에 동의어를 반환합니다.  
  
-   데이터 형식이 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**또는 기타 large object 유형의 반환 값은 이전의 클라이언트 버전으로 반환 될 수 없습니다 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] . 이러한 유형을 반환 값으로 사용하려는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용해야 합니다.  
  
-   MDAC를 사용하면 수동 및 암시적 트랜잭션을 시작할 때 다음 문을 실행할 수 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 실행할 수 없습니다. 자동 커밋 모드로 이러한 문을 실행해야 합니다.  
  
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
  
     이 형식 매핑은 열 메타데이터에 대해 반환되는 값에 영향을 줍니다. 예를 들어 **텍스트** 열의 최대 크기는 2147483647 이지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client ODBC는 **varchar (max)** 열의 최대 크기를 SQL_SS_LENGTH_UNLIMITED로 보고 하 고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client OLE DB는 플랫폼에 따라 **varchar (max)** 열의 최대 크기를 2147483647 또는-1로 보고 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 이전 버전과의 호환성을 위해 연결 문자열에서 모호성을 허용합니다. 예를 들어 일부 키워드를 여러 번 지정할 수 있으며 위치나 우선 순위에 따라 충돌하는 키워드를 해결할 수 있습니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 연결 문자열의 모호성을 허용하지 않을 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하도록 애플리케이션을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  
  
-   ODBC 또는 OLE DB 호출을 사용하여 트랜잭션을 시작하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 MDAC 사이에 동작 차이가 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하면 트랜잭션이 즉시 시작되지만 MDAC를 사용하면 첫 번째 데이터베이스 액세스 후에 트랜잭션이 시작됩니다. 일괄 처리 또는 저장 프로시저의 실행이 시작 된 후 일괄 처리 또는 저장 프로시저의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \@ \@ 실행이 완료 된 후에는 TRANCOUNT가 동일 해야 하므로 저장 프로시저 및 일괄 처리의 동작에 영향을 줄 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client를 사용 하는 경우 ITransactionLocal:: BeginTransaction를 사용 하면 트랜잭션이 즉시 시작 됩니다. MDAC를 사용할 경우 애플리케이션이 암시적 트랜잭션 모드의 트랜잭션이 필요한 문을 실행할 때까지 트랜잭션 시작이 지연되었습니다. 자세한 내용은 [SET IMPLICIT_TRANSACTIONS &#40;transact-sql&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)를 참조 하세요.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 드라이버를 system.web과 함께 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 새로운 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 데이터 형식이 나 기능을 노출 하는 서버 컴퓨터에 액세스할 때 오류가 발생할 수 있습니다. System.object는 일반 ODBC 구현을 제공 하며 이후에 공급 업체별 기능이 나 확장을 노출 하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]( Native Client 드라이버는 기본적으로 최신 기능을 지원 하도록 업데이트 됩니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . 이 문제를 해결 하려면 MDAC로 되돌리거나 System.object로 마이그레이션할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 MDAC는 모두 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리를 지원하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client만 스냅샷 트랜잭션 격리를 지원합니다. 프로그래밍 측면에서 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
