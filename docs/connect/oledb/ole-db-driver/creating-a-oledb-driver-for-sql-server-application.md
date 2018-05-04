---
title: SQL Server 응용 프로그램에 대 한 OLE DB 드라이버 만들기 | Microsoft Docs
description: OLE DB Driver for SQL Server 응용 프로그램 만들기
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 697e3f5e563c360f744e5703ca74b3b5557bfbf8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>SQL Server 응용 프로그램에 대 한 OLE DB 드라이버 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server 응용 프로그램을 만드는 다음 단계를 따르십시오.  
  
1.  데이터 원본에 대한 연결 설정  
  
2.  명령 실행  
  
3.  결과 처리  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 사용 하 여 암호화 해야 자격 증명을 유지 해야 하는 경우 [Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본에 대 한 연결을 설정합니다.](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [명령 실행](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [결과 처리](../../oledb/ole-db-driver/processing-results.md)  
  
-   [OLE DB 속성 정보](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [SQL Server용 OLE DB 드라이버에서 OLE DB와 함께 OUTPUT 절 사용](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
