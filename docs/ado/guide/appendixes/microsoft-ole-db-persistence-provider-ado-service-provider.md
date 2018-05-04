---
title: Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c47487547153426b2826792c5af0ad3bbeb7371
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 지 속성 공급자 개요
Microsoft OLE DB 지 속성 공급자를 사용 하면 저장 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 파일에 개체를 나중에 복원 하는 **레코드 집합** 파일에서 개체입니다. 스키마 정보, 데이터를 하 고 보류 중인 변경 내용이 보존 됩니다.

 저장할 수는 **레코드 집합** 전용 고급 데이터 테이블 그램 (ADTG) 형식 또는 열기 Extensible Markup Language (XML) 형식입니다.

## <a name="provider-keyword"></a>Provider 키워드
 이 공급자를 호출 하려면 연결 문자열에는 다음 키워드와 값을 지정 합니다.

```
"Provider=MSPersist"
```

## <a name="errors"></a>오류
 응용 프로그램에서이 공급자가 발급 한 다음 오류를 검색할 수 있습니다.

|상수|Description|
|--------------|-----------------|
|E_BADSTREAM|열려 있는 파일에는 올바른 형식 (즉, 형식이 ADTG 또는 XML).|
|E_CANTPERSISTROWSET|**레코드 집합** 저장 하는 개체에 저장 하지 못하게 하는 특성입니다.|

## <a name="remarks"></a>주의
 Microsoft OLE DB 지 속성 공급자는 동적 속성이 노출합니다.

 현재만 매개 변수화 계층적 **레코드 집합** 개체를 저장할 수 없습니다.

 영구적으로 저장 하는 방법에 대 한 자세한 내용은 **레코드 집합** 개체 참조 [지 속성 레코드 집합](../../../ado/guide/data/more-about-recordset-persistence.md)합니다.

 열려는 스트림을 사용 되는 경우는 **레코드 집합** 이외의 지정 하는 매개 변수 없이 있어야는 *소스* 의 매개 변수는 **열고** 메서드.

## <a name="see-also"></a>관련 항목:
[Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
