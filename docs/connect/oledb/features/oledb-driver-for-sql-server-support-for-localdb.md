---
title: SQL Server용 OLE DB 드라이버의 LocalDB 지원 | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 LocalDB 라는 경량 버전의 SQL Server에 연결하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb768c0beea3ce836586bc718e1b7757da7ce72
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727318"
---
# <a name="ole-db-driver-for-sql-server-support-for-localdb"></a>SQL Server용 OLE DB 드라이버의 LocalDB 지원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 LocalDB라고 부르는 SQL Server의 경량 버전을 사용할 수 있습니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.  
  
## <a name="remarks"></a>설명  
 LocalDB 설치 및 LocalDB 인스턴스 구성 방법을 포함하여 LocalDB에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SQL Server Express LocalDB 참조](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-express-localdb.md)  
  
 요약하자면, LocalDB를 통해 다음과 같은 기능을 수행할 수 있습니다.  
  
-   **sqllocaldb.exe i** 를 사용하여 기본 인스턴스의 이름을 확인할 수 있습니다.  
  
-   **AttachDBFilename** 연결 문자열 키워드를 사용하여 서버가 연결해야 하는 데이터베이스 파일을 지정할 수 있습니다. **AttachDBFilename**을 사용할 때 **Database** 연결 문자열 키워드를 사용하여 데이터베이스 이름을 지정하지 않으면 애플리케이션이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.  
  
-   연결 문자열에 LocalDB 인스턴스를 지정합니다.  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. **sqlcmd -S (localdb)\v11.0**).  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
