---
title: SQL Server와 통신 (ODBC) | Microsoft Docs
description: ODBC 응용 프로그램이 연결 및 연결 리소스를 사용 하 여 SQL Server 인스턴스와 통신 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6f149f8d1d714839d356d3675a19656f2ea7d53
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734904"
---
# <a name="communicating-with-sql-server-odbc"></a>SQL Server와 통신(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  ODBC 응용 프로그램에서 인스턴스와 통신 하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경 및 연결 핸들을 할당 하 고 데이터 원본에 연결 해야 합니다. 연결이 설정되면 애플리케이션에서는 서버에 쿼리를 보내고 모든 결과 집합을 처리할 수 있습니다. 데이터 원본 사용을 마치면 애플리케이션은 데이터 원본에 대한 연결을 끊고 연결 핸들을 해제한 후 연결 핸들이 모두 해제되면 환경 핸들을 해제합니다.  
  
 애플리케이션에서는 개수에 제한 없이 여러 데이터 원본에 연결할 수 있습니다. 애플리케이션은 여러 드라이버와 여러 데이터 원본의 조합, 단일 드라이버와 여러 데이터 원본 조합 또는 단일 드라이버와 단일 데이터 원본에 대한 여러 개의 연결을 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 샘플은 MSDN의 [SQL Server 다운로드](https://go.microsoft.com/fwlink/?LinkId=62796) 페이지에서 다운로드할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [환경 핸들 할당](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [연결 핸들 할당](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 데이터 원본](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [ODBC&#41;&#40;데이터 원본에 연결](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [데이터 원본에서 연결 끊기](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
