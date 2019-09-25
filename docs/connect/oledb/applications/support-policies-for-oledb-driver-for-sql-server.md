---
title: SQL Server용 OLE DB 드라이버 지원 정책 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에 대한 지원 정책
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1ae0e332de1d1e673cfd4fff1e288acafa4a0619
ms.sourcegitcommit: b016c01c47bc08351d093a59448d895cc170f8c3
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71118149"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에 대한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 다양 한 데이터 액세스 구성 요소를 SQL Server에 대 한 OLE DB 드라이버와 함께 사용 하는 방법을 설명 합니다.  

## <a name="server-support"></a>서버 지원  
 OLE DB Driver [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]for SQL Server [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]는, [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)],, 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]에 대 한 연결을 지원 합니다.

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에는 SQL Server에 대 한 OLE DB 드라이버를 지 원하는 운영 체제가 나와 있습니다.  

| 지원되는 운영 체제 |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [4 월 2014 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [k b 2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 이상 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [4 월 2014 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [k b 2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 애플리케이션에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

 ADO 응용 프로그램은 SQL Server에 OLE DB 드라이버를 사용할 수 있지만 이렇게 하려면 연결 문자열에을 `DataTypeCompatibility=80` 지정 해야 합니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
애플리케이션은 Windows 운영 체제에 포함된 OLE DB 공급자(SQLOLEDB)를 사용할 수 있습니다. 그러나이는 유지 관리 모드 이며 더 이상 업데이트 되지 않습니다. 대신 OLE DB Driver for SQL Server (MSOLEDBSQL)를 사용 합니다.

## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
