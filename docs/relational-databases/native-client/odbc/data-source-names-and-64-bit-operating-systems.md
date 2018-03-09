---
title: "데이터 원본 이름 및 64 비트 운영 체제 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 773218e7c0e141c57223f73f998c7ba2e612e927
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>데이터 원본 이름 및 64비트 운영 체제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  응용 프로그램을 64비트 운영 체제에서 32비트 응용 프로그램으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
## <a name="remarks"></a>주의  
 64비트 Windows 운영 체제에는 odbcad32.exe 파일이 두 개 있습니다.  
  
-   %SystemRoot%\system32\odbcad32.exe는 64비트 응용 프로그램의 데이터 원본 이름을 만들고 유지 관리하는 데 사용됩니다.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe는 64비트 운영 체제에서 실행되는 32비트 응용 프로그램을 포함하여 32비트 응용 프로그램의 데이터 원본 이름을 만들고 유지 관리하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
