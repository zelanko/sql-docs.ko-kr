---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bc2cd3acc56c11bdab98d58c1adc76d98eb1579d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="commandtypeenum"></a>CommandTypeEnum
명령 인수를 해석 하는 방법을 지정 합니다.  
  
 사용자가 제공한 유효성을 검사 해야 *CommandString* 을 방지 하기 위해 응용 프로그램 사용자 기회를 실행 하도록 ADO에 대 한 잠재적으로 위험한 명령을 삽입 하는 값입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|명령 유형 인수를 지정 하지 않습니다.|  
|**adCmdText**|1.|평가 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 명령 또는 저장된 프로시저의 텍스트 정의 호출 합니다.|  
|**adCmdTable**|2|평가 **CommandText** 열이 있는 모든는 내부적으로 생성 된 SQL 쿼리에 의해 반환 된 테이블 이름으로 합니다.|  
|**adCmdStoredProc**|4|평가 **CommandText** 로 저장된 프로시저 이름을 입력 합니다.|  
|**adCmdUnknown**|8|기본. 나타냅니다에 명령 유형에 **CommandText** 속성 알 수 없습니다.<br /><br /> ADO를 해석 하는 몇 차례 시도 하면 명령의 형식을 알려지지 않은 경우는 **CommandText**합니다.<br /><br /> -   **CommandText** 명령 또는 저장 프로시저 호출의 텍스트 정의로 해석 됩니다. 이 같은 동작 **adCmdText**합니다.<br />-   **CommandText** 저장된 프로시저의 이름입니다. 이 같은 동작 **adCmdStoredProc**합니다.<br />-   **CommandText** 테이블의 이름으로 해석 됩니다. 모든 열은 내부적으로 생성 된 SQL 쿼리에 의해 반환 됩니다. 이 같은 동작 **adCmdTable**합니다.|  
|**adCmdFile**|256|평가 **CommandText** 영구적으로 저장 된 파일 이름으로 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 함께 사용할 **레코드 집합.** [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 또는 [Requery](../../../ado/reference/ado-api/requery-method.md) 만 합니다.|  
|**adCmdTableDirect**|512|평가 **CommandText** 는 테이블 이름과 열이 있는 모두 반환 합니다. 함께 사용할 **Recordset.Open** 또는 **Requery** 만 합니다. 사용 하는 [Seek](../../../ado/reference/ado-api/seek-method.md) 메서드는 **레코드 집합** 으로 열어야 **adCmdTableDirect**합니다.<br /><br /> 이 값을 함께 사용할 수는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값 **adAsyncExecute**합니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[CommandType 속성(ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute 메서드(ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery 메서드](../../../ado/reference/ado-api/requery-method.md)||

