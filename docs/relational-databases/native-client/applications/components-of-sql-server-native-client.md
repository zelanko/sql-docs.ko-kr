---
title: "SQL Server Native Client의 구성 요소 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: "25"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3405727d9d62ccb68fa5e4b66f262f1279991338
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 다음 구성 요소가 포함되어 있습니다.  
  
|구성 요소|Description|  
|---------------|-----------------|  
|sqlncli11.dll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 여기에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 포함됩니다.|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 라이브러리에 대한 리소스 파일입니다.|   
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하는 데 필요한 모든 새 정의가 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일입니다. 이 헤더 파일은 odbcss.h 및 sqloledb.h 헤더 파일을 모두 대체합니다.<br /><br /> 참고: 동일한 프로그램에서 sqlncli.h 및 odbcss.h를 참조할 수는 없지만 sqloledb.h를 먼저 정의으로 동일한 프로그램에서 sqlncli.h 및 sqloledb.h를 참조할 수 있습니다.|  
|sqlncli11.lib|라이브러리 파일 하는 데 필요한 직접 호출 된 **bcp** 의 일부인 유틸리티 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버.<br /><br /> 참고: 프로그래밍 코드에서 sqlncli11.lib 파일 참조를 하는 경우 필요한 sqlncli11.dll 파일이 해당 시스템 경로 및 확인 하는 사용자의 시스템 경로에 있는지 확인 하려면 응용 프로그램을 사용 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 사용한 응용 프로그램 작성](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
