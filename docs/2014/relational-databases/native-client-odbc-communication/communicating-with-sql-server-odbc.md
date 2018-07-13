---
title: SQL Server (ODBC)와 통신 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a701075067b89e40d8dfe44bf9dccfb3240960f1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414382"
---
# <a name="communicating-with-sql-server-odbc"></a>SQL Server와 통신(ODBC)
  인스턴스와 통신 하는 ODBC 응용 프로그램에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 환경 할당 해야 합니다 및 연결 처리 및 데이터 원본에 연결 합니다. 연결이 설정되면 응용 프로그램에서는 서버에 쿼리를 보내고 모든 결과 집합을 처리할 수 있습니다. 데이터 원본 사용을 마치면 응용 프로그램은 데이터 원본에 대한 연결을 끊고 연결 핸들을 해제한 후 연결 핸들이 모두 해제되면 환경 핸들을 해제합니다.  
  
 응용 프로그램에서는 개수에 제한 없이 여러 데이터 원본에 연결할 수 있습니다. 응용 프로그램은 여러 드라이버와 여러 데이터 원본의 조합, 단일 드라이버와 여러 데이터 원본 조합 또는 단일 드라이버와 단일 데이터 원본에 대한 여러 개의 연결을 사용할 수 있습니다.  
  
 다운로드할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC에서 샘플 합니다 [SQL Server 다운로드](http://go.microsoft.com/fwlink/?LinkId=62796) MSDN 페이지를 참조 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [환경 핸들 할당](allocating-an-environment-handle.md)  
  
-   [연결 핸들 할당](allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 데이터 원본](../../integration-services/connection-manager/data-sources.md)  
  
-   [데이터 원본에 연결 &#40;ODBC&#41;](connecting-to-a-data-source-odbc.md)  
  
-   [데이터 원본에서 연결 끊기](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
