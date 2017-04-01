---
title: "데이터 품질 프로젝트 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dqproject.newdqproject.f1"
helpviewer_keywords: 
  - "만들기, 데이터 품질 프로젝트"
  - "데이터 품질 프로젝트, 만들기"
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 데이터 품질 프로젝트 만들기
  이 항목에서는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]를 사용하여 데이터 품질 프로젝트를 만드는 방법에 대해 설명합니다. 데이터 품질 프로젝트는 DQS([!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)])에서 정리 또는 일치 작업을 실행하는 데 사용됩니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 데이터 품질 프로젝트에서 정리 및 일치 작업을 수행하는 데 사용할 관련 기술 자료가 있어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터 품질 프로젝트를 만들려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_kb_operator 역할이 있어야 합니다.  
  
##  <a name="Create"></a> 데이터 품질 프로젝트 만들기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [데이터 품질 클라이언트 응용 프로그램 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **새 데이터 품질 프로젝트**를 클릭합니다.  
  
3.  **새 데이터 품질 프로젝트** 화면에서  
  
    1.  **이름** 상자에 새 데이터 품질 프로젝트의 이름을 입력합니다.  
  
    2.  (선택 사항) 에 **설명** 상자에 새 데이터 품질 프로젝트에 대 한 설명을 입력 합니다.  
  
    3.  **기술 자료 사용** 목록에서 데이터 품질 프로젝트에 사용할 기술 자료를 선택합니다.  **기술 자료 정보: \< Knowledge_Base_Name >** 영역 오른쪽에 선택한 기술 자료에서 사용할 수 있는 도메인 이름을 표시 합니다.  
  
    4.  **작업 선택** 영역에서 이 데이터 품질 프로젝트를 사용하여 수행할 작업을 클릭합니다.  
  
        -   **정리**: 원본 데이터를 정리하려면 이 작업을 선택합니다.  
  
        -   **일치**: 일치를 수행하려면 이 작업을 선택합니다. 데이터 품질 프로젝트를 위해 선택한 기술 자료에 일치 정책이 포함된 경우에만 이 작업을 사용할 수 있습니다.  
  
4.  **만들기** 를 클릭하여 데이터 품질 프로젝트를 만듭니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 데이터 품질 프로젝트를 만든 후  
 데이터 품질 프로젝트를 만든 후에는 선택한 작업(정리 또는 일치)을 수행하는 데 사용할 마법사가 나타납니다. 정리 및 일치 작업에 대 한 자세한 내용은 참조 [데이터 정리](../data-quality-services/data-cleansing.md) 및 [일치 하는 데이터](../data-quality-services/data-matching.md)합니다.  
  
  