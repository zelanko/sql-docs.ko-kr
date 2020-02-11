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
ms.openlocfilehash: 5a2de155d9c4a61246245b2c7f9c3c73a535994a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919685"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
명령 인수를 해석 하는 방법을 지정 합니다.  
  
 사용자가 제공한 *Commandstring* 값의 유효성을 검사 하 여 응용 프로그램 사용자에 게 ADO 실행에 잠재적으로 위험한 명령이 삽입 될 수 없도록 하는 것이 중요 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified 되지 않음**|-1|명령 유형 인수를 지정 하지 않습니다.|  
|**adCmdText**|1|[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 를 명령 또는 저장 프로시저 호출의 텍스트 정의로 평가 합니다.|  
|**adCmdTable**|2|는 내부적으로 생성 된 SQL 쿼리에서 반환 되는 열이 포함 된 테이블 이름으로 **CommandText** 를 평가 합니다.|  
|**adCmdStoredProc**|4|**CommandText** 를 저장 프로시저 이름으로 평가 합니다.|  
|**adCmdUnknown**|8|Default. **CommandText** 속성의 명령 유형을 알 수 없음을 나타냅니다.<br /><br /> 명령 유형을 알 수 없는 경우 ADO는 **CommandText**를 해석 하려는 여러 시도를 수행 합니다.<br /><br /> -   **CommandText** 는 명령 또는 저장 프로시저 호출의 텍스트 정의로 해석 됩니다. 이 동작은 **Adcmdtext**와 동일 합니다.<br />-   **CommandText** 는 저장 프로시저의 이름입니다. 이 동작은 **adCmdStoredProc**와 동일 합니다.<br />-   **CommandText** 는 테이블 이름으로 해석 됩니다. 모든 열은 내부적으로 생성 된 SQL 쿼리에서 반환 됩니다. 이는 **Adcmdtable**과 동일한 동작입니다.|  
|**adCmdFile**|256|는 **CommandText** 를 영구적으로 저장 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)의 파일 이름으로 평가 합니다. **레코드 집합과 함께 사용 됩니다.** [열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 또는 다시 [쿼리해야](../../../ado/reference/ado-api/requery-method.md) 합니다.|  
|**adCmdTableDirect**|512|는 열이 모두 반환 되는 테이블 이름으로 **CommandText** 를 평가 합니다. **레코드 집합과** 함께 사용 됩니다. **** [Seek](../../../ado/reference/ado-api/seek-method.md) 메서드를 사용 하려면 **adCmdTableDirect**를 사용 하 여 **레코드 집합** 을 열어야 합니다.<br /><br /> 이 값을 [Executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md) 값 **adasyncexecute**와 함께 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums STOREDPROC|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums TABLEDIRECT|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[CommandType 속성(ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Execute 메서드(ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Requery 메서드](../../../ado/reference/ado-api/requery-method.md)||
