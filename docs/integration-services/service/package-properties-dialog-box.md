---
title: "패키지 속성 대화 상자 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 2a3d348ee8bfe53c20d66b5dc39f96b4a4be635c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="package-properties-dialog-box"></a>패키지 속성 대화 상자
  **패키지 속성** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 저장된 패키지의 속성을 볼 수 있습니다.  
  
 자세한 내용은 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)를 참조하세요.  
  
 **수행 작업**  
  
-   [패키지 속성 대화 상자 열기](#open_dialog)  
  
-   [옵션 구성](#options)  
  
##  <a name="open_dialog"></a> 패키지 속성 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  속성을 확인할 패키지가 포함된 폴더를 확장합니다.  
  
5.  패키지를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
##  <a name="options"></a> 옵션 구성  
 **일반** 페이지를 사용하여 선택한 패키지의 속성을 볼 수 있습니다.  
  
 **일반** 페이지에 표시된 속성은 모두 읽기 전용입니다.  
  
 **이름**  
 패키지의 이름을 표시합니다.  
  
 **ID**  
 패키지 ID를 나열합니다.  
  
 **진입점**  
 **True** 값은 패키지가 직접 시작됨을 나타냅니다. **False** 값은 패키지가 패키지 실행 태스크로 다른 패키지에 의해 시작됨을 나타냅니다. 기본값은 **True**입니다.  
  
 솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭하고 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 진입점 패키지 **를 클릭하여**에서 부모 패키지 및 자식 패키지 모두에 대해 이 속성을 설정합니다.  
  
 **Description**  
 패키지에 대한 설명(옵션)을 표시합니다.  
  
  

