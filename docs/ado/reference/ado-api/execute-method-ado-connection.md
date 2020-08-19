---
description: Execute 메서드(ADO 연결)
title: Execute 메서드 (ADO 연결) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: rothja
ms.author: jroth
ms.openlocfilehash: 1acbdc4966f46d5e155dab3fac059568699d4727
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443915"
---
# <a name="execute-method-ado-connection"></a>Execute 메서드(ADO 연결)
지정 된 쿼리, SQL 문, 저장 프로시저 또는 공급자별 텍스트를 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Return Value  
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 참조를 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *CommandText*  
 실행할 SQL 문, 저장 프로시저, URL 또는 공급자별 텍스트를 포함 하는 **문자열** 값입니다. **필요에 따라**테이블 이름을 사용할 수 있지만 공급자가 SQL을 인식 하는 경우에만 사용할 수 있습니다. 예를 들어 "Customers"의 테이블 이름이 사용 되는 경우 ADO는 자동으로 표준 SQL Select 구문을 구성 하 고 공급자에 게 "SELECT * FROM Customers"를 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문으로 전달 합니다.  
  
 *RecordsAffected*  
 (선택 사항) 공급자가 작업에서 영향을 받은 레코드 수를 반환 하는 **Long** 변수입니다.  
  
 *옵션*  
 (선택 사항) 공급자가 CommandText 인수를 평가 하는 방법을 나타내는 **Long** 값입니다. 하나 이상의 CommandTypeEnum 또는 [Execute 열거형](../../../ado/reference/ado-api/executeoptionenum.md) 값 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 의 비트 마스크 일 수 있습니다.  
  
 **참고** Visual Basic 6.0에서 이식 하는 응용 프로그램 및 내부 처리를 최소화 하 여 성능을 향상 시키려면 **ExecuteadExecuteNoRecords 열거형** 값을 사용 합니다. **adExecuteNoRecords**  
  
 **Connection** 개체의 **Execute** 메서드와 함께 **adExecuteStream** 를 사용 하지 마십시오.  
  
 AdCmdFile 또는 adCmdTableDirect의 CommandTypeEnum 값을 Execute와 함께 사용 하지 마세요. 이러한 값은 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 및 **레코드 집합**의 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md) 메서드와 함께 옵션 으로만 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 **Execute** 메서드를 사용 하면 지정 된 연결에서 CommandText 인수의 메서드에 전달 하는 모든 쿼리가 실행 됩니다. CommandText 인수가 행 반환 쿼리를 지정 하는 경우 실행에 의해 생성 되는 모든 결과는 새 **레코드 집합** 개체에 저장 됩니다. 명령이 결과를 반환 하기에 적합 하지 않은 경우 (예: SQL 업데이트 쿼리) **adExecuteNoRecords** 옵션이 지정 된 경우에는 공급자가 **아무 것도** 반환 하지 않습니다. 그렇지 않으면 Execute는 닫힌 **레코드 집합**을 반환 합니다.  
  
 반환 된 **레코드 집합** 개체는 항상 읽기 전용, 앞 으로만 이동 가능한 커서입니다. 더 많은 기능을 포함 하는 **레코드 집합** 개체가 필요한 경우 먼저 원하는 속성 설정을 사용 하 여 **레코드 집합** 개체를 만든 다음 **레코드 집합** 개체의 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 사용 하 여 쿼리를 실행 하 고 원하는 커서 유형을 반환 합니다.  
  
 *CommandText* 인수의 내용은 공급자와 관련이 있으며 공급자가 지 원하는 특수 명령 형식 또는 표준 SQL 구문이 될 수 있습니다.  
  
 이 작업이 완료 되 면 ExecuteComplete 이벤트가 발생 합니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
