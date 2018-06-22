---
title: SQL Server Native Client의 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c1a53fe3338f7b987bdf2b26312d634964f3587e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082465"
---
# <a name="components-of-sql-server-native-client"></a>SQL Server Native Client의 구성 요소
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에는 다음 구성 요소가 포함되어 있습니다.  
  
|구성 요소|Description|  
|---------------|-----------------|  
|sqlncli11.dll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 여기에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 포함됩니다.|  
|sqlnclir11.rll|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 라이브러리에 대한 리소스 파일입니다.|  
|s10ch_sqlncli.chm|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB Provider를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 원본을 만드는 방법을 문서화하는 데이터 원본 마법사 도움말 파일입니다.|  
|sqlncli.h|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하는 데 필요한 모든 새 정의가 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 파일입니다. 이 헤더 파일은 odbcss.h 및 sqloledb.h 헤더 파일을 모두 대체합니다. **참고:** 동일한 프로그램에서 sqlncli.h 및 odbcss.h를 참조할 수 없습니다 없지만 sqloledb.h를 먼저 정의으로 동일한 프로그램에서 sqlncli.h 및 sqloledb.h를 참조할 수 있습니다.|  
|sqlncli11.lib|라이브러리 파일 하는 데 필요한 직접 호출 된 **bcp** 의 일부인 유틸리티 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. **참고:** sqlncli11.dll 파일이 해당 시스템 경로 및 확인 하는 사용자의 시스템 경로에 있는지 확인 해야 하는 프로그래밍 코드에서 sqlncli11.lib 파일 참조를 하는 경우 응용 프로그램을 사용 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client를 사용하여 응용 프로그램 빌드](building-applications-with-sql-server-native-client.md)  
  
  