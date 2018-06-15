---
title: ActiveConnection 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6988f743abe5a6a0bf875da0b7e52bed23f7500
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35275162"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 속성 (ADO)
나타내는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 지정 된 개체 [명령](../../../ado/reference/ado-api/command-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 또는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체 현재 속해 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 연결이 닫힌 경우 또는 연결에 대 한 정의 포함 하는 값 **Variant** 현재 포함 된 **연결** 경우 개체는 연결이 열려 있습니다. 기본값은 null 개체 참조입니다. 참조는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **ActiveConnection** 속성을 확인는 **연결** 개체는 지정 된 **명령** 개체는 실행 또는 지정 된  **레코드 집합** 열립니다.  
  
## <a name="command"></a>Command  
 에 대 한 **명령** 개체는 **ActiveConnection** 속성은 읽기/쓰기가 가능 합니다.  
  
 호출 하려고 하면는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 한 **명령** 열린이 속성을 설정 하기 전에 개체 **연결** 개체나 유효한 연결 문자열에서 오류가 발생 합니다.  
  
 경우는 **연결** 개체에 할당 된 **ActiveConnection** 속성을 개체를 열어야 합니다. 닫힌된 연결 개체를 할당 하면 오류가 발생 합니다.  
  
### <a name="note"></a>참고  
 **Microsoft Visual Basic** 설정은 **ActiveConnection** 속성을 *Nothing* 연결을 끊습니다는 **명령** 개체는 현재 **연결** 때문에 공급자 데이터 원본에 연결 된 리소스를 해제 하 고 있습니다. 그런 다음 연결할 수는 **명령** 개체를 동일한 문서나 다른 **연결** 개체입니다. 일부 공급자를 사용 하면 하나에서 속성 설정을 변경할 수 있도록 **연결** 먼저 속성을 설정 하지 않고도 다른 *Nothing*합니다.  
  
 경우는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 의 컬렉션은 **명령** 공급자가 제공 하는 매개 변수를 포함 하는 개체, 컬렉션 설정 하는 경우 선택이 취소 되는 **ActiveConnection** 속성을 *Nothing* 또는 다른 **연결** 개체입니다. 수동으로 만드는 경우 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체를 사용 하 여 채울 수는 **매개 변수** 의 컬렉션은 **명령** 설정 개체는 **ActiveConnection**  속성을 *Nothing* 또는 다른 **연결** 리프 개체는 **매개 변수** 컬렉션 그대로 유지 합니다.  
  
 닫기는 **연결** 개체와 개체는 **명령** 개체는 관련된 set는 **ActiveConnection** 속성을 *Nothing*합니다. 이 속성을 닫힌 **연결** 개체에 오류가 발생 합니다.  
  
## <a name="recordset"></a>레코드 집합  
 열기 **레코드 집합** 개체 또는 **레코드 집합** 개체 [소스](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성이 유효한 **명령** 개체는 **ActiveConnection** 속성은 읽기 전용입니다. 그렇지 않으면은 읽기/쓰기입니다.  
  
 유효한이 속성을 설정할 수 **연결** 개체 또는 유효한 연결 문자열입니다. 이 경우 공급자에서는 새 **연결** 이 정의 사용 하 여 연결을 엽니다. 공급자가 새이 속성을 설정 수는 또한 **연결** 액세스할 수 있는 방법을 제공 하는 개체는 **연결** 확장된 오류 정보 또는 다른 명령을 실행할 개체입니다.  
  
 사용 하는 경우는 *ActiveConnection* 의 인수는 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md) 여 메서드를 한 **레코드 집합** 개체는 **ActiveConnection** 속성은 인수의 값을 상속 합니다.  
  
 설정 하는 경우는 **소스** 의 속성은 **레코드 집합** 을 유효한 개체 **명령** 개체 변수는 **ActiveConnection** 의 속성 **레코드 집합** 의 설정을 상속 된 **명령** 개체의 **ActiveConnection** 속성입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 개체, 연결 문자열 또는 (Microsoft Visual Basic 또는 Visual Basic Scripting Edition)에이 속성을 설정할 수 있습니다를 *Nothing* .  
  
## <a name="record"></a>레코드  
 이 속성은 읽기/쓰기 때는 **레코드** 개체 닫혀 있고 연결 문자열이 나 열린에 대 한 참조를 포함할 수 **연결** 개체입니다. 이 속성은 읽기 전용 시기는 **레코드** 개체를 열면 및 열기에 대 한 참조를 포함 **연결** 개체입니다.  
  
 A **연결** 개체가 암시적으로 만들어진 때의 **레코드** URL에서 개체를 열입니다. 열기는 **레코드** 기존, 사용 하 여 열 **연결** 할당 하 여 개체는 **연결** 이 속성을 가지 거 나 사용 하 여는 **연결** 개체의 매개 변수로 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드를 호출 합니다. 경우는 **레코드** 기존 열릴 **레코드** 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 자동 연결 하는 것이 **레코드** 또는  **레코드 집합** 개체의 **연결** 개체입니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 속성(ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
