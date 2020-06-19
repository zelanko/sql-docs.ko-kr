---
title: SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6b32a3ac28174b60f955f8c91428d0874f43719b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962803"
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services
  
[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 엔터프라이즈 수준 데이터 통합 및 데이터 변환 솔루션을 빌드하기 위한 플랫폼입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 파일을 복사 또는 다운로드하고 이벤트에 응답하여 전자 메일 메시지를 보내며 데이터 웨어하우스를 업데이트하고 데이터를 정리 및 마이닝하며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체와 데이터를 관리하여 복잡한 비즈니스 문제를 해결할 수 있습니다. 패키지는 단독으로 또는 다른 패키지와 함께 작동하여 복잡한 비즈니스 요구를 처리할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 XML 데이터 파일, 플랫 파일, 관계형 데이터 원본과 같은 다양한 원본에서 데이터를 추출 및 변환한 다음 하나 이상의 대상으로 로드할 수 있습니다.<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에는 다양한 기본 제공 태스크와 변환 집합, 패키지 생성 도구, 패키지 실행 및 관리를 위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 포함되어 있습니다. 그래픽 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 도구를 사용하여 코드를 한 줄도 작성하지 않고 솔루션을 만들거나 광범위한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델을 프로그래밍하여 패키지를 프로그래밍 방식으로 만들고 사용자 지정 태스크 및 기타 패키지 개체를 코딩할 수 있습니다.<br /><br /> **영역별 내용 찾아보기**<br /> ![작은 파일 폴더 아이콘](media/filefolder-small.gif "작은 파일 폴더 아이콘") [새로운 기능](what-s-new-in-integration-services-in-sql-server-2016.md)<br /><br /> ![작은 파일 폴더 아이콘](media/filefolder-small.gif "작은 파일 폴더 아이콘") [이전 버전과의 호환성](integration-services-backward-compatibility.md)<br /><br /> ![작은 파일 폴더 아이콘](media/filefolder-small.gif "작은 파일 폴더 아이콘") [Integration Services 기능 및 작업](../../2014/integration-services/integration-services-features-and-tasks.md)<br /><br /> ![작은 파일 폴더 아이콘](media/filefolder-small.gif "작은 파일 폴더 아이콘") [기술 참조](../../2014/integration-services/technical-reference-integration-services.md)  
  
 웹캐스트, [EIM (엔터프라이즈 정보 관리): channel9.msdn.com에서 SSIS, DQS 및 MDS를 함께](https://go.microsoft.com/fwlink/?LinkId=258672)제공 합니다.  
  
![Integration Services 아이콘 (작은 아이콘)](media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
  
