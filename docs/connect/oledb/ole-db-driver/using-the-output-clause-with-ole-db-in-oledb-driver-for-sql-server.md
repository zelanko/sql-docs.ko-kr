---
title: SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ad3408d0419e408809b151114d83a09d976505fa
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109395"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  INSERT, UPDATE, DELETE 또는 MERGE 명령에 OUTPUT 절을 사용하는 경우 영향을 받는 행 수를 사용할 수 없습니다. 응용 프로그램이 OUTPUT 절에서 반환되는 행 집합의 행 수를 계산해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 응용 프로그램용 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
