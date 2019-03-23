---
title: '6단원: 매개 변수를 사용 하 여 프로젝트 배포 모델로 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d559defe1dd08f26077738cdd0aea219e8f7554b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384961"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>6단원: 프로젝트 배포 모델에 매개 변수 사용
  SQL Server 2012에는 Integration Services 서버에 프로젝트를 배포할 수 있는 새로운 배포 모델이 도입되었습니다. Integration Services 서버에서는 패키지를 관리 및 실행하고 패키지에 대한 런타임 값을 구성할 수 있습니다.  
  
 이 단원에서 만든 패키지를 수정 [5 단원: 패키지 배포 모델을 위한 패키지 구성 추가](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) 프로젝트 배포 모델을 사용 하도록 합니다. 구성 값을 예제 데이터 위치를 지정하는 매개 변수로 바꿉니다. 또한 자습서에 포함된 완료된 5단원 패키지를 복사할 수도 있습니다.  
  
 Integration Services 프로젝트 구성 마법사를 사용하여 프로젝트를 프로젝트 배포 모델로 변환하고 구성 값이 아닌 매개 변수를 사용해서 디렉터리 속성을 설정합니다. 이 단원에서는 기존 SSIS 패키지를 새로운 프로젝트 배포 모델로 변환하기 위해 수행해야 하는 단계에 대해 일부 설명합니다.  
  
 패키지를 다시 실행하면 Integration Services 서비스가 매개 변수를 사용해서 변수 값을 채우고, 이 변수는 다시 디렉터리 속성을 업데이트합니다. 따라서 패키지 구성 파일에 설정된 폴더가 아니라 매개 변수 값으로 지정된 새 데이터 폴더의 파일이 패키지에서 반복 처리됩니다.  
  
> [!IMPORTANT]  
>  이 자습서를 실행하려면 **AdventureWorksDW2012** 예제 데이터베이스가 필요합니다. **AdventureWorksDW2012**설치 및 배포 방법에 대한 자세한 내용은 [SQL Server 예제 및 예제 데이터베이스 설치 시 고려 사항](https://technet.microsoft.com/library/ms161556%28v=sql.105%29)을 참조하십시오.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 다룹니다.  
  
1.  [1단계: 5 단원 패키지 복사](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [2단계: 프로젝트를 프로젝트 배포 모델로 변환](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [3단계: 6 단원 패키지 테스트](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [4단계: 6 단원 패키지 배포](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>단원 시작  
 [1단계: 5 단원 패키지 복사](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
