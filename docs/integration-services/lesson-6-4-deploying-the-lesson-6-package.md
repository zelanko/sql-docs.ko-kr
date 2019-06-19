---
title: '4단계: 6단원 패키지 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4c843fa7af8e3390e820714886b7988edab878d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65720816"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>6-4단원: 6단원 패키지 배포

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



패키지를 배포하려면 SQL Server 인스턴스의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 SSISDB 카탈로그에 패키지를 추가해야 합니다. 이 단원에서는 6단원 패키지를 SSISDB 카탈로그에 추가하고, 매개 변수를 설정하고 패키지를 실행하세요. 이 단원에서는 SQL Server Management Studio를 사용하여 SSISDB 카탈로그에 6단원 패키지를 추가하고 패키지를 배포하세요. 패키지를 배포한 후에 새 위치를 가리키도록 매개 변수를 수정한 다음, 패키지를 실행하세요.   
이 작업에서는 다음을 수행합니다.  

1. SQL Server의 SSIS 노드에서 SSISDB 카탈로그에 패키지를 추가합니다.  
  
2. 패키지를 배포합니다.  
  
3. 패키지 매개 변수 값을 설정합니다.  

4. SSMS에서 패키지를 실행합니다.  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>SSISDB 카탈로그 찾기 또는 추가  
  
1.  **시작** > **모든 프로그램** > **Microsoft SQL Server 2017**을 선택한 다음, **SQL Management Studio**를 선택합니다.  
  
2.  **서버에 연결** 대화 상자에서 기본 설정을 확인한 다음, **연결**을 선택합니다. 연결하려면 **서버** 이름이 SQL Server가 설치된 컴퓨터의 이름이어야 합니다. **데이터베이스 엔진**이 명명된 인스턴스인 경우 **서버** 이름이 *\<computer_name>\\\<instance_name>* 과 같은 형식의 인스턴스 이름이어야 합니다. 
  
3.  **개체 탐색기**에서 **Integration Services 카탈로그**를 확장합니다.  
  
4.  **Integration Services 카탈로그** 아래에 나열된 카탈로그가 없는 경우에 SSISDB 카탈로그를 추가합니다.  
  
5.  SSISDB 카탈로그를 추가하려면 **Integration Services 카탈로그**를 마우스 오른쪽 단추로 클릭하고 **카탈로그 만들기**를 선택합니다.  
  
6.  **카탈로그 만들기** 대화 상자에서 **CLR 통합 사용**을 선택합니다.  
  
7.  **암호** 상자에 새 암호를 입력한 다음, **암호 다시 입력** 상자에 다시 입력합니다. 
  
8.  SSISDB 카탈로그를 추가하려면 **확인**을 선택합니다.  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>SSISDB 카탈로그에 패키지 추가  
  
1.  **개체 탐색기**에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **폴더 만들기**를 선택합니다.  
  
2.  **폴더 만들기** 대화 상자에서 폴더 이름 상자에 SSIS 자습서를 입력하고 **확인**을 선택합니다.  
  
3.  **SSIS 자습서** 폴더를 확장하고 **프로젝트**를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 선택합니다.  
  
4.  **Integration Services 프로젝트 변환 마법사** **소개** 페이지에서 **다음**을 선택합니다.  
  
5.  **패키지 찾기** 페이지에서 **파일 시스템**이 **원본** 목록에서 선택되어 있는지 확인한 다음, **찾아보기**를 선택합니다.  
  
6.  **폴더 찾아보기** 대화 상자에서 SSIS 자습서 프로젝트를 포함하는 폴더를 찾은 다음, **확인**을 선택합니다.  
  
7.  **다음**을 선택합니다.  
  
8.  패키지 선택 페이지에서 SSIS 자습서의 패키지 6개가 모두 표시되어야 합니다. **패키지** 목록에서 **Lesson 6.dtsx**를 선택한 다음, **다음**을 선택합니다.  
  
9. **대상 선택** 페이지에서 **프로젝트 이름** 상자에 **SSIS 자습서 배포**를 입력한 다음, **다음**을 선택합니다.

10. **검토** 페이지에 도달할 때까지 나머지 마법사의 각 페이지에서 **다음**을 선택합니다.  
  
11. **검토** 페이지에서 **변환**을 선택합니다.  
  
12. 변환이 완료되면 **닫기**를 선택합니다.  
  
Integration Services 프로젝트 변환 마법사를 닫으면 SSIS가 Integration Services 배포 마법사를 표시합니다. 이제 이 마법사를 사용하여 6단원 패키지를 배포하세요.  
  
1.  **Integration Services 배포 마법사** **소개** 페이지에서 프로젝트를 배포하기 위한 단계를 검토한 다음, **다음**을 선택합니다.  
  
2.  **대상 선택** 페이지에서 서버 이름이 SSISDB 카탈로그를 포함하는 SQL Server의 인스턴스이고 경로에 **SSIS 자습서 배포**가 표시되는지 확인한 다음, **다음**을 선택합니다.  
  
3.  **검토** 페이지에서 **요약**을 검토한 다음, **배포**를 선택합니다.  
  
4.  배포가 완료되면 **닫기**를 선택합니다.  
  
5.  **개체 탐색기**에서 **Integration Services 카탈로그**를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
6.  **Integration Services 카탈로그**를 확장한 다음, **SSISDB**를 확장합니다. 프로젝트가 완전히 확장될 때까지 **SSIS 자습서**에서 트리를 계속 확장합니다. **SSIS 자습서 배포** 노드의 **패키지** 노드 아래에 **Lesson 6.dtsx**가 표시되어야 합니다.  
  
7.  패키지가 완료되었는지 확인하려면 **Lesson 6.dtsx**를 마우스 오른쪽 단추로 클릭하고 **구성**을 선택합니다. **구성** 대화 상자에서 **매개 변수**를 선택하고, **컨테이너**가 **Lesson 6.dtsx**이고, **이름**이 **VarFolderName**이고, 값이 **새 샘플 데이터** 경로인 항목이 있는지 확인한 다음, **닫기**를 선택합니다.  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>새 샘플 데이터 폴더 만들기 및 채우기  
  
1.  **Windows 탐색기**의 드라이브 루트 수준(예: **C:\\** )에서 **Sample Data Two**라는 폴더를 만듭니다.  
  
2.  [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)에서 **샘플 데이터** 폴더를 연 다음, 세 가지 샘플 파일을 복사하세요.  
  
3.  **Sample Data Two** 폴더로 이동하고 복사된 파일을 붙여넣습니다.  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>새 샘플 데이터를 가리키도록 패키지 매개 변수 변경  
  
1.  **개체 탐색기**에서 **Lesson 6.dtsx**를 마우스 오른쪽 단추로 클릭하고 **구성**을 선택합니다.  
  
2.  **구성** 대화 상자에서 매개 변수 값을 **Sample Data Two** 경로로 변경합니다(예: **C:\\Sample Data Two**).  
  
3.  **확인**을 선택하여 **구성** 대화 상자를 닫습니다.  
  
## <a name="test-the-lesson-6-package-deployment"></a>6단원 패키지 배포 테스트  
  
1.  **개체 탐색기**에서 **Lesson 6.dtsx**를 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
2.  **패키지 실행** 대화 상자에서 **확인**을 선택합니다.  
  
3.  메시지 대화 상자에서 **예**를 선택하여 **개요 보고서**를 엽니다.  
  
패키지에 대한 **개요 보고서**는 패키지의 이름과 요약 상태를 표시합니다. **실행 개요** 섹션은 패키지에서 각 작업의 결과를 보여줍니다. **사용된 매개 변수** 섹션은 **VarFolderName**을 포함하여 패키지 실행에 사용된 모든 매개 변수의 이름과 값을 보여줍니다.  
  
