---
title: Microsoft OLE DB 원격 공급자 (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da4daddadce73d58dcaa58d5fb56cde1d532ec87
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984075"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 원격 공급자 개요
Microsoft OLE DB 원격 공급자에는 원격 컴퓨터에서 데이터 공급자를 호출 하는 클라이언트 컴퓨터에서 로컬 사용자를 수 있습니다. 원격 컴퓨터의 로컬 사용자와 원격 컴퓨터에 대 한 데이터 공급자 매개 변수를 지정 합니다. 원격 공급자는 원격 컴퓨터에 액세스 하는 데 사용할 매개 변수를 지정 합니다. 그런 다음 로컬 사용자 처럼 원격 컴퓨터를 액세스할 수 있습니다.

> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.

## <a name="provider-keyword"></a>공급자 키워드
 OLE DB 원격 공급자를 호출 하려면 연결 문자열에 다음 키워드와 값을 지정 합니다. (공급자 이름에 공백이 참고 합니다.)

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>추가 키워드
 이 서비스 공급자가 호출 되 면 다음과 같은 추가 키워드 관련이 있습니다.

|키워드|Description|
|-------------|-----------------|
|**데이터 원본**|원격 데이터 원본의 이름을 지정합니다. 처리를 위해 OLE DB 원격 공급자에 게 전달 됩니다.<br /><br /> 이 키워드는 해당 하는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.|

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자가 호출 된 다음 동적 속성에 추가 됩니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md)개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.

|동적 속성 이름|Description|
|---------------------------|-----------------|
|**DFMode**|DataFactory 모드를 나타냅니다. 원하는 버전을 지정 하는 문자열을 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 서버의 개체입니다. 특정 버전의 요청에 대 한 연결을 열기 전에이 속성을 설정 합니다 **DataFactory**합니다. 요청 된 버전을 사용할 수 없는 경우 이전 버전을 사용 하는 시도가 수행 됩니다. 이전 버전이 없는 경우 오류가 발생 합니다. 하는 경우 **DFMode** 보다 작으면 사용 가능한 버전을 오류가 발생 합니다. 연결 된 후이 속성은 읽기 전용입니다.<br /><br /> 다음 유효한 문자열 값 중 하나일 수 있습니다.<br /><br /> -"25"-버전 2.5 (기본값)<br />-"21", 버전 2.1<br />-"20"-버전 2.0<br />-"15"-버전 1.5|
|**명령 속성**|MS 원격 공급자가 서버에 전송 하는 명령 (행 집합) 속성의 문자열에 추가 될 값을 나타냅니다. 이 문자열에 대 한 기본값은 vt_empty 합니다.|
|**현재 DFMode**|실제 버전 번호를 나타내는 합니다 **DataFactory** 서버의 합니다. 버전에서 요청 된 경우를 확인 하려면이 속성을 확인 합니다 **DFMode** 속성 적용 되었습니다.<br /><br /> 다음 유효한 정수 (Long) 값 중 하나일 수 있습니다.<br /><br /> -25-버전 2.5 (기본값)<br />-21-버전 2.1<br />-20-버전 2.0<br />-15-버전 1.5<br /><br /> 추가 "DFMode = 20;"을 사용 하는 경우 연결 문자열을 **MSRemote** 데이터가 업데이트 될 때 공급자 서버의 성능을 향상 시킬 수 있습니다. 이 설정을 사용 합니다 **업데이트할** 서버의 개체를 덜 리소스 집약적 모드를 사용 합니다. 그러나 다음과 같은 기능이이 구성에서 사용할 수 없습니다.<br /><br /> -매개 변수가 있는 쿼리를 사용 합니다.<br />-호출 하기 전에 매개 변수 또는 열의 정보를 시작 합니다 **Execute** 메서드.<br />-설정 **업데이트 &#40;transact** 하 **True**합니다.<br />-시작 행 상태입니다.<br />-호출 된 **Resync** 메서드.<br />-새로 고침 (명시적 또는 자동으로)를 통해 합니다 **업데이트를 다시 동기화** 속성입니다.<br />-설정 **명령** 하거나 **Recordset** 속성입니다.<br />사용 하 여 **adCmdTableDirect**합니다.|
|**Handler**|기능을 확장 하는 서버 쪽 사용자 지정 프로그램 (또는 처리기)의 이름을 나타냅니다 합니다 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), 및 처리기에서 사용 되는 매개 변수 *,* 쉼표 (모든 분리 된 ","). **문자열** 값입니다.|
|**인터넷 제한 시간**|요청이 서버에서 전달 될 때까지 기다리는 시간 (밀리초)의 최대 수를 나타냅니다. (기본값은 5 분입니다.)|
|**원격 공급자**|원격 서버에서 사용 하도록 데이터 공급자의 이름을 나타냅니다.|
|**원격 서버**|이 연결에서 사용할 서버 이름 및 통신 프로토콜을 나타냅니다. 이 속성은 해당 하는 [rds. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 [Server](../../../ado/reference/rds-api/server-property-rds.md) 속성입니다.|
|**업데이트 트랜잭션**|로 설정 하면 **True**, 경우에는이 값을 나타냅니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 이루어집니다 서버에서 수행 된 트랜잭션 내에서. 이 부울 동적 속성에 대 한 기본값은 **False**합니다.|

 쓰기 가능한 동적 속성의 이름을 연결 문자열 키워드를 지정 하 여 설정할 수도 있습니다. 예를 들어 설정 된 **인터넷 시간 제한** 동적 속성을 지정 하 여 5 초:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 또한 설정 하거나 인덱스 이름을 지정 하 여 동적 속성을 검색할 수 있습니다 합니다 **속성** 속성입니다. 다음 예제에서는 가져오고 현재 값을 인쇄 하는 방법을 보여 줍니다 합니다 **인터넷 시간 제한** 동적 속성을 새 값을 설정 합니다.

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Remarks
 2.0 ado, OLE DB 원격 공급자 수에 지정할 합니다 *ActiveConnection* 의 매개 변수를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **열기** 메서드. ADO 2.1부터 공급자도 지정할 수 있습니다에 *ConnectionString* 의 매개 변수를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 **열기** 메서드.

 에 해당 하는는 **rds. DataControl** 개체 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 사용할 수 없습니다. [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **열려** 메서드 *원본* 인수 대신 사용 됩니다.

 **참고** "...; 지정 원격 공급자 MS 원격 =;... "는 4 계층 시나리오를 만듭니다. 3 계층을 초과 하는 시나리오 테스트 하지 않은 하 고 필요 하지 않습니다.

## <a name="example"></a>예제
 쿼리를 수행 하는이 예제는 **작성자** 목차 합니다 **Pubs** 이라는 서버의 데이터베이스 *해당 서버*합니다. 원격 데이터 원본 및 원격 서버의 이름을 제공 됩니다는 [열기](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드는[연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 지정 된 개체 및 SQL 쿼리를[열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드의 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. A **레코드 집합** 개체 반환, 편집 및 데이터 소스를 업데이트 하는 데 사용 합니다.

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>관련 항목
 [OLE DB 원격 공급자 개요](http://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
