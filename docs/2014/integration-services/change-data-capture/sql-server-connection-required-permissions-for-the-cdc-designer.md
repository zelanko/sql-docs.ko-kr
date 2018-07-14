---
title: SQL Server 연결을 위해 CDC Designer에 대해 필요한 권한 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b577e54ea4fc138f63a46ef5a588303439e0fe91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201903"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>SQL Server 연결을 위해 CDC Designer에 대해 필요한 권한
  CDC Designer 콘솔에서 태스크를 수행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 정보가 필요합니다. 이 항목에서는 **연결 설정을 위해** SQL Server에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]대화 상자에서 지정할 수 있는 정보에 대해 설명합니다.  
  
 **연결 정보를 사용할 수 없거나 정보가 있지만 연결에 필요한 권한이 없는 경우와 같이 필요한 경우** SQL Server에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대화 상자가 열립니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결이 필요한 다양한 태스크와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인/사용자의 필요한 권한에 대해 설명합니다.  
  
|태스크|최소 권한|  
|----------|-------------------------|  
|연관된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하여 CDC Service 및 인스턴스 목록 보기|`db_datareader` 역할|  
|CDC 인스턴스 시작/중지|`db_datareader` 및 `db_datawriter` 역할|  
|CDC 인스턴스 상태 보기|`db_owner` 역할|  
|새 Oracle CDC 인스턴스 데이터베이스 만들기|`dbcreator` 고정 서버 역할|  
|새 Oracle CDC 인스턴스 만들기|`db_datareader` 역할<br /><br /> `db_owner` 역할|  
|배포 스크립트 가져오기|`db_datareader` 및 `db_datawriter` 역할<br /><br /> `db_owner` 역할|  
|구성 변경 및 캡처 인스턴스 추가/제거|`db_datareader` 및 `db_datawriter` 역할<br /><br /> `db_owner` 역할|  
  
## <a name="see-also"></a>관련 항목  
 [CDC Designer 콘솔 액세스](access-the-cdc-designer-console.md)   
 [인스턴스를 만들기 위한 SQL Server 연결](sql-server-connection-for-instance-creation.md)  
  
  
