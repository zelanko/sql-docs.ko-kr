---
title: 데이터 원본 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6e399cf6c145f36febd9b32ae7a84c54741bb43
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62893598"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>데이터 원본 선택(SQL Server 가져오기 및 내보내기 마법사)
  **데이터 원본 선택** 페이지를 사용 하 여 복사할 데이터의 원본을 지정할 수 있습니다.  
  
 이 마법사에 대해 자세히 알아보려면 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조 하세요. 마법사 시작 옵션 및 마법사를 성공적으로 실행 하는 데 필요한 권한에 대 한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 실행](start-the-sql-server-import-and-export-wizard.md)을 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본에서 대상으로 데이터를 복사할 목적으로 사용됩니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **데이터 원본**  
 원본의 데이터 스토리지 형식과 일치하는 데이터 공급자를 선택합니다. 데이터 원본에 사용할 수 있는 공급자가 여러 개 있을 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, .Net Framework Data Provider for SQL Server 또는 Microsoft OLE DB Provider for SQL Server를 사용할 수 있습니다.  
  
 **데이터 원본** 속성의 옵션은 컴퓨터에 설치된 공급자에 따라 달라집니다. 다음 표에서는 자주 사용되는 일부 대상에 대한 옵션을 나열합니다. 다른 공급자에 대한 내용은 공급자 설명서를 참조하십시오.  
  
## <a name="dynamic-options"></a>동적 옵션  
 다음 섹션에서는 여러 개의 데이터 원본에 사용 가능한 옵션을 보여 줍니다. 대상 드롭다운에서 사용 가능한 모든 대상이 여기에 나열된 것은 아닙니다.  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>데이터 원본 = SQL Server Native Client 및 Microsoft OLE DB Provider for SQL Server  
 **서버 이름**  
 데이터가 포함된 서버의 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 패키지에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증을 사용하여 데이터베이스에 로그인하도록 할지 여부를 지정합니다. 보안을 강화하려면 Windows 인증을 사용하는 것이 좋습니다.  
  
 **SQL Server 인증 사용**  
 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 데이터베이스에 로그인할지 여부를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 사용자 이름을 지정합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 암호를 입력합니다.  
  
 **Database**  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 데이터베이스 목록에서 선택합니다.  
  
 **새로 고침**  
 **새로 고침**을 클릭하여 사용 가능한 데이터베이스 목록을 복원합니다.  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>데이터 원본 = .NET Framework Data Provider for SQL Server  
 이 페이지에서는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 옵션을 사전순으로 나열합니다. 다음 표에서는 가장 중요한 옵션을 나열합니다.  
  
 **데이터 원본**  
 데이터가 포함된 서버의 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **초기 카탈로그**  
 원본 데이터베이스의 이름을 입력합니다.  
  
 **통합 보안**  
 Windows 통합 인증을 사용하여 연결(권장)하려면 `True`를 지정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하려면 `False`를 지정합니다. `False`를 지정하면 사용자 ID와 암호를 입력해야 합니다. 기본값은 `False`입니다.  
  
 **사용자 ID**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 사용자 이름을 지정합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 암호를 입력합니다.  
  
 이 공급자 선택 시 나열되는 추가 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 데이터베이스에 성공적으로 연결하기 위해 꼭 필요한 옵션은 아닙니다. 이러한 추가 옵션에 대한 자세한 설명은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 소프트웨어 개발 키트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Provider for [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 에 대한 설명서를 참조하십시오.  
  
### <a name="data-source--microsoft-excel"></a>데이터 원본 = Microsoft Excel  
  
> [!NOTE]  
>  Excel 2003 또는 이전 버전을 사용하는 데이터 원본에 연결하려는 경우에만 **Microsoft Excel** 을 선택하십시오. Excel 2007를 사용 하는 데이터 원본에 연결 하려면 **Microsoft Office 12.0 Access 데이터베이스 엔진 OLE DB 공급자**를 선택 하 **고 속성**을 클릭 한 다음 **데이터 연결 속성** 대화 상자의 **모두** 탭에서 **확장 속성**에 `Excel 12.0` 대 한 값을 입력 합니다.  
  
 **Excel 파일 경로**  
 데이터를 가져올 스프레드시트의 경로 및 파일 이름(예: 예를 들면 **C:\mydata.xls, \\\Sales\Database\Northwind.xls**입니다. 또는 **찾아보기**를 클릭합니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 스프레드시트를 찾습니다.  
  
 **Excel 버전**  
 원본 데이터가 저장된 Excel 버전을 선택합니다.  
  
> [!NOTE]  
>  데이터를 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 원본에서 가져올 때 마법사는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 원본 구성 요소를 사용합니다. 사용 시 고려 사항 및 알려진 문제에 대한 자세한 내용은 [Excel Source](../data-flow/excel-source.md)을 참조하십시오.  
  
### <a name="data-source--microsoft-access"></a>데이터 원본 = Microsoft Access  
  
> [!NOTE]  
>  Access 2003 또는 이전 버전을 사용하는 데이터베이스에 연결하려는 경우에만 **Microsoft Access** 를 선택하십시오. Access 2007를 사용 하는 데이터베이스에 연결 하려면 대신 **Microsoft Office 12.0 access 데이터베이스 엔진 OLE DB 공급자** 를 선택 합니다.  
  
 **파일 이름**  
 데이터를 가져올 데이터베이스 파일의 경로 및 파일 이름(예: 예를 들어 **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**와 같이 지정할 수 있습니다. 또는 **찾아보기**를 클릭합니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 데이터베이스 파일을 찾습니다.  
  
 **사용자 이름**  
 작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 유효한 사용자 이름을 지정합니다.  
  
 **암호**  
 작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 대한 사용자 암호를 입력합니다. 그러나 데이터베이스가 모든 사용자에 대해 단일 암호로 보호되는 경우 **고급** 을 클릭하여 액세스할 수 있는 **데이터 연결 속성**대화 상자에 해당 값을 입력해야 합니다.  
  
 **고급**  
 **데이터 연결 속성** 대화 상자를 사용 하 여 데이터베이스 암호 또는 기본이 아닌 작업 그룹 정보 파일과 같은 고급 옵션을 지정할 수 있습니다. OLE DB 공급자 속성에 대 한 자세한 내용은 [MSDN library](https://go.microsoft.com/fwlink/?linkid=62553)의 데이터 액세스 섹션을 검색 하십시오.  
  
### <a name="data-source--flat-file-source"></a>데이터 원본 = 플랫 파일 원본  
 플랫 파일 데이터 원본 옵션에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
 [플랫 파일 연결 관리자 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
 [플랫 파일 연결 관리자 편집기&#40;열 페이지&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
 [플랫 파일 연결 관리자 편집기&#40;고급 페이지&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [플랫 파일 연결 관리자 편집기&#40;미리 보기 페이지&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
  
