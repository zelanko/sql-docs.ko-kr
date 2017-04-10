---
title: "복합 도메인의 값 관계 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dm.cdvaluerelations.f1"
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
caps.latest.revision: 12
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 12
---
# 복합 도메인의 값 관계 사용
  이 항목에서는 DQS([!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)])에서 기술 자료 검색 프로세스 중에 복합 도메인에 대해 발견된 값 조합을 보는 방법에 대해 설명합니다. 이 페이지에서는 값 조합의 발생 횟수를 보여줍니다. 복합 도메인에는 값 관리가 지원되지 않으므로 이러한 값에 대해 어떠한 작업도 수행할 수 없습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 값 관계를 보려면 복합 도메인을 만들고 열어 두어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 복합 도메인의 값 관계를 보려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Use"></a> 값 관계 보기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [데이터 품질 클라이언트 응용 프로그램 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 기술 자료를 열거나 만듭니다. **도메인 관리** 를 작업으로 선택한 다음 **열기** 또는 **만들기**를 클릭합니다. 자세한 내용은 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) 또는 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)를 참조하세요.  
  
3.  **도메인 관리** 페이지의 **도메인 목록** 에서 도메인 규칙을 만들 복합 도메인을 선택하거나 새 복합 도메인을 만듭니다. 새 도메인을 만들어야 하는 경우 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)를 참조하세요.  
  
4.  **값 관계** 탭을 클릭합니다.  
  
5.  각 값 조합에 대해 표시되는 빈도를 봅니다.  
  
    > [!NOTE]  
    >  **값** 테이블에서는 복합 도메인에 있는 각각의 값 조합을 보여 줍니다. 각 값은 값이 적용되는 단일 도메인에 표시됩니다. 값 관계 테이블은 기본적으로 빈도순으로 정렬되지만 다른 열을 클릭하여 해당 열을 기준으로 정렬할 수 있습니다. 빈도가 20보다 크거나 같은 해당 값만 표시됩니다.  
  
6.  테이블의 값은 변경할 수 없습니다. 다른 작업을 수행한 경우 **마침** 을 클릭하여 도메인 관리 작업을 완료합니다. 그렇지 않은 경우 **취소**를 클릭합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 값 관계를 본 후  
 값 관계를 본 후 도메인에 대해 다른 도메인 관리 태스크를 수행하거나, 기술 자료 검색을 수행하여 도메인에 정보를 추가하거나, 도메인에 일치 정책을 추가할 수 있습니다. 자세한 내용은 참조 [기술 자료 검색 수행](../data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../data-quality-services/managing-a-domain.md), 또는 [일치 정책 만들기](../data-quality-services/create-a-matching-policy.md)합니다.  
  
  