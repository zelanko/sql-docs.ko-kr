---
title: .dqs 파일에서 도메인 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5a6ef09783b69f6920d5421a52fbe8dbd13ed0e4
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410000"
---
# <a name="import-a-domain-from-a-dqs-file"></a>.dqs 파일에서 도메인 가져오기
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 .dqs 파일의 도메인을 기존 기술 자료로 가져오는 방법에 대해 설명합니다. .dqs 데이터 파일은 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 애플리케이션에서 도메인이나 기술 자료를 내보내면 생성됩니다. .dqs 데이터 파일은 암호화되어 있으므로 볼 수 없습니다.  
  
 .dqs 데이터 파일을 사용하여 한 기술 자료의 도메인을 내보낸 다음 다른 기술 자료로 가져오면 기술 자료 생성 프로세스가 간소화되어 시간과 노력을 절감할 수 있습니다. 도메인과 정보를 다른 사람과 공유하여 다른 사람의 시간을 절감할 수도 있습니다. 단일 도메인 하나 또는 복합 도메인 하나(여러 단일 도메인 포함)를 가져올 수 있습니다. 단일 도메인을 포함하는 .dqs 파일에는 매핑된 참조 데이터 정보를 제외하고 도메인 속성, 값 및 규칙 데이터를 비롯하여 모든 도메인 데이터가 포함됩니다. 복합 도메인을 포함하는 .dqs 파일에는 매핑된 참조 데이터를 제외하고 복합 도메인에 포함된 단일 도메인에 대한 모든 도메인 데이터와 복합 도메인 속성, 값 관계 및 CD 규칙을 비롯하여 모든 복합 도메인 데이터가 포함됩니다. 게시된 데이터와 게시되지 않은 데이터를 가져올 수 있습니다.  
  
 도메인을 가져올 때 도메인 이름은 원래 내보내진 도메인의 이름과 동일하게 유지됩니다. 단, 도메인 이름이 이미 있는 경우에는 DQS에서 이름에 "_1"을 추가합니다. 또한 기존 도메인과 동일한 이름을 가진 개별 도메인이 포함된 복합 도메인을 가져오는 경우에도 마찬가지입니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 .dqs 파일에서 도메인을 가져오려면 단일 도메인 하나 또는 복합 도메인 하나(여러 단일 도메인 포함)를 .dqs 파일로 이미 내보낸 상태여야 합니다. .dqs 파일에는 도메인이 하나만 포함되어야 합니다. 또한 도메인을 가져올 기술 자료를 만들고 열어 두어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 .dqs 데이터 파일에서 도메인을 가져오려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Import"></a> Import a domain from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면의 도메인 관리 작업에서 기술 자료를 엽니다.  
  
3.  **데이터 파일에서 도메인 가져오기** 아이콘을 클릭합니다.  
  
4.  **데이터 파일에서 가져오기** 대화 상자에서 가져올 파일이 있는 폴더로 이동하고 파일을 선택한 다음(DQS 파일 형식) **열기**를 클릭합니다.  
  
5.  **도메인 가져오기** 대화 상자에서 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  도메인을 가져올 .dqs 파일에 단일 도메인 또는 복합 도메인(여러 단일 도메인 포함)이 하나만 포함된 경우에만 가져오기 작업이 성공합니다.  
  
6.  가져온 도메인이 **도메인** 목록에 표시되는지 확인합니다. 복합 도메인을 가져온 경우 복합 도메인과 포함된 단일 도메인이 모두 **도메인** 목록에 있는지 확인합니다.  
  
##  <a name="FollowUp"></a> 후속편: .dqs 파일에서 도메인을 가져온 후  
 .dqs 파일에서 도메인을 가져온 후 도메인에 정보를 추가하거나 도메인의 내용에 따라 정리 또는 일치 프로젝트에서 도메인을 사용할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../../2014/data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../../2014/data-quality-services/managing-a-domain.md), [복합 도메인 관리](../../2014/data-quality-services/managing-a-composite-domain.md), [일치 정책 만들기](../../2014/data-quality-services/create-a-matching-policy.md), [데이터 정리](../../2014/data-quality-services/data-cleansing.md) 또는 [데이터 일치](../../2014/data-quality-services/data-matching.md)를 참조하세요.  
  
  
