---
title: "도구 및 Analysis Services에서 사용 되는 응용 프로그램 | Microsoft Docs"
ms.custom: 
ms.date: 05/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6dbb05ab73e9994d4f3c14a9bdfd919ec48c6f29
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services에서 사용되는 도구 및 응용 프로그램
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  도구 및 Analysis Services 모델 개발에 필요한 응용 프로그램을 찾아 배포 된 데이터베이스를 관리 합니다.  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 모델 디자이너  
 모델은 프로젝트 템플릿의 데이터 도구 SSDT (SQL Server), Visual Studio 셸을 사용 하 여 작성 됩니다. 프로젝트 템플릿은 Analysis Services 솔루션을 구성 하는 데이터 모델 개체를 만들기 위한 모델 디자이너를 제공 합니다. SSDT는 매달 업데이트 하는 무료 웹 다운로드입니다.

 **[SQL Server Data Tools (SSDT) 다운로드](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 모델은 기능 가용성을 결정하고 Analysis Services의 릴리스가 모델을 실행하는 호환성 수준 설정을 가지고 있습니다.  모델 디자이너에서 파트를 결정 하는지 여부 지정된 된 호환성 수준을 지정할 수 있습니다.  
  
 BIM 파일 테이블 형식 JSON 형식의 및 양방향 교차 필터링을 같은 최신 기능을 사용 하 여 테이블 형식 모델을 생성 또는 호환성 수준 1200 이상에서 업그레이드 해야 합니다.  
  
 호환성 수준이 이보다 낮지 필요한 경우 아마도 Analysis Services의 이전 버전에서 모델을 배포 하고자 하기 때문에 사용할 수 있습니다 여전히 모델 디자이너 SSDT에서. 이 도구의 최신 버전 모든 호환성 수준에서 모든 모델 유형과 (테이블 형식 또는 다차원) 만들기를 지원 합니다.   

## <a name="administrative-tools"></a>관리 도구  
  
 SQL Server Management Studio (SSMS)는 Analysis Services를 포함 하 여 모든 SQL Server 기능에 대 한 기본 관리 도구입니다. SSMS는 매달 업데이트 하는 무료 웹 다운로드입니다. 
  
**[SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS-SQL Server 2016 및 Azure Analysis Services 서버에서 문제를 진단할 모니터링 작업에 사용 되는 SQL Server Profiler 추적의 경량급 대안을 제공 하 확장된 이벤트 (xEvents)를 포함 되어 있습니다. 자세한 내용은 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 을(를) 참조하세요.  
  
### <a name="sql-server-profiler"></a>SQL Server 프로파일러  
 공식적으로는 xEvents에 유리하게 사용되지 않지만 SQL Server Profiler는 연결, MDX 쿼리 실행 및 기타 서버 작동을 모니터링하는 친숙한 방법을 제공합니다. SQL Server Profiler는 기본적으로 설치됩니다. Windows에서 앱에서 SQL Server 응용 프로그램과 함께 찾을 수 있습니다.  
  
### <a name="powershell"></a>PowerShell  
 PowerShell 명령을 사용하여 많은 관리 작업을 수행할 수 있습니다. 참조 [PowerShell 참조](../analysis-services/powershell/analysis-services-powershell-reference.md) 자세한 정보에 대 한 합니다.  
  
### <a name="community-and-third-party-tools"></a>커뮤니티 및 타사 도구  
 커뮤니티 코드 샘플은 [Analysis Services codeplex 페이지](http://sqlsrvanalysissrvcs.codeplex.com/) (영문)를 참조하세요. Analysis Services를 지원하는 타사 도구에 대한 추천을 검색하는 경우에는[포럼](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 이 도움이 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 데이터베이스의 호환성 수준](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [테이블 형식 모델에 대 한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
