---
title: 프로젝트 속성 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectprop.general.f1
- sql13.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9aee0d7233b5f163a5f9c39f9053b9f0842aa7e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298951"
---
# <a name="project-properties-dialog-box"></a>프로젝트 속성 대화 상자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 하나의 배포 단위입니다. 각 프로젝트는 패키지, 매개 변수 및 환경 참조를 포함할 수 있습니다. 프로젝트는 검색 가능한 개체이며 데이터베이스 보안 주체의 사용 권한을 정의할 수 있습니다. 프로젝트를 다시 배포하는 경우 이전 버전의 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 저장할 수 있습니다.  
  
 프로젝트 매개 변수와 패키지 매개 변수는 실행 시 패키지 내의 속성에 값을 할당하는 데 사용됩니다. 일부 매개 변수 값은 패키지를 실행하는 데 필요합니다. 환경 변수를 참조하는 매개 변수 값이 있는 경우 프로젝트에 해당 환경 참조가 있어야 프로젝트가 실행됩니다.  
  
 **수행 작업**  
  
-   [프로젝트 속성 대화 상자 열기](#open_dialog)  
  
-   [일반 페이지의 옵션 설정](#general)  
  
-   [권한 페이지의 옵션 설정](#permissions)  
  
##  <a name="open-the-project-properties-dialog-box"></a><a name="open_dialog"></a> 프로젝트 속성 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  속성을 설정할 프로젝트가 포함된 폴더를 확장합니다.  
  
5.  프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a> 일반 페이지의 옵션 설정  
 일반 페이지를 사용하여 프로젝트 속성을 봅니다.  
  
 **이름**  
 프로젝트 이름을 나열합니다.  
  
 **식별자**  
 프로젝트 ID를 나열합니다.  
  
 **설명**  
 프로젝트에 대한 설명(옵션)을 표시합니다.  
  
 **프로젝트 버전**  
 프로젝트 버전을 나열합니다.  
  
 **배포 날짜**  
 프로젝트를 마지막으로 배포하거나 다시 배포한 날짜 및 시간을 나열합니다.  
  
##  <a name="set-the-options-on-the-permissions-page"></a><a name="permissions"></a> 권한 페이지의 옵션 설정  
 **권한** 페이지를 사용하여 프로젝트에 대한 명시적 권한을 보고 설정합니다.  
  
 찾아보기  
 **찾아보기** 를 클릭하여 **모든 보안 주체 찾아보기** 대화 상자를 사용하여 권한을 설정하려는 사용자 및 역할을 선택합니다.  
  
 **이름**  
 사용자 또는 역할의 이름을 나열합니다.  
  
 **형식**  
 사용자 또는 역할의 유형을 나열합니다.  
  
 **사용 권한**  
 사용 권한을 나열합니다.  
  
 **Grantor**  
 사용 권한을 부여하는 사용자 또는 역할을 나열합니다.  
  
 **허용**  
 **권한 부여** 를 선택하면 선택한 사용자 또는 역할에 사용 권한이 부여됩니다.  
  
 **거부**  
 **거부** 를 선택하면 선택한 사용자 또는 역할에 대해 사용 권한이 거부됩니다.  
  
  
