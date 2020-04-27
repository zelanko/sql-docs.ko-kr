---
title: '2단계: 배포 프로젝트 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f5b0cc2c86ef483a7e2b2c0f5dccba21383641f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62891850"
---
# <a name="step-2-creating-the-deployment-project"></a>2단계: 배포 프로젝트 만들기
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 배포 가능한 단위는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트입니다. 패키지를 배포할 수 있으려면 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만들고 모든 패키지 및 패키지와 함께 배포할 모든 보조 파일을 해당 프로젝트에 추가해야 합니다.  
  
### <a name="to-create-the-integration-services-project"></a>Integration Services 프로젝트를 만들려면  
  
1.  **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 후 **SQL Server Data Tools**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트** 를 클릭하여 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만듭니다.  
  
3.  **새 프로젝트** 대화 상자의 **템플릿** 창에서 **Integration Services 프로젝트** 를 선택합니다.  
  
4.  **이름** 상자에서 기본 이름을 **Deployment Tutorial**로 변경합니다. 필요에 따라 **솔루션용 디렉터리 만들기** 확인란의 선택을 취소합니다.  
  
5.  기본 위치를 적용하거나 **찾아보기** 를 클릭하여 사용할 폴더를 찾습니다.  
  
6.  **프로젝트 위치** 대화 상자에서 해당 폴더를 클릭한 다음 **열기**를 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  기본적으로 Package.dtsx라는 빈 패키지가 만들어지고 프로젝트에 추가됩니다. 그러나 이 패키지를 사용하는 대신에 기존 패키지를 프로젝트에 추가합니다. 프로젝트의 모든 패키지가 배포에 포함되므로 Package.dtsx를 삭제해야 합니다. 이 패키지를 삭제하려면 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [3단계: 패키지 및 기타 파일 추가](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 프로젝트](integration-services-ssis-projects-and-solutions.md)  
  
  
