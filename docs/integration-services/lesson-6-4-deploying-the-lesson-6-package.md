---
title: "4 단계: 6 단원 패키지를 배포 하 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d9be296088cf3f455f8790ff013ab0c1df14b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-6-4---deploying-the-lesson-6-package"></a>6-4-6 단원 패키지를 배포 단원
패키지를 배포하려면 SQL Server 인스턴스의 Integration Services에서 SSISDB 카탈로그에 패키지를 추가해야 합니다. 이 단원에서는 6 단원 패키지를 SSISDB 카탈로그에 추가하고, 매개 변수를 설정하 고 패키지를 실행합니다. 이 단원에서 SQL Server Management Studio를 사용하여 SSISDB 카탈로그에 6 단원 패키지를 추가하고 패키지를 배포합니다. 패키지를 배포한 후 새 위치를 가리키도록 패키지를 수정한 다음 매개 변수를 실행합니다.  
  
이 단원에서는 다음을 수행합니다.  
  
-   SQL Server의 SSIS 노드에서 SSISDB 카탈로그에 패키지를 추가합니다.  
  
-   패키지를 배포합니다.  
  
-   패키지 매개 변수 값을 설정합니다.  
  
-   SSMS에서 패키지를 실행합니다.  
  
### <a name="to-locate-or-add-the-the-ssisdb-catalog"></a>SSISDB 카탈로그를 찾거나 추가하려면  
  
1.  시작, 모든 프로그램, Microsoft SQL Server 2012를 가리킨 다음 SQL Management Studio를 클릭합니다.  
  
2.  서버에 연결 대화 상자에서 기본 설정을 확인한 다음 연결을 클릭합니다. 연결하려면 서버 이름 상자에 SQL Server가 설치된 컴퓨터의 이름을 입력해야 합니다. 데이터베이스 엔진이 명명된 인스턴스인 경우 서버 이름 상자에 <computer_name>\\<instance_name> 형식으로 인스턴스 이름도 입력해야 합니다.  
  
3.  개체 탐색기에서 Integration Services 카탈로그를 확장합니다.  
  
4.  Integration Services 카탈로그 아래에 나열된 카탈로그가 없는 경우에 SSISDB 카탈로그를 추가합니다.  
  
5.  SSISDB 카탈로그를 추가하려면 Integration Services 카탈로그를 마우스 오른쪽 단추로 클릭하고 카탈로그 만들기를 클릭합니다.  
  
6.  카탈로그 만들기 대화 상자에서 CLR 통합 사용을 선택합니다.  
  
7.  암호 상자에 새 암호를 입력한 다음 암호를 다시 입력 상자에 다시 입력합니다. 입력한 암호를 기억해야 합니다.  
  
8.  SSISDB 카탈로그를 추가하려면 확인을 클릭합니다.  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>SSISDB 카탈로그에 패키지를 추가하려면  
  
1.  개체 탐색기에서 SSISDB를 마우스 오른쪽 단추로 클릭하고 폴더 만들기를 클릭합니다.  
  
2.  폴더 만들기 대화 상자에서 폴더 이름 상자에 SSIS 자습서를 입력하고 확인을 클릭합니다.  
  
3.  SSIS 자습서 폴더를 확장하고 프로젝트를 마우스 오른쪽 단추로 클릭하고 패키지 가져오기를 클릭합니다.  
  
4.  Integration Services 프로젝트 변환 마법사 소개 페이지에서 다음을 클릭합니다.  
  
5.  패키지 찾기 페이지에서 파일 시스템이 원본 목록에서 선택되어 있는지 확인한 다음 찾아보기를 클릭합니다.  
  
6.  폴더 찾아보기 대화 상자에서 SSIS 자습서 프로젝트를 포함하는 폴더를 찾은 다음 확인을 클릭합니다.  
  
7.  다음을 클릭합니다.  
  
8.  패키지 선택 페이지에서 SSIS 자습서의 패키지 6개가 모두 표시되어야 합니다. 패키지 목록에서 Lesson 6.dtsx를 선택하고 클릭합니다.  
  
9. 대상 선택 페이지에서 프로젝트 이름 상자에 SSIS 자습서 배포를 입력하고 다음을 클릭합니다.  
  
10. 검토 페이지에 도달할 때까지 나머지 마법사의 각 페이지에서 다음을 클릭합니다.  
  
11. 검토 페이지에서 변환을 클릭합니다.  
  
12. 변환이 완료되면 닫기를 클릭합니다.  
  
Integration Services 프로젝트 변환 마법사를 닫으면 SSIS가 Integration Services 배포 마법사를 표시합니다. 6 단원 패키지를 배포하려면 지금 이 마법사를 사용합니다.  
  
1.  Integration Services 배포 마법사 소개 페이지에서 프로젝트를 배포하기 위한 단계를 검토하고 다음을 클릭합니다.  
  
2.  대상 선택 페이지에서 서버 이름이 SSISDB 카탈로그를 포함하는 SQL Server의 인스턴스이고 경로에 SSIS 자습서 배포가 표시되는지 확인한 후 다음을 클릭합니다.  
  
3.  검토 페이지에서 요약을 검토한 다음 배포를 클릭합니다.  
  
4.  배포가 완료되면 닫기를 클릭합니다.  
  
5.  개체 탐색기에서 Integration Services 카탈로그를 마우스 오른쪽 단추로 클릭하고 새로고침을 클릭합니다.  
  
6.  Integration Services 카탈로그를 확장한 다음 SSISDB를 확장합니다. 프로젝트가 완전히 확장될 때까지 SSIS 자습서에서 트리를 계속 확장합니다. SSIS 자습서 배포 노드의 패키지 노드 아래에 Lesson 6.dtsx가 표시되어야 합니다.  
  
패키지가 완료되었는지 확인하려면 Lesson 6.dtsx를 마우스 오른쪽 단추로 클릭하고 구성을 클릭합니다. 구성 대화 상자에서 매개 변수를 선택하고, 컨테이너에 Lesson 6.dtsx, 이름에 VarFolderName, 값에 새 New Sample Data 경로가 입력되어 있는지 확인한 다음, 닫기를 클릭 합니다.  
  
새 샘플 데이터 폴더 만들기를 진행하기 전에 Sample Data Two라고 이름을 지정하고 원래의 샘플 파일 3개를 여기에 복사합니다.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>새 예제 데이터 폴더를 만들고 채우려면  
  
1.  Windows 탐색기의 드라이브 루트 수준(예: C:\\)에서 Sample Data Two라는 새 폴더를 만듭니다.  
  
2.  C:\Program Files\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data 폴더를 열고 폴더에서 3개 샘플 파일 중 하나를 복사합니다.  
  
3.  New Sample Data 폴더에 복사한 파일을 붙여 넣습니다.  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>새 샘플 데이터를 가리키도록 패키지 매개 변수를 변경하려면  
  
1.  개체 탐색기에서 Lesson 6.dtsx를 마우스 오른쪽 단추로 클릭한 다음 구성을 클릭합니다.  
  
2.  구성 대화 상자에서 매개 변수 값을 Sample Data Two 경로로 변경합니다. 예를 들어, C 드라이브의 루트 폴더에 새 폴더를 배치하는 경우 C:\Sample Data Two가 됩니다.  
  
3.  확인을 클릭하여 구성 대화 상자를 닫습니다.  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>6 단원 패키지 배포를 테스트하려면  
  
1.  개체 탐색기에서 Lesson 6.dtsx를 마우스 오른쪽 단추로 클릭한 다음 실행을 클릭합니다.  
  
2.  패키지 실행 대화 상자에서 확인을 클릭합니다.  
  
3.  메시지 대화 상자에서 예를 클릭하여 개요 보고서를 엽니다.  
  
패키지에 대한 개요 보고서는 패키지의 이름과 요약 상태를 보여줍니다. 실행 개요 섹션은 패키지의 각 작업에서 결과를 보여주고 사용된 매개 변수 섹션은 VarFolderName을 포함하여 패키지 실행에 사용된 모든 매개 변수의 이름과 값을 보여줍니다.  
  
  
  

