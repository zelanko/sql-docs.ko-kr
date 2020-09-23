---
title: SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용 | Microsoft Docs
description: OLE DB Driver for SQL Server에서 INSERT, UPDATE, DELETE 또는 MERGE 명령에 OUTPUT 절을 사용하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1374dab2ac4954d173d8d131d59bfa4b39f2ad0a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861512"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  INSERT, UPDATE, DELETE 또는 MERGE 명령에 OUTPUT 절을 사용하는 경우 영향을 받는 행 수를 사용할 수 없습니다. 애플리케이션이 OUTPUT 절에서 반환되는 행 집합의 행 수를 계산해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 애플리케이션용 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
