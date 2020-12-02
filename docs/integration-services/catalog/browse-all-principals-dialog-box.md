---
description: 모든 보안 주체 찾아보기 대화 상자
title: 모든 보안 주체 찾아보기 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5ec280020b966a1d23b5ebb9dfb2c740692a6d1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123792"
---
# <a name="browse-all-principals-dialog-box"></a>모든 보안 주체 찾아보기 대화 상자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **모든 보안 주체 찾아보기** 대화 상자를 사용하여 데이터베이스 보안 주체를 선택한 후 선택한 프로젝트 또는 선택한 폴더에 포함된 모든 프로젝트에 대해 보안 주체가 가지는 권한을 변경할 수 있습니다.  
  
 **수행 작업**  
  
-   [모든 보안 주체 찾아보기 대화 상자 열기](#open_dialog)  
  
-   [옵션 구성](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> 모든 보안 주체 찾아보기 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 카탈로그를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  선택한 폴더에 포함된 모든 프로젝트에 대해 보안 주체가 가지는 권한을 변경하려면 폴더를 마우스 오른쪽 단추로 클릭한 다음, **속성** 을 클릭합니다.  
  
     선택한 프로젝트에 대해 보안 주체가 가지는 권한을 변경하려면 프로젝트가 포함된 폴더를 확장하고 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **속성** 을 클릭합니다.  
  
5.  **사용 권한** 페이지를 선택한 다음 **찾아보기** 를 클릭합니다.  
  
##  <a name="configure-the-options"></a><a name="options"></a> 옵션 구성  
 이 페이지에는 SSISDB 데이터베이스의 sys.database_principals 카탈로그 뷰에 있는 보안 주체가 표시됩니다.  
  
 보안 주체를 선택한 후 **확인** 을 클릭하고 **모든 보안 주체 찾아보기** 대화 상자를 닫으면 선택한 보안 주체가 상위 대화 상자의 **사용 권한** 페이지에 있는 **로그인 또는 역할** 목록에 추가됩니다. **로그인 또는 역할** 목록에 보안 주체를 추가한 후에는 선택한 프로젝트에 대한 해당 보안 주체의 사용 권한을 변경할 수 있습니다.  
  
 **선택 열**  
 상위 대화 상자의 **사용 권한** 페이지에 있는 **로그인 또는 역할** 목록에 보안 주체를 추가하려면 선택합니다.  
  
 **아이콘 열**  
 보안 주체의 **유형** 에 해당하는 아이콘입니다.  
  
 **이름**  
 보안 주체의 이름입니다.  
  
 **유형**  
 보안 주체의 유형입니다. 일반적인 유형은 다음과 같습니다.  
  
-   SQL 사용자  
  
-   Windows 사용자  
  
-   데이터베이스 역할  
  
  
