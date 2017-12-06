---
title: "SSMA Oracle 구성 요소 (OracleToSQL)에 대 한 제거 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: ef4562dfbb3551edcb921cf4850ed002c55db978
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>SSMA Oracle 구성 요소 (OracleToSQL)에 대 한 제거
완료 했을 때 Oracle에서 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA 구성 요소를 제거 해야 할 경우가 있습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나 제거해 서는 안에서 확장 팩 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 마이그레이션된 데이터베이스의 함수를 더 이상 사용 하지 않는 한는 **ssma_oracle** 의 스키마는 **sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>SSMA는 Oracle 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Oracle**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 하려는 경우에 **sysdb.ssma_oracle** 스키마를 사용 하 여 확장 팩을 제거할 수 **프로그램 추가 / 제거**합니다.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판을 열고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Oracle 확장 팩**, 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  인스턴스에서 데이터베이스 스크립트 유틸리티 페이지와 인스턴스를 선택 하 고 클릭 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의에 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 입력 해야 인증을 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인 이름 및 암호.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  완료 페이지에서 클릭 **종료**합니다.  
  
후 제거, 확인할 수 있습니다 하는 개체에 **sysdb.ssma_oracle** 스키마 및 전체 **sysdb** , 데이터베이스를 사용 하 여 제거 된 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우 사용 된 **sysdb** 데이터베이스입니다. 데이터베이스가 존재 하는 경우 다른 데이터베이스가이 데이터베이스에서 개체를 참조 하는지 확인 했으면 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[Oracle 클라이언트 &#40; OracleToSQL &#41; 용 SSMA를 설치합니다.](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server &#40; OracleToSQL &#41;에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
