---
title: SQL Server용 OLE DB 드라이버에 대한 지원 정책 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에 대한 지원 정책
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ac76aabc7ba96ec5c867d7cb623f81909c577c3d
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106129"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에 대한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 문서에서는 SQL Server에 OLE DB 드라이버를 사용 하 여 다양 한 데이터 액세스 구성 요소를 사용할 수 있습니다.  

## <a name="server-support"></a>서버 지원  
 OLE DB Driver for SQL Server 연결을 지원 합니다 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]를[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]를 [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]합니다.

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에서 SQL Server는 운영 체제 지원은 OLE DB 드라이버를 나열합니다.  

|지원되는 운영 체제|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 응용 프로그램에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

 ADO 응용 프로그램에 대 한 SQL Server, OLE DB 드라이버를 사용할 수 있지만 그렇게 하는 경우 지정 해야 합니다 `DataTypeCompatibility=80` 연결 문자열에 있습니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
응용 프로그램은 Windows 운영 체제에 포함된 OLE DB 공급자(SQLOLEDB)를 사용할 수 있습니다. 그러나 유지 관리 모드에 하 고 더 이상 업데이트 합니다. 대신 사용 해야 OLE DB 드라이버 SQL Server (MSOLEDBSQL)에 대 한 합니다.

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
