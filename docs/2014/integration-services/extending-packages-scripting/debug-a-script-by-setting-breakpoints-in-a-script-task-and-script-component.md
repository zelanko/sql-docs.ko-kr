---
title: 스크립트 태스크 및 스크립트 구성 요소에서 중단점을 설정하여 스크립트 디버깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 97c41b4ca75336f70b049239112132c89b05fba5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768489"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>스크립트 태스크 및 스크립트 구성 요소에서 중단점을 설정하여 스크립트 디버깅
  이 절차에서는 스크립트 태스크 및 스크립트 구성 요소에 사용되는 스크립트에서 중단점을 설정하는 방법에 대해 설명합니다.  
  
 스크립트에 중단점을 설정하면 중단점이 기본 제공 중단점과 함께** 중단점 설정 - \<개체 이름>** 대화 상자에 나열됩니다.  
  
> [!IMPORTANT]  
>  스크립트 태스크 및 스크립트 구성 요소의 중단점이 무시되는 경우도 있습니다. 자세한 내용은 스크립트 [태스크 코딩 및 디버깅](../control-flow/script-task.md) 의 스크립트 **태스크 디버깅** 섹션 및 [스크립트 구성 요소 코딩 및 디버깅]의 스크립트 **구성 요소 디버깅** 섹션을 참조 하십시오. /extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.  
  
### <a name="to-set-a-breakpoint-in-script"></a>스크립트에 중단점을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  중단점을 설정하려는 스크립트를 포함하는 패키지를 두 번 클릭합니다.  
  
3.  
  **제어 흐름** 탭을 클릭하고 스크립트 태스크를 두 번 클릭하여 스크립트 태스크를 엽니다.  
  
4.  
  **데이터 흐름** 탭을 클릭하고 스크립트 구성 요소를 두 번 클릭하여 스크립트 구성 요소를 엽니다.  
  
5.  
  **스크립트**를 클릭한 다음 **스크립트 편집**을 클릭합니다.  
  
6.  
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications)에서 중단점을 설정할 스크립트 줄을 찾아 마우스 오른쪽 단추로 클릭하고 **중단점**을 가리킨 다음 **중단점 삽입**을 클릭합니다.  
  
     코드 줄에 중단점 아이콘이 나타납니다.  
  
7.  **파일** 메뉴에서 **끝내기**를 클릭합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
  
