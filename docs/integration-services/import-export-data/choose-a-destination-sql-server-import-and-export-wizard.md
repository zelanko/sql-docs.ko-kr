---
title: "대상 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.chooseadestination.f1"
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 95
---
# 대상 선택(SQL Server 가져오기 및 내보내기 마법사)
 데이터 원본 및 연결하는 방법에 대한 정보를 제공하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **대상 선택**을 표시합니다. 이 페이지에서는 데이터 대상 및 연결하는 방법에 대한 정보를 제공합니다.
  
사용할 수 있는 데이터 대상에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)를 참조하세요. 

## <a name="screen-shot-of-the-destination-page"></a>대상 페이지의 스크린샷
다음 스크린샷은 마법사의 **대상 선택** 페이지의 첫 번째 부분을 보여 줍니다.

![대상 선택](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>대상 선택
 **대상**  
 데이터를 대상으로 가져올 수 있는 데이터 공급자를 선택하여 대상을 지정합니다. 대부분의 경우 필요한 데이터 공급자는 이름으로 알 수 있습니다. 공급자 이름에 대상 이름(예: SQL Server, Oracle, 플랫 파일, Excel, Access 등)이 포함되어 있기 때문입니다.
 
**대상** 목록에서 사용 가능한 데이터 공급자 목록은 컴퓨터에 설치된 공급자에 따라 달라집니다. 또한 64비트 또는 32비트 마법사를 실행하는지에 따라 달라집니다.

대상에 사용할 수 있는 공급자가 여러 개 있을 수 있습니다. 일반적으로 대상에서 작동하는 모든 공급자를 선택할 수 있습니다. 예를 들어 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, .NET Framework Data Provider for SQL Server 또는 Microsoft OLE DB Provider for SQL Server를 사용할 수 있습니다.
 
먼저 일반 데이터 공급자를 선택해야 하는 경우도 있습니다. 예를 들어 대상에 대한 ODBC 드라이버가 있는 경우 .Net Framework Data Provider for ODBC를 선택합니다.

일부 대상의 경우 Microsoft 또는 타사의 데이터 공급자를 다운로드해야 할 수도 있습니다. 사용할 수 있는 데이터 대상에 대한 자세한 내용은 [어떤 데이터 원본 및 대상을 사용할 수 있나요?](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)를 참조하세요.

## <a name="after-you-choose-a-destination"></a>대상을 선택한 후
대상을 선택한 후 **대상 선택** 페이지의 나머지 속성에 대해 표시되는 옵션 수는 선택한 데이터 공급자에 따라 달라집니다.

다음 섹션에는 자주 사용되는 일부 대상에 대한 중요한 옵션 목록이 나와 있습니다. **대상** 드롭다운에서 사용할 수 있는 모든 대상이 여기에 나열된 것은 아닙니다. 추가 옵션 및 다른 공급자에 대한 자세한 내용은 공급자별 설명서를 참조하세요.

> [!TIP] 대상에 연결 문자열이 필요한 경우 타사 사이트인 [연결 문자열 참조](https://www.connectionstrings.com/)에서 예제를 찾을 수 있습니다.  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

새 SQL Server 데이터베이스를 대상으로 만들려는 경우 SQL Server Native Client 또는 Microsoft OLE DB Provider for SQL Server를 선택합니다. .Net Framework Data Provider for SQL Server를 선택하면 새 데이터베이스를 만드는 옵션을 사용할 수 없습니다.  

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>SQL Server Native Client 또는 Microsoft OLE DB Provider for SQL Server를 사용하여 SQL Server에 연결  

SQL Server Native Client 및 Microsoft OLE DB Provider for SQL Server는 동일한 옵션 집합을 표시합니다. 다음 스크린샷은 SQL Server Native Client에 대한 옵션을 예로 보여 줍니다.

![SQL 기본 대상](../../integration-services/import-export-data/media/sql-native-destination.png)

 **서버 이름**  
 대상 서버의 이름 또는 IP 주소를 입력하거나 목록에서 서버를 선택합니다.  
  
> [!NOTE] 네트워크에 여러 서버가 있는 경우 서버 이름을 입력하는 것이 더 쉬울 수 있습니다. 드롭다운 목록을 클릭할 경우 네트워크에 사용 가능한 모든 서버를 쿼리하는 데 많은 시간이 걸릴 수 있으며, 해당 서버 이름이 결과에 나열되지 않을 수도 있습니다.  
 
 표준이 아닌 TCP 포트를 지정하려면 해당 서버 이름 또는 IP 주소 뒤에 쉼표를 입력한 다음 포트 번호를 입력합니다.
 
 **Windows 인증 사용**  
 마법사에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증을 사용하여 데이터베이스에 로그인하도록 할지 여부를 지정합니다. Windows 인증을 사용하는 것이 좋습니다.  
  
 **SQL Server 인증 사용**  
 마법사에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 데이터베이스에 로그인할지 여부를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 암호를 입력합니다.  
  
 **데이터베이스**  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 데이터베이스 목록에서 선택합니다.  
  
 **새로 고침**  
 **새로 고침**을 클릭하여 사용 가능한 데이터베이스 목록을 복원합니다.  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>.NET Framework Data Provider for SQL Server를 사용하여 SQL Server에 연결 

이 페이지에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 그룹화된 옵션 목록이 나와 있습니다. 중요한 옵션이 여기에 나열됩니다. 이 공급자 선택 시 나열되는 추가 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 데이터베이스에 성공적으로 연결하기 위해 꼭 필요한 옵션은 아닙니다. 

자세한 내용은 [.NET Framework Data Provider for SQL Server 연결 문자열](https://www.connectionstrings.com/sqlconnection/)을 참조하세요.

![SQL Server 대상 네트워크](../../integration-services/import-export-data/media/sql-server-destination-net.png)
  
 **대상**  
 대상 서버의 이름 또는 IP 주소를 입력하거나 목록에서 서버를 선택합니다.  
  
> [!NOTE] 네트워크에 여러 서버가 있는 경우 서버 이름을 입력하는 것이 더 쉬울 수 있습니다. 드롭다운 목록을 클릭할 경우 네트워크에 사용 가능한 모든 서버를 쿼리하는 데 많은 시간이 걸릴 수 있으며, 해당 서버 이름이 결과에 나열되지 않을 수도 있습니다.  
 
 표준이 아닌 TCP 포트를 지정하려면 해당 서버 이름 또는 IP 주소 뒤에 쉼표를 입력한 다음 포트 번호를 입력합니다.
 
 **초기 카탈로그**  
 대상 데이터베이스의 이름을 입력하거나 목록에서 데이터베이스를 선택합니다.  
  
 **통합 보안**  
 Windows 통합 인증을 사용하여 연결(권장)하려면 **True**를 지정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려면 **False**를 지정합니다. **False**를 지정하면 사용자 ID와 암호를 입력해야 합니다. 기본값은 **False**입니다.  
  
 **사용자 ID**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 암호를 입력합니다.  

## <a name="oracle"></a>Oracle

.Net Framework Data Provider for Oracle 또는 Microsoft OLE DB Provider for Oracle을 사용하여 Oracle에 연결합니다. 다음 스크린샷에 표시된 .Net Framework Data Provider for Oracle이 구성하기 더 쉽습니다.

자세한 내용은 [.NET Framework Data Provider for Oracle 연결 문자열](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) 또는 [Microsoft OLE DB Provider for Oracle 연결 문자열](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/)을 참조하세요.

![Oracle 대상](../../integration-services/import-export-data/media/oracle-destination.png)

## <a name="odbc-destinations"></a>ODBC 대상

ODBC 드라이버를 제공하는 대상에 데이터를 저장하려면 .Net Framework Data Provider for ODBC를 선택합니다.

ODBC 대상에 대한 연결 문자열을 제공하려면 사용할 ODBC 드라이버에 대한 설명서를 참조하거나 [The Connection Strings Reference](https://www.connectionstrings.com/)(연결 문자열 참조)에서 예제를 확인하세요. 

다음 스크린샷은 SQL Server에 대한 ODBC 연결을 예제로 보여 줍니다. 예제에서 사용된 연결 문자열은 다음과 같습니다.

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

**ConnectionString** 필드에 연결 문자열을 입력하면 마법사에서 문자열을 구문 분석하고 목록의 **기타** 섹션에 개별 속성과 속성 값을 표시합니다.

![ODBC 연결 SQL 대상](../../integration-services/import-export-data/media/odbc-connection-sql-destination.png)

 ## <a name="text-files-flat-files"></a>텍스트 파일(플랫 파일)
 
![플랫 파일 대상](../../integration-services/import-export-data/media/flat-file-destination.png)  

**파일 이름**  
 데이터를 저장할 파일의 경로 및 파일 이름을 지정합니다. 또는 **찾아보기** 를 클릭하여 파일을 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 파일을 찾습니다.  
  
 **로캘**  
 문자 정렬 순서와 날짜 및 시간 형식을 정의하는 로캘 ID(LCID)를 지정합니다.  
  
 **유니코드**  
 유니코드를 사용할지 여부를 나타냅니다. 유니코드를 사용하면 코드 페이지를 지정할 필요가 없습니다.  
  
 **코드 페이지**  
 사용할 언어의 코드 페이지를 지정합니다.  
  
 **형식**  
 구분 기호로 분리됨, 고정 폭, 왼쪽 정렬 중 어떤 서식을 사용할지를 지정합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|구분 기호로 분리됨|열이 구분 기호로 구분됩니다.|  
|고정 폭|열에 고정 폭이 지정됩니다.|  
|왼쪽 정렬|왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 구분됩니다.|  
  
 **텍스트 한정자**  
 사용할 텍스트 한정자를 입력합니다. 예를 들어 각 텍스트 열을 따옴표로 묶도록 지정할 수 있습니다.  
  
 **첫 번째 데이터 행의 열 이름**  
 첫 번째 데이터 행에 열 이름을 표시할지 여부를 나타냅니다.  
 
 ## <a name="microsoft-excel"></a>Microsoft Excel

>  **동영상**: 데이터를 Excel로 내보내는 마법사의 일반적인 용도입니다. 다음은 이렇게 하는 방법을 이해하기 쉬운 간단한 지침과 함께 설명하는 4분 길이의 YouTube 동영상입니다. [SQL Server 가져오기 및 내보내기 마법사를 사용하여 Excel로 내보내기](https://go.microsoft.com/fwlink/?linkid=829049) (이 동영상에서는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2012를 사용합니다.)

다음 스크린샷은 Microsoft Excel 통합 문서에 대한 샘플 연결을 보여 줍니다.

![Excel 대상](../../integration-services/import-export-data/media/excel-destination.png) 
 
 **Excel 파일 경로**  
 데이터를 내보낼 스프레드시트의 경로 및 파일 이름을 지정합니다. 예를 들어 로컬 컴퓨터에 있는 파일의 경우 **C:\\MyData.xlsx**, 네트워크 공유에 있는 파일의 경우 **\\\\Sales\\Database\\Northwind.xlsx**를 지정합니다. 또는 **찾아보기**를 클릭합니다.   
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  

> [!NOTE] 마법사에서는 암호로 보호된 Excel 파일을 열 수 없습니다.

 **Excel 버전**  
대상 통합 문서에서 사용할 Excel 버전을 선택합니다.  

선택한 Excel 버전에 연결할 추가 파일을 다운로드하여 설치해야 할 수 있습니다. 자세한 내용은 이 페이지의 [Excel 및 Access에 필요한 다운로드 가져오기](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads)를 참조하세요.

버전을 지정할 때 문제가 발생하는 경우(예: Microsoft Office 365가 있어서 Access 2016 런타임을 설치할 수 없는 경우) 이전 버전을 비롯한 다른 버전(예: 2016 대신 2013)을 지정해 보세요.

**첫 행은 열 이름으로**  
이 옵션은 Excel 대상에는 영향을 주지 않는 것 같습니다. 대상에 열 이름이 없는 경우 드라이버는 이 옵션을 사용하도록 설정한 경우에도 열 이름을 출력하지 않습니다. 내부적으로 마법사는 F1, F2 등을 임시 열 머리글로 사용합니다.
 
## <a name="microsoft-access"></a>Microsoft Access  

다음 스크린샷은 Microsoft Access 데이터베이스에 대한 샘플 연결을 보여 줍니다.

![Access 대상](../../integration-services/import-export-data/media/access-destination.png)

 **파일 이름**  
 데이터를 내보낼 데이터베이스 파일의 경로 및 파일 이름을 지정합니다. 예를 들어 **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**와 같이 지정할 수 있습니다. 또는 **찾아보기**를 클릭합니다.
 
 >   [!NOTE] 마법사는 .MDB 파일 형식의 Access 데이터베이스에만 연결할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 데이터베이스 파일을 찾습니다.  
  
 **사용자 이름**  
작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 유효한 사용자 이름을 입력합니다.  
  
 **암호**  
작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 대한 사용자 암호를 입력합니다.

데이터베이스가 모든 사용자에 대해 단일 암호로 보호되는 경우 **데이터 연결 속성** 대화 상자에서 해당 값을 입력합니다. **데이터 연결 속성** 대화 상자를 열려면 **고급**을 클릭합니다.    
  
 **고급**  
**데이터 연결 속성** 대화 상자를 사용하여 데이터베이스 암호 또는 기본이 아닌 작업 그룹 정보 파일과 같은 고급 옵션을 지정합니다.  
  
## <a name="a-nameofficedownloadsaget-the-downloads-you-need-for-excel-and-access"></a><a name="officeDownloads"></a>Excel 및 액세스에 필요한 다운로드 가져오기  
Microsoft Excel 및 Access 데이터 원본용 연결 구성 요소가 아직 설치되지 않은 경우 다운로드해야 할 수 있습니다.

최신 버전 구성 요소는 이전 버전의 프로그램에서 만든 파일을 열 수 있습니다. 경우에 따라 이전 버전의 구성 요소가 최신 버전의 프로그램에서 만든 파일을 열 수도 있습니다.  
  
컴퓨터에 32비트 버전의 Office가 설치된 경우 32비트 버전의 구성 요소를 설치해야 합니다. 또한 마법사(또는 마법사에서 만드는 Integration Services 패키지)를 32비트 모드에서 실행해야 합니다. 
 |Microsoft Office 버전|다운로드|  
|------------------------------|--------------|  
|2007|[2007 Office System 드라이버: 데이터 연결 구성 요소](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|  
 
## <a name="azure-blob-storage"></a>Azure Blob Storage  
Azure Blob 대상을 사용하려면 SSIS용 Azure 기능 팩을 설치해야 합니다. 자세한 내용은 [Integration Services용 Azure 기능 팩&#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)을 참조하세요.  

>   [!NOTE] Azure Storage 연결 관리자와 이를 사용하는 구성 요소(Blob 대상 포함)에서 일반 용도 저장소 계정과 Blob Storage 계정 모두에 연결할 수 있도록 하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 이러한 두 가지 유형의 저장소 계정에 대한 자세한 내용은 [Microsoft Azure Storage 소개](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)를 참조하세요.

![Azure Blob 대상](../../integration-services/import-export-data/media/azure-blob-destination.png)

**Azure 계정 사용**  
온라인 계정을 사용할지 여부를 지정합니다.

 **Storage 계정 이름**  
 Azure 저장소 계정의 이름을 지정합니다.  
  
 **계정 키**  
 Azure 저장소 계정의 키를 입력합니다.  
  
 **HTTPS 사용**  
 저장소 계정에 연결할 때 사용할 프로토콜(HTTP 또는 HTTPS)을 지정합니다.  
  
 **로컬 개발자 계정 사용**  
 로컬 컴퓨터의 저장소 에뮬레이터를 사용할지 여부를 지정합니다.  
  
 **Blob 컨테이너 이름**  
 지정된 저장소 계정에서 사용할 수 있는 저장소 컨테이너 목록에서 컨테이너를 선택합니다.  
  
 **Blob 파일 형식**  
 텍스트 또는 Avro 파일 형식을 선택합니다.  
  
 **열 구분 기호 문자**  
 텍스트 형식을 선택한 경우 열 구분 기호 문자를 지정합니다.  
  
 **첫 행은 열 이름으로**  
 첫 번째 데이터 행에 열 이름을 포함할지 여부를 지정합니다.  

## <a name="whats-next"></a>다음 단계  
 데이터 대상 및 연결하는 방법에 대한 정보를 제공한 후 다음 페이지는 **테이블 복사 또는 쿼리 지정**입니다. 이 페이지에서는 전체 테이블을 복사할지 또는 특정 행만 복사할지 지정합니다. 자세한 내용은 [테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)을 참조하세요.  
