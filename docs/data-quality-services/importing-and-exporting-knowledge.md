---
title: "기술 자료 가져오기 및 내보내기 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0963e7fc98cc0489d6f93c2381b701bd26ef569
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="importing-and-exporting-knowledge"></a>기술 자료 가져오기 및 내보내기
  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램에서 직접 기술 자료와 도메인을 만들거나 기술 자료의 정보를 가져오거나 내보낼 수 있습니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램에서 가져오기 및 내보내기 작업에 데이터 파일을 사용하거나 가져오기 작업에 Excel 파일을 사용할 수 있습니다. 사용되는 데이터 파일은 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )로 만들어 암호화된 파일로서 확장명이 .dqs입니다. Microsoft Excel에서 만든 파일은 .xlsx, .xls 또는.csv 확장명을 가질 수 있습니다. 이러한 작업을 통해 데이터 정리와 일치를 수행하는 데 사용하는 기술 자료를 보다 융통성 있게 작성하고 공유할 수 있습니다.  
  
> [!IMPORTANT]  
>  명령 프롬프트에서 DQSInstaller.exe 파일을 실행하여 *의* 모든 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 기술 자료를 한 번에 DQS 백업 파일(.dqsb)로 내보낼 수 있습니다. 마찬가지로 명령 프롬프트에서 DQSInstaller.exe 파일을 실행하여 DQS 백업 파일(.dqsb)의 *모든* 기술 자료를 한 번에 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 로 가져올 수 있습니다. 방법은 DQS 설치 설명서에서 [Dqsinstaller.exe를 사용하여 DQS 기술 자료 내보내기 및 가져오기](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) 를 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음과 같은 가져오기 및 내보내기 작업을 수행할 수 있습니다.  
  
|||  
|-|-|  
|기술 자료의 도메인을 .dqs 데이터 파일로 내보내기|[.dqs 파일로 도메인 내보내기](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|.dqs 데이터 파일에서 기존의 기술 자료로 도메인 가져오기|[.dqs 파일에서 도메인 가져오기](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|전체 기술 자료를 .dqs 데이터 파일로 내보내기|[.dqs 파일로 기술 자료 내보내기](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|전체 기술 자료를 .dqs 데이터 파일로 가져오기|[.dqs 파일에서 기술 자료 가져오기](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|Excel 파일에서 도메인으로 값 가져오기|[Excel 파일에서 도메인으로 값 가져오기](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|Excel 파일에서 기술 자료로 도메인 가져오기|[기술 자료 검색 시 Excel 파일에서 도메인 가져오기](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|정리 도중 수집한 정보를 기술 자료로 가져오기|[도메인으로 정리 프로젝트 값 가져오기](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>관련 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|기술 자료 검색을 실행하고 대화식으로 정보를 관리하여 기술 자료 구축|[기술 자료 구축](../data-quality-services/building-a-knowledge-base.md)|  
|단일 도메인 만들기 및 단일 도메인에 정보 추가|[도메인 관리](../data-quality-services/managing-a-domain.md)|  
|복합 도메인 만들기 및 단일 도메인에 정보 추가|[복합 도메인 관리](../data-quality-services/managing-a-composite-domain.md)|  
  
  

