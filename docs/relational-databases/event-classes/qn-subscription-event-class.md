---
title: QN:Subscription 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], QN:Subscription
ms.assetid: 4916167e-8541-43b4-900e-ec8e6adcbc34
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 10ce803c5ba92915d17be754e3d70c2841d16629
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="qnsubscription-event-class"></a>QN:Subscription 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  QN:Subscription 이벤트는 알림 구독에 대한 정보를 보고합니다.  
  
## <a name="qnsubscription-event-class-data-columns"></a>QN:Subscription 이벤트 클래스 데이터 열  
  
|데이터 열|형식|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|**int**|이벤트 유형 = 199|27|아니오|  
|EventSequence|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니오|  
|EventSubClass|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **Subscription registered**: 쿼리 알림 구독이 데이터베이스에 등록되었음을 나타냅니다.<br /><br /> **Subscription rewound**: [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 기존 구독과 정확히 일치하는 구독 요청을 받았음을 나타냅니다. 이러한 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 기존 구독의 시간 제한 값을 새 구독 요청에서 지정한 시간 제한으로 설정합니다.<br /><br /> **Subscription fired**: 알림 구독이 알림 메시지를 생성함을 나타냅니다.<br /><br /> **Firing failed with broker error**: [!INCLUDE[ssSB](../../includes/sssb-md.md)] 오류로 인해 알림 메시지를 표시할 수 없을 나타냅니다.<br /><br /> **Firing failed without broker error**: [!INCLUDE[ssSB](../../includes/sssb-md.md)] 오류가 아닌 다른 이유로 인해 알림 메시지를 표시할 수 없을 나타냅니다.<br /><br /> **Broker error intercepted**: [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 쿼리 알림이 사용하는 대화에서 오류를 전달했음을 나타냅니다.<br /><br /> **Subscription deletion attempt**: [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 만료된 구독을 삭제하여 리소스를 늘리려고 했음을 나타냅니다.<br /><br /> **Subscription deletion failed**: 만료된 구독 삭제 시도가 실패했음을 나타냅니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 자동으로 구독 삭제 일정을 다시 조정하여 리소스를 늘립니다.<br /><br /> **Subscription destroyed**: [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 만료된 구독을 삭제했음을 나타냅니다.|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|아니오|  
|LoginName|**nvarchar**|사용자 로그인 이름( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인 또는 DOMAIN\Username 형식의 Windows 로그인 자격 증명)입니다.|11|아니오|  
|LoginSID|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|RequestID|**int**|문을 포함하는 요청의 식별자입니다.|49|예|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 응용 프로그램이 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행하는 경우 SessionLoginName은 "Login1"을 표시하고 LoginName은 "Login2"를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|이 이벤트에 해당하는 정보가 포함된 XML 문서를 반환합니다. 이 문서는 [SQL Server 쿼리 알림 프로파일러 이벤트 스키마](http://go.microsoft.com/fwlink/?LinkId=63331) 페이지에서 사용할 수 있는 XML 스키마를 따릅니다.|1|예|  
  
  
