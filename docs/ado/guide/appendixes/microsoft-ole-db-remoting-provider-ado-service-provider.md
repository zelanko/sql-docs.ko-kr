---
title: Microsoft OLE DB Remoting 공급자 (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c60567da677564c168f0601625686bdfb8b3d67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926595"
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB Remoting 공급자 개요
Microsoft OLE DB Remoting 공급자는 클라이언트 컴퓨터의 로컬 사용자가 원격 컴퓨터에서 데이터 공급자를 호출할 수 있도록 합니다. 원격 컴퓨터의 로컬 사용자 인 경우와 같이 원격 컴퓨터에 대 한 데이터 공급자 매개 변수를 지정 합니다. 원격 컴퓨터에 액세스 하기 위해 원격 공급자에서 사용 하는 매개 변수를 지정 합니다. 그런 다음 로컬 사용자 인 것 처럼 원격 컴퓨터에 액세스할 수 있습니다.

> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.

## <a name="provider-keyword"></a>Provider 키워드
 OLE DB Remoting 공급자를 호출 하려면 연결 문자열에 다음 키워드 및 값을 지정 합니다. 공급자 이름의 빈 공간을 확인 합니다.

```vb
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>추가 키워드
 이 서비스 공급자를 호출 하면 다음과 같은 추가 키워드가 관련 됩니다.

|키워드|설명|
|-------------|-----------------|
|**데이터 원본**|원격 데이터 원본의 이름을 지정 합니다. 처리를 위해 OLE DB 원격 공급자로 전달 됩니다.<br /><br /> 이 키워드는 RDS와 동일 합니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.|

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자를 호출 하면 다음과 같은 동적 속성이 [Connection](../../../ado/reference/ado-api/connection-object-ado.md)개체의 [properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 추가 됩니다.

|동적 속성 이름|설명|
|---------------------------|-----------------|
|**DFMode**|DataFactory 모드를 나타냅니다. 서버에서 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체의 원하는 버전을 지정 하는 문자열입니다. 특정 버전의 **DataFactory**를 요청 하려면 연결을 열기 전에이 속성을 설정 합니다. 요청 된 버전을 사용할 수 없는 경우 이전 버전을 사용 하려고 시도 합니다. 이전 버전이 없는 경우 오류가 발생 합니다. **DFMode** 가 사용 가능한 버전 보다 작은 경우 오류가 발생 합니다. 연결이 설정 된 후에는이 속성이 읽기 전용입니다.<br /><br /> 다음 유효한 문자열 값 중 하나일 수 있습니다.<br /><br /> -"25"-버전 2.5 (기본값)<br />-"21"-버전 2.1<br />-"20"-버전 2.0<br />-"15"-버전 1.5|
|**명령 속성**|MS 원격 공급자에 의해 서버에 전송 되는 명령 (행 집합) 속성의 문자열에 추가 되는 값을 나타냅니다. 이 문자열의 기본값은 vt_empty입니다.|
|**현재 DFMode**|서버에 있는 **DataFactory** 의 실제 버전 번호를 나타냅니다. **DFMode** 속성에서 요청 된 버전이 허용 되는지 확인 하려면이 속성을 확인 합니다.<br /><br /> 다음의 유효한 정수 (Long) 값 중 하나일 수 있습니다.<br /><br /> -25-버전 2.5 (기본값)<br />-21-버전 2.1<br />-20-버전 2.0<br />-15-버전 1.5<br /><br /> **Msremote** provider를 사용 하는 경우 연결 문자열에 "DFMode = 20;"을 추가 하면 데이터를 업데이트할 때 서버 성능이 향상 될 수 있습니다. 이 설정을 사용 하는 경우 서버의 **RDSServer DataFactory** 개체는 리소스를 많이 사용 하는 모드를 사용 합니다. 그러나이 구성에서는 다음과 같은 기능을 사용할 수 없습니다.<br /><br /> -매개 변수가 있는 쿼리 사용<br />- **Execute** 메서드를 호출 하기 전에 매개 변수 또는 열 정보를 가져옵니다.<br />- **Transact-sql 업데이트** 를 **True**로 설정 합니다.<br />-행 상태를 가져오는 중입니다.<br />- **Resync** 메서드를 호출 합니다.<br />- **업데이트 다시 동기화** 속성을 통해 (명시적 또는 자동으로) 새로 고침<br />- **명령** 또는 **레코드 집합** 속성을 설정 합니다.<br />- **AdCmdTableDirect**을 사용 합니다.|
|**Handler**|[RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)의 기능을 확장 하는 서버 쪽 사용자 지정 프로그램 (또는 처리기)의 이름과 처리기에서 사용 하는 모든 매개 변수를 쉼표 (",")로 구분 하 여 나타냅니다. **문자열** 값입니다.|
|**인터넷 제한 시간**|요청을 서버에서 이동할 때까지 대기할 최대 시간 (밀리초)을 나타냅니다. 기본값은 5 분입니다.|
|**원격 공급자**|원격 서버에서 사용할 데이터 공급자의 이름을 나타냅니다.|
|**원격 서버**|이 연결에서 사용할 서버 이름 및 통신 프로토콜을 나타냅니다. 이 속성은 RDS와 동일 합니다 [. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체 [서버](../../../ado/reference/rds-api/server-property-rds.md) 속성입니다.|
|**Transact-sql 업데이트**|**True**로 설정 된 경우이 값은 서버에서 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 가 수행 될 때 트랜잭션 내에서 수행 됨을 나타냅니다. 이 부울 동적 속성의 기본값은 **False**입니다.|

 연결 문자열에서 해당 이름을 키워드로 지정 하 여 쓰기 가능한 동적 속성을 설정할 수도 있습니다. 예를 들어 다음을 지정 하 여 **인터넷 제한 시간** 동적 속성을 5 초로 설정 합니다.

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 또한 **속성** 속성의 인덱스로 이름을 지정 하 여 동적 속성을 설정 하거나 검색할 수 있습니다. 다음 예제에서는 **인터넷 제한 시간** 동적 속성의 현재 값을 가져오고 인쇄 한 다음 새 값을 설정 하는 방법을 보여 줍니다.

```vb
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>설명
 ADO 2.0에서 OLE DB 원격 공급자는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 **Open** 메서드의 *ActiveConnection* 매개 변수에만 지정할 수 있습니다. ADO 2.1 부터는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 **Open** 메서드의 *ConnectionString* 매개 변수에 공급자를 지정할 수도 있습니다.

 RDS와 동일 합니다 **. DataControl** 개체 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 사용할 수 없습니다. [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 **Open** 메서드 *소스* 인수가 대신 사용 됩니다.

 **참고** "...;" 지정 원격 공급자 = MS Remote; ... " 4 계층 시나리오를 만듭니다. 3 계층 이상으로 이루어진 시나리오는 테스트 되지 않았으므로 필요 하지 않습니다.

## <a name="example"></a>예제
 이 예에서는 서버 라는 서버에서 **Pubs** 데이터베이스의 **Authors** 테이블에 대해 쿼리를 수행 *합니다.* 원격 데이터 원본 및 원격 서버의 이름은[Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [open](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드에서 제공 되며 SQL 쿼리는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의[open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드에서 지정 됩니다. **레코드 집합** 개체를 반환 하 고, 편집 하 고, 데이터 소스를 업데이트 하는 데 사용 합니다.

```vb
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=https://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>참고 항목
 [OLE DB 원격 공급자 개요](https://msdn.microsoft.com/4083b72f-68c4-4252-b366-abb70db5ca2b)
