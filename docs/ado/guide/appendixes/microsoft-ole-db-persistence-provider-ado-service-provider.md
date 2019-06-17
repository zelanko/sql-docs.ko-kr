---
title: Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d1ae4f8cba9235700edf410904862d39ed4f7f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702999"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 지 속성 공급자 개요
Microsoft OLE DB 지 속성 공급자를 사용 하면 저장 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 파일에 개체를 나중에 복원 하는 **레코드 집합** 파일에서 개체입니다. 스키마 정보, 데이터, 보류 중인 변경 내용이 유지 됩니다.

 저장할 수 있습니다 합니다 **레코드 집합** 전용 고급 데이터 테이블 그램 (ADTG) 형식 또는 open Extensible Markup Language (XML) 형식입니다.

## <a name="provider-keyword"></a>공급자 키워드
 이 공급자를 호출 하려면 연결 문자열에 다음 키워드와 값을 지정 합니다.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>오류
 응용 프로그램에서이 공급자에서 발급 한 다음 오류를 검색할 수 있습니다.

|상수|Description|
|--------------|-----------------|
|E_BADSTREAM|열려 있는 파일에 올바른 형식이 없습니다 (즉, 형식이 ADTG 또는 XML).|
|E_CANTPERSISTROWSET|합니다 **레코드 집합** 저장 하는 개체에 저장 되는 것을 방지 하는 특징이 있습니다.|

## <a name="remarks"></a>Remarks
 Microsoft OLE DB 지 속성 공급자는 없는 동적 속성을 표시합니다.

 현재만 매개 변수화 계층적 **레코드 집합** 개체를 저장할 수 없습니다.

 영구적으로 저장 하는 방법에 대 한 자세한 내용은 **Recordset** 개체를 참조 하십시오 [레코드 집합 지 속성](../../../ado/guide/data/more-about-recordset-persistence.md)합니다.

 열려는 스트림에 사용 되는 경우를 **레코드 집합** 이외의 지정 하는 매개 변수가 없는 없어야 합니다 *원본* 의 매개 변수는 **엽니다** 메서드.

## <a name="see-also"></a>관련 항목
[Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
