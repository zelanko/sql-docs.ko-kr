---
title: SQL Server용 OLE DB 드라이버에서 UTF-16 지원 | Microsoft Docs
description: SQL Server용 OLE DB 드라이버에서 UTF-16 지원
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 71b4298fa3e843e6e9a15dce638f2f068fe5d4b3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007239"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버에서 UTF-16 지원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공하는 경우, 종결 문자 이전에 버퍼에 작성된 **wchar** 문자가 서로게이트 쌍의 상위 서로게이트 코드 포인트인 경우 및 다음 **wchar** 문자가 하위 서로게이트 코드 포인트인 경우 SQL Server용 OLE DB 드라이버에서 상위 서로게이트 코드 포인트를 버퍼에 추가하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
