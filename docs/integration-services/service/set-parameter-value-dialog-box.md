---
title: "매개 변수 값 설정 대화 상자 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce9c2201-4e9a-4495-948f-b68deeaa7955
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d2e74c467cc0f94d15bdd4a42a300a842012ecd5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="set-parameter-value-dialog-box"></a>매개 변수 값 설정 대화 상자
  **매개 변수 값 설정** 대화 상자를 사용하여 패키지 및 프로젝트에 대한 매개 변수 및 연결 관리자 속성 값을 설정할 수 있습니다.  
  
 **수행 작업**  
  
-   [매개 변수 값 설정 대화 상자 열기](#open_dialog)  
  
-   [옵션 구성](#option)  
  
##  <a name="open_dialog"></a> 매개 변수 값 설정 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  패키지 또는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **구성**을 클릭한 다음 **매개 변수** 탭 또는 **연결 관리자** 탭에서 줄임표 단추를 클릭합니다.  
  
##  <a name="option"></a> 옵션 구성  
 **매개 변수**  
 매개 변수 이름을 나열합니다.  
  
 **형식**  
 매개 변수 값의 데이터 형식을 나열합니다.  
  
 **Description**  
 매개 변수에 대한 선택적 설명을 표시합니다.  
  
 **값 편집**  
 매개 변수 값을 편집하려면 이 옵션을 선택합니다.  
  
 **패키지에서 기본값 사용**  
 패키지에 저장된 기본 매개 변수 값을 사용하려면 이 옵션을 선택합니다.  
  
 **환경 변수 사용**  
 프로젝트 또는 패키지에서 참조하는 환경에 저장된 변수 값을 사용하려면 이 옵션을 선택합니다. 프로젝트 또는 패키지에 대한 환경 참조를 추가하려면 **구성** 대화 상자를 사용합니다. 자세한 내용은 [Configure Dialog Box](../../integration-services/service/configure-dialog-box.md)을 참조하세요.  
  
  
