---
title: OLE DB Driver를 사용하는 경우
description: OLE DB Driver for SQL Server를 사용하는 경우와 다른 드라이버와 차별화되는 상위 수준 데이터 액세스 개념에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd5237556ec0bbe1bf4101cb5adde9734088217c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860185"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버를 사용해야 하는 경우
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터에 액세스할 때 사용할 수 있는 한 가지 기술입니다.  다른 데이터 액세스 기술에 대한 자세한 내용은 [데이터 액세스 기술 로드맵](https://go.microsoft.com/fwlink/?LinkID=179186) 참조  
  
 SQL Serverd용 OLE DB 드라이버를 애플리케이션의 데이터 액세스 기술로 사용할지 여부를 결정할 때는 여러 요인을 고려해야 합니다.  
  
 새 애플리케이션의 경우 Microsoft Visual C# 또는 Visual Basic과 같은 관리되는 프로그래밍 언어를 사용하고 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스해야 한다면 .NET Framework의 일부인 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용해야 합니다.  
  
 COM 기반 애플리케이션을 개발하고 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 도입된 새 기능에 액세스해야 하는 경우에는 SQL Serverd용 OLE DB 드라이버를 사용해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스할 필요가 없으면 WDAC(Windows Data Access Components)를 계속 사용할 수 있습니다.  
  
 기존 OLE DB 애플리케이션의 경우 주된 문제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스해야 하는지 여부입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능이 필요 없는 완성된 애플리케이션인 경우 계속 MDAC를 사용할 수 있습니다. 그러나 [xml 데이터 형식](../../t-sql/xml/xml-transact-sql.md)과 같은 새 기능에 액세스해야 하는 경우에는 SQL Serverd용 OLE DB 드라이버를 사용해야 합니다.  
  
 OLE DB Driver for SQL Server와 MDAC는 모두 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 격리를 지원하지만 OLE DB Driver for SQL Server에서만 스냅샷 트랜잭션 격리를 지원합니다. 프로그래밍 측면에서 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  
  
 OLE DB Driver for SQL Server와 MDAC 간의 차이점에 대한 자세한 내용은 [애플리케이션을 MDAC에서 OLE DB Driver for SQL Server로 업데이트](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버](oledb-driver-for-sql-server.md)  
 [OLE DB 방법 도움말 항목](ole-db-how-to/ole-db-how-to-topics.md)  
  
  
