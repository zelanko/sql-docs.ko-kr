---
description: ActiveConnection 속성(ADO)
title: ActiveConnection 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: rothja
ms.author: jroth
ms.openlocfilehash: 058f1e16c6bdd84978c1131c436764f584fd80c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451675"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 속성(ADO)
지정 된 [명령](../../../ado/reference/ado-api/command-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)또는 [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체가 현재 속해 있는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 연결이 닫힌 경우에는 연결에 대 한 정의를 포함 하는 **문자열** 값을 설정 하거나 반환 하 고, 연결이 열린 경우에는 현재 **연결** 개체를 포함 하는 **Variant** 를 설정 하거나 반환 합니다. 기본값은 null 개체 참조입니다. [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을 참조 하세요.  
  
## <a name="remarks"></a>설명  
 **ActiveConnection** 속성을 사용 하 여 지정 된 **명령** 개체가 실행 되는 **연결** 개체를 확인 하거나 지정 된 **레코드 집합** 을 열 수 있습니다.  
  
## <a name="command"></a>명령  
 **Command** 개체의 경우 **ActiveConnection** 속성은 읽기/쓰기입니다.  
  
 이 속성을 열려 있는 **연결** 개체 또는 유효한 연결 문자열로 설정 하기 전에 **명령** 개체에 대해 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 호출 하려고 하면 오류가 발생 합니다.  
  
 **연결** 개체가 **ActiveConnection** 속성에 할당 된 경우 개체를 열어야 합니다. 폐쇄형 연결 개체를 할당 하면 오류가 발생 합니다.  
  
### <a name="note"></a>참고  
 **Microsoft Visual Basic** **ActiveConnection** 속성을로 설정 하면 현재 **연결** 에서 **명령** 개체의 *연결을 해제* 하 고 공급자가 데이터 원본에서 연결 된 모든 리소스를 해제 합니다. 그런 다음 동일한 또는 다른 **연결** 개체와 **명령** 개체를 연결할 수 있습니다. 일부 공급자에서는 먼저 속성을 *Nothing*으로 설정 하지 않고도 속성 설정을 다른 **연결** 로 변경할 수 있습니다.  
  
 **명령** 개체의 [parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션에 공급자가 제공 하는 매개 변수가 포함 된 경우 **ActiveConnection** 속성을 *Nothing* 으로 설정 하거나 다른 **연결** 개체로 설정 하면 컬렉션이 지워집니다. 수동으로 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체를 만들고이 개체를 사용 하 여 **명령** 개체의 **Parameters** 컬렉션을 채울 경우 **ActiveConnection** 속성을 *Nothing* 으로 설정 하거나 다른 **연결** 개체로 설정 하 여 **매개 변수** 컬렉션을 그대로 유지 합니다.  
  
 **Command** 개체가 연결 된 **연결** 개체를 닫으면 **ActiveConnection** 속성이 *Nothing*으로 설정 됩니다. 이 속성을 닫힌 **연결** 개체로 설정 하면 오류가 발생 합니다.  
  
## <a name="recordset"></a>레코드 집합  
 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성이 유효한 **명령** 개체로 설정 **된 레코드 집합 개체 또는** 열려 있는 **레코드** 집합 개체의 경우 **ActiveConnection** 속성은 읽기 전용입니다. 그렇지 않으면 읽기/쓰기가 됩니다.  
  
 이 속성을 유효한 **연결** 개체나 유효한 연결 문자열로 설정할 수 있습니다. 이 경우 공급자는이 정의를 사용 하 여 새 **연결** 개체를 만들고 연결을 엽니다. 또한 공급자는이 속성을 새 **연결** 개체로 설정 하 여 확장 오류 정보에 대 한 **연결** 개체에 액세스 하거나 다른 명령을 실행 하는 방법을 제공할 수 있습니다.  
  
 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드의 *ActiveConnection* 인수를 사용 하 여 **레코드 집합** 개체를 열면 **ActiveConnection** 속성이 인수 값을 상속 합니다.  
  
 **Recordset** 개체의 **Source** 속성을 유효한 **명령** 개체 변수로 설정 하면 **레코드 집합** 의 **ActiveConnection** 속성은 **Command** 개체의 **ActiveConnection** 속성 설정을 상속 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **레코드 집합** 개체에서 *사용 하는*경우이 속성은 연결 문자열 또는 (Microsoft Visual Basic 또는 Visual Basic Scripting Edition)로만 설정할 수 있습니다.  
  
## <a name="record"></a>레코드  
 **Record** 개체가 닫혀 있는 경우이 속성은 읽기/쓰기이 고, 연결 문자열 또는 열린 **연결** 개체에 대 한 참조를 포함할 수 있습니다. **Record** 개체가 열려 있고 열린 **연결** 개체에 대 한 참조를 포함 하는 경우이 속성은 읽기 전용입니다.  
  
 **연결** 개체는 URL에서 **Record** 개체를 열 때 암시적으로 생성 됩니다. **연결** 개체를이 속성에 할당 하거나 **연결** 개체를 [open](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드 호출의 매개 변수로 사용 하 여 열려 있는 기존 **연결** 개체를 사용 하 여 **레코드** 를 엽니다. 기존 **레코드나** 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md)에서 **레코드** 를 **열면 해당 레코드 또는 레코드** **집합** 개체의 **연결** 개체에 자동으로 연결 됩니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString 속성(ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
