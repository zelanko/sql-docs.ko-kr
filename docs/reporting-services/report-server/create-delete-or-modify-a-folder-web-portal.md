---
title: 폴더 만들기, 삭제 또는 수정 - Reporting Services | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 874fb7ba143c8f08a0f25501e1852b4d2b280cb2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67492860"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>폴더 만들기, 삭제 또는 수정 - Reporting Services
  폴더를 만들어 보고서 서버에 게시하는 항목을 구성하고 관리할 수 있습니다. 폴더를 만들면 관심 있는 보고서를 찾는 데 도움이 될 수 있습니다. 내용 관리자의 경우 폴더는 사용 권한을 적용하는 프레임워크를 제공합니다. 개발 중인 보고서나 배포되면 안 되는 보고서에 대한 액세스를 제한하기 위해 특정 폴더에 역할 할당을 만들 수 있습니다.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>폴더를 만들려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)를 시작합니다.  
  
2.  보고서 관리자에서 홈 폴더를 선택하고 **새 폴더**를 클릭합니다. 또는 기존 폴더 아래에 폴더를 만들려면 **내용** 페이지에서 해당 폴더로 이동한 후 폴더를 클릭하여 엽니다. 그런 후 **새 폴더**를 클릭합니다.  
  
     **새 폴더** 페이지가 열립니다.  
  
3.  폴더 이름을 입력합니다. 폴더 이름에 공백을 포함할 수 있지만 다음과 같이 URL 인코딩용으로 예약된 문자는 사용할 수 없습니다. \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. 한 번에 여러 개의 폴더 이름을 입력하여 여러 폴더를 만들 수는 없습니다.  
  
4.  설명을 입력합니다(옵션).  
  
5.  **내용** 페이지의 기본 보기에서 폴더를 표시하지 않으려면 **목록 뷰에서 숨기기** 를 선택합니다. **내용** 페이지에서 **자세한 정보 표시** 를 클릭하면 숨겨진 폴더가 표시됩니다.  
  
6.  **확인**을 클릭합니다.  
  
## <a name="to-delete-a-folder"></a>폴더를 삭제하려면  
  
1.  보고서 관리자에서 **내용** 페이지로 이동한 다음 수정할 항목을 찾습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **삭제**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>폴더를 수정하거나 삭제하려면  
  
1.  보고서 관리자에서 **내용** 페이지로 이동한 다음 수정할 항목을 찾습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 일반 속성 페이지가 열립니다.  
  
4.  폴더 위치를 변경하려면 **이동**을 클릭합니다. 대상 폴더의 위치를 입력하거나 트리에서 대상 폴더를 선택한 후 **확인**을 클릭합니다.  
  
5.  또는 다음과 같은 방법으로 폴더 속성을 수정합니다.  
  
    -   폴더에 대한 표시 텍스트를 수정하려면 이름이나 설명을 입력합니다.  
  
    -   **내용** 페이지에서 폴더를 기본 보기로 표시하려면 **목록 뷰에서 숨기기**의 선택을 취소합니다.  
  
6.  또는 폴더 및 해당 내용을 제거하려면 **삭제**를 클릭합니다.  
  
7.  **적용**을 클릭하여 변경 내용을 저장합니다.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>폴더를 만들려면  
  
1. [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)을 엽니다.  
  
2. 새 폴더를 찾으려는 폴더 또는 하위 폴더로 이동합니다. 페이지 왼쪽 상단에 있는 도구 모음에서 **찾아보기** 단추를 선택해 **홈** 폴더를 선택하여 폴더 계층 구조의 맨 위에 해당 폴더를 만듭니다.  
  
3. 보고서 서버 도구 모음의 오른쪽 위에 있는 **새로 만들기** 단추를 선택한 다음 드롭다운 메뉴에서 **폴더**를 선택합니다.  
  
4. **(현재 폴더 이름)에 새 폴더 만들기** 대화 상자에서 만들 새 폴더의 이름을 입력합니다. 폴더 이름에 공백을 포함할 수 있지만 다음과 같이 URL 인코딩용으로 예약된 문자는 사용할 수 없습니다. \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. 또한 한 번에 일련의 폴더 이름을 입력하여 여러 폴더를 만들 수는 없습니다.  
  
5. **만들기**를 선택하여 작업을 완료합니다.  
  
## <a name="to-delete-a-folder"></a>폴더를 삭제하려면  
  
1. 웹 포털에서 폴더 계층을 탐색하고 삭제하려는 폴더를 찾습니다.  
  
2. 폴더를 마우스 오른쪽 단추로 클릭하고 드롭다운 메뉴에서 **삭제**를 선택합니다.  
  
3. **<foldername> 삭제** 대화 상자에서 **삭제** 단추를 선택하여 삭제를 확인합니다.  
  
## <a name="to-modify-a-folders-properties"></a>폴더의 속성을 수정하려면  
  
1. 웹 포털에서 폴더 계층을 탐색하고 삭제하려는 폴더를 찾습니다.  
  
2. 폴더를 마우스 오른쪽 단추로 클릭하고 드롭다운 메뉴에서 **삭제**를 선택합니다.  
  
3. **속성** 탭을 선택합니다. **속성** 페이지가 표시됩니다.  
  
4. *이름** 텍스트 상자에서 폴더의 이름을 변경할 수 있습니다.  
  
5. *설명** 텍스트 상자에서 폴더 설명을 추가하거나 변경할 수 있습니다.  
  
6. **이 항목 숨기기** 확인란을 선택하거나 선택 취소하여 폴더를 숨기거나 표시할 수 있습니다.  
  
7. **적용**을 선택하여 속성 변경 내용을 저장합니다.  
  
8. 필요에 따라 **속성** 페이지 맨 위에 있는 **이동** 또는 **삭제** 단추를 선택하여 폴더를 이동하거나 삭제할 수 있습니다. 자세한 내용은 [항목 이동 또는 삭제(웹 포털)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md) 문서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [폴더 만들기, 삭제 또는 수정(웹 포털)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [보고서 서버 콘텐츠 관리(SSRS 기본 모드)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end