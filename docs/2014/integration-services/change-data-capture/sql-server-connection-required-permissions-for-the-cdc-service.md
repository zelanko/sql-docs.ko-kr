---
title: SQL Server 연결 CDC Service에 필요한 권한 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ecc6c5ccff5f5ccff8a0625e1adde24aebe2f603
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62835179"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>SQL Server 연결 CDC Service에 필요한 권한
  CDC Service 구성 콘솔에서 태스크를 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보가 필요합니다. 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 설정을 위해 SQL Server에 연결 대화 상자에서 지정할 수 있는 정보에 대해 설명합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보를 사용할 수 없거나 정보가 있지만 연결에 필요한 권한이 없는 경우와 같이 필요한 경우 SQL Server에 연결 대화 상자가 열립니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 필요한 다양한 태스크와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인/사용자의 필요한 권한에 대해 설명합니다.  
  
|Task|최소 권한|  
|----------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 준비합니다.|`dbcreator` 고정 서버 역할|  
|Oracle CDC Service에서 사용할 Oracle CDC Service-SQL Server 로그인을 만듭니다.|`public` 고정 서버 역할|  
|MSXDBCDC에서 새 서비스를 등록하는 데 사용할 Oracle CDC Service-로그인을 만듭니다.|`db_datareader` 및 `db_datawriter` 역할|  
|MSXDBCDC에서 서비스의 등록을 업데이트하는 데 사용할 Oracle CDC Service-로그인을 편집합니다.|`db_datareader` 및 `db_datawriter` 역할|  
|MSXDBCDC에서 서비스의 등록을 업데이트하는 데 사용할 Oracle CDC Service-로그인을 삭제합니다.|`db_datareader` 및 `db_datawriter` 역할|  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버에 연결](connection-to-sql-server.md)   
 [삭제를 위해 SQL Server에 연결](connection-to-sql-server-for-delete.md)  
  
  
