---
title: TOM API (Analysis Services AMO-TOM)에서 오류 처리 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d13c9318acbc70b2024d2f4f6b901d39e716e747
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="handling-errors-in-the-tom-api-analysis-services-amo-tom"></a>TOM API (Analysis Services AMO-TOM)에서 오류 처리
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
관리 되는 라이브러리와 같은 Analysis Services Management Objects (AMO) 테이블 형식 개체 모델 (TOM)에 대 한 일반적으로 사용자에 게 오류 상태를 보고 하기 위한 메커니즘으로 예외를 사용 하는 것입니다.  

AMO TOM에서 오류가 검색 되 면 throw 이외의 몇 가지 표준.NET 예외와 같은 **ArgumentException** 및 **InvalidOperationException**, TOM 수 예외를 throw 할 몇 가지 TOM 관련 됩니다.  

TOM 예외에서 파생 됩니다 [AmoException 클래스](http://msdn.microsoft.com/library/microsoft.analysisservices.amoexception.aspx), AMO 및 TOM 관련 예외가 모두 포함 합니다. 

TOM에서 예외 처리를 보여 주기 위해 검토해 보겠습니다는 보다 일반적인 예외 중 하나가 [OperationException 클래스](http://msdn.microsoft.com/library/microsoft.analysisservices.operationexception.aspx)합니다.

**OperationException** 사용자가 Analysis Services 서버에서 작업이 시작 작업, 잘못 되었습니다. 또는 다른 내부 또는 외부 오류로 인해 작업을 수행 하는 서버 실패 했을 때 throw 됩니다. 

Throw 되 면 * * OperationException * * 개체는 서버에서 반환 하는 XMLA 오류 목록이 포함 됩니다. 

참고는 서버는 유효 하지 않은 변경 내용을 받지 않습니다. 이 문제가 발생 하는 경우 되돌릴는 **모델** 다시 사용 하 여 마지막 알려진된 좋은 상태에 트리는 [UndoLocalChanges 메서드](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.model.undolocalchanges.aspx)모델을 수정한 후 다시 전송 합니다. 

## <a name="code-example-handle-exceptions"></a>코드 예: 예외 처리 
 
```
 try 
 { 
  // Change the Model, for example create a table. 
  // … 
   model.saveChanges(); 
 } 
  catch(operationException ex) 
 { 
  foreach(XmlaError err in ex.Results.OfType<XmlaError>().cast<XmlaError>()) 
  { 
   Console.WriteLine(“Error returned from the server:” + err.Messsage ); 
  } 
 } 
```

## <a name="next-steps"></a>다음 단계

다른 관련 된 예외는 다음과 같습니다.

- [TomInternalException 클래스](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tominternalexception.aspx)
- [TomValidationException 클래스](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tomvalidationexception.aspx)
- [JsonSerializationException 클래스](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_JsonSerializationException.htm)
