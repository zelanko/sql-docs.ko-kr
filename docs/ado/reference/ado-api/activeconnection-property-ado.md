---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 951f43a2842162aa00f664dc83b754d06d8aafb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065541"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection 속성(ADO)
나타냅니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 지정 된 개체 [명령](../../../ado/reference/ado-api/command-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 또는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체가 현재 속한.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **문자열** 연결이 닫혀 있는 경우 또는 연결에 대 한 정의 포함 하는 값 **Variant** 현재 포함 된 **연결** 경우 개체는 연결이 열려 있습니다. 기본값은 null 개체 참조입니다. 참조 된 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **ActiveConnection** 속성을는 **연결** 개체는 지정 된 **명령** 개체는 실행 또는 지정 된  **레코드 집합** 열립니다.  
  
## <a name="command"></a>Command  
 에 대 한 **명령** 개체를 **ActiveConnection** 속성은 읽기/쓰기가 가능 합니다.  
  
 호출 하려는 경우는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드를 **명령** 개방적으로이 속성을 설정 하려면 먼저 개체 **연결** 오류가 발생 하는 개체 또는 올바른 연결 문자열.  
  
 경우는 **연결** 개체에 할당 합니다 **ActiveConnection** 속성 개체를 열어야 합니다. 닫힌된 연결 개체를 할당 하면 오류가 발생 합니다.  
  
### <a name="note"></a>참고  
 **Microsoft Visual Basic** 설정 합니다 **ActiveConnection** 속성을 *Nothing* 분리 합니다 **명령** 현재에서개체**연결** 때문에 공급자 데이터 원본에 연결 된 모든 리소스를 해제 하 고 있습니다. 연결할 수 있습니다 합니다 **명령** 개체와 같은 또는 다른 **연결** 개체입니다. 일부 공급자를 사용 하면 하나에서 속성 설정을 변경 하려면 **연결** 먼저 속성을 설정 하지 않고 다른 *Nothing*합니다.  
  
 경우는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 의 컬렉션을 **명령** 공급자가 제공한 매개 변수를 포함 하는 개체, 설정 하는 경우 컬렉션은 지워지지 합니다 **ActiveConnection** 속성을 *아무* 또는 다른 **연결** 개체입니다. 수동으로 만들어야 하는 경우 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체를 사용 하 여 입력 합니다 **매개 변수** 컬렉션을 **명령** 개체를 설정는 **ActiveConnection**  속성을 *Nothing* 또는 다른 **연결** 리프 개체를 **매개 변수** 컬렉션 그대로 유지 됩니다.  
  
 닫기는 **연결** 개체를 **명령** 개체가 연결된 집합을 **ActiveConnection** 속성을 *Nothing*합니다. 이 속성을 닫힌 **연결** 개체에 오류가 발생 합니다.  
  
## <a name="recordset"></a>레코드 집합  
 열기에 대 한 **레코드 집합** 개체 또는 **레코드 집합** 갖는 개체 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성은 유효한 **명령** 개체, 합니다 **ActiveConnection** 속성은 읽기 전용입니다. 그렇지 않을 경우 읽기/쓰기입니다.  
  
 유효한이 속성을 설정할 수 있습니다 **연결** 개체 또는 유효한 연결 문자열입니다. 이 경우 공급자를 만듭니다 **연결** 이 정의 사용 하 여 연결을 엽니다. 공급자가 새이 속성을 설정 수는 또한 **연결** 액세스 하는 방법을 제공 하는 개체를 **연결** 확장된 오류 정보 또는 다른 명령을 실행할 개체입니다.  
  
 사용 하는 경우는 *ActiveConnection* 인수를 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md) 를 여는 메서드를 **레코드 집합** 개체를 **ActiveConnection** 속성은 인수의 값을 상속 합니다.  
  
 설정 하는 경우는 **원본** 의 속성을 **레코드 집합** 유효한 개체 **명령** 개체 변수를를 **ActiveConnection** 의 속성 합니다 **레코드 집합** 의 설정을 상속 합니다 **명령** 개체의 **ActiveConnection** 속성입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용 되 면 **레코드 집합** 개체를 연결 문자열 또는 (Microsoft Visual Basic 또는 Visual Basic Scripting Edition)에이 속성을 설정할 수 있습니다 *Nothing* .  
  
## <a name="record"></a>레코드  
 이 속성은 읽기/쓰기 경우 합니다 **레코드** 개체가 닫혀 있고 연결 문자열 또는 개방적이 고에 대 한 참조를 포함할 수 있습니다 **연결** 개체입니다. 이 속성이 읽기 전용인 경우 합니다 **레코드** 개체를 열면 및 개방적이 고에 대 한 참조를 포함 **연결** 개체입니다.  
  
 A **연결** 개체는 암시적으로 생성 하면 합니다 **레코드** URL에서 개체를 열입니다. 엽니다는 **레코드** 기존의 엽니다 **연결** 할당 하 여 개체를 **연결** 또는이 속성에 개체를 사용 하 여는 **연결** 매개 변수로 개체를 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드를 호출 합니다. 경우는 **레코드** 기존에서 열리는 **레코드** 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)에 자동으로 연관 됩니다 **레코드** 또는  **레코드 집합** 개체의 **연결** 개체입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
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
