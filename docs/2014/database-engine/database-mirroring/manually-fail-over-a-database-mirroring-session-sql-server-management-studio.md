---
title: 데이터베이스 미러링 세션 수동 장애 조치(SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 4ecf9c63-b3a4-4c54-b553-5bc37973232b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b42fdb9d53a4aa0444a98ee311000fb1c2929ff1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62756163"
---
# <a name="manually-fail-over-a-database-mirroring-session-sql-server-management-studio"></a>데이터베이스 미러링 세션 수동 장애 조치(failover)(SQL Server Management Studio)
  미러된 데이터베이스가 동기화되면, 즉 데이터베이스가 SYNCHRONIZED 상태인 경우 데이터베이스 소유자가 미러 서버에 수동 장애 조치(failover)를 시작할 수 있습니다.  
  
 수동 장애 조치 중에는 장애 조치가 발생하는 데이터베이스에 대해 주 서버와 미러 서버 역할이 바뀝니다. 미러 데이터베이스는 주 데이터베이스가 되고 주 데이터베이스는 미러 데이터베이스가 됩니다. 예를 들어, 다음 표에서는 수동 장애 조치가 두 개의 미러링 파트너인 `SQLDBENGINE0_1` 및 `SQLDBENGINE0_2`의 역할을 바꾸는 방법을 보여 줍니다.  
  
|서버|장애 조치 이전|장애 조치 이후|  
|------------|---------------------|--------------------|  
|`SQLDBENGINE0_1`|PRINCIPAL|MIRROR|  
|`SQLDBENGINE0_2`|MIRROR|PRINCIPAL|  
  
 다른 데이터베이스 미러링 세션의 서버 역할은 영향을 받지 않습니다. 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.  
  
### <a name="to-manually-fail-over-database-mirroring"></a>데이터베이스 미러링에 수동으로 장애 조치를 수행하려면  
  
1.  주 서버 인스턴스에 연결한 다음 **개체 탐색기** 창에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 장애 조치를 수행할 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  **장애 조치**를 클릭합니다.  
  
     확인 상자가 나타납니다.  먼저 주 서버가 Windows 인증을 사용하여 미러 서버에 대한 연결을 시도합니다. Windows 인증을 사용할 수 없는 경우 주 서버는 **서버에 연결** 대화 상자를 표시합니다. 미러 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 **인증** 상자에서 **SQL Server 인증** 을 선택합니다. **로그인** 입력란에 미러 서버에서 연결에 사용할 로그인 계정을 지정하고 **암호** 입력란에 해당 계정의 암호를 지정합니다.  
  
     장애 조치가 성공할 경우 **데이터베이스 속성** 대화 상자가 닫힙니다. 미러 데이터베이스는 주 데이터베이스가 되고 주 데이터베이스는 미러 데이터베이스가 됩니다.  
  
     장애 조치가 실패할 경우 오류 메시지가 표시되고 대화 상자는 열린 상태로 유지됩니다.  
  
    > [!IMPORTANT]  
    >  **미러링** 페이지를 연 이후 속성을 수정한 경우에는 해당 변경 내용이 저장되지 않습니다.  
  
     대화 상자가 자동으로 닫힙니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [데이터베이스 미러링 세션 수동 장애 조치&#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md)   
 [데이터베이스 미러링 세션 일시 중지 또는 재개&#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
  
