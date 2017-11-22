---
title: Microsoft OLE DB Provider for Oracle | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5dc6f23b468637ee9de35644493f668341ad0e39
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 개요
> [!IMPORTANT]
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신, Oracle의 OLE DB 공급자를 사용 합니다.

 Microsoft OLE DB Provider for Oracle에는 ADO를 Oracle 데이터베이스에 액세스할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결할 설정는 *공급자* 의 인수는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성:

```
MSDAORA
```

 읽기는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성은이 문자열을 반환 합니다.

 키 집합 또는 동적 커서 조인 쿼리를 Oracle 데이터베이스에서 실행 오류가 발생 합니다. Oracle에는 정적 읽기 전용 커서를 지원합니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 이러한 키워드의 문자열 구성 됩니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|OLE DB Provider for Oracle 지정합니다.|
|**데이터 원본**|서버 이름을 지정합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정합니다.|

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 또는 **통합 보안 = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

## <a name="provider-specific-connection-parameters"></a>공급자 관련 연결 매개 변수
 공급자는 ADO에서 정의 된 권한과 함께 여러 공급자의 연결 매개 변수를 지원 합니다. ADO 연결 속성으로 이러한 공급자별 속성을 통해 설정할 있습니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 또는의 일부로 **ConnectionString**.

 이러한 매개 변수는에서 완벽 하 게 설명는 [OLE DB Programmer's Reference](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)합니다. [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 이러한 매개 변수 이름 및 해당 OLE DB 속성 간의 상호 참조를 제공 합니다.

|매개 변수|Description|
|---------------|-----------------|
|**창 핸들**|추가 정보에 대 한 메시지를 표시 하는 데 창 핸들을 나타냅니다.|
|**로캘 ID**|사용자의 언어와 관련 된 기본 설정을 지정 하는 (예: 1033)는 고유 32 비트 숫자를 나타냅니다. 이러한 기본 설정을 나타내는 날짜 및 시간 서식이 지정 되 방법을 항목이 사전순으로 정렬 되는 문자열을 비교 하 고, 합니다.|
|**OLE DB 서비스**|OLE DB 서비스를 사용 하거나 사용 하지 않도록 지정 하는 비트 마스크를 나타냅니다.|
|**메시지를 표시합니다**|연결이 설정 되는 동안 사용자에 게 확인 여부를 나타냅니다.|
|**확장된 속성**|공급자별 확장된 연결 정보를 포함 하는 문자열입니다. 속성 메커니즘을 통해 설명할 수 없는 공급자 특정 연결 정보에 대해서만이 속성을 사용 합니다.|

## <a name="see-also"></a>관련 항목:
 [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Provider 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [(ADO) 레코드 집합 개체](../../../ado/reference/ado-api/recordset-object-ado.md)
