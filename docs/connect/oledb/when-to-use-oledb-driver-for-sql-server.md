---
title: SQL Server 용 OLE DB 드라이버를 사용 하는 경우 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하는 경우
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b3fa8f071055f33bb256d3b28ed4aaa807f093a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32856238"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버를 사용 하는 경우
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 데이터에 액세스 하는 데 사용할 수 있는 하나의 기술은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  서로 다른 데이터 액세스 기술 논의 알려면 [데이터 액세스 기술 로드맵](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 SQL Server 용 OLE DB 드라이버를 사용 하 여 응용 프로그램의 데이터 액세스 기술로 것인지를 결정할 때는 여러 가지 요소를 고려해 야 합니다.  
  
 새 응용 프로그램의 경우 Microsoft Visual C# 또는 Visual Basic과 같은 관리되는 프로그래밍 언어를 사용하고 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스해야 한다면 .NET Framework의 일부인 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용해야 합니다.  
  
 에 도입 된 새로운 기능에 액세스 해야 하는 COM 기반 응용 프로그램을 개발 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL Server 용 OLE DB 드라이버를 사용 해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스할 필요가 없으면 WDAC(Windows Data Access Components)를 계속 사용할 수 있습니다.  
  
 기존 OLE DB 응용 프로그램의 경우 주된 문제는의 새로운 기능에 액세스 해야 하는지 여부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능이 필요 없는 완성된 응용 프로그램인 경우 계속 MDAC를 사용할 수 있습니다. 와 같은 새 기능에 액세스 해야 하는 경우는 [xml 데이터 형식](../../t-sql/xml/xml-transact-sql.md), SQL Server 용 OLE DB 드라이버를 사용 해야 합니다.  
  
 두 OLE DB Driver for SQL Server 및 MDAC 지원 커밋된 읽기 트랜잭션 격리 행 버전 관리만 OLE DB 드라이버를 사용 하 여 SQL Server 지원 스냅숏 트랜잭션 격리에 대 한 합니다. 프로그래밍 측면에서 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  
  
 OLE DB Driver for SQL Server와 MDAC의 차이점에 대 한 정보를 참조 하십시오. [MDAC에서 SQL Server 용 OLE DB Driver로 응용 프로그램 업데이트](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)     
 [OLE DB 방법 도움말 항목](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
