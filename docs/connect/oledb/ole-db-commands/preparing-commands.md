---
title: 명령 준비 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 명령 준비
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55dd38bef585a473f7c84504d9d0263808e099b8
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="preparing-commands"></a>명령 준비
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server; 단일 명령으로 여러 번 실행 액세스에 최적화 된 명령 준비를 지원 그러나 명령 준비 오버 헤드를 생성 하 고 두 번 이상 실행할 명령을 준비 하는 소비자 필요 하지 않습니다. 일반적으로 4번 이상 실행할 명령을 준비해야 합니다.  
  
 성능상의 이유로 명령 준비는 명령이 실행될 때까지 지연되며 이것이 기본 동작입니다. 따라서 준비 중인 명령에서 발생하는 모든 오류는 명령이 실행되거나 메타 속성 작업이 수행될 때까지 알려지지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 속성 SSPROP_DEFERPREPARE를 FALSE로 설정하면 이 기본 동작을 해제할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 명령을 먼저 준비하지 않고 직접 실행하면 실행 계획이 만들어져 캐시됩니다. SQL 문을 다시 실행하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 효율적인 알고리즘을 통해 새 문을 캐시의 기존 실행 계획과 비교하고 해당 문에 실행 계획을 다시 사용합니다.  
  
 준비된 명령의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 명령 문 준비와 실행을 위한 기본 지원을 제공합니다. 문을 준비할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 실행 계획을 만들어 캐시하고 이 실행 계획에 대한 핸들을 공급자에 반환합니다. 그러면 공급자는 이 핸들을 사용하여 문을 반복적으로 실행합니다. 이때 저장 프로시저는 만들어지지 않습니다. 핸들에서는 직접 실행의 경우와 같이 문을 캐시의 실행 계획과 비교하는 대신 SQL 문의 실행 계획을 직접 식별하므로 문을 여러 번 실행할 경우 직접 실행하기보다 문을 준비하는 것이 더 효율적입니다.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 준비된 문은 임시 개체를 만드는 데 사용할 수 없고 임시 테이블과 같은 임시 개체를 만드는 시스템 저장 프로시저를 참조할 수 없습니다. 이러한 프로시저는 직접 실행해야 합니다.  
  
 일부 명령은 준비하면 안 됩니다. 예를 들어 저장 프로시저 실행을 지정하거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저 생성에 대한 잘못된 텍스트를 포함하는 명령은 준비하면 안 됩니다.  
  
 임시 저장된 프로시저를 만든 경우의 OLE DB Driver for SQL Server 실행 임시 저장된 프로시저를 문 자체를 실행 하는 경우 결과 반환 합니다.  
  
 임시 저장된 프로시저를 만들 SQL Server 용 OLE DB 드라이버에 의해 제어 됩니다-초기화 속성 SSPROP_INIT_USEPROCFORPREP 합니다. 속성 값 SSPROPVAL_USEPROCFORPREP_ON 또는 SSPROPVAL_USEPROCFORPREP_ON_DROP 이면는 OLE DB Driver for SQL Server에서는 명령이 준비 될 때 저장된 프로시저를 만들 하려고 합니다. 응용 프로그램 사용자에게 충분한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 권한이 있으면 저장 프로시저가 성공적으로 만들어집니다.  
  
 연결이 자주 끊기지 않는 소비자, 임시 저장된 프로시저의 만들기의 리소스가 상당히 필요 **tempdb**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 임시 개체가 만들어지는 시스템 데이터베이스입니다. SQL Server 용 OLE DB 드라이버에서 만든 임시 저장된 프로시저는 명령을 만든 세션 연결이 끊어져서 서비스를 인스턴스의경우에삭제됩니다SSPROP_INIT_USEPROCFORPREP값이SSPROPVAL_USEPROCFORPREP_ON이면[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 해당 연결이 데이터 원본 초기화 시 만들어진 기본 연결인 경우 임시 저장 프로시저는 데이터 원본 초기화가 취소되는 경우에만 삭제됩니다.  
  
 Ssprop_init_useprocforprep 값이 SSPROPVAL_USEPROCFORPREP_ON_DROP 이면 OLE DB Driver for SQL Server 임시 저장 프로시저는 다음 중 하나가 발생 하면 삭제 됩니다.  
  
-   소비자는 **icommandtext:: Setcommandtext** 새 명령을 나타냅니다.  
  
-   소비자는 **icommandprepare:: Unprepare** 명령 텍스트가 더 이상 필요 함을 나타냅니다.  
  
-   소비자가 임시 저장 프로시저를 사용하여 명령 개체에 대한 모든 참조를 해제합니다.  
  
 명령 개체 최대 하나의 임시 저장된 프로시저에 **tempdb**합니다. 기존 임시 저장 프로시저는 특정 명령 개체의 현재 명령 텍스트를 나타냅니다.  
  
## <a name="see-also"></a>관련 항목:  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
