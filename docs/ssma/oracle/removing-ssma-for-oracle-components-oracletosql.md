---
title: SSMA 용 Oracle 구성 요소 제거 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da54f9fc21b74be790ac86c9690738b71fd3e1c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672912"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Oracle용 SSMA 구성 요소 제거(OracleToSQL)
완료 했을 때 Oracle에서 데이터베이스를 마이그레이션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 확장 팩을 제거 하면 안 되는 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 데이터베이스의 함수를 더 이상 사용 하지 않는 한는 **ssma_oracle** 의 스키마를 **sysdb** 데이터베이스입니다.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>SSMA는 Oracle 클라이언트에 대 한 제거  
SSMA를 사용 하 여 제거할 수 있습니다 **프로그램 추가 / 제거**합니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 SSMA를 제거 하려면 클릭 하십시오 **예**합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩을 제거  
마이그레이션된 데이터베이스의 개체를 사용 하지 마십시오 확실 합니다 **sysdb.ssma_oracle** 스키마를 사용 하 여 확장 팩을 제거할 수 있습니다 **프로그램 추가 / 제거**.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판에서 엽니다 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Oracle 확장 팩**를 클릭 하 고 **제거**합니다.  
  
3.  확인 하려면 확장 팩을 제거 하려면 클릭 하십시오 **예**합니다.  
  
4.  인스턴스에서 유틸리티 데이터베이스 스크립트 페이지를 사용 하 여 인스턴스를 선택 하 고 클릭 **다음**합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 클릭 **다음**합니다.  
  
    Windows 인증 Windows 자격 증명을 사용 하 여 인스턴스의 로그온 하려고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 입력 해야 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호입니다.  
  
6.  작업이 완료 페이지에서 클릭 **확인**합니다.  
  
7.  마침 페이지에서 클릭 **종료**합니다.  
  
제거 후 확인할 수 있습니다 하는 개체를 **sysdb.ssma_oracle** 스키마 및 전체 **sysdb** 데이터베이스를 사용 하 여 제거 되었습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 그러나 다른 SSMA 제품을 사용 하는 경우도 사용 합니다 **sysdb** 데이터베이스입니다. 데이터베이스 존재 하 고 다른 데이터베이스가이 데이터베이스에서 개체 참조는 확신을 하는 경우에 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[Oracle 클라이언트 용 SSMA 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server에 SSMA 구성 요소를 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
