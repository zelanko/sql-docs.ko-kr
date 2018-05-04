---
title: SQL Server 용 OLE DB 드라이버에서 u t F-16 지원 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버의 utf-16 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f88dea7bbc4fbd2ea6307647e1cbce47b07a0558
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>SQL Server 용 OLE DB 드라이버의 utf-16 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  부터는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하 고 경우는 **wchar** 종결 문자 크기의 상위 서로게이트 코드 포인트를 버퍼에 기록 되는 문자는 서로게이트 쌍을 쓰고 다음 **wchar** 문자 하위 서로게이트 코드 포인트는, OLE DB Driver for SQL Server 버퍼를 상위 서로게이트 코드 포인트를 추가 하지 것입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
