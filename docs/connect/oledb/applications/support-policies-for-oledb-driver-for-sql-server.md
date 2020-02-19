---
title: SQL Server용 OLE DB 드라이버 지원 정책 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에 대한 지원 정책
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381855"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에 대한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 OLE DB Driver for SQL Server와 함께 여러 데이터 액세스 구성 요소를 사용하는 방법에 대해 설명합니다.  

## <a name="server-support"></a>서버 지원  
 OLE DB Driver for SQL Server는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]를 통해 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 대한 연결을 지원합니다.

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에서는 OLE DB Driver for SQL Server를 지원하는 운영 체제를 보여 줍니다.  

| 지원되는 운영 체제 |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [2014년 4월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 이상 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [2014년 4월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 애플리케이션에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

 ADO 애플리케이션에서는 OLE DB Driver for SQL Server를 사용할 수 있으나 그렇게 할 경우 연결 문자열에서 `DataTypeCompatibility=80`을 지정해야 합니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
애플리케이션은 Windows 운영 체제에 포함된 OLE DB 공급자(SQLOLEDB)를 사용할 수 있습니다. 그러나 이는 유지 관리 모드이며 더 이상 업데이트되지 않습니다. 대신 OLE DB Driver for SQL Server(MSOLEDBSQL)를 사용하세요.

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
