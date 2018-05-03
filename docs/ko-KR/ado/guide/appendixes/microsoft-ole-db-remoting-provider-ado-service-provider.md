---
title: Microsoft OLE DB Remoting Provider (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
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
ms.openlocfilehash: 125ec1708c93abf78b4d4fa4663b287579d45f5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB 공급자 개요
Microsoft OLE DB 원격 공급자에는 원격 컴퓨터에서 데이터 공급자를 호출 하는 클라이언트 컴퓨터에서 로컬 사용자 수 있습니다. 원격 컴퓨터에서 로컬 사용자 인 경우와 마찬가지로 원격 컴퓨터에 대 한 데이터 공급자 매개 변수를 지정 합니다. 원격 컴퓨터에 액세스할 수는 원격 공급자에서 사용 하는 매개 변수를 지정 합니다. 그런 다음 로컬 사용자 인 경우에 따라 원격 컴퓨터를 액세스할 수 있습니다.

> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.

## <a name="provider-keyword"></a>Provider 키워드
 OLE DB 원격 서비스 공급자를 호출 하려면 연결 문자열에는 다음 키워드와 값을 지정 합니다. (공급자 이름에 공백 참고 합니다.)

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>다른 키워드
 이 서비스 공급자를 호출 하면 다음과 같은 추가 키워드 관련이 있습니다.

|키워드|Description|
|-------------|-----------------|
|**데이터 원본**|원격 데이터 원본의 이름을 지정합니다. 처리를 위해 OLE DB 원격 공급자에 전달 됩니다.<br /><br /> 이 키워드는 해당 하는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 [연결](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.|

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자가 호출 되는 다음과 같은 동적 속성에 추가 됩니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md)개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.

|동적 속성 이름|Description|
|---------------------------|-----------------|
|**DFMode**|DataFactory 모드를 나타냅니다. 원하는 버전을 지정 하는 문자열은 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 서버 개체입니다. 특정 버전의 요청에 대 한 연결을 열기 전에이 속성을 설정 합니다.는 **DataFactory**합니다. 요청 된 버전에 사용할 수 없는 경우 이전 버전을 사용 하는 시도가 수행 됩니다. 이전 버전이 없는 경우 오류가 발생 합니다. 경우 **DFMode** 가 사용할 수 있는 버전 보다 작은 오류가 발생 합니다. 연결 된 후이 속성은 읽기 전용입니다.<br /><br /> 다음 유효한 문자열 값 중 하나일 수 있습니다.<br /><br /> -"25"-버전 2.5 (기본값)<br />-"21"-버전 2.1<br />-"20"-버전 2.0<br />-"15"-버전 1.5|
|**명령 속성**|MS 원격 공급자가 서버에 전송 되는 명령 (행 집합) 속성의 문자열에 추가 될 값을 나타냅니다. 이 문자열에 대 한 기본값은 vt_empty 합니다.|
|**현재 DFMode**|실제 버전 수를 나타내는 **DataFactory** 서버에 있습니다. 버전에서 요청 된 경우를 확인 하려면이 속성을 확인는 **DFMode** 속성 적용 합니다.<br /><br /> 다음과 같은 올바른 정수 (Long) 값 중 하나일 수 있습니다.<br /><br /> -25-버전 2.5 (기본값)<br />-21-버전 2.1<br />-20-버전 2.0<br />-15-버전 1.5<br /><br /> 추가 "DFMode = 20;" 연결 문자열을 사용 하는 경우에 **MSRemote** 데이터를 업데이트할 때 공급자 서버 성능이 향상 시킬 수 있습니다. 이 설정을 통해는 **업데이트할** 많이 모드를 사용 하는 서버에서 개체입니다. 그러나 다음과 같은 기능을이 구성에서 사용할 수 없습니다.<br /><br /> -매개 변수가 있는 쿼리를 사용 합니다.<br />-호출 하기 전에 매개 변수 또는 열 정보를 가져오는 **Execute** 메서드.<br />-설정 **업데이트 Transact** 를 **True**합니다.<br />-행 상태 가져오기<br />-호출는 **Resync** 메서드.<br />-새로 고침 (명시적으로 또는 자동으로)를 통해는 **업데이트 Resync** 속성입니다.<br />-설정 **명령** 또는 **레코드 집합** 속성입니다.<br />-를 사용 하 여 **adCmdTableDirect**합니다.|
|**Handler**|기능을 확장 하는 서버 쪽 사용자 지정 프로그램 (또는 처리기)의 이름을 나타냅니다는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), 및 매개 변수 처리기가 사용 되는 *,* 쉼표 (로 모두 분리 된 ","). A **문자열** 값입니다.|
|**인터넷 제한 시간**|서버에서 이동 하는 요청 될 때까지 기다리는 시간 (밀리초)의 최대 수를 나타냅니다. (기본값은 5 분입니다.)|
|**원격 공급자**|원격 서버에서 사용 가능 하도록 데이터 공급자의 이름을 나타냅니다.|
|**원격 서버**|이 연결에서 사용할 서버 이름 및 통신 프로토콜을 나타냅니다. 이 속성은 해당 하는 [.rds입니다 DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 [서버](../../../ado/reference/rds-api/server-property-rds.md) 속성입니다.|
|**Transact 업데이트**|로 설정 하면 **True**때가이 값을 나타냅니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 수행 서버에서 하나의 트랜잭션으로 완료 일 됩니다. 부울이 동적 속성에 대 한 기본값은 **False**합니다.|

 또한 연결 문자열에서 키워드로 이름을 지정 하 여 쓰기 가능한 동적 속성을 설정할 수 있습니다. 예를 들어 설정 된 **인터넷 제한 시간** 을 5 초로 지정 하 여 동적 속성:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 또한 설정 하거나 인덱스의 이름을 지정 하 여 동적 속성을 검색할 수 있습니다는 **속성** 속성입니다. 가져오고의 현재 값을 인쇄 하는 방법을 보여 주는 다음 예제는 **인터넷 제한 시간** 동적 속성을 선택한 다음 새 값을 설정 합니다.

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>주의
 2.0 ado, OLE DB 원격 서비스 공급자만에서 지정 될 수는 *ActiveConnection* 의 매개 변수는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **열려** 메서드. ADO 2.1 이상에서는 공급자도 지정할 수 있습니다에 *ConnectionString* 의 매개 변수는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 **열려** 메서드.

 해당 하는 **.rds입니다 DataControl** 개체 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성은 사용할 수 없습니다. [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **열려** 메서드 *소스* 인수 대신 사용 됩니다.

 **참고** "...; 지정 원격 공급자 = MS 원격;... "4 계층 시나리오를 만듭니다. 3 계층을 초과 하는 시나리오 테스트 하지 않은 및 필요 하지 않습니다.

## <a name="example"></a>예제
 쿼리를 수행 하는이 예제는 **작성자** 목차는 **Pubs** 이라는 서버에 데이터베이스 *해당 서버*합니다. 원격 데이터 원본 및 원격 서버 이름에 제공 됩니다는 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 의 메서드는[연결](../../../ado/reference/ado-api/connection-object-ado.md) 에 지정 된 개체 및 SQL 쿼리는[열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 의 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. A **레코드 집합** 개체 반환, 편집 및 데이터 소스를 업데이트 하는 데 사용 합니다.

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

## <a name="see-also"></a>관련 항목:
 [OLE DB Remoting 공급자 개요](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
