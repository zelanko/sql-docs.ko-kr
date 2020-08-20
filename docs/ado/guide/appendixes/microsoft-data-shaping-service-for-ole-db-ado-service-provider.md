---
description: OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자)
title: OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c61e40220b99bd68c92e2651d58ea13ee10be29
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454105"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>OLE DB에 대 한 Microsoft 데이터 셰이핑 서비스 개요
> [!IMPORTANT]
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 응용 프로그램은 XML을 사용 해야 합니다.

 OLE DB 서비스 공급자를 위한 Microsoft 데이터 셰이핑 서비스는 데이터 공급자 로부터 계층적 (셰이프) [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 생성 하는 것을 지원 합니다.

## <a name="provider-keyword"></a>Provider 키워드
 OLE DB에 대 한 데이터 셰이핑 서비스를 호출 하려면 연결 문자열에 다음 키워드 및 값을 지정 합니다.

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자를 호출 하면[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [properties](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 다음과 같은 동적 속성이 추가 됩니다.

|동적 속성 이름|설명|
|---------------------------|-----------------|
|**고유한 이름 변경**|**변경 된 이름** 속성 값이 중복 되는 **레코드 집합** 개체가 허용 되는지 여부를 나타냅니다. 이 동적 속성이 **True** 이 고 새 레코드 **집합이** 기존 **레코드 집합과**동일한 사용자 지정 된 이름을 사용 하 여 만들어진 경우에는 새 **레코드 집합** 개체의 변형 된 이름이 고유 하 게 변경 됩니다. 이 속성이 **False** 이 고 기존 **레코드 집합과**동일한 사용자 지정 된 이름을 사용 하 여 새 **레코드 집합** 을 만든 경우에는 두 **레코드 집합** 개체의 모양 변경 이름이 동일 합니다. 따라서 두 레코드 집합 모두에 해당 하는 경우에는 **레코드 집합** 의 모양을 변경할 수 없습니다.<br /><br /> 속성의 기본값은 **False**입니다.|
|**Data Provider**|셰이프를 지정 하는 데 사용할 공급자의 이름을 나타냅니다. 공급자를 사용 하 여 행을 제공 하지 않을 경우에는이 값을 사용할 수 없습니다.|

 연결 문자열에서 해당 이름을 키워드로 지정 하 여 쓰기 가능한 동적 속성을 설정할 수도 있습니다. 예를 들어 Microsoft Visual Basic에서 다음을 지정 하 여 **Data Provider** 동적 속성을 "MSDASQL"로 설정 합니다.

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 또한 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 속성의 인덱스로 이름을 지정 하 여 동적 속성을 설정 하거나 검색할 수 있습니다. 예를 들어 다음 코드 예제에서는 **Data Provider** 동적 속성의 현재 값을 가져오고 인쇄 한 다음 cn 인 경우 새 값을 설정 합니다. DataProvider가 "MSDataShape" (연결 문자열을 통해 직접 또는 간접적으로)로 설정 되 고 연결이 열려 있지 않습니다.

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  **Data Provider**동적 속성은 열려 있지 않은 **연결** 개체에만 설정할 수 있습니다. 연결이 열리면 **Data Provider** 속성은 읽기 전용이 됩니다.

 데이터 셰이핑에 대 한 자세한 내용은 [데이터 셰이핑](../../../ado/guide/data/data-shaping-overview.md)을 참조 하세요.

## <a name="see-also"></a>참고 항목
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
