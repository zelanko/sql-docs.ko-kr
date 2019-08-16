---
title: Analysis Services에서 관리 태스크 스크립팅 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic Analysis Services administration
- administering Analysis Services
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69ccdaf9bf0f8b67309a1f88c0c44a90f3167b6b
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530923"
---
# <a name="script-administrative-tasks-in-analysis-services"></a>Analysis Services의 스크립트 관리 태스크
  SQL Server 에이전트를 통해 예약하거나 수동으로 실행할 수 있는 스크립트를 작성하거나 생성하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관리 태스크를 자동화할 수 있습니다. 다음 표에서는 사용할 수 있는 스크립팅 옵션을 요약하여 보여 주고 추가 정보에 대한 링크를 제공합니다.  
  
 아래에 나열된 모든 방법은 파일로 저장하거나 독립적인 작업으로 실행할 수 있는 스크립트를 지원합니다. 테이블 형식 모델과 PowerPivot 통합 문서에 사용되는 DAX(Data Analysis Expression) 언어는 조건을 충족하지 않으므로 다음 목록에 포함되어 있지 않습니다.  
  
|방법|파일 형식|Description|링크|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|Analysis Services는 백업, 복원, 처리, 역할 관리 등의 관리 작업에 명령줄뿐 아니라 새로운 cmdlet을 사용한 개체 탐색을 추가하는 새 공급자를 통해 SQL Server PowerShell 스크립팅 환경을 지원합니다.<br /><br /> 또한 SQL Server PowerPivot(SQLPS) 공급자에는 범용 cmdlet인 `Invoke-ASCmd`가 포함되어 있습니다. 이 cmdlet을 사용하면 PowerShell 내에서 XMLA, MDX 또는 DMX 스크립트 파일을 실행할 수 있습니다.<br /><br /> Analysis Services PowerShell 스크립팅은 다차원 모델과 테이블 형식 모델 모두에 사용할 수 있지만 SharePoint에서 액세스하는 PowerPivot 통합 문서에는 사용할 수 없습니다.|[Analysis Services PowerShell](analysis-services-powershell.md)<br /><br /> [Windows PowerShell 유지 가이드](https://go.microsoft.com/fwlink/?LinkId=233747)|  
|ASSL 또는 XMLA 스크립트|.xmla|ASSL(Analysis Services Scripting Language)은 테이블 형식 모드 또는 다차원 모드에서 실행되는 Analysis Services 인스턴스의 개체 및 작업에 대한 데이터 액세스를 제공하는 XMLA에 대한 확장 프로그램입니다. ASSL에는 XML 형식의 전체 Analysis Services 개체 및 작업 식을 사용할 수 있도록 하는 데이터 정의 및 명령 언어 정의가 포함되어 있습니다. ASSL에서 제공하는 개체 및 명령을 사용하는 스크립트는 .xmla 파일로 저장됩니다. Analysis Services 컨텍스트 내에서는 ASSL을 XMLA 스크립트로 참조하는 것이 일반적입니다. 요구 사항에 다음 사항이 포함되어 있는 경우 이 방법을 선택합니다.<br /><br /> 스크립트가 서버에서 직접 개체를 만들거나 데이터 정의 및 작동 태스크 둘 다를 수행합니다(예: 데이터베이스 다시 만들기 및 처리).<br /><br /> 여러 도구와 기술에 최대한 많이 스크립트를 재사용해야 합니다. XMLA 스크립트를 SQL Server 에이전트의 Analysis Services 명령 태스크에 추가하거나 SSIS 패키지에서 참조하거나 PowerShell 스크립트에서 참조할 수 있습니다.<br /><br /> 스크립트를 무인 모드로 실행해야 합니다. SQL Server 에이전트를 사용하여 XMLA 스크립트가 포함된 작업이나 XMLA가 포함된 SSIS 패키지를 예약할 수 있습니다.<br /><br /> XMLA를 사용하기 위한 애플리케이션 요구 사항이 있습니다. XMLA는 관리 코드 환경이 필요하지 않은 인터페이스입니다. .NET Framework를 사용하지 않는 애플리케이션에서 XMLA 스크립트를 실행할 수 있습니다.|[Management Studio에서 Analysis Services 스크립트 만들기](instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [SQL Server Management Studio에서 Analysis Services 템플릿 사용](instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [SQL Server 에이전트를 사용하여 SSAS 관리 태스크 예약](instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [ASSL&#40;Analysis Services Scripting Language&#41;을 사용하여 개발](multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd cmdlet](/powershell/module/sqlserver/invoke-ascmd)|  
|||Management Studio에서 스크립트 생성기를 사용하여 XMLA 스크립트를 만들 수 있습니다. 개체 수준에서 개체를 마우스 오른쪽 단추로 클릭하여 개체를 만들거나 변경하거나 삭제하는 스크립트를 생성합니다. 명령 수준에서 처리, 백업이나 복원, 집계 디자인 또는 다른 명령에 사용하는 등의 용도로 새 창, 파일 또는 클립보드에 스크립트를 배치하는 옵션을 선택하고 대화 상자의 스크립트 기능을 사용하여 스크립트를 생성할 수 있습니다. 텍스트 편집기 또는 코드 편집기에서 수동으로 XMLA 스크립트를 작성하거나 템플릿 탐색기에서 템플릿을 사용할 수도 있습니다. 스크립트를 실행하려면 이러한 방법 중 하나를 사용합니다.<br /><br /> Management Studio를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 직접 개체를 만들거나 수정합니다.<br /><br /> SQL Server 에이전트를 사용하여 Analysis Services 명령 태스크가 포함된 작업을 예약합니다.<br /><br /> Invoke-ASCmd cmdlet을 사용하여 PowerShell 세션에서 스크립트를 실행합니다.||  
|MDX Script|.mdx|MDX(Multidimensional Expression) 언어는 분석 데이터 원본의 업계 표준 쿼리 언어로, XMLA 사양의 일부이기도 합니다.<br /><br /> 데이터 또는 시스템 정보를 쿼리하는 독립 실행형 MDX 스크립트 파일을 만들 수 있습니다. 예를 들어 로컬 서버 작업 및 서버 상태에 대한 정보를 표시하는 DMV(동적 관리 뷰)에는 MDX Select 문을 통해 액세스할 수 있습니다.<br /><br /> MDX 스크립트는 다차원 및 테이블 형식 모드 서버 모두에서 실행됩니다. `Invoke-ASCmd`를 사용하여 SQL Server Management Studio 또는 PowerShell 세션에서 스크립트를 대화형으로 실행할 수 있습니다.|[MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [DMV&#40;동적 관리 뷰&#41;를 사용하여 Analysis Services 모니터링](instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [SQL Server Management Studio에서 Analysis Services 템플릿 사용](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX Script|.dmx|DMX(Data Mining Extensions)는 데이터 마이닝 모델에 대한 데이터 정의, 데이터 조작 및 데이터 쿼리 언어입니다. 템플릿을 사용하여 시작할 수 있습니다.|[SQL Server Management Studio에서 DMX 쿼리 만들기](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [SQL Server Management Studio에서 Analysis Services 템플릿 사용](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지|.dtsx|[!INCLUDE[ssIS](../includes/ssis-md.md)] 에서는 데이터 마이닝 모델을 포함하여 Analysis Services 개체를 만들고 수정, 삭제 및 처리하는 태스크 및 데이터 흐름을 제공합니다. SQL Server 에이전트를 사용하여 실행할 패키지를 예약할 수 있습니다.|[Analysis Services DDL 실행 태스크](../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Analysis Services 처리 태스크](../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [데이터 마이닝 쿼리 태스크](../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [데이터 마이닝 모델 학습 대상](../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [차원 처리 대상](../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [파티션 처리 대상](../integration-services/data-flow/partition-processing-destination.md)|  
|AMO||AMO(Analysis Management Objects)는 프로그래머가 관리 작업을 자동화하는 사용자 지정 애플리케이션을 개발하는 데 사용할 수 있는 관리 인터페이스입니다. AMO를 사용하면 제공하는 XMLA, MDX 또는 DMX 스크립트를 실행하는 사용자 지정 애플리케이션을 개발할 수 있습니다.|[AMO로 관리 태스크 프로그래밍](https://docs.microsoft.com/bi-reference/amo/programming-administrative-tasks-with-amo)|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 &#40;인 l&#41; 참조](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)   
 [다차원 모델 개체 처리](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
