---
description: CommandTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 994fe5eb0cf10189477e11154b8814f5e73c9194
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776082"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
명령 인수를 해석 하는 방법을 지정 합니다.  
  
 사용자가 제공한 *Commandstring* 값의 유효성을 검사 하 여 응용 프로그램 사용자에 게 ADO 실행에 잠재적으로 위험한 명령이 삽입 될 수 없도록 하는 것이 중요 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified 되지 않음**|-1|명령 유형 인수를 지정 하지 않습니다.|  
|**adCmdText**|1|[CommandText](./commandtext-property-ado.md) 를 명령 또는 저장 프로시저 호출의 텍스트 정의로 평가 합니다.|  
|**adCmdTable**|2|는 내부적으로 생성 된 SQL 쿼리에서 반환 되는 열이 포함 된 테이블 이름으로 **CommandText** 를 평가 합니다.|  
|**adCmdStoredProc**|4|**CommandText** 를 저장 프로시저 이름으로 평가 합니다.|  
|**adCmdUnknown**|8|기본값 **CommandText** 속성의 명령 유형을 알 수 없음을 나타냅니다.<br /><br /> 명령 유형을 알 수 없는 경우 ADO는 **CommandText**를 해석 하려는 여러 시도를 수행 합니다.<br /><br /> -   **CommandText** 는 명령 또는 저장 프로시저 호출의 텍스트 정의로 해석 됩니다. 이 동작은 **Adcmdtext**와 동일 합니다.<br />-   **CommandText** 는 저장 프로시저의 이름입니다. 이 동작은 **adCmdStoredProc**와 동일 합니다.<br />-   **CommandText** 는 테이블 이름으로 해석 됩니다. 모든 열은 내부적으로 생성 된 SQL 쿼리에서 반환 됩니다. 이는 **Adcmdtable**과 동일한 동작입니다.|  
|**adCmdFile**|256|는 **CommandText** 를 영구적으로 저장 된 [레코드 집합](./recordset-object-ado.md)의 파일 이름으로 평가 합니다. **레코드 집합과 함께 사용 됩니다.** [열기](./open-method-ado-recordset.md) 또는 다시 [쿼리해야](./requery-method.md) 합니다.|  
|**adCmdTableDirect**|512|는 열이 모두 반환 되는 테이블 이름으로 **CommandText** 를 평가 합니다. **레코드 집합과** 함께 사용 됩니다. **Requery** [Seek](./seek-method.md) 메서드를 사용 하려면 **adCmdTableDirect**를 사용 하 여 **레코드 집합** 을 열어야 합니다.<br /><br /> 이 값을 [Executeoptionenum](./executeoptionenum.md) 값 **adasyncexecute**와 함께 사용할 수 없습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums STOREDPROC|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums TABLEDIRECT|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [CommandType 속성(ADO)](./commandtype-property-ado.md)  
        [Execute 메서드(ADO 명령)](./execute-method-ado-command.md)  
    :::column-end:::
    :::column:::
        [Execute 메서드(ADO 연결)](./execute-method-ado-connection.md)  
        [Open 메서드(ADO 레코드 집합)](./open-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Requery 메서드](./requery-method.md)  
    :::column-end:::
:::row-end:::