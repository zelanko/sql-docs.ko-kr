---
title: ISSCommandWithParameters(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63209763"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters(OLE DB)
  **ISSCommandWithParameters** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 및 UDT(사용자 정의 형식)에 대한 지원을 노출합니다. 이 인터페이스는 선택적 인터페이스이며 핵심 OLE DB 인터페이스인 **ICommandWithParameters**에서 상속됩니다. **ICommandWithParameters**에서 상속되는 3개의 메서드인 **GetParameterInfo**, **MapParameterNames**및 **SetParameterInfo**외에도 **ISSCommandWithParameters** 는 서버별 데이터 형식을 처리하는 데 사용되는 두 개의 새 메서드를 제공합니다.  
  
> [!NOTE]  
>   서비스 구성 요소가 사용되는 경우 **ISSCommandWithParameters** 인터페이스를 사용할 수 있지만 서비스 구성 요소 자체는 이 인터페이스를 사용하지 않습니다.  
  
|방법|Description|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|명령에 전달된 각 UDT 또는 XML 매개 변수에 대해 배열의 **SSPARAMPROPS** 속성 집합 구조를 하나씩 반환하지만 다른 유형의 매개 변수에 대해서는 아무 것도 반환되지 않습니다.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|매개 변수별 서수로 매개 변수 속성을 설정하거나, **SSPARAMPROPS** 구조의 배열을 지정하여 대량 매개 변수 속성을 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [XML 데이터 형식 사용](../native-client/features/using-xml-data-types.md)   
 [사용자 정의 형식 사용](../native-client/features/using-user-defined-types.md)  
  
  
