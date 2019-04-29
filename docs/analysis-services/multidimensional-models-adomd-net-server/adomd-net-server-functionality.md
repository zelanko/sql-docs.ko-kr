---
title: ADOMD.NET Server 기능 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c1f37be45b702828d3c663eac0fb575a0af3bbd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63059469"
---
# <a name="adomdnet-server-functionality"></a>ADOMD.NET Server 기능
  모든 ADOMD.NET 서버 개체는 서버의 데이터 및 메타데이터에 대해 읽기 전용 액세스를 제공하므로 ADOMD.NET 서버 개체 모델을 사용하여 데이터 및 메타데이터를 검색할 수 있습니다. 그러나 이 서버 개체 모델은 스키마 행 집합을 지원하지 않습니다.  
  
 ADOMD.NET 서버 개체를 사용 하 여 사용자 정의 함수 (UDF) 또는 저장된 프로시저를 만들 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 이러한 in-process 메서드는 MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 또는 SQL과 같은 언어로 만들어진 쿼리 문을 통해 호출됩니다. 이러한 in-process 메서드는 네트워크 통신에 따른 지연 시간 없이 추가 기능을 제공하기도 합니다.  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 개체는 DMX만을 지원합니다.  
  
## <a name="what-is-a-udf"></a>UDF 정의  
 A *UDF* 다음과 같은 특징이 있는 메서드입니다.  
  
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
 A *저장 프로시저* 다음과 같은 특징이 있는 메서드입니다.  
  
-   호출 저장된 프로시저에서 MDX를 사용 하 여 자체 [호출](../../mdx/mdx-data-manipulation-call.md) 문입니다.  
  
-   저장 프로시저는 매개 변수 수에 제한이 없습니다.  
  
-   저장된 프로시저는 데이터 집합을 반환할 수는 **IDataReader**, 또는 빈 결과.  
  
 다음 예제에서는 가상 저장 프로시저인 `FinalSalesNumbers`를 사용합니다.  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET 서버 프로그래밍](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
