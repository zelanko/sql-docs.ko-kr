---
title: "Microsoft 데이터를 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3510664e97b64c36b7c1c7b42ca475194b6d01e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft 데이터를 셰이핑 OLE DB 개요에 대 한 서비스
> [!IMPORTANT]
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신, 응용 프로그램 XML을 사용 해야 합니다.

 OLE DB 서비스 공급자에 대 한 Microsoft Data Shaping Service 계층적의 생성을 지원 (모양) [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 는 데이터 공급자에서 개체입니다.

## <a name="provider-keyword"></a>Provider 키워드
 OLE db Data Shaping Service를 호출 하려면 연결 문자열에는 다음 키워드와 값을 지정 합니다.

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>동적 속성
 이 서비스 공급자가 호출 되는 다음과 같은 동적 속성에 추가 됩니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션은[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.

|동적 속성 이름|Description|
|---------------------------|-----------------|
|**모양 변경 고유 이름**|나타냅니다 있는지 여부를 **레코드 집합** 개체에 대 한 중복 값을 해당 **Name 모양 변경** 속성을 사용할 수 있습니다. 이 동적 속성이 **True** 와 새 **레코드 집합** 기존와 같은 모양 사용자 지정 이름을 사용 하 여 만들어집니다 **레코드 집합**, 다음 새 ** 레코드 집합** 개체의 모양 변경 이름을 고유 하 게 수정 합니다. 이 속성이 **False** 와 새 **레코드 집합** 기존와 같은 모양 사용자 지정 이름을 사용 하 여 만들어집니다 **레코드 집합**모두 **레코드 집합 ** 개체 동일한 모양 변경 이름을 갖습니다. 따라서 둘 다 **레코드 집합** 레코드 집합이 모두 존재으로 바꿀 수 있습니다.<br /><br /> 속성의 기본값은 **False**합니다.|
|**데이터 공급자**|행 모양이을 제공 하는 공급자의 이름을 나타냅니다. 행을 제공 하는 공급자를 사용할 수는 경우이 값은 NONE 수 있습니다.|

 또한 연결 문자열에서 키워드로 이름을 지정 하 여 쓰기 가능한 동적 속성을 설정할 수 있습니다. 예를 들어 Microsoft Visual Basic에서 설정 된 **데이터 공급자** 지정 하 여 동적 속성을 "MSDASQL":

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 설정 하거나 인덱스의 이름을 지정 하 여 동적 속성을 검색할 수도 있습니다는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 속성입니다. 예를 들어 다음 코드 예제를 가져오고의 현재 값을 출력에서 **데이터 공급자** 동적 속성에는 다음 새 값을를 설정 하는 경우 cn 합니다. DataProvider "MSDataShape"로 설정 된 (직접 또는 간접적으로 연결 문자열을 통해) 및 연결이 열리지 않았습니다.

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  동적 속성 **데이터 공급자**, 열려 있지 않은에 설정 될 수 있습니다 **연결** 개체입니다. 연결이 열리면는 **데이터 공급자** 속성은 읽기 전용 상태가 됩니다.

 데이터 모양 지정에 대 한 자세한 내용은 참조 [데이터 셰이핑](../../../ado/guide/data/data-shaping-overview.md)합니다.

## <a name="see-also"></a>관련 항목:
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)

