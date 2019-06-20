---
title: 만들기, 삭제 또는 공유 데이터 원본 (보고서 관리자)를 수정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c554215ba716a35f3e2851a5042be1989ee5648c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109608"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>공유 데이터 원본 만들기, 삭제 및 수정(보고서 관리자)
  공유 데이터 원본은 데이터 원본에 대한 연결 속성을 지정합니다. 많은 보고서, 모델 또는 데이터 기반 구독에서 사용되는 데이터 원본이 있는 경우 여러 위치에서 같은 연결 정보를 유지 관리해야 하는 오버헤드를 없애기 위해 공유 데이터 원본을 만드십시오.  
  
 다음 아이콘은 보고서 관리자 폴더 계층의 공유 데이터 원본을 나타냅니다.  
  
 ![공유 데이터 원본 아이콘](media/hlp-16datasource.png "공유 데이터 원본 아이콘")  
공유 데이터 원본 아이콘  
  
### <a name="to-create-a-shared-data-source"></a>공유 데이터 원본을 만들려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동합니다.  
  
3.  **새 데이터 원본**을 클릭합니다. **새 데이터 원본** 페이지가 열립니다.  
  
4.  항목의 이름을 입력합니다. 이름은 한 글자 이상이어야 하며 문자로 시작되어야 합니다. 특정 기호도 포함할 수 있지만 공백 또는 ; ? : \@ & = + , $ / * \< > | " /.  
  
5.  연결 정보를 제공하는 설명을 입력합니다(옵션). 이 설명은 보고서 관리자의 **내용** 페이지에 나타납니다.  
  
6.  **데이터 원본 유형** 목록에서 데이터 원본의 데이터를 처리하는 데 사용할 데이터 처리 확장 프로그램을 지정합니다.  
  
7.  **연결 문자열**에는 보고서 서버가 데이터 원본에 연결하는 데 사용하는 연결 문자열을 지정합니다. 연결 문자열에는 자격 증명을 지정하지 않는 것이 좋습니다.  
  
     다음 예에서는 로컬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스에 연결하기 위한 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  **연결 방법**에서 보고서를 실행할 때 자격 증명을 가져오는 방법을 지정합니다.  
  
    -   로그온 이름과 암호를 입력하라는 메시지를 표시하려면 **보고서를 실행하는 사용자가 제공한 자격 증명**을 클릭합니다. 사용자가 Windows 자격 증명으로 입력한 자격 증명을 사용하려면 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 클릭합니다. 사용자 이름과 암호가 데이터베이스 자격 증명인 경우 이 옵션을 선택하지 마십시오.  
  
    -   데이터 원본을 해당 소유자가 관리하는 저장된 자격 증명을 포함하는 공유 데이터 원본으로 사용하거나 자동화된 보고서 기록 생성과 같은 예약된 다른 작업이나 구독을 지원하는 보고서에 사용하려면 **보고서 서버에 안전하게 저장된 자격 증명**을 클릭합니다. 데이터베이스 서버가 가장 또는 위임을 지원하는 경우에는 **데이터 원본에 연결한 후 인증된 사용자로 가장**을 선택할 수 있습니다.  
  
    -   보고서 서버가 보고서에 액세스하는 사용자의 자격 증명을 외부 데이터 원본을 호스팅하는 서버에 전달하도록 하려면 **Windows 통합 보안**을 클릭합니다. 이 경우 사용자 이름이나 암호를 입력하라는 메시지가 표시되지 않습니다.  
  
    -   데이터 원본이 파일 시스템에서 액세스되는 XML 파일인 경우와 같이 데이터 원본이 자격 증명을 사용하지 않는 경우 **자격 증명 필요 없음**을 클릭합니다. 이 자격 증명 유형은 데이터 원본에 대해 유효한 경우에만 지정해야 합니다. 인증이 필요한 데이터 원본에 대해 이 옵션을 선택하면 연결이 실패합니다. 이 옵션을 선택할 때는 사용자 자격 증명을 사용할 수 없는 경우 보고서 서버가 다른 컴퓨터에 연결하여 데이터나 파일을 검색할 수 있도록 허용하는 무인 실행 계정을 구성해야 합니다.  
  
     자격 증명 구성 방법에 대한 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요. 무인 실행 계정에 대한 자세한 내용은 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)을 참조하세요.  
  
9. **연결 테스트** 단추를 클릭하여 데이터 원본 구성의 유효성을 검사합니다.  
  
    > [!NOTE]  
    >  XML 데이터 원본 유형에서는 연결 테스트 단추를 지원하지 않습니다.  
  
10. **확인**을 클릭합니다.  
  
### <a name="to-modify-a-shared-data-source"></a>공유 데이터 원본을 수정하려면  
  
1.  보고서 관리자에서 내용 페이지로 이동합니다.  
  
2.  공유 데이터 원본 항목으로 이동하고 항목을 마우스로 가리킨 다음 드롭다운 목록을 클릭하고 상황에 맞는 메뉴에서 **관리**를 클릭합니다. **속성** 페이지가 열립니다.  
  
3.  데이터 원본을 수정한 후 **적용**을 클릭합니다.  
  
### <a name="to-delete-a-shared-data-source"></a>공유 데이터 원본을 삭제하려면  
  
-   보고서 관리자에서 **내용** 페이지로 이동한 후 다음 중 하나를 수행합니다.  
  
    -   공유 데이터 원본 항목으로 이동합니다.  
  
         항목을 클릭하여 엽니다. 일반 속성 페이지가 열립니다.  
  
         **삭제**를 클릭한 다음 **확인**을 클릭합니다.  
  
    -   **내용** 페이지에서 삭제할 데이터 원본이 들어 있는 폴더로 이동합니다.  
  
         항목을 마우스로 가리키고 드롭다운 목록을 클릭한 다음 상황에 맞는 메뉴에서 **삭제**를 클릭합니다.  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [내용 페이지&#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [보고서 데이터 원본 관리](report-data/manage-report-data-sources.md)   
 [보고서의 데이터 원본 속성 구성&#40;보고서 관리자&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
