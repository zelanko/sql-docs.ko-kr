---
title: SQL Server Native Client를 사용 하 여 Azure SQL Database에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5599bbb0aa1736ba5c88904ae5152a0d73856dc5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213783"
---
# <a name="connecting-to-a-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client를 사용하여 Azure SQL 데이터베이스에 연결
  에 연결 하는 방법을 보여 주는 샘플을 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] 를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native client를 [개발: 방법 도움말 항목 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/ee621787.aspx)합니다.  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL Database에 연결할 때 알려진 문제  
 다음은 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 알려진 문제입니다.  
  
-   단계에 `SQLBrowseConnect`가 사용되는 경우 `SQLBrowseConnect`를 사용한 연결은 거부됩니다.  예를 들어 첫 번째 호출에서 드라이버 이름을 보내고, 두 번째 호출에서 서버 및 자격 증명(사용자 및 암호)을 보내 연결을 설정하고, 세 번째 호출에서 데이터베이스 이름 및 언어를 보내는 경우입니다.  세 번째 호출은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 USE 문을 실행하여 데이터베이스를 변경하도록 합니다. 그러나 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 USE 문이 지원되지 않으므로 다음과 같은 오류가 발생합니다.  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client를 사용하여 응용 프로그램 빌드](building-applications-with-sql-server-native-client.md)  
  
  
