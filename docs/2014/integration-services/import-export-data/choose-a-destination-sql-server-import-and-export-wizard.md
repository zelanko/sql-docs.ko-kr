---
title: 대상 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 50c9419911f83c98fba5baf0f995ffbeafb916ad
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965653"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>대상 선택(SQL Server 가져오기 및 내보내기 마법사)
  **대상 선택** 페이지를 사용하여 복사할 데이터의 대상을 지정할 수 있습니다.  
  
 이 마법사에 대해 자세히 알아보려면 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조 하세요. 마법사 시작 옵션 및 마법사를 성공적으로 실행 하는 데 필요한 사용 권한에 대 한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사 실행](start-the-sql-server-import-and-export-wizard.md)을 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사는 원본에서 대상으로 데이터를 복사할 목적으로 사용됩니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **대상**  
 대상의 데이터 스토리지 형식과 일치하는 데이터 공급자를 선택합니다. 데이터 원본에 사용할 수 있는 공급자가 여러 개 있을 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, .Net Framework Data Provider for SQL Server 또는 Microsoft OLE DB Provider for SQL Server를 사용할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 대상에 데이터를 저장하려면 .NET Framework Data Provider for ODBC를 선택합니다.  
  
 **데이터 원본** 속성의 옵션은 컴퓨터에 설치된 공급자에 따라 달라집니다. 다음 표에서는 일반적으로 사용하는 몇 가지 대상에 대한 옵션을 나열합니다. 다른 공급자에 대한 내용은 공급자 설명서를 참조하십시오.  
  
## <a name="dynamic-options"></a>동적 옵션  
 다음 섹션에서는 여러 개의 데이터 원본에 사용 가능한 옵션을 보여 줍니다. 대상 드롭다운 목록에서 사용 가능한 대상 중 일부는 여기에 나열되지 않았습니다.  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>대상 = SQL Server Native Client 또는 Microsoft OLE DB Provider for SQL Server  
 **서버 이름**  
 데이터를 받을 서버 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 패키지에서 Microsoft Windows 인증을 사용하여 데이터베이스에 로그인해야 하는지 여부를 지정합니다. 보안을 강화하려면 Windows 인증을 사용하는 것이 좋습니다.  
  
 **SQL Server 인증 사용**  
 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 데이터베이스에 로그인할지 여부를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 사용자 이름을 지정합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 데이터베이스 연결에 대한 암호를 입력합니다.  
  
 **Database**  
 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 데이터베이스 목록에서 선택하거나 **새로 만들기**단추를 클릭하여 새 데이터베이스를 만듭니다.  
  
 **새로 고침**  
 **새로 고침**을 클릭하여 사용 가능한 데이터베이스 목록을 복원합니다.  
  
 **새 항목**  
 **데이터베이스 만들기** 대화 상자를 사용하여 새 대상 데이터베이스를 만듭니다.  
  
### <a name="destination--flat-file-destination"></a>대상 = 플랫 파일 대상  
 **파일 이름**  
 데이터를 저장할 파일의 경로 및 파일 이름을 지정합니다. 또는 **찾아보기** 를 클릭하여 파일을 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 파일을 찾습니다.  
  
 **Locale**  
 문자 정렬 순서와 날짜 및 시간 형식을 정의하는 로캘 ID(LCID)를 지정합니다.  
  
 **유니코드**  
 유니코드를 사용할지 여부를 나타냅니다. 유니코드를 사용하면 코드 페이지를 지정할 필요가 없습니다.  
  
 **코드 페이지**  
 사용할 언어의 코드 페이지를 지정합니다.  
  
 **Format**  
 구분 기호로 분리됨, 고정 폭, 왼쪽 정렬 중 어떤 서식을 사용할지를 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|구분됨|**열** 페이지에 지정된 구분 기호로 열을 구분합니다.|  
|고정 폭|열에 고정 폭이 지정됩니다.|  
|왼쪽 정렬|왼쪽 정렬 파일은 마지막 열을 제외한 모든 열에 고정 폭이 지정된 파일입니다. 마지막 열은 행 구분 기호로 구분됩니다.|  
  
 **텍스트 한정자**  
 사용할 텍스트 한정자를 입력합니다. 예를 들어 각 텍스트 열을 따옴표로 묶도록 지정할 수 있습니다.  
  
 **첫 번째 데이터 행의 열 이름**  
 첫 번째 데이터 행에 열 이름을 표시할지 여부를 나타냅니다.  
  
### <a name="destination--microsoft-excel"></a>대상 = Microsoft Excel  
  
> [!NOTE]  
>  Excel 2003 또는 이전 버전을 사용하는 데이터 원본에 연결하려는 경우에만 **Microsoft Excel** 을 선택하십시오. Excel 2007를 사용 하는 데이터 원본에 연결 하려면 **Microsoft Office 12.0 Access 데이터베이스 엔진 OLE DB 공급자**를 선택 하 **고 속성**을 클릭 한 다음 **데이터 연결 속성** 대화 상자의 **모두** 탭에서 **확장 속성**에을 입력 `Excel 12.0` 합니다.  
  
 **Excel 파일 경로**  
 데이터를 저장할 통합 문서의 경로 및 파일 이름을 지정 합니다 (예: C:\MyData.xls \\\Sales\Database\Northwind.xls). 또는 **찾아보기** 를 클릭하여 통합 문서를 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 Excel 통합 문서를 찾습니다.  
  
 **Excel 버전**  
 대상 통합 문서에서 사용할 Excel 버전을 선택합니다.  
  
> [!NOTE]  
>  데이터를 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 대상으로 내보낼 때 마법사는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 대상 구성 요소를 사용합니다. 몇 가지 사용 시 고려 사항 및 알려진 문제에 대한 자세한 내용은 [Excel Destination](../data-flow/excel-destination.md)을 참조하십시오.  
  
### <a name="destination--microsoft-access"></a>대상 = Microsoft Access  
  
> [!NOTE]  
>  Access 2003 또는 이전 버전을 사용하는 데이터베이스에 연결하려는 경우에만 **Microsoft Access** 를 선택하십시오. Access 2007을 사용하는 데이터베이스에 연결하려면 **Microsoft Office 12.0 Access Database Engine OLE DB Provider**를 선택하십시오.  
  
 **파일 이름**  
 데이터를 저장할 데이터베이스 파일의 경로 및 파일 이름 (예: C:\MyData.mdb, \Sales\Database\Northwind.mdb)을 지정 합니다 \\ . 또는 **찾아보기** 를 클릭하여 데이터베이스 파일을 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 해당 데이터베이스 파일을 찾습니다.  
  
 **사용자 이름**  
 작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 유효한 사용자 이름을 지정합니다.  
  
 **암호**  
 작업 그룹 정보 파일이 데이터베이스에 연결된 경우 데이터베이스 연결에 대한 사용자 암호를 입력합니다. 그러나 모든 사용자에 대해 단일 암호를 사용하여 데이터베이스를 보호하는 경우 **고급** 단추를 클릭하여 액세스하는 **데이터 연결 속성** 대화 상자에서 이 값을 제공해야 합니다.  
  
 **고급**  
 **데이터 연결 속성** 대화 상자를 사용하여 데이터베이스 암호 또는 기본이 아닌 작업 그룹 정보 파일과 같은 고급 옵션을 지정합니다. OLE DB 공급자 속성에 대한 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553)의 데이터 액세스 섹션을 검색하십시오.  
  
  
