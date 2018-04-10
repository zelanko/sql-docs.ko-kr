---
title: SQL Server 프로그래밍에 대 한 OLE DB 드라이버 | Microsoft Docs
description: OLE DB Driver SQL Server 프로그래밍에 대 한
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fe6342e3a61ecc59594917431c026681e51f8e63
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server-programming"></a>SQL Server 프로그래밍에 대 한 OLE DB 드라이버
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server는 독립 실행형 데이터 액세스 응용 프로그래밍 인터페이스 (API) OLE DB에 도입 된에 사용 되는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다. OLE DB Driver for SQL Server는 하나의 동적 연결 라이브러리 (DLL)에 SQL OLE DB 드라이버를 제공합니다. 또한 Windows Data Access Components(Windows DAC, 이전의 Microsoft Data Access Components 또는 MDAC)에서 제공하는 것보다 뛰어난 새로운 기능을 제공합니다. OLE DB Driver for SQL Server를 사용 하 여 새 응용 프로그램을 만들거나에 도입 된 기능을 활용 하는 기존 응용 프로그램을 향상 시킬 수 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 여러 활성 결과 집합 (MARS), 사용자 정의 데이터 형식 (UDT), 쿼리 등 알림, 스냅샷 격리 및 XML 데이터 형식을 지원합니다.  
  
> [!NOTE]  
>  목록이 OLE DB Driver for SQL Server 용 OLE DB 드라이버를 Windows DAC 응용 프로그램을 업데이트 하기 전에 고려해 야 할 문제에 대 한 정보와 함께 SQL Server 및 Windows DAC 간의 차이점에 대 한 참조 [SQL에 대 한 OLE DB Driver로 응용 프로그램 업데이트 MDAC에서 서버](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.  
  
 OLE DB 핵심 서비스와 Windows DAC와 함께 제공 되는 OLE DB Driver for SQL Server 수 함께 사용할 수 있지만 이것이 요구 사항이 적용 않으며 아닙니다. 개별 응용 프로그램 (예: 연결 풀링이 필요한 경우)의 요구 사항에 따라 위해 핵심 서비스 사용할지 선택 합니다.  
  
 ActiveX 데이터 개체 (ADO) 응용 프로그램에서는 SQL Server 용 OLE DB 드라이버를 사용할 수 있지만와 함께에서 ADO를 사용 하는 것이 좋습니다.는 **DataTypeCompatibility** 연결 문자열 키워드 (또는 해당  **데이터 원본** 속성). ADO 응용 프로그램에 도입 된 새로운 기능을 이용할 수 있습니다 OLE DB Driver for SQL Server를 사용할 때 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 는 제공 되는 OLE DB Driver for SQL Server를 통해 연결 문자열 키워드 또는 OLE DB 속성 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. ADO와 이러한 기능 사용에 대 한 자세한 내용은 참조 [OLE DB Driver for SQL Server를 사용 하 여 ADO를 사용 하 여](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)합니다.  
  
 OLE DB Driver for SQL Server OLE DB를 사용 하 여 SQL Server에 네이티브 데이터에 액세스 하는 간단한 방법을 제공 하도록 설계 되었습니다. 혁신적이 고 새 데이터 액세스 기능을 이제는 Microsoft Windows 플랫폼의 일부인는 현재 Windows DAC 구성 요소를 변경 하지 않고 발전 하는 방법을 제공 합니다.  
  
 Windows DAC의 구성 요소를 사용 하는 OLE DB Driver for SQL Server, 것은 불가능 명시적으로 Windows DAC의 특정 버전에 따라 다릅니다. SQL Server 용 OLE DB 드라이버에서 지 원하는 모든 운영 체제에서 설치 된 Windows DAC의 버전과 SQL Server 용 OLE DB 드라이버를 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server용 OLE DB 드라이버](../oledb/oledb-driver-for-sql-server.md)  
 중요 한 새 OLE DB 드라이버를 SQL Server 기능을 나열합니다.  
  
 [SQL Server용 OLE DB 드라이버를 사용해야 하는 경우](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 OLE DB Driver for SQL Server 적용 되는 방식으로 Microsoft 데이터 액세스 기술에 설명 Windows DAC 및 ADO.NET, 비교 하는 방법을 결정 하기 위한 데이터 액세스 기술을 사용 하는 팁을 제공 합니다.  
  
 [SQL Server 기능용 OLE DB 드라이버](../oledb/features/oledb-driver-for-sql-server-features.md )  
 SQL Server 용 OLE DB 드라이버에서 지 원하는 기능에 설명 합니다.  
  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 가 Windows DAC를 사용 하는 구성 요소와 다른 방법 및 ADO는 함께 사용할 수 있습니다 하는 방법을 포함 하는 SQL Server 개발에 대 한 OLE DB Driver에 대 한 개요를 제공 합니다.  
  
 이 섹션도 SQL Server 설치 및 배포 시는 OLE DB Driver for SQL Server 라이브러리를 재배포 하는 방법을 비롯 하 여 OLE DB Driver를 설명 합니다.  
  
 [SQL Server용 OLE DB 드라이버의 시스템 요구 사항](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 SQL Server 용 OLE DB 드라이버를 사용 하는 데 필요한 시스템 리소스에 설명 합니다.  
  
 [OLE DB Driver for SQL Server &#40;OLE DB&#41;](../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
 SQL Server 용 OLE DB 드라이버를 사용 하는 방법에 대 한 정보를 제공 합니다.  
  
 [SQL Server 정보에 대한 더 많은 OLE DB 드라이버 찾기](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 추가 도움말 및 외부 리소스에 대 한 링크를 포함 하 여 SQL Server 용 OLE DB 드라이버에 대 한 추가 리소스를 제공 합니다.  
  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 방법 도움말 항목](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
