---
title: "사용자 정의 함수 및 저장 프로시저 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [ADOMD.NET]
- ADOMD.NET, user defined functions
- user defined functions [ADOMD.NET]
- ADOMD.NET, UDFs
- ADOMD.NET, stored procedures
ms.assetid: 07e8aa47-37d4-4bbc-8bff-49e422d12897
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 367f55ab474a2dc03cf1427ffed8c8f78268dc93
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="user-defined-functions-and-stored-procedures"></a>사용자 정의 함수 및 저장 프로시저
  ADOMD.NET 서버 개체를 만들 수 있습니다 (UDF) 사용자 정의 함수 또는 저장된 프로시저에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 메타 데이터 및 서버에서 데이터 상호 작용 하는 합니다. 이러한 in-process 메서드는 MDX(Multidimensional Expressions) 또는 DMX(Data Mining Extensions) 문을 통해 호출되어 네트워크 통신에 따른 지연 시간 없이 추가 기능을 제공합니다.  
  
## <a name="udf-examples"></a>UDF 예  
 UDF는 MDX 또는 DMX 문의 컨텍스트 내에서 호출할 수 있는 메서드로, 사용 가능한 매개 변수 수와 반환하는 데이터 형식에 제한이 없습니다.  
  
 MDX를 사용하여 만든 UDF는 DMX용으로 만든 UDF와 비슷합니다. 주된 차이점은 <xref:Microsoft.AnalysisServices.AdomdServer.Context> 및 <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentCube%2A> 속성과 같은 <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentMiningModel%2A> 개체의 일부 속성을 각각 한 가지 스크립팅 언어에만 사용할 수 있다는 것입니다.  
  
 다음 예에서는 UDF를 사용하여 노드 설명을 반환하고 튜플을 반환하고 튜플에 필터를 적용하는 방법을 보여 줍니다.  
  
### <a name="returning-a-node-description"></a>노드 설명 반환  
 다음 예에서는 지정한 노드에 대한 노드 설명을 반환하는 UDF를 만듭니다. 이 UDF에서는 UDF가 실행되는 현재 컨텍스트를 사용하고 DMX FROM 절을 사용하여 현재 마이닝 모델에서 노드를 검색합니다.  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 위의 예를 배포한 후에는 가장 가능성이 높은 예측 노드를 검색하는 다음 DMX 식으로 해당 UDF를 호출할 수 있습니다. 반환된 설명에는 예측 노드를 구성하는 조건을 설명하는 정보가 들어 있습니다.  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>튜플 반환  
 다음 예에서는 집합과 반환 개수를 매개 변수로 받아 해당 집합에서 무작위로 튜플을 검색한 다음 최종 하위 집합을 반환합니다.  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 위의 예는 다음 MDX 예에서 호출됩니다. 다섯 개의 국가 또는 주를 무작위로이 MDX 예에서는 검색 된 **Adventure Works** 데이터베이스입니다.  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>튜플에 필터 적용  
 다음 예의 UDF는 집합을 매개 변수로 받고 Expression 개체를 사용하여 집합의 각 튜플에 필터를 적용하도록 정의되어 있습니다. 필터에 맞는 모든 튜플은 반환 집합에 추가됩니다.  
  
 [!code-cs[Adomd.NetServer#FilterSet](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_1.cs)]  
  
 위의 예는 이름이 'A'로 시작하는 도시로 집합을 필터링하는 다음 MDX 예에서 호출됩니다.  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>저장 프로시저 예  
 다음 예의 MDX 기반 저장 프로시저는 필요한 경우 AMO를 사용하여 인터넷 판매를 위한 파티션을 만듭니다.  
  
 [!code-cs[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_2.cs)]  
  
  
