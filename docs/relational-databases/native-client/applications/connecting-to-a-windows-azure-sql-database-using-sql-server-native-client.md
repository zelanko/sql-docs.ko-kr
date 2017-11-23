---
title: "SQL Server Native Client를 사용 하 여 Windows Azure SQL 데이터베이스에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: native-client|applications
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 145d1ff520240283d01bb0dce7f85ba3c0faeb8b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-to-a-windows-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client를 사용하여 Microsoft Azure SQL Database에 연결
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  에 연결 하는 방법을 보여 주는 샘플에 대 한 한 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client를 [개발: 방법 도움말 항목 (Windows Azure SQL 데이터베이스)](http://msdn.microsoft.com/library/ee621787.aspx)합니다.  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL Database에 연결할 때 알려진 문제  
 다음은 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 알려진 문제입니다.  
  
-   사용한 연결은 **SQLBrowseConnect** 경우 거부 될 수 있습니다 **SQLBrowseConnect** 단계에 사용 됩니다.  예를 들어 첫 번째 호출에서 드라이버 이름을 보내고, 두 번째 호출에서 서버 및 자격 증명(사용자 및 암호)을 보내 연결을 설정하고, 세 번째 호출에서 데이터베이스 이름 및 언어를 보내는 경우입니다.  세 번째 호출은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 USE 문을 실행하여 데이터베이스를 변경하도록 합니다. 그러나 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 USE 문이 지원되지 않으므로 다음과 같은 오류가 발생합니다.  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client를 사용하여 응용 프로그램 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
