---
title: ADOMD.NET 서버 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 622a7c51bfd6c2a8a9defba70a412967a48dee50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088723"
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
  
-   저장된 프로시저 호출에서 자체적으로 MDX [호출](/sql/mdx/mdx-data-manipulation-call) 문.  
  
-   저장 프로시저는 매개 변수 수에 제한이 없습니다.  
  
-   저장 프로시저는 데이터 집합, `IDataReader` 또는 빈 결과를 반환할 수 있습니다.  
  
 다음 예제에서는 가상 저장 프로시저인 `FinalSalesNumbers`를 사용합니다.  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET 서버 프로그래밍](adomd-net-server-programming.md)  
  
  
