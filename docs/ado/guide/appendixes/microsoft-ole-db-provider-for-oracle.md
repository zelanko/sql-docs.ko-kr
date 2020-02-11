---
title: Microsoft OLE DB Provider for Oracle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60510302525562d9c3007a6ef57213fc261b4c60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926629"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 개요
> [!IMPORTANT]
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle의 OLE DB 공급자를 사용 합니다.

 Microsoft OLE DB Provider for Oracle ADO를 사용 하 여 Oracle 데이터베이스에 액세스할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성의 *공급자* 인수를로 설정 합니다.

```vb
MSDAORA
```

 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성을 읽으면이 문자열도 반환 됩니다.

 Oracle 데이터베이스에서 키 집합 또는 동적 커서를 사용 하는 조인 쿼리를 실행 하는 경우 오류가 발생 합니다. Oracle은 정적 읽기 전용 커서만 지원 합니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|Oracle에 대 한 OLE DB 공급자를 지정 합니다.|
|**데이터 원본**|서버의 이름을 지정합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정 합니다.|

> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.

## <a name="provider-specific-connection-parameters"></a>공급자별 연결 매개 변수
 공급자는 ADO에 의해 정의 된 매개 변수 외에도 여러 공급자별 연결 매개 변수를 지원 합니다. ADO 연결 속성과 마찬가지로 이러한 공급자별 속성은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션을 통해 설정 하거나 **ConnectionString**의 일부로 설정할 수 있습니다.

 이러한 매개 변수는 [OLE DB 프로그래머 참조](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)에 자세히 설명 되어 있습니다. [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 는 이러한 매개 변수 이름과 해당 OLE DB 속성 간의 상호 참조를 제공 합니다.

|매개 변수|Description|
|---------------|-----------------|
|**창 핸들**|추가 정보를 확인 하는 데 사용할 창 핸들을 나타냅니다.|
|**로캘 식별자**|사용자 언어와 관련 된 기본 설정을 지정 하는 고유한 32 비트 숫자 (예: 1033)를 나타냅니다. 이러한 기본 설정은 날짜 및 시간 형식을 지정 하는 방법, 항목을 사전순으로 정렬 하 고 문자열을 비교 하는 등의 방법을 지정 합니다.|
|**OLE DB 서비스**|사용 하거나 사용 하지 않도록 설정할 OLE DB 서비스를 지정 하는 비트 마스크를 나타냅니다.|
|**prompt**|연결을 설정 하는 동안 사용자에 게 메시지를 표시할지 여부를 나타냅니다.|
|**확장 속성**|공급자별 확장 연결 정보를 포함 하는 문자열입니다. 속성 메커니즘을 통해 설명할 수 없는 공급자별 연결 정보에 대해서만이 속성을 사용 합니다.|

## <a name="see-also"></a>참고 항목
 [ConnectionString 속성 (ado)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [공급자 속성 (](../../../ado/reference/ado-api/provider-property-ado.md) Ado) [레코드 집합 개체 (ado)](../../../ado/reference/ado-api/recordset-object-ado.md)
