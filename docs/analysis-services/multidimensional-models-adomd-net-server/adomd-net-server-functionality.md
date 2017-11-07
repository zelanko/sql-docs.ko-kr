---
title: "ADOMD.NET 서버 기능 | Microsoft Docs"
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
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 40d68e739a9628113b7adfeab5db2a6b1445981f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET Server 기능
  모든 ADOMD.NET 서버 개체는 서버의 데이터 및 메타데이터에 대해 읽기 전용 액세스를 제공하므로 ADOMD.NET 서버 개체 모델을 사용하여 데이터 및 메타데이터를 검색할 수 있습니다. 그러나 이 서버 개체 모델은 스키마 행 집합을 지원하지 않습니다.  
  
 ADOMD.NET 서버 개체를 만들 수 있습니다 (UDF) 사용자 정의 함수 또는 저장된 프로시저에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 이러한 in-process 메서드는 MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 또는 SQL과 같은 언어로 만들어진 쿼리 문을 통해 호출됩니다. 이러한 in-process 메서드는 네트워크 통신에 따른 지연 시간 없이 추가 기능을 제공하기도 합니다.  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 개체는 DMX만을 지원합니다.  
  
## <a name="what-is-a-udf"></a>UDF 정의  
 A *UDF* 는 다음과 같은 특징이 있는 메서드입니다.  
  
-   UDF는 쿼리 컨텍스트에서 호출할 수 있습니다.  
  
-   UDF는 매개 변수 수에 제한이 없습니다.  
  
-   UDF는 여러 데이터 형식을 반환할 수 있습니다.  
  
 다음 예제에서는 가상 UDF인 `FinalSalesNumber`를 사용합니다.  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>저장 프로시저 정의  
 A *저장 프로시저* 는 다음과 같은 특징이 있는 메서드입니다.  
  
-   저장된 프로시저 호출에서 자체적으로 MDX [호출](../../mdx/mdx-data-manipulation-call.md) 문.  
  
-   저장 프로시저는 매개 변수 수에 제한이 없습니다.  
  
-   저장된 프로시저는 데이터 집합을 반환할 수 있습니다는 **IDataReader**, 또는 빈 결과입니다.  
  
 다음 예제에서는 가상 저장 프로시저인 `FinalSalesNumbers`를 사용합니다.  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET 서버 프로그래밍](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  

