---
title: MDAC에서 SQL Server Native Client로 응용 프로그램 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b8015e130ce45c7d3864532b9cb841a4f2fc16d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061286"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>MDAC에서 SQL Server Native Client로 응용 프로그램 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 및 MDAC(Microsoft Data Access Components) 사이에는 많은 차이점이 있습니다. Windows Vista부터 이제 데이터 액세스 구성 요소를 Windows Data Access Components 또는 Windows DAC라고 합니다. 양쪽 모두 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 네이티브 데이터에 액세스하기 위한 것이지만, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 특히 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 새 기능을 노출하도록 설계되었으며 동시에 이전 버전과의 호환성도 유지합니다.  
  
 이 항목의 정보는 MDAC(또는 Windows DAC) 응용 프로그램을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 버전과 최신 상태로 업데이트하는 데 유용합니다. 최신 버전을 사용 하 여이 응용 프로그램을 내릴 수 있도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 제공 되는 네이티브 클라이언트 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 참조 하세요 [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)합니다.  
  
 또한 MDAC에는 OLE DB, ODBC 및 ADO(ActiveX Data Objects)를 사용하기 위한 구성 요소가 포함되어 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 OLE DB 및 ODBC만 구현합니다(단, ADO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 기능에 액세스할 수 있음).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 및 MDAC는 다음과 같은 영역에서 차이가 있습니다.  
  
-   ADO를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 공급자에 액세스하는 사용자는 SQL OLE DB 공급자에 액세스할 때보다 더 적은 필터링 기능을 사용할 수 있습니다.  
  
-   ADO 응용 프로그램이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하고 계산된 열을 업데이트하는 경우 오류가 보고됩니다. MDAC를 사용하면 업데이트가 허용되지만 무시되었습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 자체 포함된 하나의 DLL(동적 연결 라이브러리) 파일입니다. 공개적으로 노출되는 인터페이스는 편리한 배포 및 보안 노출 제한을 위해 최소한으로 유지되었습니다.  
  
-   OLE DB 및 ODBC 인터페이스만 지원됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 ODBC 드라이버 이름은 MDAC에서 사용된 이름과 다릅니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하는 경우 MDAC 구성 요소에서 제공하는 사용자가 액세스할 수 있는 기능을 사용할 수 있습니다. 여기에는 연결 풀링, ADO 지원 및 클라이언트 커서 지원이 포함되지만 이에 제한되지 않습니다. 이러한 기능을 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 데이터베이스 연결만 제공합니다. MDAC는 추적, 관리 컨트롤 및 성능 카운터와 같은 기능을 제공합니다.  
  
-   응용 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 함께 OLE DB 핵심 서비스를 사용할 수 있지만, OLE DB 커서 엔진을 사용하는 경우 커서 엔진이 새로운 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 데이터 형식을 모르기 때문에 발생할 수 있는 잠재적 문제를 방지하기 위해 데이터 형식 호환성 옵션을 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 이전 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 액세스를 지원합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 XML 통합이 포함되어 있지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 지원 선택... XML 쿼리, 하지만 다른 XML 기능은 지원 하지 않습니다. 그러나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 합니다 **xml** 데이터 형식에 도입 된 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결 문자열 특성만 사용하여 클라이언트 쪽 네트워크 라이브러리 구성을 지원합니다. 보다 완전한 네트워크 라이브러리 구성이 필요한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 odbcbcp.dll과 호환되지 않습니다. 모두 ODBC를 사용 하는 응용 프로그램 및 **bcp** Api를 사용 하려면 sqlncli11.lib와 연결 하기 빌드해야 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 ODBC용 Microsoft OLE DB 공급자(MSDASQL)에서 지원되지 않습니다. MDAC SQLODBC 드라이버를 MSDASQL과 함께 사용하거나 MDAC SQLODBC 드라이버를 ADO와 함께 사용하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 OLE DB를 사용하십시오.  
  
-   MDAC 연결 문자열을 허용 하는 부울 값 (**true**)에 대 한 합니다 **Trusted_Connection** 키워드입니다. A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 연결 문자열 사용 해야 합니다 **예** 하거나 **없음**합니다.  
  
-   경고와 오류가 약간 변경되었습니다. 이제 서버에서 반환되는 경고와 오류가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client로 전달될 때 동일한 심각도를 유지합니다. 특정 경고 및 오류 트래핑을 사용하는 경우 응용 프로그램을 완전히 테스트해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 MDAC보다 엄격한 오류 검사 기능이 있으므로 ODBC 및 OLE DB 사양을 엄격하게 준수하지 않는 일부 응용 프로그램이 다르게 동작할 수 있습니다. SQLOLEDB 공급자 매개 변수 이름을 사용 하 여 시작 해야 하는 규칙을 적용 하지 않은 예를 들어, '\@' 결과 매개 변수에 대 한 하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결 실패와 관련해서 MDAC와 다르게 동작합니다. 예를 들어 MDAC는 실패한 연결에 대해 캐시된 속성 값을 반환하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 호출 응용 프로그램에 오류를 보고합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 Visual Studio Analyzer 이벤트를 생성하지 않고 대신 Windows 추적 이벤트를 생성합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 perfmon과 함께 사용할 수 없습니다. Perfmon은 Windows에 포함된 MDAC SQLODBC 드라이버를 사용하는 DSN에서만 사용할 수 있는 Windows 도구입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에 연결되어 있으면 서버 오류 16947이 SQL_ERROR로 반환됩니다. 이 오류는 현재 위치 업데이트나 삭제 시 행이 업데이트 또는 삭제되지 않을 때 발생합니다. 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 MDAC를 사용할 경우 서버 오류 16947이 경고(SQL_SUCCESS_WITH_INFO)로 반환됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 구현 합니다 **IDBDataSourceAdmin** 인터페이스에 이전에 구현 되지 않은 선택적 OLE DB 인터페이스인 합니다 **CreateDataSource** 이 선택적 메서드 인터페이스 구현 됩니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 TABLE_TYPE이 SYNONYM으로 설정된 TABLES 및 TABLE_INFO 스키마 행 집합에 동의어를 반환합니다.  
  
-   데이터 형식의 값을 반환 **varchar (max)**, **nvarchar (max)**, **varbinary (max)** 하십시오 **xml**, **udt**, 다른 큰 개체 유형의 클라이언트 버전을 반환할 수 없습니다 또는 이전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. 이러한 유형을 반환 값으로 사용하려는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용해야 합니다.  
  
-   MDAC를 사용하면 수동 및 암시적 트랜잭션을 시작할 때 다음 문을 실행할 수 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 실행할 수 없습니다. 자동 커밋 모드로 이러한 문을 실행해야 합니다.  
  
    -   모든 전체 텍스트 작업(인덱스 및 카탈로그 DDL)  
  
    -   모든 데이터베이스 작업(데이터베이스 만들기, 데이터베이스 변경, 데이터베이스 삭제)  
  
    -   다시 구성  
  
    -   시스템 종료  
  
    -   중지  
  
    -   백업  
  
-   MDAC 응용 프로그램이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하면 다음 그림과 같이 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 데이터 형식이 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 호환 데이터 형식으로 나타납니다.  
  
    |SQL Server 2005 형식|SQL Server 2000 형식|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  
  
     이 형식 매핑은 열 메타데이터에 대해 반환되는 값에 영향을 줍니다. 예를 들어를 **텍스트** 열에는 최대 크기는 2,147,483,647 이지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC의 최대 크기를 보고 **varchar (max)** 열 SQL_SS_LENGTH_UNLIMITED, 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB의 최대 크기를 보고 **varchar (max)** 열 2,147,483,647 또는 플랫폼에 따라-1입니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 이전 버전과의 호환성을 위해 연결 문자열에서 모호성을 허용합니다. 예를 들어 일부 키워드를 여러 번 지정할 수 있으며 위치나 우선 순위에 따라 충돌하는 키워드를 해결할 수 있습니다. 이후 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 연결 문자열의 모호성을 허용하지 않을 수도 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하도록 응용 프로그램을 수정하는 경우 연결 문자열 모호성에 대한 종속성을 제거하는 것이 좋습니다.  
  
-   ODBC 또는 OLE DB 호출을 사용하여 트랜잭션을 시작하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 MDAC 사이에 동작 차이가 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하면 트랜잭션이 즉시 시작되지만 MDAC를 사용하면 첫 번째 데이터베이스 액세스 후에 트랜잭션이 시작됩니다. 이 수에 영향 저장된 프로시저 및 일괄 처리의 동작 때문 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 필요 \@ \@TRANCOUNT 일괄 처리 또는 저장된 프로시저가 완료 된 후 실행 일괄 처리 또는 저장된 프로시저를 시작할 때와 동일 해야 합니다.  
  
-   사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ITransactionLocal::BeginTransaction으로 인해 트랜잭션이 즉시 시작 됩니다. MDAC를 사용할 경우 응용 프로그램이 암시적 트랜잭션 모드의 트랜잭션이 필요한 문을 실행할 때까지 트랜잭션 시작이 지연되었습니다. 자세한 내용은 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)를 참조하세요.  
  
-   사용 하는 경우 오류가 발생할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] System.Data.Odbc 액세스를 사용 하 여 Native Client 드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 새 노출 하는 서버 컴퓨터 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-관련 데이터 형식이 나 기능입니다. System.Data.Odbc는 일반 ODBC 구현을 제공 하 고 이후에 노출 하지 않습니다 공급 업체별 기능이 나 확장 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 드라이버는 기본적으로 최신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 지원하도록 업데이트됩니다. 문제를 해결 하려면이 문제를 MDAC 되돌리려면 하거나 System.Data.SqlClient를 마이그레이션합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 MDAC는 모두 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리를 지원하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client만 스냅숏 트랜잭션 격리를 지원합니다. 프로그래밍 측면에서 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client를 사용하여 응용 프로그램 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
