---
title: 확장 저장 프로시저의 실행 특징
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 74ecd20f28e58e133b5710d3cbd9d18b27ca7756
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095984"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>확장 저장 프로시저의 실행 특징
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저 실행에는 다음과 같은 세 가지 특징이 있습니다.  
  
-   확장 저장 프로시저 함수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 보안 컨텍스트에서 실행 됩니다.  
  
-   확장 저장 프로시저 함수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 공간에서 실행됩니다.  
  
-   확장 저장 프로시저 실행과 연결되는 스레드는 클라이언트 연결에 사용되는 스레드와 같은 것입니다.  
  
    > [!IMPORTANT]  
    >  시스템 관리자는 확장 저장 프로시저를 서버에 추가하고 다른 사용자에게 실행 권한을 부여하기 전에 각 확장 저장 프로시저를 철저히 검토하여 유해 코드 또는 악성 코드가 포함되어 있는지 확인해야 합니다.  
  
-  
  
 확장 저장 프로시저 DLL이 로드 된 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 중지 될 때까지 DLL이 서버의 주소 공간에 로드 된 상태로 유지 되거나 관리자가 DBCC *DLL_name* (무료)를 사용 하 여 dll을 명시적으로 언로드합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 EXECUTE 문을 사용하여 확장 저장 프로시저를 저장 프로시저처럼 사용할 수 있습니다.  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>매개 변수  
 \@ *retval*  
 반환 값입니다.  
  
 \@ *param1*  
 입력 매개 변수입니다.  
  
 \@ *param2*  
 입/출력 매개 변수입니다.  
  
> [!CAUTION]  
>  확장 저장 프로시저는 성능 향상과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 확장을 제공합니다. 그러나 확장 저장 프로시저 DLL과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 같은 주소 공간을 공유하므로 문제가 있는 프로시저가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작동에 부정적인 영향을 줄 수 있습니다. 확장 저장 프로시저 DLL에서 throw하는 예외는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 처리되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 영역에 손상을 줄 수 있습니다. 보안 예방 조치로서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자만 확장 저장 프로시저를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 추가할 수 있습니다. 이러한 프로시저는 설치하기 전에 철저히 테스트해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [확장 저장 프로시저 프로그래밍](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [SQL Server에 설치된 확장 저장 프로시저 쿼리](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
