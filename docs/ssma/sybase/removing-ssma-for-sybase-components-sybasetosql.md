---
title: Sybase 구성 요소 (SybaseToSQL) 용 SSMA 제거 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6e676ff9adb8d098cf795d7599788bcfa3d0f515
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393261"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Sybase용 SSMA 구성 요소 제거(SybaseToSQL)
완료 했을 때에서 Sybase 적응형 Server Enterprise (ASE)에 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지, 클라이언트 구성 요소를 제거할 수 있지만 확장 팩에서 제거 하면 안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 아니라면 마이그레이션된 데이터베이스의 함수는 더 이상 사용 해야 합니다 **ssma_syb** 는의스키마**sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>SSMA는 Sybase 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Sybase**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 확실 합니다 **sysdb.ssma_syb** 스키마를 사용 하 여 확장 팩을 제거할 수 있습니다 **프로그램 추가 / 제거**.  
  
확장 팩을 제거 하려면  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Sybase 확장 팩**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  유틸리티 데이터베이스 스크립트 페이지를 사용 하 여 인스턴스를 클릭 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 SQL Server 인스턴스에 로그온 하려고 됩니다. SQL Server 인증을 선택 하면 SQL Server 로그인 이름과 암호를 입력 해야 합니다.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  마침 페이지에서 클릭 **종료**합니다.  
  
를 제거한 후를 확인할 수 있습니다 합니다 **sysdb.ssma_syb** 스키마 및 전체 **sysdb** 데이터베이스를 사용 하 여 제거 되었습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우도 사용 합니다 **sysdb** 데이터베이스입니다. 데이터베이스 존재 하 고 다른 데이터베이스가이 데이터베이스에서 개체 참조는 확신을 하는 경우에 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[클라이언트 Sybase 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server에 SSMA 구성 요소를 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
