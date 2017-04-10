---
title: "데이터 마이닝 저장 프로시저(Analysis Services - 데이터 마이닝) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "저장 프로시저 [Analysis Services], 데이터 마이닝"
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# 데이터 마이닝 저장 프로시저(Analysis Services - 데이터 마이닝)
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 관리되는 모든 언어로 작성된 저장 프로시저가 지원됩니다. 지원되는 관리 언어에는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# 및 Managed C++가 포함됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 저장 프로시저를 **CALL** 문을 사용하여 직접 호출하거나 DMX(Data Mining Extensions) 쿼리의 일부로 호출할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 저장 프로시저 호출에 대한 자세한 내용은 [저장 프로시저 호출](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)을 참조하세요.  
  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]의 프로그래밍 기능에 대한 일반적인 내용은 [데이터 마이닝 프로그래밍](../../analysis-services/data-mining-programming.md)을 참조하세요.  
  
 데이터 마이닝 개체 프로그래밍 방법은 MSDN 라이브러리에서 "[SQL Server 데이터 마이닝 프로그래밍 기능(SQL Server Data Mining Programmability)](http://go.microsoft.com/fwlink/?LinkId=93735)" 문서를 참조하십시오.  
  
> [!NOTE]  
>  마이닝 모델을 쿼리할 경우 특히 새 데이터 마이닝 솔루션을 테스트할 경우에는 데이터 마이닝 엔진에 내부적으로 사용되는 시스템 저장 프로시저를 호출하는 것이 편리할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 추적을 만든 다음 데이터 마이닝 모델을 작성하고 찾아보고 쿼리하여 이러한 시스템 저장 프로시저의 이름을 볼 수 있습니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 버전 간에 시스템 저장 프로시저의 호환성을 보장하지 않으므로 프로덕션 시스템에서는 시스템 저장 프로시저를 호출하지 않도록 해야 합니다. 대신 호환성을 위해 DMX 또는 XML/A를 사용하여 쿼리를 직접 작성하는 것이 좋습니다.  
  
## 섹션 내용  
  
-   [SystemGetCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## 참조  
 [Analysis Services의 스크립트 관리 태스크](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
## 관련 항목:  
 [교차 유효성 검사&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [교차 유효성 검사 탭&#40;마이닝 정확도 차트 뷰&#41;](../Topic/Cross-Validation%20Tab%20\(Mining%20Accuracy%20Chart%20View\).md)   
 [저장 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  