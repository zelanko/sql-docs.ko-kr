---
title: SQL Server용 OLE DB 드라이버에 대한 지원 정책
description: OLE DB Driver for SQL Server에 대한 지원 정책과 각 드라이버 버전에서 지원되는 운영 체제 및 SQL 데이터베이스 버전에 대해 알아봅니다.
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa01dec4758bb91a4b05d65af372ee66c1c53672
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506424"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에 대한 지원 정책
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

이 문서에서는 OLE DB Driver for SQL Server와 함께 여러 데이터 액세스 구성 요소를 사용하는 방법에 대해 설명합니다.  

## <a name="sql-version-support"></a>SQL 버전 지원  

OLE DB Driver for SQL Server는 다음 버전의 SQL Server에 대한 연결이 테스트되었으며 이를 지원합니다.

| 데이터베이스 버전&nbsp;&#8594;<br />&#8595; 드라이버 버전 | Azure SQL Database | Azure Synapse Analytics | Azure SQL Managed Instance | SQL Server 2019 | SQL Server 2017 | SQL Server 2016 | SQL Server 2014 | SQL Server 2012 |
|----|---|---|---|---|---|---|---|---|
|18.5|예|예|예|예|예|예|예|예|
|18.4|예|예|예|예|예|예|예|예|
|18.3|예|예|예|예|예|예|예|예|
|18.2|예|예|예|예|예|예|예|예|
|18.1|예|예|예|   |예|예|예|예|
|18.0|예|예|예|   |예|예|예|예|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  

다음 표에서는 OLE DB Driver for SQL Server에서 지원하는 운영 체제를 보여 줍니다.  

| 운영 체제&nbsp;&#8594;<br />&#8595; 드라이버 버전 | Windows Server 2019 | Windows Server 2016 | Windows Server 2012<sup>1</sup> | Windows Server 2012 R2<sup>2</sup> | 윈도우 10 | Windows 8.1<sup>3</sup> |
|----|---|---|---|---|---|---|
|18.5|예|예|예|예|예|예|
|18.4|예|예|예|예|예|예|
|18.3|예|예|예|예|예|예|
|18.2|예|예|예|예|예|예|
|18.1|   |예|예|예|예|예|
|18.0|   |예|예|예|예|예|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)이 적용된 Windows Server 2012에서 지원됩니다.  
<sup>2</sup> [2014년 4월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) 및 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)이 적용된 Windows Server 2012 R2에서 지원됩니다.  
<sup>3</sup> [2014년 4월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) 및 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)이 적용된 Windows 8.1에서 지원됩니다.  

## <a name="ado-support-policies"></a>ADO 지원 정책  

ADO 애플리케이션에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

ADO 애플리케이션에서는 OLE DB Driver for SQL Server를 사용할 수 있으나 그렇게 할 경우 연결 문자열에서 `DataTypeCompatibility=80`을 지정해야 합니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  

애플리케이션은 Windows 운영 체제에 포함된 OLE DB 공급자(SQLOLEDB)를 사용할 수 있습니다. 그러나 이는 유지 관리 모드이며 더 이상 업데이트되지 않습니다. 대신 OLE DB Driver for SQL Server(MSOLEDBSQL)를 사용하세요.

## <a name="see-also"></a>참고 항목  

[SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)
