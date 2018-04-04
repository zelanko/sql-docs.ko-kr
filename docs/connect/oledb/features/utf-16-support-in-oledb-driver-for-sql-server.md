---
title: SQL Server 용 OLE DB 드라이버에서 u t F-16 지원 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버의 utf-16 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f4e1103b25deb46d03ce26a79ba3649305c283d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버의 utf-16 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  부터는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하 고 경우는 **wchar** 종결 문자 크기의 상위 서로게이트 코드 포인트를 버퍼에 기록 되는 문자는 서로게이트 쌍을 쓰고 다음 **wchar** 문자 하위 서로게이트 코드 포인트는, OLE DB Driver for SQL Server 버퍼를 상위 서로게이트 코드 포인트를 추가 하지 것입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server 기능](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
