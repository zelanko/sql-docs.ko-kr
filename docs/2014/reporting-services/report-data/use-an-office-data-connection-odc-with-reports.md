---
title: (SharePoint 통합된 모드의 Reporting Services) 보고서에 Office 데이터 연결 (.odc) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 983f60396f48e488b20e25f18751f615ded799ff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106955"
---
# <a name="use-an-office-data-connection-odc-with-reports-reporting-services-in-sharepoint-integrated-mode"></a>보고서에 Office 데이터 연결(.odc) 사용(SharePoint 통합 모드의 Reporting Services)
  제한된 시나리오에서 기존 Office 데이터 연결 파일(.odc)을 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 연결 정보를 제공할 수 있습니다. 공유 데이터 원본을 만들 때 .rsds 파일 대신 .odc 파일을 사용할 수 있습니다. 보고서 서버는 .rsds 파일과 같은 방식으로 .odc 파일을 사용합니다. 즉, 이 파일을 읽어 데이터 원본 유형, 연결 문자열 및 자격 증명 정보를 확인합니다.  
  
 모든 .odc 파일을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에 사용할 수 있는 것은 아닙니다. 보고서 및 .odc 파일의 데이터 처리 확장 프로그램과 특징에 따라 .odc의 사용 가능 여부가 결정됩니다.  
  
-   보고서가 OLE DB 또는 ODBC 데이터 공급자에서 작동하도록 디자인되어야 합니다. 다른 데이터 처리 확장 프로그램을 사용하여 보고서를 만든 경우 보고서나 해당 쿼리에 OLE DB 또는 ODBC 데이터 공급자가 지원하지 않는 기능이 있을 수 있습니다.  
  
-   .odc 파일에 필요한 요소와 구조가 있어야 합니다. 데이터 공급자 및 자격 증명 설정이 보고서 서버에서 읽을 수 있도록 파일에 명시적으로 설정되어 있어야 합니다. 이러한 값을 설정하는 최상의 방법은 .odc 파일을 SharePoint 라이브러리로 업로드하기 전에 이 파일을 내보내는 것입니다.  
  
-   .odc 파일에서 OLE DB 또는 ODBC 연결 형식을 지정해야 합니다.  
  
-   .odc 파일에서 연결 문자열을 지정해야 합니다.  
  
-   자격 증명은 `None`, `Stored` 또는 `Integrated`로 설정될 수 있습니다. 자격 증명 방법을 `Stored`로 설정하면 보고서 서버가 저장된 자격 증명을 사용하는 대신 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 보고서 서버는 .odc 파일에 정의된 대로 저장된 자격 증명을 사용할 수 없습니다.  
  
-   보고서를 만드는 데 사용된 스키마와 동일한 스키마가 데이터 원본에 있어야 합니다. 데이터 구조가 다른 경우 보고서가 실행되지 않습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007에서 만든 .odc 파일이어야 합니다. 이전 버전의 .odc는 보고서 정의 파일과 호환되지 않습니다.  
  
 .odc 데이터 원본 유형이 지원되는 데이터 원본 유형과 비슷해 보이지만 보고서 서버에서 처리할 수 없는 데이터 원본에 대한 연결을 지정하는 .odc 파일은 사용할 수 없습니다. 특히 Microsoft Excel 2007에서 Microsoft Access, 웹 또는 텍스트 파일의 데이터를 검색하는 .odc 파일을 만든 경우 이 .odc 파일을 사용하여 보고서에 데이터를 제공할 수 없습니다.  
  
 보고서 작성기 보고서와 모델은 .odc 파일에서 작동하지 않습니다. .odc 파일을 사용하여 모델을 생성할 수 없으며 .odc 파일에 연결된 공유 데이터 원본을 사용하도록 모델을 구성할 수도 없습니다.  
  
 .odc 파일에 익숙하지 않을 경우 다음 지침을 사용하여 .odc 파일을 만들고 내보낼 수 있습니다. OLE DB 데이터 원본에 사용할 .odc 파일을 만드는 한 가지 쉬운 방법은 Excel 2007과 데이터 연결 마법사를 사용하는 것입니다. 이때 마법사에서 데이터 원본을 만들지 않으며 이미 정의된 외부 데이터 원본이 있어야 합니다.  
  
 기존 .odc 파일은 보고서 및 쿼리와 완전히 호환되는 경우에만 사용해야 합니다. 보고서나 .odc 파일을 완전히 수정해야 하는 오류가 발생하면 보고서에 대해 새 .rsds 파일을 만들어야 합니다. .rsds 파일을 사용하는 공유 데이터 원본을 만드는 방법은 [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)를 참조하세요.  
  
### <a name="to-create-and-export-an-odc-file"></a>.odc 파일을 만들고 내보내려면  
  
1.  Excel 2007을 시작합니다.  
  
2.  **데이터** 탭의 **외부 데이터 가져오기** 그룹에서 **기타 원본**을 클릭한 다음 **데이터 연결 마법사**를 클릭합니다.  
  
3.  **기타/고급**을 선택한 후 **다음**을 클릭합니다.  
  
4.  **Microsoft OLE DB Provider for SQL Server**를 선택한 후 **다음**을 클릭합니다.  
  
5.  서버의 이름(기본적으로 컴퓨터의 네트워크 이름) 및 유효한 로그인과 데이터베이스 사용 권한을 가진 사용자 계정을 입력합니다. **다음**을 클릭합니다.  
  
6.  데이터베이스를 선택한 다음 **확인** 을 클릭하여 **데이터 연결** 대화 상자를 닫습니다.  
  
7.  **특정 테이블에 연결** 확인란은 기본적으로 선택되어 있으며 특정 테이블에서 데이터를 검색하는 데 사용됩니다. 보고서 서버는 .odc 파일의 모든 쿼리를 무시하므로 이 확인란의 선택 여부는 상관이 없습니다. 보고서 데이터를 검색하는 쿼리는 외부 파일이 아닌 보고서 정의에 포함되어 있습니다.  
  
8.  연결이 열려 있는 동안 속성을 편집하여 내보낼 수 있습니다. **데이터** 탭의 **연결** 그룹에서 **속성**을 클릭한 다음 연결 이름 옆에 있는 **연결 속성** 단추를 클릭합니다.  
  
9. **정의** 탭에서 **연결 파일 내보내기**를 클릭합니다.  
  
10. 파일 이름을 입력한 다음 **저장**을 클릭합니다. 애플리케이션과 열려 있는 모든 파일을 닫습니다.  
  
### <a name="to-upload-and-use-an-odc-file"></a>.odc 파일을 업로드하고 사용하려면  
  
1.  연결 파일을 업로드할 라이브러리를 엽니다.  
  
2.  **업로드** 메뉴에서 **문서 업로드**를 클릭합니다.  
  
3.  **찾아보기**를 클릭합니다.  
  
4.  직접 만든 .odc 파일을 선택합니다. 기본적으로 .odc 파일은 My Documents 폴더의 My Data Sources에 있습니다.  
  
5.  **열기** 를 클릭하여 파일을 선택하고 **확인** 을 클릭하여 선택 내용을 저장합니다. 새 항목의 속성 페이지가 자동으로 열립니다.  
  
6.  콘텐츠 형식에서 **보고서 데이터 원본**을 선택한 다음 **확인**을 클릭합니다.  
  
7.  보고서를 가리킵니다.  
  
8.  아래쪽 화살표를 클릭하고 **데이터 원본 관리**를 선택합니다.  
  
9. 데이터 원본 이름을 클릭합니다.  
  
10. 보고서에서 사용자 지정 데이터 원본 정보를 사용하는 경우 **공유**를 클릭합니다.  
  
11. **데이터 원본 연결**에서 찾아보기(**...**) 단추를 클릭합니다.  
  
12. 방금 업로드한 .odc 파일을 선택합니다.  
  
13. **확인** 을 클릭하여 파일을 선택한 다음 **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
     [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스와 예제 보고서를 사용하여 이러한 단계를 수행하는 경우 Company Sales 보고서만 .odc 파일에서 추가 작업 없이 작동한다는 사실에 유의하십시오. 다른 예제 보고서에는 OLE DB 공급자에서 작동하지 않는 쿼리 매개 변수와 기능이 들어 있습니다. 하지만 먼저 보고서 디자이너에서 이러한 보고서를 수정하면 OLE DB 공급자에서 작동하도록 만들 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
