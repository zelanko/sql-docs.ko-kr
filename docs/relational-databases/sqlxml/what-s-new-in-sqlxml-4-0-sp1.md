---
title: 새로운&#39;의 SQLXML 4.0 SP1 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3e39c7e7d6c94ce83889fbd6e29b26da278862f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618477"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>새로운&#39;의 SQLXML 4.0 SP1
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1에는 다양한 업데이트와 향상된 기능이 포함되어 있습니다. 이 항목에서는 업데이트를 요약하고 사용 가능한 경우 자세한 정보 링크를 제공합니다. SQLXML 4.0 SP1에서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 도입된 새로운 데이터 형식을 지원하기 위한 향상된 기능을 추가로 제공합니다. 이 항목은 다음과 같은 주제로 이루어져 있습니다.  
  
-   SQLXML 4.0 SP1 설치  
  
-   병렬 설치 문제  
  
-   SQLXML 4.0 및 MSXML  
  
-   SQLXML 4.0 재배포  
  
-   에 대 한 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 데이터 형식 지원  
  
-   SQLXML 4.0에 대한 XML 대량 로드 변경 내용  
  
-   SQLXML 4.0에 대한 레지스트리 키 변경 내용  
  
-   마이그레이션 문제  
  
## <a name="installing-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 설치  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전에 SQLXML 4.0은 SQL Server와 함께 제공되었으며 SQL Server Express를 제외한 모든 버전의 SQL Server에 기본적으로 함께 설치되었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 최신 버전의 SQLXML(SQLXML 4.0 SP1)이 더 이상 SQL Server에 포함되지 않습니다. SQLXML 4.0 SP1을 설치 하려면 사이트에서 다운로드할 [SQLXML 4.0 SP1 설치 위치](http://www.microsoft.com/download/details.aspx?id=30403)합니다.  
  
 SQLXML 4.0 SP1 파일은 다음 위치에 설치됩니다.  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  설치 프로세스의 일부로 SQLXML 4.0에 적합한 모든 레지스트리 설정이 지정됩니다.  
  
 64비트 Windows 운영 체제의 Windows on Windows(WOW64)에서 32비트 SQLXML 응용 프로그램을 실행하려면 sqlxml4.msi라는 64비트 SQLXML 4.0 SP1 패키지를 실행해야 합니다. 이 패키지는 다운로드 센터에서 찾을 수 있습니다.  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 제거  
 SQLXML 3.0 SP3, SQLXML 4.0 및 SQLXML 4.0 SP1 사이에는 공유되는 레지스트리 키가 있습니다. SQLXML 3.0 SP3이 설치되어 있는 컴퓨터에서 이후 버전의 SQLXML을 제거한 경우 SQLXML 3.0 SP3을 다시 설치해야 할 수도 있습니다.  
  
## <a name="side-by-side-installation-issues"></a>병렬 설치 문제  
 SQLXML 4.0 설치 프로세스에서는 이전 버전의 SQLXML에 의해 설치된 파일을 제거하지 않습니다. 따라서 버전별 여러 SQLXML 설치에 대한 DLL이 컴퓨터에 있을 수 있습니다. 이러한 함께 설치를 실행할 수 있습니다. SQLXML 4.0에는 버전 독립 및 버전 종속 PROGID가 모두 포함되어 있습니다. 모든 프로덕션 응용 프로그램은 버전 종속 PROGID를 사용해야 합니다.  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 및 MSXML  
 SQLXML 4.0은 MSXML을 설치하지 않습니다. SQLXML 4.0은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이후 설치의 일부로 설치되는 MSXML 6.0을 사용합니다.  
  
## <a name="redistributing-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 재배포  
 재배포 가능 설치 관리자 패키지를 사용하여 SQLXML 4.0 SP1을 배포할 수 있습니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 Authoring a Custom Bootstrapper Package for Visual Studio 2005 및 사용자 지정 필수 구성 요소 추가를 참조하십시오.  
  
 응용 프로그램을 처음에 개발된 플랫폼이 아니라 다른 플랫폼에서 사용하려는 경우에는 Microsoft 다운로드 센터에서 x64, Itanium 및 x86용 sqlncli.msi 버전을 다운로드할 수 있습니다.  
  
 MSXML 6.0용 개별 재배포 설치 프로그램(msxml6.msi)도 있습니다. 해당 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 CD의 다음 위치에 있습니다.  
  
 `%CD%\Setup\`  
  
 이러한 설치 파일을 사용하여 CD에서 직접 MSXML 6.0을 설치할 수 있습니다. 사용자 지정 응용 프로그램과 함께 MSXML 6.0 및 SQLXML 4.0 SP1을 자유롭게 재배포하는 데 설치 파일을 사용할 수도 있습니다.  
  
 응용 프로그램에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 데이터 공급자로 사용하는 경우 이 프로그램도 재배포해야 합니다. 자세한 내용은 [Installing SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)(SQL Server Native Client 설치)를 참조하세요.  
  
## <a name="support-for-sql-server-native-client"></a>SQL Server Native Client 지원  
 SQLXML 4.0에서는 모두 SQLOLEDB 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자입니다. 동일한 버전을 사용 하는 것이 좋습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 같은 서버에서 제공 되는 모든 새로운 데이터 형식을 지원 하기 위해 개발 된는 **Date, Time**, **DateTime2**, 및 **dateTimeOffset** 의 데이터 형식이 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 고 지 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 처음 도입된 데이터 액세스 기술입니다. 이 기술은 SQLOLEDB 공급자와 SQLODBC 드라이버를 하나의 네이티브 DLL(동적 링크 라이브러리)로 조합한 것이며 MDAC(Microsoft Data Access Components)와는 분리된 고유한 새 기능을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 새 응용 프로그램을 만들 수도 있고 MDAC 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows의 SQLOLEDB 및 SQLODBC에서 지원하지 않지만 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 도입된 기능을 활용해야 하는 기존 응용 프로그램을 향상시킬 수도 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용 하 여 FOR XML과 같은 클라이언트 쪽 SQLXML 기능에 필요 합니다 **xml** 데이터 형식입니다. 자세한 내용은 [클라이언트 쪽 XML 서식 지정 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)를 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md), 및 [SQL Server Native Client 프로그래밍](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
> [!NOTE]  
>  SQLXML 4.0은 SQLXML 3.0과 완전히 호환되지 않습니다. 일부 버그 수정 및 기타 기능 변경, 특히 SQLXML ISAPI 지원 제거로 인해 SQLXML 4.0에서는 IIS 가상 디렉터리를 사용할 수 없습니다. 대부분의 응용 프로그램은 약간만 수정해도 실행되지만 SQLXML 4.0과 함께 프로덕션에 배치하기 전에 테스트해야 합니다.  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>SQL Server 2005 및 SQL Server 2008에 도입된 데이터 형식 지원  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 도입 합니다 **xml** 데이터 형식 및 SQLXML 4.0 지원 합니다 **xml** 데이터 형식. 자세한 내용은 [xml 데이터 형식 지원 SQLXML 4.0에서](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)합니다.  
  
 사용 하는 방법에 대 한 예제는 **xml** 데이터 XML 뷰를 매핑할 때 SQLXML에서 입력, XML 대량 로드 하거나 XML updategram을 실행한 다음 항목에서 제공 하는 예제를 참조 하십시오.  
  
-   [XSD 요소 및 테이블과 열에 특성의 기본 매핑](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [XML Updategram을 사용 하 여 데이터 삽입](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [XML 문서 대량 로드의 예](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 도입 된 **날짜, 시간**, **DateTime2**, 및 **DateTimeOffset** 데이터 형식입니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 기본 제공되는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB Provider(SQLNCLI11)와 함께 SQLXML 4.0 SP1을 사용하는 경우 이러한 네 가지 새로운 데이터 형식이 기본 제공 스칼라 형식으로 사용됩니다.  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>SQLXML 4.0 SP1에 대한 XML 대량 로드 변경 내용  
  
-   SQLXML 4.0에서는 SchemaGen 오버플로 필드는 사용 하 여 생성 된 **xml** 데이터 형식. 자세한 내용은 [SQL Server XML 대량 로드 개체 모델](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md)합니다.  
  
-   이전에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 응용 프로그램을 만들었으며 SQLXML 4.0을 사용하려는 경우 Xblkld4.dll을 참조하여 응용 프로그램을 다시 컴파일해야 합니다.  
  
-   Visual Basic Scripting Edition 응용 프로그램의 경우 사용할 DLL을 등록해야 합니다. 다음 예에서 버전 독립 PROGID를 지정하면 응용 프로그램은 마지막으로 등록된 DLL을 사용합니다.  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  버전 종속 PROGID는 SQLXMLBulkLoad.SQLXMLBulkLoad.4.0입니다.  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>SQLXML 4.0에 대한 레지스트리 키 변경 내용  
 SQLXML 4.0에서는 이전 버전의 레지스트리 키가 다음으로 변경되었습니다.  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 SQLXML 4.0에 대해 이러한 키를 적용하려는 경우 설정을 변경해야 합니다.  
  
 또한 SQLXML 4.0에서는 다음 레지스트리 키가 도입되었습니다.  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     기본적으로 SQLXML 4.0은 이전 버전의 SQLXML과 같이 고급 SQLXML 오류를 반환하는 대신 OLE DB 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제공하는 원시 오류 정보를 반환합니다. 이 동작을 사용하지 않으려면 DWORD 유형의 이 레지스트리 키 값을 0으로 설정해야 합니다(기본값은 1임).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     기본적으로 SQLXML은 묶는 괄호 없이 SQL Server GUID 값을 반환합니다. 중괄호를 사용 하 여 반환 되는 GUID 값을 원하는 경우 (예를 들어 {*some GUID*}),이 레지스트리 키의 값을 1로 설정 해야 합니다 (기본값은 0).  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     기본적으로 XML 파서가 데이터를 로드할 때 XML 1.0 규칙에 따라 공백이 정규화됩니다. 이로 인해 데이터의 일부 공백 문자가 손실됩니다. 따라서 의미상으로는 데이터가 같지만 구문 분석 후에 데이터의 텍스트 표현이 달라질 수 있습니다.  
  
     이 키는 데이터의 공백 문자를 유지할 수 있도록 도입되었습니다. 이 레지스트리 키를 추가하고 해당 값을 0으로 설정하면 특성 값의 경우 XML의 공백 문자(LF, CR 및 탭)가 인코딩되어 반환됩니다. 요소 값의 경우 CR만 인코딩되어 반환됩니다.  
  
     이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>마이그레이션 문제  
 다음은 SQLXML 4.0로의 레거시 SQLXML 응용 프로그램 마이그레이션에 영향을 줄 수 있는 문제입니다.  
  
### <a name="ado-and-sqlxml-40-queries"></a>ADO 및 SQLXML 4.0 쿼리  
 SQLXML의 이전 버전에서는 IIS 가상 디렉터리와 SQLXML ISAPI 필터를 사용한 URL 기반 쿼리 실행에 대한 지원이 제공되었습니다. SQLXML 4.0을 사용하는 응용 프로그램에서는 더 이상 이 지원을 사용할 수 없습니다.  
  
 대신 MDAC(Microsoft Data Access Components) 2.6 이상 버전에서 처음 도입된 ADO(ActiveX Data Objects)에 대한 SQLXML 확장을 사용하여 SQLXML 쿼리, 템플릿 및 Updategram을 실행할 수 있습니다.  
  
 자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>SQL Server 2005에서 도입된 데이터 형식 및 SQLXML 3.0 ISAPI 지원 가능성  
 에 도입 된 기능은 ISAPI 지원 솔루션의 향상 된 데이터 입력을 요구 하는 경우 SQLXML 4.0에서 제거 되었으므로 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 와 같은 합니다 [xml 데이터 형식](../../t-sql/xml/xml-transact-sql.md) 또는 [사용자 정의 데이터 형식 (Udt)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)와 같은 다른 솔루션을 사용 하도록 해야 웹 기반 액세스 [SQLXML 관리 되는 클래스](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md) 또는 다른 유형의 SQL Server 2005 용 네이티브 XML 웹 서비스와 같은 HTTP 처리기입니다.  
  
 또는 이러한 형식 확장에 필요 하지 않은 경우 할 수 있습니다 SQLXML 3.0을 사용 하 여 연결할 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 고 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 설치 합니다. SQLXML 3.0 ISAPI 지원은 이러한 이후 버전에 대해 작동 하지만 지원 하지도, 인식 합니다 **xml** 데이터 형식 또는 UDT 유형 지원을에 도입 된 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>임시 파일에 대한 XML 대량 로드 보안 변경  
 SQLXML 4.0 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 XML 대량 로드 파일 권한이 대량 로드 작업을 실행하는 사용자에게 부여됩니다. 읽기 및 쓰기 권한은 파일 시스템에서 상속됩니다. SQLXML 및 SQL Server의 이전 버전에서는 SQLXML 하의 XML 대량 로드 시 보안이 유지되지 않고 모든 사용자가 읽을 수 있는 임시 파일이 만들어졌습니다.  
  
### <a name="migration-issues-for-client-side-for-xml"></a>클라이언트 쪽 FOR XML에 대한 마이그레이션 문제  
 실행 엔진의 변경으로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 FOR XML 쿼리를 실행할 경우 반환 되는 보다는 기본 테이블의 메타 데이터에 다른 값을 반환할 수 있습니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]합니다. 이 경우 FOR XML 쿼리 결과에 대한 클라이언트 쪽 형식 지정으로 인해 쿼리가 실행되는 버전에 따라 다른 출력이 생성됩니다.  
  
 FOR XML 쿼리를 실행된 한 클라이언트 쪽 사용 하는 경우 SQLXML 3.0을 통해는 **xml** 데이터 형식 열을 결과에 데이터가 완전히 엔터티 화 문자열로 다시 돌아옵니다. SQLXML 4.0에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client(SQLNCLI11)를 공급자로 지정하면 데이터가 XML로 반환됩니다.  
  
  
