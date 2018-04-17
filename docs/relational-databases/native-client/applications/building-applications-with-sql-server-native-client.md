---
title: SQL Server Native Client와 함께 응용 프로그램을 구축 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], building applications
- SQLNCLI, building applications
- applications [SQL Server Native Client]
- SQL Server Native Client, building applications
ms.assetid: 254a2b48-f0e3-43b5-a48d-3d666c2a779f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4f4cf78541c48739b4ddcf94cd879fc7a56fe18d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="building-applications-with-sql-server-native-client"></a>SQL Server Native Client를 사용하여 응용 프로그램 빌드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 라이브러리를 사용하는 응용 프로그램을 개발할 때 발생하는 많은 문제가 있습니다. 이 섹션의 항목에서는 MDAC에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client로의 업그레이드, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 사용할 수 있는 다양한 연결 문자열 개요를 비롯하여 이러한 많은 문제를 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 설치 방법, 다양한 구성 요소가 설치되는 위치 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 제거 방법에 대해 설명합니다.  
  
 [SQL Server Native Client의 구성 요소](../../../relational-databases/native-client/applications/components-of-sql-server-native-client.md)  
 라이브러리, 리소스, 도움말 및 헤더 파일을 비롯하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 구성하는 구성 요소에 대해 설명합니다.  
  
 [SQL Server Native Client 연결 문자열 키워드 사용](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 통해 데이터베이스에 연결할 때 사용할 수 있는 다양한 연결 문자열 유형에 대해 설명합니다.  
  
 [SQL Server Native Client 헤더 및 라이브러리 파일을 사용 하 여](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)  
 응용 프로그램 내에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일을 사용하는 방법에 대해 설명합니다.  
  
 [MDAC에서 SQL Server Native Client로 응용 프로그램 업데이트](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)  
 MDAC에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client로 업그레이드할 때 고려해야 하는 문제 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 MDAC의 차이점에 대해 설명합니다.  
  
 [SQL Server 2005 Native Client에서 응용 프로그램 업데이트](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client로 업그레이드할 때 고려해야 하는 문제에 대해 설명합니다.  
  
 [SQL Server Native Client와 함께 ADO 사용](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)  
 ADO에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 액세스하고 사용하는 방법에 대해 설명합니다.  
  
 [SQL Server Native Client에 대 한 지원 정책](../../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 여러 버전에서 다양한 데이터 액세스 구성 요소를 사용하는 방법에 대해 설명합니다.  
  
 [SQL Server Native Client를 사용하여 Microsoft Azure SQL Database에 연결](../../../relational-databases/native-client/applications/connecting-to-a-windows-azure-sql-database-using-sql-server-native-client.md)  
 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 방법 도움말 항목](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 방법 도움말 항목](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
