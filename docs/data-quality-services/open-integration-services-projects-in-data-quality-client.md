---
title: "데이터 품질 클라이언트에서 Integration Services 프로젝트 열기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 데이터 품질 클라이언트에서 Integration Services 프로젝트 열기
  Integration Services의 DQs 정리 구성 요소를 사용 하면 일괄 처리 모드에서 정리 프로젝트를 실행할 수 있도록 합니다. 그러나 경우에 따라 DQS의 데이터 품질 프로젝트에서 정리 작업의 **결과 관리 및 보기** 탭에 있는 정리 결과를 검토하는 방법과 유사한 방식으로 Integration Services 패키지의 정리 결과를 검토할 수도 있습니다. DQS는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 의 Integration Services 프로젝트를 다른 데이터 품질 프로젝트와 마찬가지로 **프로젝트 열기** 화면에서 열 수 있도록 지원하고 Integration Services 프로젝트의 정리 결과에 대한 대화식 정리 환경을 제공합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
  
-   **의** 프로젝트 열기 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]화면에서는 완료된 Integration Services 프로젝트만 사용할 수 있습니다. 실패한 프로젝트나 실행 중인 프로젝트는 **프로젝트 열기** 화면에서 사용할 수 없습니다.  
  
-   대화형 정리 단계에서 integration Services 프로젝트를 엽니다 (**결과 관리 및 보기** 탭)에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]합니다. **정리** 또는 **맵** 탭으로는 이동할 수 없습니다. **다음** 을 클릭하여 **내보내기**탭으로만 이동할 수 있습니다.  
  
-   잠긴 Integration Services 프로젝트는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 삭제할 수 없습니다. 삭제하려면 먼저 잠금을 해제해야 합니다.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 DQS 정리 구성 요소 패키지가 포함된 Integration Services 프로젝트를 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 보고 열려면 올바르게 실행이 완료된 상태여야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 Integration Services 프로젝트를 열려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_kb_operator 역할이 있어야 합니다.  
  
  
##  <a name="Open"></a> Integration Services 프로젝트 열기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [데이터 품질 클라이언트 응용 프로그램 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭합니다. **프로젝트 열기** 화면이 나타납니다.  
  
3.  **프로젝트 열기** 화면에서 다음 방법 중 하나로 Integration Services 프로젝트를 식별할 수 있습니다.  
  
    1.  **프로젝트 이름**: Integration Services 프로젝트는 다음과 같은 명명 용어를 사용 하 여 나열 됩니다: "Package.DQS Cleansing_*\< 날짜>**\< 시간>*_ {GUID}." [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 동일한 패키지를 올바르게 실행할 때마다 **프로젝트 열기** 화면에 새 프로젝트가 나열됩니다.  
  
    2.  **프로젝트 유형**: Integration Services 프로젝트는 **프로젝트 열기** 화면에서 **SSIS** 라는 프로젝트 형식을 가집니다.  
  
     프로젝트를 선택하고 **다음**을 클릭합니다.  
  
4.  대화형 정리 단계에서 Integration Services 프로젝트를 엽니다 (**결과 관리 및 보기** 탭). Integration Services 프로젝트의 데이터에 대해 대화식 정리를 수행할 수 있습니다. 에 대 한 자세한 내용은 **결과 관리 및 보기** 탭, 참조 [대화형 정리 단계](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) 에서 [데이터를 사용 하 여 DQS 정리 &#40; 내부 &#41; 기술](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)합니다.  
  
5.  **다음** 을 클릭하여 **내보내기** 탭으로 이동합니다. 여기서 SQL Server 데이터베이스, .csv 파일 또는 Excel 파일의 새 테이블 중 하나에 처리된 데이터를 내보낼 수 있습니다. 에 대 한 자세한 내용은 **내보내기** 탭, 참조 [내보내기 단계](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) 에서 [데이터를 사용 하 여 DQS 정리 &#40; 내부 &#41; 기술](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  데이터를 내보낸 후 **마침** 을 클릭하여 Integration Services 프로젝트를 닫습니다.  

  
## 관련 항목:  
 [DQS 정리 변환](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services (SSIS) 프로젝트](https://msdn.microsoft.com/library/ms138028.aspx)  
  
  