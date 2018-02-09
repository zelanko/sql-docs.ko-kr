---
title: "부록 a: 공급자 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad762b73bd91ed92bf32a74587105a2be64e5192
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="appendix-a-data-and-service-providers"></a>부록 a: 데이터 및 서비스 공급자
이 섹션에서는 다음과 같은 세 가지 종류의 공급자: 데이터 공급자, 서비스 공급자 및 서비스 구성 요소입니다. 공급자 두 범주로 나누어집니다: 데이터 및 서비스를 제공 하는 것을 제공 하는 것입니다. A *데이터 공급자* 자체 데이터를 소유 하 고 응용 프로그램에 테이블 형식으로 제공 합니다. A *서비스 공급자* 생성 하 고 데이터를 확대 ADO 응용 프로그램의 기능을 사용 하 여 서비스를 캡슐화 합니다. 서비스 공급자 수 정의할 수도로 *서비스 구성 요소*는 다른 서비스 공급자 또는 구성 요소와 함께 작업 해야 합니다.

## <a name="data-providers"></a>데이터 공급자
 ADO는 여러 다른 데이터 공급자에 연결할 수 있고 지정된 된 공급자의 특정 기능에 관계 없이 동일한 프로그래밍 모델을 계속 제공 하기 때문에 강력 하 고 유연한 합니다.

 그러나 각 데이터 공급자가 고유 하므로 ADO와 응용 프로그램이 어떻게 조금씩 다릅니다 데이터 공급자가 있습니다. 차이 일반적으로 세 가지 범주 중 하나에 속합니다.

-   에 연결 매개 변수는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성입니다.

-   [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 사용 합니다.

-   공급자별 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 동작 합니다.

 각 Microsoft에서 현재 사용할 수 있는 데이터 공급자에 대 한 세부 정보는 다음과 같이 나열 됩니다.

|영역|항목|
|----------|-----------|
|ODBC 데이터베이스|[Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Microsoft 인덱싱 서비스|[Microsoft 인덱싱 서비스용 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Active Directory Service|[Microsoft Active Directory 서비스에 대 한 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet 데이터베이스|[Microsoft Jet 용 OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Oracle 데이터베이스|[Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|인터넷 게시|[인터넷 게시에 대 한 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|간단한 데이터 소스|[단순한 Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>공급자 관련 동적 속성
 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션의는 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [명령](../../../ado/reference/ado-api/command-object-ado.md), 및 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 관련 동적 속성을 포함 하는 개체는 공급자입니다. 이러한 속성에 ADO에서 지 원하는 기본 제공 속성 외에도 공급자 특정 기능에 대 한 정보를 제공 합니다.

 연결을 설정 하 고 이러한 개체를 만든를 사용 하 여는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 에서 메서드는 **속성** 공급자별 속성을 가져올 개체의 컬렉션입니다. 공급자 설명서를 참조 및 [OLE DB Programmer's Guide](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) 이러한 동적 속성에 대 한 자세한 내용은 합니다.

## <a name="service-providers"></a>서비스 공급자
 서비스 공급자를 사용 하려면 키워드를 제공 해야 합니다. 또한 각 서비스 공급자와 연결 된 공급자 특정 동적 속성에 주의 합니다. 공급자 관련 세부 정보는 Microsoft에서 현재 사용할 수 있는 각 서비스 공급자에 대해 나열 됩니다.

-   [OLE DB의 Microsoft 데이터 셰이핑 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Microsoft OLE DB 지 속성 공급자](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [원격 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>서비스 구성 요소
 [OLE DB에 대 한 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 서비스 구성 요소는 데이터 공급자의 커서 지원 기능을 보완 합니다. 또한 키워드 필요 하 고 동적 속성이 합니다.

 OLE DB 공급자에 대 한 자세한 내용은 참조 [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)합니다.

## <a name="provider-commands"></a>공급자 명령
 각 공급자에 대해 여기에 나열 된 응용 프로그램 공급자 명령으로 SQL 문을 입력할 수 있도록 하는 경우, 항상 사용자 입력의 유효성을 검사 하며 해커의 공격와 같은 잠재적으로 위험한 SQL 문을 사용 하 여 경계 해야 `DROP TABLE t1`, 사용자 입력의 일부로 합니다.

## <a name="see-also"></a>관련 항목:
 [개체 (ADO) 명령](../../../ado/reference/ado-api/command-object-ado.md) [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [인터넷 게시에 대 한 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [Microsoft Active Directory 용 Microsoft OLE DB Provider 서비스](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft 인덱싱 서비스용 Microsoft OLE DB Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [Microsoft OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh (RDS) 메서드](../../../ado/reference/rds-api/refresh-method-rds.md)
