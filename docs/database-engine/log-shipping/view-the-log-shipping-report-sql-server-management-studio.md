---
title: 로그 전달 보고서 보기(SSMS)
description: SQL Server Management Studio에서 트랜잭션 로그 전달 상태 보고서를 확인합니다. 모니터 서버, 주 서버 또는 보조 서버에서 상태 보고서를 실행합니다.
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- viewing log shipping reports
- displaying log shipping reports
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], viewing reports
ms.assetid: 3b549f2f-3683-45e5-b8e8-8095276c41ab
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ba4a8e1d48587046ecceb9007ca57f580b0338c2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748547"
---
# <a name="view-the-log-shipping-report-sql-server-management-studio"></a>로그 전달 보고서 보기(SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 트랜잭션 로그 전달 상태 보고서를 보는 방법을 설명합니다. 모니터 서버, 주 서버 또는 보조 서버에서 상태 보고서를 실행할 수 있습니다. 로그 전달 구성에 대해 가장 완전한 정보를 보려면 모니터 서버 인스턴스에서 보고서를 보십시오.  
  
 이 보고서에는 모든 로그 전달 작업의 상태가 표시됩니다. 상태는 연결된 서버 인스턴스에서 제공됩니다. 한 데이터베이스에 대해서는 모니터 서버 역할을 하고 다른 데이터베이스에 대해서는 보조 서버 역할을 하는 등 서버 인스턴스가 다양한 역할로 여러 가지 구성과 관련되어 있으면 각 역할과 연관된 모든 구성 정보가 결과에 표시됩니다. 저장 프로시저가 특정한 로그 전달 구성을 위해 모니터 서버 인스턴스에 연결할 수 있으면 보고서에 해당 구성의 추가 상태가 표시됩니다.  
  
 현재 서버 인스턴스에서 수행하는 각 역할에 대해 다음 정보를 볼 수 있습니다.  
  
|역할|표시되는 정보|  
|----------|---------------------------|  
|모니터|이 서버 인스턴스를 모니터 서버로 사용하는 모든 주 서버 및 보조 서버의 이름과 상태|  
|주|주 데이터베이스 각각에 대한 주 데이터베이스 이름 및 주 서버로서 현재 서버 인스턴스의 상태와 이름. 보고서에는 주 서버에 로컬로 저장되어 있는 백업 작업의 상태가 표시됩니다.<br /><br /> 보고서에는 해당되는 각 보조 서버에 대한 행도 포함됩니다. 구성에서 모니터 서버를 사용하고 저장 프로시저가 모니터에 연결할 수 있으면 이러한 행에 최신 로그 백업의 복사 상태 및 복원 상태가 표시됩니다.|  
|보조|보조 데이터베이스 각각에 대한 보조 데이터베이스 이름 및 보조 서버로서 현재 서버 인스턴스의 상태와 이름<br /><br /> 보고서에는 보조 서버에서 수행되는 복사 및 복원 작업의 상태가 표시됩니다.<br /><br /> 보고서에는 해당되는 주 서버에 대한 행도 포함됩니다. 구성에서 모니터 서버를 사용하고 저장 프로시저가 모니터에 연결할 수 있으면 이 행에 최신 로그 백업의 상태가 표시됩니다.|  
  
 표시되는 정보는 서버 인스턴스가 모니터 서버인지, 주 서버인지 또는 보조 서버인지에 따라 다릅니다. 정보를 사용할 수 없으면 해당 셀이 회색으로 나타납니다.  
  
 보고서는 **sp_help_log_shipping_monitor**를 호출하여 데이터를 가져옵니다. 필요한 권한에 대한 자세한 내용은 [sp_help_log_shipping_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql.md)를 참조하세요.  
  
### <a name="to-display-the-transaction-log-shipping-status-report-on-a-server-instance"></a>서버 인스턴스의 트랜잭션 로그 전달 상태 보고서를 표시하려면  
  
1.  모니터 서버, 주 서버 또는 보조 서버에 연결합니다.  
  
2.  개체 탐색기에서 서버 인스턴스를 마우스 오른쪽 단추로 클릭하고 **보고서**를 가리킨 후 **표준 보고서**를 선택합니다.  
  
3.  **트랜잭션 로그 전달 상태**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 모니터링&#40;Transact-SQL&#41;](../../database-engine/log-shipping/monitor-log-shipping-transact-sql.md)  
  
  
