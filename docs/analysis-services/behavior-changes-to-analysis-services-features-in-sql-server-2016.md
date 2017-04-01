---
title: "SQL Server 2016 Analysis Services 기능의 동작 변경 내용 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# SQL Server 2016 Analysis Services 기능의 동작 변경 내용
  *동작 변경 내용* 은 이전 버전의 SQL Server와 비교해서 현재 버전에서 기능이 작동하고 상호 작용하는 방법에 영향을 줍니다.  
  
 기본값에 대한 수정, 업그레이드 또는 복원 기능을 완료하는 데 필요한 수동 구성 또는 기존 기능의 새로운 구현 작업 시제품에서 동작을 변경할 수 있습니다.  
  
 이 릴리스에서 변경되고 업그레이드 후 기존 모델 또는 코드를 중단하지 않는 기능 동작이 여기에 나열됩니다.  
  
> [!NOTE]  
>  *동작 변경 내용*과 달리 *주요 변경 내용* 은 서버, 클라이언트 도구 또는 모델을 업그레이드한 후 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에 통합된 데이터 모델 또는 응용 프로그램이 실행되지 않도록 하는 변경 내용입니다. 목록을 보려면 [SQL Server 2016의 Analysis Services 기능과 관련된 새로운 변경](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)을 참조하세요.  
  
## SharePoint 모드의 Analysis Services  
 사후 설치 태스크로 더 이상 파워 피벗 구성 마법사를 실행할 필요가 없습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 현재 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 릴리스에서 모델을 로드하는 모든 지원되는 SharePoint 버전의 경우에도 적용됩니다.  
  
## 테이블 형식 모델의 DirectQuery 모드  
 *DirectQuery* 는 테이블 형식 모델의 데이터 액세스 모드입니다. 여기서 쿼리 실행은 백 엔드 관계형 데이터베이스에서 수행되며 결과 집합을 실시간으로 검색합니다. 메모리에 맞출 수 없는 매우 큰 데이터 집합이나 데이터가 불안정한 경우, 테이블 형식 모델에 대한 쿼리에서 반환된 최근 데이터를 원하는 경우 주로 사용됩니다.  
  
 DirectQuery는 지난 몇 번의 릴리스에서 데이터 액세스 모드로 존재해왔습니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서는 구현이 약간 수정되었으며 테이블 형식 모델이 호환성 수준 1200에 있다고 가정합니다. DirectQuery는 이전보다 제한이 적습니다. 또한 데이터베이스 속성도 다릅니다.  
  
 기존 테이블 형식 모델에서 DirectQuery를 사용하는 경우 현재 호환성 수준 1100 또는 1103에서 모델을 유지하고 해당 수준에 대해 구현된 것으로 DirectQuery를 계속 사용할 수 있습니다. 또는 이 릴리스의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 DirectQuery의 향상된 기능을 활용하기 위해 1200으로 업그레이드할 수 있습니다.  
  
 이전 호환성 수준의 설정은 최신 1200 호환성 수준에서 정확한 해당 항목이 없으므로 DirectQuery 모델의 전체 업그레이드가 없습니다. DirectQuery 모드에서 실행되는 기존 테이블 형식 모델이 없는 경우 SQL Server Data Tools에서 모델을 열고 DirectQuery를 해제하며 **호환성 수준** 속성을 1200으로 설정한 후 DirectQuery 속성을 테이블 형식 1200 모델에 정의된 대로 다시 구성해야 합니다. 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)를 참조하세요.  
  
## 관련 항목:  
 [이전 버전과의 호환성_삭제됨](../Topic/Backward%20Compatibility_deleted.md)   
 [SQL Server 2016의 Analysis Services 기능과 관련된 새로운 변경](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [SQL Server Data Tools 다운로드](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  