---
title: SQL Server 용 OLE DB 드라이버에 대 한 지원 정책 | Microsoft Docs
description: OLE DB Driver for SQL Server에 대 한 지원 정책
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 374660fdba66e5c445ae441d988a3701de548427
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server에 대 한 지원 정책
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 문서에서는 다양 한 데이터 액세스 구성 요소가 사용 하 여 OLE DB Driver for SQL Server에 설명 합니다.  

## <a name="server-support"></a>서버 지원  
 OLE DB Driver for SQL Server 연결을 지원 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], 및 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]합니다.

## <a name="supported-operating-system-versions"></a>지원되는 운영 체제 버전  
 다음 표에서 지 원하는 운영 체제 OLE DB Driver for SQL Server를 나열합니다.  

|지원되는 운영 체제|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 지원 정책  
 ADO 응용 프로그램에서는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 기능이 필요하지 않은 경우 Windows에 포함된 SQLOLEDB OLE DB 공급자를 사용할 수 있습니다.  

 ADO 응용 프로그램에서는 SQL Server 용 OLE DB 드라이버를 사용할 수 있지만 그럴 경우를 지정 해야 `DataTypeCompatibility=80` 연결 문자열에 있습니다. 연결 문자열에 `DataTypeCompatibility=80`이 있으면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]의 기능만 사용할 수 있습니다.  

## <a name="ole-db-support-policies"></a>OLE DB 지원 정책  
응용 프로그램은 Windows 운영 체제에 포함 된 OLE DB 공급자 (SQLOLEDB)를 사용할 수 있습니다. 그러나 유지 관리 모드에 하 고 더 이상 업데이트 합니다. 대신 사용 해야 OLE DB Driver SQL Server (MSOLEDBSQL)에 대 한 합니다.

## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
