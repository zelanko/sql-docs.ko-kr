---
title: SQL Server (ODBC)와 통신 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ed036ebb7bdcf5c9789263c1a18ae4ea4eae243c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537133"
---
# <a name="communicating-with-sql-server-odbc"></a>SQL Server와 통신(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  인스턴스와 통신 하는 ODBC 응용 프로그램에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 환경 할당 해야 합니다 및 연결 처리 및 데이터 원본에 연결 합니다. 연결이 설정되면 응용 프로그램에서는 서버에 쿼리를 보내고 모든 결과 집합을 처리할 수 있습니다. 데이터 원본 사용을 마치면 응용 프로그램은 데이터 원본에 대한 연결을 끊고 연결 핸들을 해제한 후 연결 핸들이 모두 해제되면 환경 핸들을 해제합니다.  
  
 응용 프로그램에서는 개수에 제한 없이 여러 데이터 원본에 연결할 수 있습니다. 응용 프로그램은 여러 드라이버와 여러 데이터 원본의 조합, 단일 드라이버와 여러 데이터 원본 조합 또는 단일 드라이버와 단일 데이터 원본에 대한 여러 개의 연결을 사용할 수 있습니다.  
  
 다운로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC에서 샘플 합니다 [SQL Server 다운로드](http://go.microsoft.com/fwlink/?LinkId=62796) MSDN 페이지를 참조 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [환경 핸들 할당](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [연결 핸들 할당](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 데이터 원본](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [데이터 원본에 연결 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [데이터 원본에서 연결 끊기](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
