---
title: '2단계: 패키지 구성 설정 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ee2c54b072cf9cd219bed10b0ade7f59fa8bc354
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721516"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>5-2단원: 패키지 구성 설정 및 구성

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 작업에서는 프로젝트를 패키지 배포 모델로 변환하고 패키지 구성 마법사를 사용하여 패키지 구성을 설정합니다. 이 마법사를 사용하여 Foreach 루프 컨테이너의 **Directory** 속성에 대한 구성 설정을 포함하는 XML 구성 파일을 생성합니다. 런타임에서 업데이트할 수 있는 새 패키지 수준 변수에서 **Directory** 속성 값을 제공합니다. 테스트에 사용할 새 샘플 데이터 폴더를 채울 수도 있습니다.  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>Directory 속성에 매핑된 새 패키지 수준 변수 만들기  
  
1.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서**제어 흐름** 탭의 배경을 선택합니다. 이 선택 영역에서는 패키지에 만든 변수의 범위를 설정합니다.  
  
2.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 메뉴에서 **변수**를 선택합니다.  
  
3.  **변수** 창에서 **변수 추가** 아이콘을 선택합니다.  
  
4.  **이름** 상자에 **varFolderName**을 입력합니다.  
  
    > [!IMPORTANT]  
    > 변수 이름은 대소문자를 구분합니다.  
  
5.  **범위** 상자에 패키지 이름 **5단원**이 표시되는지 확인합니다.  
  
6.  **변수의** 데이터 형식 `varFolderName` 상자 값을 **String**으로 설정합니다.  
  
7.  **제어 흐름** 탭으로 돌아가 **Foreach File in Folder** 컨테이너를 두 번 클릭합니다.  
  
8.  **Foreach 루프 편집기**의 **컬렉션** 페이지에서 **식**을 선택한 다음, 줄임표 단추 **(...)** 를 선택합니다.  
  
9. **속성 식 편집기**에서 **속성** 목록을 선택한 다음, **Directory**를 선택합니다.  
  
10. **식** 상자에서 줄임표 단추 **(...)** 를 선택합니다.  
  
11. **식 작성기**에서 **변수 및 매개 변수** 폴더를 확장하고 **User::varFolderName** 변수를 **식** 상자로 끌어옵니다.  
  
12. **확인**을 선택하여 **식 작성기**를 종료합니다.  
  
13. **확인**을 선택하여 **속성 식 편집기**를 종료합니다.  
  
14. **확인**을 선택하여 **Foreach 루프 편집기**를 종료합니다.  
  
## <a name="enable-package-configurations"></a>패키지 구성 설정  
  
1.  **프로젝트 메뉴**에서 **패키지 배포 모델로 변환**을 선택합니다.  
  
2.  경고 프롬프트에서 **확인**을 선택하고, 변환이 완료되면 **패키지 배포 모델로 변환** 대화 상자에서 **확인**을 선택합니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서**제어 흐름** 탭의 배경을 선택합니다.  
  
4.  **SSIS** 메뉴에서 **패키지 구성**을 선택합니다.  
  
5.  **패키지 구성 이끌이** 대화 상자에서 **패키지 구성 설정**을 선택한 다음, **추가**를 선택합니다.  
  
6.  **패키지 구성 마법사**의 시작 페이지에서 **다음**을 선택합니다.  
  
7.  **구성 유형 선택** 페이지에서 **구성 유형** 이 **XML 구성 파일**로 설정되었는지 확인합니다.  
  
8.  **구성 형식 선택** 페이지에서 **찾아보기**를 선택합니다.  
  
9. **구성 파일 위치 선택** 대화 상자가 프로젝트 폴더에 열립니다.  
  
10. **구성 파일 위치 선택** 대화 상자에서 **파일 이름**에 **SSISTutorial**을 입력한 다음, **저장**을 선택합니다.  
  
11. **구성 형식 선택** 페이지에서 **다음**을 선택합니다.
  
12. **내보낼 속성 선택** 페이지의 **개체** 창에서 **변수**, **varFolderName**, **속성**을 차례로 확장한 다음, **값**을 선택합니다.  
  
13. **내보낼 속성 선택** 페이지에서 **다음**을 선택합니다.  
  
14. **마법사 완료** 페이지에서 **SSIS 자습서 디렉터리 구성**과 같은 구성 이름을 입력합니다. 이 구성 이름이 **패키지 구성 이끌이** 대화 상자에 표시됩니다.  
  
15. **마침**을 선택합니다.  
  
16. **닫기**를 선택합니다.  
  
17. 이 마법사는 열거자의 **Directory** 속성을 설정하는 변수의 **값**에 대한 구성 설정을 포함하는 **SSISTutorial.dtsConfig** 구성 파일을 생성합니다.  
  
    > [!NOTE]  
    > 일반적으로 구성 파일에는 패키지 속성에 대한 복잡한 정보가 있지만 이 자습서에서는 구성 정보는 다음과 같아야 합니다.

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>새 샘플 데이터 폴더 만들기 및 채우기  
  
1.  Windows 탐색기의 드라이브 루트 수준(예: **C:\\**)에서 **New Sample Data**라는 폴더를 만듭니다.  
  
2.  컴퓨터에서 예제 파일을 찾아 폴더에서 3개의 파일을 복사합니다.  
  
3.  **New Sample Data** 폴더에 복사한 파일을 붙여넣습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[3단계: Directory 속성 구성 값 수정](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
