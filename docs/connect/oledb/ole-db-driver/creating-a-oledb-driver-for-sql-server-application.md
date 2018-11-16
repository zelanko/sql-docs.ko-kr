---
title: SQL Server 응용 프로그램용 OLE DB 드라이버 만들기 | Microsoft Docs
description: SQL Server 응용 프로그램용 OLE DB 드라이버 만들기
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
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: fb718e2288b1d5e2aaccc1cbafc0c85037bd8082
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605773"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>SQL Server 응용 프로그램용 OLE DB 드라이버 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 드라이버 만들기 SQL Server 응용 프로그램에 대해 이러한 단계가 포함 됩니다.  
  
1.  데이터 원본에 대한 연결 설정  
  
2.  명령 실행  
  
3.  결과 처리  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [the Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본에 대한 연결 설정](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [명령 실행](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [결과 처리](../../oledb/ole-db-driver/processing-results.md)  
  
-   [OLE DB 속성 정보](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
