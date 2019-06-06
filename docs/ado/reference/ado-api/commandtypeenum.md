---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 09874df6d9e09da8b6dc0df3e9670e4ff130c511
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695972"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
명령 인수를 해석 하는 방법을 지정 합니다.  
  
 사용자가 제공한 유효성을 검사 하는 것이 반드시 *CommandString* 응용 프로그램 사용자에 게 실행 하는 ADO에 대 한 잠재적으로 위험한 명령을 삽입 하는 기회를 제공 하지 않으려면 값입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|명령 유형 인수를 지정 하지 않습니다.|  
|**adCmdText**|1|평가 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 명령 또는 저장된 프로시저의 텍스트 정의로 호출 합니다.|  
|**adCmdTable**|2|평가 **CommandText** 열이 있는 모든는 내부적으로 생성 된 SQL 쿼리에 의해 반환 된 테이블 이름으로 합니다.|  
|**adCmdStoredProc**|4|평가 **CommandText** 저장된 프로시저 이름으로 합니다.|  
|**adCmdUnknown**|8|기본. 나타내는에서 명령의 형식을 합니다 **CommandText** 속성 알 수 없습니다.<br /><br /> ADO를 해석 하는 여러 시도 하 게 명령의 형식을 알려지지 않은 경우에 **CommandText**합니다.<br /><br /> -   **CommandText** 명령 또는 저장 프로시저 호출의 텍스트 정의로 해석 됩니다. 동일한 동작을 이것이 **adCmdText**합니다.<br />-   **CommandText** 저장된 프로시저의 이름입니다. 동일한 동작을 이것이 **adCmdStoredProc**합니다.<br />-   **CommandText** 테이블의 이름으로 해석 됩니다. 모든 열을 내부적으로 생성 된 SQL 쿼리에 의해 반환 됩니다. 동일한 동작을 이것이 **adCmdTable**합니다.|  
|**adCmdFile**|256|평가 **CommandText** 영구적으로 저장 된 파일 이름으로 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)합니다. 사용한 **레코드 집합.** [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md) 하거나 [Requery](../../../ado/reference/ado-api/requery-method.md) 만 합니다.|  
|**adCmdTableDirect**|512|평가 **CommandText** 는 테이블 이름과 열이 모두 반환 됩니다. 사용한 **Recordset.Open** 하거나 **Requery** 만 합니다. 사용 하는 [Seek](../../../ado/reference/ado-api/seek-method.md) 메서드는 **레코드 집합** 으로 열어야 합니다 **adCmdTableDirect**합니다.<br /><br /> 이 값과 결합할 수 없습니다는 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 값 **adAsyncExecute**합니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
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
