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
manager: craigg
ms.openlocfilehash: 790f19d136470458620e0c00de00885e079256bf
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744603"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에 대한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 SQL Server에 OLE DB 드라이버를 사용 하 여 다양 한 데이터 액세스 구성 요소를 사용할 수 있습니다.  

## <a name="server-support"></a>서버 지원  
 OLE DB Driver for SQL Server 연결을 지원 합니다 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]를 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]를 [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]합니다.

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에서 SQL Server는 운영 체제 지원은 OLE DB 드라이버를 나열합니다.  

|지원되는 운영 체제|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1 + [2014 년 4 월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 이상 [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [2014 년 4 월 업데이트](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 애플리케이션에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

 ADO 응용 프로그램에 대 한 SQL Server, OLE DB 드라이버를 사용할 수 있지만 그렇게 하는 경우 지정 해야 합니다 `DataTypeCompatibility=80` 연결 문자열에 있습니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
애플리케이션은 Windows 운영 체제에 포함된 OLE DB 공급자(SQLOLEDB)를 사용할 수 있습니다. 그러나 유지 관리 모드에 하 고 더 이상 업데이트 합니다. OLE DB 드라이버 SQL Server (MSOLEDBSQL)에 대 한을 대신 사용 합니다.

## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
