---
title: SQL Server와 통신 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bf07f4e83cb58966b384a4bf0f523b7a1dd3881
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63032878"
---
# <a name="communicating-with-sql-server-odbc"></a>SQL Server와 통신(ODBC)
  ODBC 응용 프로그램에서 인스턴스와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]통신 하려면 환경 및 연결 핸들을 할당 하 고 데이터 원본에 연결 해야 합니다. 연결이 설정되면 애플리케이션에서는 서버에 쿼리를 보내고 모든 결과 집합을 처리할 수 있습니다. 데이터 원본 사용을 마치면 애플리케이션은 데이터 원본에 대한 연결을 끊고 연결 핸들을 해제한 후 연결 핸들이 모두 해제되면 환경 핸들을 해제합니다.  
  
 애플리케이션에서는 개수에 제한 없이 여러 데이터 원본에 연결할 수 있습니다. 애플리케이션은 여러 드라이버와 여러 데이터 원본의 조합, 단일 드라이버와 여러 데이터 원본 조합 또는 단일 드라이버와 단일 데이터 원본에 대한 여러 개의 연결을 사용할 수 있습니다.  
  
 Native Client ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 샘플은 MSDN의 [SQL Server 다운로드](https://go.microsoft.com/fwlink/?LinkId=62796) 페이지에서 다운로드할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [환경 핸들 할당](allocating-an-environment-handle.md)  
  
-   [연결 핸들 할당](allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 데이터 원본](../../integration-services/connection-manager/data-sources.md)  
  
-   [ODBC&#41;&#40;데이터 원본에 연결](connecting-to-a-data-source-odbc.md)  
  
-   [데이터 원본에서 연결 끊기](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
