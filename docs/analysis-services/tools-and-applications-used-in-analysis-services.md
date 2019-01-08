---
title: Analysis Services에 사용 되는 응용 프로그램과 도구 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210079"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services에서 사용되는 도구 및 애플리케이션
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  도구 및 Analysis Services 모델을 빌드하기 위한 해야 하는 응용 프로그램 찾기 및 배포 된 데이터베이스를 관리 합니다.  
  
## <a name="analysis-services-model-designers"></a>Analysis Services 모델 디자이너  
 모델에서 데이터 도구 SSDT (SQL Server), Visual Studio shell 프로젝트 템플릿을 사용 하 여 작성 됩니다. 프로젝트 템플릿은 Analysis Services 솔루션을 구성 하는 데이터 모델 개체를 만들기 위한 모델 디자이너를 제공 합니다. SSDT는 매월 업데이트 무료 웹 다운로드입니다.

 **[SQL Server Data Tools (SSDT) 다운로드](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 모델은 기능 가용성을 결정하고 Analysis Services의 릴리스가 모델을 실행하는 호환성 수준 설정을 가지고 있습니다.  모델 디자이너에서 파트를 결정 하는지 여부 지정된 된 호환성 수준을 인지 지정할 수 있습니다.  
  
 테이블 형식 모델 BIM 파일이 JSON 형식으로 테이블 형식 및 양방향 교차 필터링을 같은 최신 기능을 사용 하 여 만들거나 호환성 수준 1200 이상에서 업그레이드 해야 합니다.  
  
 낮은 호환성 수준에 필요한 경우 아마도 Analysis Services의 이전 버전에서 모델을 배포 하려고 하기 때문에 사용할 수 있습니다 여전히 모델 디자이너 SSDT에서. 도구의 최신 버전 (테이블 형식 또는 다차원)에 모든 모델 유형과 모든 호환성 수준에서 만들기를 지원 합니다.   

## <a name="administrative-tools"></a>관리 도구  
  
 SQL Server Management Studio (SSMS)는 Analysis Services를 비롯 한 모든 SQL Server 기능에 대해 기본 관리 도구입니다. SSMS는 매월 업데이트 무료 웹 다운로드입니다. 
  
**[SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS 모니터링 작업 및 SQL Server 2016 및 Azure Analysis Services 서버에서 문제를 진단할에 사용 되는 SQL Server Profiler 추적의 경량 대체 제공 확장된 이벤트 (xEvents)를 포함 합니다. 자세한 내용은 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 을(를) 참조하세요.  
  
### <a name="sql-server-profiler"></a>SQL Server 프로파일러  
 공식적으로는 xEvents에 유리하게 사용되지 않지만 SQL Server Profiler는 연결, MDX 쿼리 실행 및 기타 서버 작동을 모니터링하는 친숙한 방법을 제공합니다. SQL Server Profiler는 기본적으로 설치됩니다. Windows에서 앱에 SQL Server 응용 프로그램을 찾을 수 있습니다.  
  
### <a name="powershell"></a>PowerShell  
 PowerShell 명령을 사용하여 많은 관리 작업을 수행할 수 있습니다. 참조 [PowerShell 참조](../analysis-services/powershell/analysis-services-powershell-reference.md) 자세한 내용은 합니다.  
  
### <a name="community-and-third-party-tools"></a>커뮤니티 및 타사 도구  
 커뮤니티 코드 샘플은 [Analysis Services codeplex 페이지](http://sqlsrvanalysissrvcs.codeplex.com/) (영문)를 참조하세요. Analysis Services를 지원하는 타사 도구에 대한 추천을 검색하는 경우에는[포럼](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) 이 도움이 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 데이터베이스의 호환성 수준](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [테이블 형식 모델에 대 한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
