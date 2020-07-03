---
title: Data Quality Client에서 Integration Services (SSIS) 프로젝트 열기
description: SQL Server Data Quality Services에 대 한 Data Quality Client를 사용 하 여 SQL Server Integration Services (SSIS) 프로젝트를 여는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 08373864f30b6fec68834377df531966d49edfcf
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896424"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>데이터 품질 클라이언트에서 Integration Services 프로젝트 열기

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Integration Services의 DQS 정리 구성 요소를 사용 하면 정리 프로젝트를 일괄 처리 모드로 실행할 수 있습니다. 그러나 경우에 따라 DQS의 데이터 품질 프로젝트에서 정리 작업의 **결과 관리 및 보기** 탭에 있는 정리 결과를 검토하는 방법과 유사한 방식으로 Integration Services 패키지의 정리 결과를 검토할 수도 있습니다. DQS는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 의 Integration Services 프로젝트를 다른 데이터 품질 프로젝트와 마찬가지로 **프로젝트 열기** 화면에서 열 수 있도록 지원하고 Integration Services 프로젝트의 정리 결과에 대한 대화식 정리 환경을 제공합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
  
-   **의** 프로젝트 열기 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]화면에서는 완료된 Integration Services 프로젝트만 사용할 수 있습니다. 실패한 프로젝트나 실행 중인 프로젝트는 **프로젝트 열기** 화면에서 사용할 수 없습니다.  
  
-   Integration Services 프로젝트는**의 대화식 정리 단계(** 결과 관리 및 보기 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]탭)에서 열립니다. **정리** 또는 **맵** 탭으로는 이동할 수 없습니다. **다음** 을 클릭하여 **내보내기**탭으로만 이동할 수 있습니다.  
  
-   잠긴 Integration Services 프로젝트는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 삭제할 수 없습니다. 삭제하려면 먼저 잠금을 해제해야 합니다.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 DQS 정리 구성 요소 패키지가 포함된 Integration Services 프로젝트를 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]에서 보고 열려면 올바르게 실행이 완료된 상태여야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 Integration Services 프로젝트를 열려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_kb_operator 역할이 있어야 합니다.  
  
  
##  <a name="open-an-integration-services-project"></a><a name="Open"></a> Integration Services 프로젝트 열기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]홈 화면에서 **데이터 품질 프로젝트 열기**를 클릭 합니다. **프로젝트 열기** 화면이 나타납니다.  
  
3.  **프로젝트 열기** 화면에서 다음 방법 중 하나로 Integration Services 프로젝트를 식별할 수 있습니다.  
  
    1.  **프로젝트 이름**: Integration Services 프로젝트는 다음과 같은 명명 용어를 사용 하 여 나열 됩니다. "package.productname Cleansing_ *\<DATE>\<TIME>* _ {GUID}" [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 동일한 패키지를 올바르게 실행할 때마다 **프로젝트 열기** 화면에 새 프로젝트가 나열됩니다.  
  
    2.  **프로젝트 유형**: Integration Services 프로젝트는 **프로젝트 열기** 화면에서 **SSIS** 라는 프로젝트 형식을 가집니다.  
  
     프로젝트를 선택하고 **다음**을 클릭합니다.  
  
4.  대화식 정리 단계(**결과 관리 및 보기** 탭)에서 Integration Services 프로젝트가 열립니다. Integration Services 프로젝트의 데이터에 대해 대화식 정리를 수행할 수 있습니다. **결과 관리 및 보기** 탭에 대한 자세한 내용은 [DQS&#40;내부&#41; 기술 자료를 사용하여 데이터 정리](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)에서 [대화형 정리 단계](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive)를 참조하세요.  
  
5.  **다음** 을 클릭하여 **내보내기** 탭으로 이동합니다. 여기서 SQL Server 데이터베이스, .csv 파일 또는 Excel 파일의 새 테이블 중 하나에 처리된 데이터를 내보낼 수 있습니다. **내보내기** 탭에 대한 자세한 내용은 [DQS&#40;내부&#41; 기술 자료를 사용하여 데이터 정리](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)에서 [내보내기 단계](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export)를 참조하세요.  
  
6.  데이터를 내보낸 후 **마침** 을 클릭하여 Integration Services 프로젝트를 닫습니다.  

  
## <a name="see-also"></a>참고 항목  
 [DQS 정리 변환](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services(SSIS) 프로젝트](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
