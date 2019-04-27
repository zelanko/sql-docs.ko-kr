---
title: '2단계: 프로젝트를 프로젝트 배포 모델로 변환 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba6dcb7052fed3d209dd87f55789a99df24116c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767355"
---
# <a name="step-2-converting-the-project-to-the-project-deployment-model"></a>2단계: 프로젝트를 프로젝트 배포 모델로 변환
  이 작업에서는 프로젝트를 프로젝트 배포 모델로 변환하기 위해 Integration Services 프로젝트 변환 마법사를 사용합니다.  
  
### <a name="converting-the-project-to-the-project-deployment-model"></a>프로젝트를 프로젝트 배포 모델로 변환  
  
1.  프로젝트 메뉴에서 프로젝트 배포 모델로 변환을 클릭합니다.  
  
2.  Integration Services 프로젝트 변환 마법사 소개 페이지에서 단계를 검토한 후 다음을 클릭합니다.  
  
3.  패키지 선택 페이지의 패키지 목록에서 Lesson 6.dtsx를 제외한 모든 확인란의 선택을 취소한 후 다음을 클릭합니다.  
  
4.  프로젝트 속성 지정 페이지에서 다음을 클릭합니다.  
  
5.  실행 패키지 태스크 업데이트 페이지에서 다음을 클릭합니다.  
  
6.  구성 선택 페이지의 구성 목록에서 Lesson 6.dtsx 패키지가 선택되었는지 확인한 후 다음을 클릭합니다.  
  
7.  매개 변수 만들기 페이지에서 Lesson 6.dtsx 패키지가 선택되었는지 확인하고 구성 속성 목록에서 범위를 패키지로 설정한 후 다음을 클릭합니다.  
  
8.  구성 속성 페이지에서 이름 및 값이 변수 및 구성 값에 대한 Lesson 5에서 지정된 이름 및 값과 동일한지 확인한 후 다음을 클릭합니다.  
  
9. 검토 페이지의 요악 창에서 속성을 변경하도록 설정된 구성 파일의 정보에 마법사가 사용됩니다.  
  
10. 변환을 클릭합니다.  
  
     변환이 완료되면 프로젝트가 Visual Studio에 저장될 때까지 변경 내용이 저장되지 않음을 경고하는 메시지가 표시됩니다. 경고 대화 상자에서 확인을 클릭합니다.  
  
11. Integration Services 프로젝트 변환 마법사에서 닫기를 클릭합니다.  
  
12. 변환된 패키지를 저장하려면 SQL Server Data Tools에서 파일 메뉴를 클릭한 후 저장을 클릭합니다.  
  
13. 매개 변수 탭을 클릭하고 패키지가 VarFolderName에 대한 매개 변수를 포함하게 되었는지 및 Lesson 5 구성 파일의 새 예제 데이터 폴더에서 지정된 것과 같은 경로의 값인지 확인합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [3단계: 6 단원 패키지 테스트](lesson-6-3-testing-the-lesson-6-package.md)  
  
  
