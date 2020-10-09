---
description: SQL Server Native Client를 사용하여 Azure SQL Database에 연결
title: Azure SQL Database에 연결
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b5335f05060bf40431621dc3c45cfb11e22c914
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868416"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client를 사용하여 Azure SQL Database에 연결
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Native Client를 사용 하 여에 연결 하는 방법을 보여 주는 샘플은 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [개발: 방법 도움말 항목 (Azure SQL Database)](/previous-versions/azure/ee621787(v=azure.100))을 참조 하세요.  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL Database에 연결할 때 알려진 문제  
 다음은 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 때 알려진 문제입니다.  
  
-   **SQLBrowseConnect** 가 단계에서 사용 되는 경우 **SQLBrowseConnect** 를 사용 하 여 만든 연결이 거부 될 수 있습니다.  예를 들어 첫 번째 호출에서 드라이버 이름을 보내고, 두 번째 호출에서 서버 및 자격 증명(사용자 및 암호)을 보내 연결을 설정하고, 세 번째 호출에서 데이터베이스 이름 및 언어를 보내는 경우입니다.  세 번째 호출은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 USE 문을 실행하여 데이터베이스를 변경하도록 합니다. 그러나 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]에서 USE 문이 지원되지 않으므로 다음과 같은 오류가 발생합니다.  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client를 사용하여 애플리케이션 빌드](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
