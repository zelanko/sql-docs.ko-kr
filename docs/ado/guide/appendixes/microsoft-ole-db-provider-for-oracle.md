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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926629"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle 개요
> [!IMPORTANT]
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. Oracle OLE DB 공급자를 대신 사용 합니다.

 Microsoft OLE DB Provider for Oracle에는 ADO를 Oracle 데이터베이스에 액세스할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결을 설정 합니다 *공급자* 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```vb
MSDAORA
```

 읽기를 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 이 문자열로 반환 됩니다.

 Keyset 또는 dynamic 커서를 사용 하 여 조인 쿼리는 Oracle 데이터베이스에서 실행 하는 경우 오류가 발생 했습니다. Oracle 정적 읽기 전용 커서를 지원합니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|OLE DB Provider for Oracle 지정합니다.|
|**데이터 원본**|서버의 이름을 지정합니다.|
|**사용자 ID**|사용자 이름을 지정합니다.|
|**암호**|사용자 암호를 지정 합니다.|

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

## <a name="provider-specific-connection-parameters"></a>공급자별 연결 매개 변수
 공급자는 ADO를 정의한 것 외에도 여러 공급자별 연결 매개 변수를 지원 합니다. 으로 ADO 연결 속성을 이러한 공급자별 속성을 통해 설정할 수 있습니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 의 일부로 **ConnectionString**.

 이러한 매개 변수는에 자세히 설명 합니다 [OLE DB Programmer's Reference](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)합니다. 합니다 [ADO 동적 속성 인덱스](../../../ado/reference/ado-api/ado-dynamic-property-index.md) 이러한 매개 변수 이름과 해당 OLE DB 속성 간의 상호 참조를 제공 합니다.

|매개 변수|설명|
|---------------|-----------------|
|**창 핸들**|창 핸들을 사용 하 여 추가 정보를 묻는 메시지를 나타냅니다.|
|**로캘 ID**|(예: 1033) 사용자의 언어와 관련 된 기본 설정을 지정 하는 고유한 32 비트 숫자를 나타냅니다. 이러한 기본 설정을 나타내는 날짜 및 시간 형식 지정 방법을, 문자열 비교 되 고, 항목이 사전순으로 정렬 됩니다.|
|**OLE DB 서비스**|OLE DB 서비스를 사용 하거나 사용 하지 않도록 지정 하는 비트 마스크를 나타냅니다.|
|**프롬프트**|사용자에 게 프롬프트는 연결이 설정 되는 동안 여부를 나타냅니다.|
|**확장된 속성**|공급자별 확장된 연결 정보를 포함 하는 문자열입니다. 속성 메커니즘을 통해 설명할 수 없는 공급자 특정 연결 정보에 대해서만이 속성을 사용 합니다.|

## <a name="see-also"></a>관련 항목
 [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Provider 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
