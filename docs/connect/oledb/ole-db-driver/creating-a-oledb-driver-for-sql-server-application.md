---
title: SQL Server 애플리케이션용 OLE DB 드라이버 만들기 | Microsoft Docs
description: OLE DB Driver for SQL Server 애플리케이션을 만들고 추가 리소스를 찾는 데 필요한 단계에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed150ea18d1141e6116efe177e65836c235cf703
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727229"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>SQL Server 애플리케이션용 OLE DB 드라이버 만들기
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 애플리케이션을 만들려면 다음 단계를 수행합니다.  
  
1.  데이터 원본에 대한 연결 설정  
  
2.  명령 실행  
  
3.  결과 처리  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [the Win32 cryptoAPI](/windows/win32/seccng/cng-portal)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본에 대한 연결 설정](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [명령 실행](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [결과 처리](../../oledb/ole-db-driver/processing-results.md)  
  
-   [OLE DB 속성 정보](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
