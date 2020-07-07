---
title: 명령 준비 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 731f03b29f48d8e1970bdddd1f6ee2d1a7748c3e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002805"
---
# <a name="preparing-commands"></a>명령 준비
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 단일 명령을 효율적으로 여러 번 실행하기 위한 명령 준비를 지원합니다. 그러나 명령 준비로 인해 오버헤드가 늘어나며 소비자가 명령을 두 번 이상 실행하기 위해 준비할 필요는 없습니다. 일반적으로 4번 이상 실행할 명령을 준비해야 합니다.  
  
 성능상의 이유로 명령 준비는 명령이 실행될 때까지 지연되며 이것은 기본적인 동작입니다. 따라서 준비 중인 명령에서 발생하는 모든 오류는 명령이 실행되거나 메타 속성 작업이 수행될 때까지 알려지지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 속성 SSPROP_DEFERPREPARE를 FALSE로 설정하면 이 기본 동작을 해제할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 명령을 먼저 준비하지 않고 직접 실행하면 실행 계획이 만들어져 캐시됩니다. SQL 문을 다시 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 효율적인 알고리즘을 통해 새 문을 캐시의 기존 실행 계획과 비교하고 해당 문에 실행 계획을 다시 사용합니다.  
  
 준비된 명령의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 명령 문 준비와 실행을 위한 기본 지원을 제공합니다. 문을 준비할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 실행 계획을 만들어 캐시하고 이 실행 계획에 대한 핸들을 공급자에 반환합니다. 그러면 공급자는 이 핸들을 사용하여 문을 반복적으로 실행합니다. 이때 저장 프로시저는 만들어지지 않습니다. 핸들에서는 직접 실행의 경우와 같이 문을 캐시의 실행 계획과 비교하는 대신 SQL 문의 실행 계획을 직접 식별하므로 문을 여러 번 실행할 경우 직접 실행하기보다 문을 준비하는 것이 더 효율적입니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 준비된 문은 임시 개체를 만드는 데 사용할 수 없고 임시 테이블과 같은 임시 개체를 만드는 시스템 저장 프로시저를 참조할 수 없습니다. 이러한 프로시저는 직접 실행해야 합니다.  
  
 일부 명령은 준비하면 안 됩니다. 예를 들어 저장 프로시저 실행을 지정하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 생성에 대한 잘못된 텍스트를 포함하는 명령은 준비하면 안 됩니다.  
  
 임시 저장 프로시저가 만들어지면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 임시 저장 프로시저를 실행하여 문 자체를 실행한 것처럼 결과를 반환합니다.  
  
 임시 저장 프로시저 생성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자별 초기화 속성 SSPROP_INIT_USEPROCFORPREP에서 제어합니다. 이 속성 값이 SSPROPVAL_USEPROCFORPREP_ON 또는 SSPROPVAL_USEPROCFORPREP_ON_DROP이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 명령을 준비할 때 저장 프로시저를 만들려고 합니다. 애플리케이션 사용자에게 충분한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 있으면 저장 프로시저가 성공적으로 만들어집니다.  
  
 연결이 자주 끊기지 않는 소비자의 경우 임시 저장 프로시저 생성에는 임시 개체가 만들어지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스인 **tempdb**의 리소스가 상당히 필요합니다. SSPROP_INIT_USEPROCFORPREP 값이 SSPROPVAL_USEPROCFORPREP_ ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 만든 임시 저장 프로시저는 명령을 만든 세션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 사이의 연결이 끊기는 경우에만 삭제됩니다. 해당 연결이 데이터 원본 초기화 시 만들어진 기본 연결인 경우 임시 저장 프로시저는 데이터 원본 초기화가 취소되는 경우에만 삭제됩니다.  
  
 SSPROP_INIT_USEPROCFORPREP 값이 SSPROPVAL_USEPROCFORPREP_ON_DROP이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 임시 저장 프로시저는 다음과 같은 경우 삭제됩니다.  
  
-   소비자가 **ICommandText::SetCommandText**를 사용하여 새 명령을 지정합니다.  
  
-   소비자가 **ICommandPrepare::Unprepare**를 사용하여 명령 텍스트가 더 이상 필요 없음을 나타냅니다.  
  
-   소비자가 임시 저장 프로시저를 사용하여 명령 개체에 대한 모든 참조를 해제합니다.  
  
 명령 개체는 **tempdb**에 임시 저장 프로시저를 하나만 포함합니다. 기존 임시 저장 프로시저는 특정 명령 개체의 현재 명령 텍스트를 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [명령](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
