---
title: OLEDB Provider Information 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Provider Information event class
ms.assetid: a0316c4e-4b8c-4754-8a35-222f3c0907d1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 68cf4eb253505f6ade040eb0bf0f877f4fb91d94
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63032393"
---
# <a name="oledb-provider-information-event-class"></a>OLEDB Provider Information 이벤트 클래스
  **OLEDB Provider Information** 이벤트 클래스는 분산 쿼리가 실행되어 공급자 연결에 해당하는 정보를 수집할 때 발생합니다.  
  
 이 이벤트 클래스는 원격 공급자로부터 수집한 모든 속성을 다음에 열거한 항목을 포함하여 다수의 속성 집합으로 포함합니다.  
  
-   DBPROPSET_DATASOURCEINFO  
  
-   SQLPROPSET_OPTHINTS  
  
-   DBPROPSET_SQLSERVERDATASOURCEINFO([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에만 해당)  
  
-   DBPROPSET_SQLSERVERDBINIT([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에만 해당)  
  
-   DBPROPSET_ROWSET  
  
-   IDBInfo 인터페이스  
  
 이러한 속성은 사용 가능한 메타데이터와 함께 쿼리 최적화 프로그램이 쿼리에 가장 적합한 실행 계획을 선택할 때 사용됩니다. 이 정보는 분산 쿼리 프로파일러 추적에서 실행을 추적하고 OLE DB 호출 및 이벤트를 분석할 때 유용합니다.  
  
## <a name="oledb-provider-information-event-class-data-columns"></a>OLEDB Provider Information 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE 데이터베이스 문을 실행하지 않은 경우 기본 *database* 입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|**EventClass**|**int**|이벤트 유형 = 194|27|예|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|**LinkedServerName**|**nvarchar**|연결된 서버의 이름입니다.|45|yes|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인)입니다.|11|yes|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|**ProviderName**|**nvarchar**|OLE DB Provider의 이름입니다.|46|yes|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**TextData**|**ntext**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다.|1|yes|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL의 OLE 자동화 개체](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
