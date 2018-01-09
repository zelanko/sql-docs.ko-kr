---
title: "분석 데이터 원본에 대해 명령을 실행 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0a280ee70cd6c2545abc6a50da15d1eb938090e5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="executing-commands-against-an-analytical-data-source"></a>분석 데이터 원본에 대한 명령 실행
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]분석 데이터 원본에 대 한 연결을 만든 다음 사용할 수 있습니다는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체에 대해 명령을 실행 하 고 해당 데이터 원본에서 결과 반환 합니다. 이러한 명령은 MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 또는 제한된 SQL 구문을 사용하여 데이터를 검색할 수 있습니다. 또한 ASSL(Analysis Services Scripting Language) 명령을 사용하여 기본 데이터베이스를 수정할 수도 있습니다.  
  
## <a name="creating-a-command"></a>명령 만들기  
 명령을 실행하려면 먼저 명령을 만들어야 합니다. 다음 두 가지 방법 중 하나를 사용하여 명령을 만들 수 있습니다.  
  
-   데이터 원본에서 실행할 명령과 해당 명령을 실행할 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체를 매개 변수로 받을 수 있는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 생성자를 사용합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 메서드를 사용합니다.  
  
 실행할 명령 텍스트는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A> 속성을 사용하여 쿼리하고 수정할 수 있습니다. 개발자가 만드는 명령은 실행 후 데이터를 반환하지 않아도 됩니다.  
  
## <a name="running-a-command"></a>명령 실행  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 개체를 만든 후 해당 명령에서는 여러 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 메서드를 사용하여 다양한 동작을 수행할 수 있습니다. 다음 표에서는 이 중 몇 가지 동작을 보여 줍니다.  
  
|수행할 작업|사용할 메서드|  
|--------|---------------------|  
|결과를 데이터 스트림으로 반환|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 개체를 반환하는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 개체 반환|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|행을 반환하지 않는 명령 실행|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|반환 된 **XMLReader** xml for Analysis (XMLA) 호환 형식의 데이터가 포함 된 개체|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>명령 실행 예  
 사용 하 여이 예제는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 를 처리할 XMLA 명령을 실행 하는 **Adventure Works DW** 큐브 데이터를 반환 하지 않고 로컬 서버에 있습니다.  
  
 [!code-cs[Adomd.NetClient#ExecuteXMLAProcessCommand](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/executing-commands-again_1.cs)]  
  
  
