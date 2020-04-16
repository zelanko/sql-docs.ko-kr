---
title: 구성 요소
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c824d145b6353f96a3756f28b7446799b303889
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388212"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client의 구성 요소
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 다음 구성 요소가 포함되어 있습니다.  
  
|구성 요소|Description|  
|---------------|-----------------|  
|sqlncli11.dll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 여기에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 포함됩니다.|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 라이브러리에 대한 리소스 파일입니다.|   
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하는 데 필요한 모든 새 정의가 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일입니다. 이 헤더 파일은 odbcss.h 및 sqloledb.h 헤더 파일을 모두 대체합니다.<br /><br /> 참고: 동일한 프로그램에서 sqlncli.h 및 odbcss.h를 참조할 수는 없지만 sqloledb.h가 먼저 정의된 한 동일한 프로그램에서 sqlncli.h 및 sqloledb.h를 참조할 수 있습니다.|  
|sqlncli11.lib|라이브러리 파일은 네이티브 클라이언트 ODBC 드라이버의 일부인 bcp 유틸리티 함수를 직접 호출하는 데 필요합니다. **bcp** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]<br /><br /> 참고: 프로그래밍 코드에서 sqlncli11.lib 파일을 참조하는 경우 sqlncli11.dll 파일이 시스템 경로및 응용 프로그램을 사용하는 사용자의 시스템 경로에 있는지 확인해야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
