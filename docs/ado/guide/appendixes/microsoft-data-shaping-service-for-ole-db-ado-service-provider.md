---
title: Microsoft 데이터 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ddef2feab633627c9549b73787faa1d104d69c5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926817"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 데이터 셰이핑 서비스에 대 한 OLE DB 개요
> [!IMPORTANT]
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, 응용 프로그램 XML을 사용 해야 합니다.

 OLE DB 서비스 공급자에 대 한 Microsoft Data Shaping Service 계층의 생성을 지원 (모양) [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 데이터 공급자 개체입니다.

## <a name="provider-keyword"></a>공급자 키워드
 OLE db Data Shaping Service를 호출 하려면 연결 문자열에 다음 키워드와 값을 지정 합니다.

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자가 호출 된 다음 동적 속성에 추가 됩니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션을[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.

|동적 속성 이름|설명|
|---------------------------|-----------------|
|**이름을 고유한 모양 변경**|나타냅니다 여부를 **레코드 집합** 개체에 대 한 중복 값을 사용 하 여 해당 **변형 이름** 속성은 허용 합니다. 이 동적 속성이 **True** 새 **레코드 집합** 기존와 동일한 모양 사용자 지정 이름을 사용 하 여 만들어집니다 **레코드 집합**를 클릭 하 고 새  **레코드 집합** 개체의 모양 변경 이름을 고유 하 게 수정 합니다. 이 속성이 **False** 새 **Recordset** 기존와 동일한 모양 사용자 지정 이름을 사용 하 여 만들어집니다 **레코드 집합**모두 **레코드 집합**  개체 이름이 모양 변경 해야 합니다. 따라서 어느 **레코드 집합** 레코드 집합이 모두 존재와 모양을 변경할 수 있습니다.<br /><br /> 속성의 기본값은 **False**합니다.|
|**데이터 공급자**|셰이핑 되어야 하는 행을 제공 하는 공급자의 이름을 나타냅니다. 행을 제공 하는 공급자를 사용할 수는 경우이 값은 NONE 수 있습니다.|

 또한 연결 문자열에는 키워드와 해당 이름을 지정 하 여 쓰기 가능한 동적 속성을 설정할 수 있습니다. 예를 들어 Microsoft Visual Basic에서 설정 된 **데이터 공급자** "MSDASQL"를 지정 하 여 동적 속성:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 설정 하거나 인덱스 이름을 지정 하 여 동적 속성을 검색할 수도 있습니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 속성입니다. 예를 들어, 다음 코드 예제를 가져오고 현재 값을 인쇄 합니다 **데이터 공급자** 동적 속성에는 다음 새 값을를 설정 하는 경우 cn입니다. DataProvider "MSDataShape"로 설정 되었습니다 (직접 또는 간접적으로 연결 문자열을 통해) 및 연결이 열려 있지 않습니다.

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  동적 속성 **Data Provider**, 열려 있지 않은에 설정 될 수 있습니다 **연결** 개체입니다. 연결이 열리면 합니다 **데이터 공급자** 속성이 읽기 전용이 됩니다.

 데이터 모양 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [데이터 셰이핑](../../../ado/guide/data/data-shaping-overview.md)합니다.

## <a name="see-also"></a>관련 항목
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
