---
title: "저장된 프로시저를 호출 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e2c8656c28db458104a3793175a739d311ac379
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="calling-stored-procedures"></a>저장 프로시저 호출
  저장 프로시저는 서버나 클라이언트 응용 프로그램에서 호출할 수 있습니다. 어느 경우에나 저장 프로시저는 항상 서버에서 서버나 데이터베이스의 컨텍스트로 실행됩니다. 저장 프로시저를 실행하는 데 필요한 특별 권한은 없습니다. 어셈블리를 사용하여 서버 또는 데이터베이스 컨텍스트에 저장 프로시저를 추가한 후에는 저장 프로시저에서 수행하는 동작이 허가된 역할의 사용자는 모두 저장 프로시저를 실행할 수 있습니다.  
  
 MDX의 저장 프로시저 호출은 내부 MDX 함수 호출과 동일한 방식으로 이루어집니다. 매개 변수가 없는 저장 프로시저의 경우 아래와 같이 프로시저 이름과 빈 괄호 쌍을 사용합니다.  
  
```  
MyStoredProcedure()  
```  
  
 저장 프로시저에 매개 변수가 한 개 이상 있을 경우 매개 변수를 쉼표로 구분하여 순서대로 제공합니다. 다음 예에서는 매개 변수가 세 개 있는 예제 저장 프로시저를 보여 줍니다.  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>MDX 쿼리에서 저장 프로시저 호출  
 모든 MDX 쿼리에서 저장 프로시저는 MDX 식에 필요한 올바른 구문의 형식을 반환해야 합니다. 저장 프로시저에서 올바른 형식을 반환하지 않으면 MDX 오류가 발생합니다. 다음 예에서는 집합, 멤버 및 수치 연산의 결과를 반환하는 저장 프로시저를 보여 줍니다.  
  
### <a name="returning-a-set"></a>집합 반환  
 다음 예에서는 집합을 반환하는 저장 프로시저 MySproc를 구현합니다. 첫 번째 예에서 MySproc는 SELECT 식에서 직접 집합을 반환합니다. 나머지 두 예에서는 MySproc가 Crossjoin 및 DrilldownLevel 함수의 인수로 집합을 반환합니다.  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>멤버 반환  
 다음 예에서는 멤버를 반환하는 MySproc 함수를 보여 줍니다.  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>수치 연산의 결과 반환  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>Call 문으로 저장 프로시저 호출  
 MDX를 사용 하 여 MDX 쿼리 컨텍스트 외부에서 저장된 프로시저를 호출할 수 **호출** 문.  
  
 이 방법을 사용하면 저장 쿼리의 파생 작업을 인스턴스화하거나 응용 프로그램에서 저장 쿼리의 결과를 얻을 수 있습니다. 일반적인 용도 **호출** 문을 Analysis Management Objects (AMO)를 사용 하 여 반환 결과 갖지 않는 관리 기능을 수행 하는 것입니다. 예를 들어 다음 명령에서는 저장 프로시저를 호출합니다.  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 지원 되는 유일한 종류의 저장된 프로시저에서 반환 되는 **호출** 문의 행 집합입니다. 행 집합 직렬화는 XML for Analysis에 의해 정의됩니다. 경우의 저장된 프로시저는 **호출** 문은 다른 형식을 반환, 무시 되 고 호출 응용 프로그램에 XML에 반환 되지 않습니다. XML for Analysis 행 집합에 대한 자세한 내용은 XML for Analysis Schema Rowsets를 참조하십시오.  
  
 저장 프로시저에서 .NET 행 집합을 반환하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 서버의 결과를 XML for Analysis 행 집합으로 변환합니다. XML for Analysis 행 집합은 항상 저장된 프로시저에 의해 반환 된 **호출** 함수입니다. 데이터 집합에 XML for Analysis 행 집합으로 표현할 수 없는 기능이 있다면 실패합니다.  
  
 Void 값을 반환하는 프로시저(예: Visual Basic의 서브루틴)를 CALL 키워드와 함께 사용할 수 있습니다.  예를 들어 MDX 문에서 MyVoidFunction() 함수를 사용하려면 다음과 같은 구문을 사용합니다.  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [저장 프로시저 정의](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

