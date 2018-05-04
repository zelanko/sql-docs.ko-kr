---
title: SQL Server Support for LocalDB에 대 한 OLE DB 드라이버 | Microsoft Docs
description: OLE DB Driver LocalDB에 대 한 SQL Server 지원
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
ms.openlocfilehash: 9c68952fc7e9ebfad79955e78fe64d6550fb2c5d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-driver-for-sql-server-support-for-localdb"></a>SQL Server Support for LocalDB에 대 한 OLE DB 드라이버
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 LocalDB라고 부르는 SQL Server의 경량 버전을 사용할 수 있습니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.  
  
## <a name="remarks"></a>주의  
 LocalDB 설치 및 LocalDB 인스턴스 구성 방법을 포함하여 LocalDB에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SQL Server Express LocalDB 참조](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 요약하자면, LocalDB를 통해 다음과 같은 기능을 수행할 수 있습니다.  
  
-   **sqllocaldb.exe i** 를 사용하여 기본 인스턴스의 이름을 확인할 수 있습니다.  
  
-   **AttachDBFilename** 연결 문자열 키워드를 사용하여 서버가 연결해야 하는 데이터베이스 파일을 지정할 수 있습니다. **AttachDBFilename**을 사용할 때 **Database** 연결 문자열 키워드를 사용하여 데이터베이스 이름을 지정하지 않으면 응용 프로그램이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.  
  
-   연결 문자열에 LocalDB 인스턴스를 지정합니다.  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. **sqlcmd -S (localdb)\v11.0**).  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
