---
title: SQL Server Native Client를 사용 하는 경우 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 36ad9d7f9bad6dc16f3697977211fcd59c9daa19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031689"
---
# <a name="when-to-use-sql-server-native-client"></a>SQL Server Native Client를 사용하는 경우
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 액세스하는 데 사용할 수 있는 한 가지 기술입니다.  다른 데이터 액세스 기술에 대한 자세한 내용은 [데이터 액세스 기술 로드맵](https://go.microsoft.com/fwlink/?LinkID=179186) 참조  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 애플리케이션의 데이터 액세스 기술로 사용할지 여부를 결정할 때는 여러 요인을 고려해야 합니다.  
  
 새 애플리케이션의 경우 Microsoft Visual C# 또는 Visual Basic과 같은 관리되는 프로그래밍 언어를 사용하고 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스해야 한다면 .NET Framework의 일부인 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용해야 합니다.  
  
 COM 기반 애플리케이션을 개발하고 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 도입된 새 기능에 액세스해야 하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스할 필요가 없으면 WDAC(Windows Data Access Components)를 계속 사용할 수 있습니다.  
  
 기존 OLE DB 및 ODBC 애플리케이션의 경우 주된 문제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능에 액세스해야 하는지 여부입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 기능이 필요 없는 완성된 애플리케이션인 경우 계속 MDAC를 사용할 수 있습니다. 그러나 같은 새 기능에 액세스 해야 하는 경우는 [xml 데이터 형식](../../t-sql/xml/xml-transact-sql.md)를 사용 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 MDAC는 모두 행 버전 관리를 사용한 커밋된 읽기 트랜잭션 격리를 지원하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client만 스냅숏 트랜잭션 격리를 지원합니다. 프로그래밍 측면에서 행 버전 관리를 사용하는 커밋된 읽기 트랜잭션 격리는 커밋된 읽기 트랜잭션과 동일합니다.  
  
 간의 차이점에 대 한 자세한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 및 MDAC [MDAC에서 SQL Server Native Client로 응용 프로그램 업데이트](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 프로그래밍](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 방법 도움말 항목](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 방법 도움말 항목](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
