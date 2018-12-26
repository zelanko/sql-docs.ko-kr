---
title: 데이터 원본 이름 및 64 비트 운영 체제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2248077b8efed3ebf11f871603a6513d6b9f4a02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612571"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>데이터 원본 이름 및 64비트 운영 체제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  애플리케이션을 64비트 운영 체제에서 32비트 애플리케이션으로 작성하여 실행하려는 경우 %windir%\SysWOW64\odbcad32.exe에서 ODBC 관리자를 사용하여 ODBC 데이터 원본을 만들어야 합니다.  
  
## <a name="remarks"></a>Remarks  
 64비트 Windows 운영 체제에는 odbcad32.exe 파일이 두 개 있습니다.  
  
-   %SystemRoot%\system32\odbcad32.exe는 64비트 애플리케이션의 데이터 원본 이름을 만들고 유지 관리하는 데 사용됩니다.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe는 64비트 운영 체제에서 실행되는 32비트 애플리케이션을 포함하여 32비트 애플리케이션의 데이터 원본 이름을 만들고 유지 관리하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
