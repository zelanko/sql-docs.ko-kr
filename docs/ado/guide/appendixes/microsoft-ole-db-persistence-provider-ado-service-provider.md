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
author: rothja
ms.author: jroth
ms.openlocfilehash: cc8c8f099e703433f57e9d8ff463e229213503be
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758469"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 지 속성 공급자 개요
Microsoft OLE DB 지 속성 공급자를 사용 하면 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 파일에 저장 하 고 나중에 파일에서 해당 **레코드 집합** 개체를 복원할 수 있습니다. 스키마 정보, 데이터 및 보류 중인 변경 내용이 유지 됩니다.

 ADTG (소유 고급 데이터 테이블) 형식 또는 open XML(Extensible Markup Language) (XML) 형식으로 **레코드 집합** 을 저장할 수 있습니다.

## <a name="provider-keyword"></a>Provider 키워드
 이 공급자를 호출 하려면 연결 문자열에 다음 키워드 및 값을 지정 합니다.

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>오류
 이 공급자가 발급 한 다음 오류는 응용 프로그램에서 검색할 수 있습니다.

|상수|설명|
|--------------|-----------------|
|E_BADSTREAM|열린 파일의 형식이 잘못 되었습니다 (즉, ADTG 또는 XML 형식이 아님).|
|E_CANTPERSISTROWSET|저장 된 **레코드 집합** 개체에는 저장 되지 않도록 하는 특징이 있습니다.|

## <a name="remarks"></a>설명
 Microsoft OLE DB 지 속성 공급자는 동적 속성을 노출 하지 않습니다.

 현재 매개 변수가 있는 계층적 **레코드 집합** 개체만 저장할 수 있습니다.

 **레코드 집합** 개체를 영구적으로 저장 하는 방법은 [레코드 집합 지 속성](../../../ado/guide/data/more-about-recordset-persistence.md)을 참조 하세요.

 스트림을 사용 하 여 **레코드 집합** 을 열 때 **open** 메서드의 *Source* 매개 변수 이외의 매개 변수를 지정 하지 않아야 합니다.

## <a name="see-also"></a>참고 항목
[Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
