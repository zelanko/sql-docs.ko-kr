---
title: '부록 A: 공급자 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926976"
---
# <a name="appendix-a-data-and-service-providers"></a>부록 A: 데이터 및 서비스 공급자
이 섹션에서는 세 가지 종류의 공급자 인 데이터 공급자, 서비스 공급자 및 서비스 구성 요소를 다룹니다. 공급자는 데이터 및 서비스 제공 서비스를 제공 하는 두 가지 범주로 나뉩니다. *데이터 공급자* 는 자체 데이터를 소유 하 고 응용 프로그램에 테이블 형식으로 제공 합니다. *서비스 공급자* 는 데이터를 생성 및 사용 하 여 서비스를 캡슐화 하 고 ADO 응용 프로그램의 기능을 확대 합니다. 서비스 공급자는 다른 서비스 공급자나 구성 요소와 함께 작동 해야 하는 *서비스 구성 요소로*추가로 정의할 수도 있습니다.

## <a name="data-providers"></a>데이터 공급자
 ADO는 지정 된 공급자의 특정 기능에 관계 없이 여러 다른 데이터 공급자에 연결 하 고 동일한 프로그래밍 모델을 계속 표시할 수 있으므로 강력 하 고 유연 합니다.

 그러나 각 데이터 공급자는 고유 하기 때문에 응용 프로그램이 ADO와 상호 작용 하는 방식은 데이터 공급자에 의해 약간 달라 집니다. 차이점은 일반적으로 다음 세 가지 범주 중 하나에 속합니다.

-   [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성의 연결 매개 변수입니다.

-   [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 사용법입니다.

-   공급자별 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 동작입니다.

 현재 Microsoft에서 제공 하는 각 데이터 공급자에 대 한 세부 정보는 다음과 같습니다.

|영역|항목|
|----------|-----------|
|ODBC 데이터베이스|[ODBC용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 인덱싱 서비스|[Microsoft 인덱싱 서비스용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory Service|[Microsoft Active Directory 서비스용 microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 데이터베이스|[Microsoft Jet 용 OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[SQL Server용 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 데이터베이스|[Oracle용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|인터넷 게시|[인터넷 게시용 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|단순 데이터 원본|[Microsoft OLE DB 단순 공급자](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>공급자별 동적 속성
 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [명령](../../../ado/reference/ado-api/command-object-ado.md)및 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에는 공급자와 관련 된 동적 속성이 포함 됩니다. 이러한 속성은 ADO에서 지 원하는 기본 제공 속성 이외의 공급자 관련 기능에 대 한 정보를 제공 합니다.

 연결을 설정 하 고 이러한 개체를 만든 후에는 개체의 **properties** 컬렉션에서 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 사용 하 여 공급자별 속성을 가져옵니다. 이러한 동적 속성에 대 한 자세한 내용은 공급자 설명서 및 [OLE DB 프로그래머 가이드](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) 를 참조 하세요.

## <a name="service-providers"></a>서비스 공급자
 서비스 공급자를 사용 하려면 키워드를 제공 해야 합니다. 또한 각 서비스 공급자와 연결 된 공급자별 동적 속성에 대해 알고 있어야 합니다. 공급자별 세부 정보는 Microsoft에서 현재 사용할 수 있는 각 서비스 공급자에 대해 나열 됩니다.

-   [OLE DB의 Microsoft 데이터 셰이핑 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 지 속성 공급자](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Microsoft OLE DB Remoting 공급자](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>서비스 구성 요소
 OLE DB service 구성 요소 [에 대 한 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 는 데이터 공급자의 커서 지원 기능을 보완 합니다. 또한 키워드와 동적 속성이 있어야 합니다.

 OLE DB 공급자에 대 한 자세한 내용은 [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)를 참조 하세요.

## <a name="provider-commands"></a>공급자 명령
 여기에 나열 된 각 공급자에 대해 응용 프로그램이 사용자에 게 SQL 문을 공급자 명령으로 입력할 수 있도록 허용 하는 경우 항상 사용자 입력의 유효성을 검사 하 고 잠재적으로 `DROP TABLE t1`위험한 SQL 문 (예: 사용자 입력의 일부로)을 사용 하 여 가능한 해커 공격을 유의 해야 합니다.

## <a name="see-also"></a>참고 항목
 Microsoft Active Directory 서비스에 대 한 ado ( [Command Object](../../../ado/reference/ado-api/command-object-ado.md) [) 연결 개체 (](../../../ado/reference/ado-api/connection-object-ado.md) Ado) [Microsoft OLE DB provider For Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) microsoft [OLE DB provider for microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [OLE DB service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) for microsoft Microsoft OLE DB Provider for Oracle provider For microsoft [OLE DB provider for](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection (](../../../ado/reference/ado-api/properties-collection-ado.md) ado) [레코드 집합 개체 (ado) ado (ado)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh 메서드 (](../../../ado/reference/rds-api/refresh-method-rds.md) ado)
