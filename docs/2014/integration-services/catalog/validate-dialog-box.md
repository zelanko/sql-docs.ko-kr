---
title: 유효성 검사 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackagevalidate.f1
- sql12.ssis.ssms.isprojectvalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aaa7f88cda8c2c3cbda7ca38b2531de6354e83f5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819305"
---
# <a name="validate-dialog-box"></a>유효성 검사 대화 상자
  **유효성 검사** 대화 상자에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 또는 패키지의 일반적인 문제를 확인할 수 있습니다.  
  
 문제가 있는 경우 대화 상자의 맨 위에 메시지가 표시됩니다. 그렇지 않으면 준비가 맨 위에 표시됩니다.  
  
 **수행 작업**  
  
-   [유효성 검사 대화 상자 열기](#open_dialog)  
  
-   [일반 페이지의 옵션 설정](#general)  
  
##  <a name="open_dialog"></a> 유효성 검사 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  유효성을 검사하려는 프로젝트 또는 패키지가 포함된 폴더를 확장합니다.  
  
5.  프로젝트 또는 패키지를 마우스 오른쪽 단추로 클릭하고 **유효성 검사**를 클릭합니다.  
  
##  <a name="general"></a> 일반 페이지의 옵션 설정  
 **환경**  
 프로젝트 또는 패키지의 유효성을 검사하기 위해 사용하려는 환경을 선택합니다.  
  
 **32비트 런타임**  
 패키지를 실행하기 위해 32비트 런타임을 사용하려면 선택합니다.  
  
 **매개 변수** 탭에는 프로젝트 또는 패키지의 유효성을 검사하기 위해 사용하는 매개 변수 값이 나열됩니다. 다음은 매개 변수 탭의 옵션입니다.  
  
 **컨테이너**  
 매개 변수가 포함된 개체를 나열합니다.  
  
 **매개 변수**  
 매개 변수 이름을 나열합니다.  
  
 **Value**  
 매개 변수 값을 나열합니다.  
  
 **연결 관리자** 탭에는 프로젝트 또는 패키지의 유효성 검사를 위해 사용하는 연결 관리자 속성이 나열됩니다.  
  
 다음은 **연결 관리자** 탭의 옵션입니다.  
  
 **컨테이너**  
 연결 관리자 이름이 포함된 개체를 나열합니다.  
  
 **이름**  
 연결 관리자 이름을 나열합니다.  
  
 **속성 이름**  
 연결 관리자 속성 이름을 나열합니다.  
  
 **Value**  
 연결 관리자 속성에 할당된 값을 나열합니다.  
  
  
