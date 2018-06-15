---
title: ADOMD.NET 클라이언트 기능 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1347bad80b8fb076d3c4f2b765f06513ff76d8d8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024790"
---
# <a name="adomdnet-client-functionality"></a>ADOMD.NET 클라이언트 기능
  ADOMD.NET은 다른 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 데이터 공급자와 마찬가지로 응용 프로그램과 데이터 원본을 연결하는 데 사용됩니다. 하지만 ADOMD.NET은 다른 .NET Framework 데이터 공급자와는 달리 분석 데이터에 사용됩니다. 분석 데이터에 대한 작업을 수행하기 위해 ADOMD.NET에서는 다른 .NET Framework 데이터 공급자와는 매우 다른 기능을 지원합니다. ADOMD.NET을 사용하면 데이터를 검색할 수 있을 뿐 아니라 메타데이터를 검색하고 분석 데이터 저장소의 구조를 변경할 수도 있습니다.  
  
 **메타 데이터 검색**  
 응용 프로그램에서는 스키마 행 집합이나 개체 모델을 사용한 메타데이터 검색을 통해 데이터 원본에서 검색할 수 있는 데이터에 대한 추가 정보를 확인할 수 있습니다. 사용 가능한 각 KPI(핵심 성과 지표)의 유형, 큐브의 차원, 마이닝 모델에 필요한 매개 변수 등의 정보를 모두 검색할 수 있습니다. 메타 데이터는 가장 중요 한 *동적* 형식, 깊이, 및 데이터의 범위를 검색할 수를 결정 하는 사용자 입력을 요구 하는 응용 프로그램입니다. 이러한 응용 프로그램의 예로는 쿼리 분석기, Microsoft Excel 및 기타 쿼리 도구가 있습니다. 메타 데이터는 비교적 중요 하지 *정적* 미리 정의 된 일련의 작업을 수행 하는 응용 프로그램입니다.  
  
 자세한 내용은: [분석 데이터 원본에서 메타 데이터 가져오기](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)합니다.  
  
 **데이터 검색**  
 데이터 검색은 데이터 원본에 저장된 정보를 실제로 검색하는 것으로, 데이터 원본의 구조를 알고 있는 "정적" 응용 프로그램의 기본 기능입니다. 데이터 검색은 "동적" 응용 프로그램의 최종 결과이기도 합니다. 하루 중 특정 시간의 KPI 값, 각 매장에서 마지막 1시간 동안 판매된 자전거 수 및 직원의 연간 성과를 좌우하는 요인 등이 모두 검색할 수 있는 데이터의 예입니다. 데이터 검색 기능은 모든 쿼리 응용 프로그램에 매우 중요합니다.  
  
 자세한 내용은: [분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)합니다.  
  
 **분석 데이터의 구조 변경**  
 ADOMD.NET을 사용하여 분석 데이터 저장소의 구조를 실제로 변경할 수도 있습니다. 이 작업은 일반적으로 AMO(Analysis Management Objects) 개체 모델을 통해 수행되지만 ADOMD.NET을 사용하여 ASSL(Analysis Services Scripting Language) 명령을 보내 서버의 개체를 만들거나 변경하거나 삭제할 수도 있습니다.  
  
 자세한 내용은: [실행 명령에 대해는 분석 데이터 원본](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md), [Analysis Management Objects를 사용 하 여 개발 &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md), [Analysis Services Scripting 언어 &#40;ASSL XMLA에 대 한&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 메타데이터 검색, 데이터 검색 및 데이터 구조 변경은 각각 일반적인 ADOMD.NET 응용 프로그램의 워크플로에서 특정 시점에 수행됩니다.  
  
## <a name="typical-process-flow"></a>일반적인 프로세스 흐름  
 기존 ADOMD.NET 응용 프로그램에서는 일반적으로 분석 데이터베이스 작업에 사용되는 워크플로와 동일한 워크플로를 따릅니다.  
  
1.  먼저 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 사용하여 데이터베이스에 대한 연결이 만들어집니다. 이 연결을 열면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에서는 연결한 대상 서버에 대한 메타데이터를 제공합니다. 동적 응용 프로그램에서는 일반적으로 이 정보의 일부가 사용자에게 표시되므로 사용자가 쿼리할 큐브와 같은 사항을 선택할 수 있습니다. 응용 프로그램에서는 이 단계에서 만들어진 연결을 여러 번 재사용하여 오버헤드를 줄일 수 있습니다.  
  
     자세한 내용은: [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  연결이 만들어진 후 동적 응용 프로그램은 서버에서 보다 구체적인 메타데이터를 쿼리합니다. 정적 응용 프로그램의 경우에는 응용 프로그램에서 쿼리할 개체를 프로그래머가 미리 알고 있으므로 이 메타데이터를 검색할 필요가 없습니다. 검색된 메타데이터는 응용 프로그램이나 사용자가 다음 단계에 사용할 수 있습니다.  
  
     자세한 내용은: [분석 데이터 원본에서 메타 데이터 가져오기](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  그런 다음 응용 프로그램에서 서버에 대해 명령을 실행합니다. 이 명령은 추가 메타데이터를 검색하거나, 데이터를 검색하거나, 데이터베이스를 수정하기 위한 명령일 수 있습니다. 응용 프로그램에서는 이러한 모든 태스크에 대해 미리 결정한 쿼리를 사용하거나 새로 검색된 메타데이터를 사용하여 추가 쿼리를 만들 수 있습니다.  
  
     자세한 내용은: [분석 데이터 원본에서 메타 데이터 가져오기](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md), [분석 데이터 원본에서 데이터 검색](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md), [실행 명령에 대해는 분석 데이터 원본](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  서버로 명령을 보낸 후 서버에서는 클라이언트에 메타데이터나 데이터를 반환하기 시작합니다. 사용 하 여이 정보를 볼 수는 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 개체 또는 **System.XmlReader** 개체입니다.  
  
 이 일반적인 워크플로를 보여 주기 위해 다음 예에는 데이터베이스에 대한 연결을 열고 알려진 큐브에 대해 명령을 실행하고 결과를 셀 집합으로 가져오는 메서드가 포함되어 있습니다. 그러면 셀 집합은 열 머리글, 행 머리글 및 셀 데이터가 들어 있는 탭으로 구분된 문자열을 반환합니다.  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 클라이언트 프로그래밍](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
