---
title: SSMA Sybase 구성 요소 (SybaseToSQL)에 대 한 제거 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
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
ms.openlocfilehash: 4b0eec2884ce2a1a0e16009101068520e2b46acf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>SSMA Sybase 구성 요소 (SybaseToSQL)에 대 한 제거
완료 했을 때에서 Sybase 적응형 Server Enterprise (ASE)에 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 구성 요소를 제거 해야 할 경우가 있습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있지만 데이터베이스 엔진이 제거해 서는 안 확장 팩에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션된 데이터베이스의 함수를 더 이상 사용 하는 경우가 아니면는 **ssma_syb** 의 스키마는 **sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>SSMA는 Sybase 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Sybase**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 하려는 경우에 **sysdb.ssma_syb** 스키마를 사용 하 여 확장 팩을 제거할 수 **프로그램 추가 / 제거**합니다.  
  
확장 팩을 제거 하려면  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Sybase 확장 팩**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  인스턴스에서 유틸리티 데이터베이스 스크립트 페이지를 클릭 하 여 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증의 SQL Server 인스턴스에 로그온 할를 Windows 자격 증명을 사용 합니다. SQL Server 인증을 선택 하면 SQL Server 로그인 이름과 암호를 입력 해야 합니다.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  완료 페이지에서 클릭 **종료**합니다.  
  
를 제거한 후 되는지 확인할 수 있습니다는 **sysdb.ssma_syb** 스키마 및 전체 **sysdb** , 데이터베이스를 사용 하 여 제거 된 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우 사용 된 **sysdb** 데이터베이스입니다. 데이터베이스가 존재 하는 경우 다른 데이터베이스가이 데이터베이스에서 개체를 참조 하는지 확인 했으면 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[SSMA Sybase 클라이언트에 대 한 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
