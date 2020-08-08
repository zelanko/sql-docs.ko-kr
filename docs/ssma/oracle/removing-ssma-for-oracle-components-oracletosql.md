---
title: Oracle 용 SSMA 구성 요소 제거 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 4fbac66cfd7cf549a6321534901ca8a33900f986
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933154"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Oracle용 SSMA 구성 요소 제거(OracleToSQL)
Oracle에서로 데이터베이스 마이그레이션을 완료 한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션된 데이터베이스가 **sysdb** 데이터베이스의 **ssma_oracle** 스키마에서 함수를 더 이상 사용 하지 않는 경우에는에서 확장 팩을 제거 하면 안 됩니다.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Oracle 용 SSMA 클라이언트 제거  
**프로그램 추가/제거**를 사용 하 여 ssma를 제거할 수 있습니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 **프로그램 추가 또는 제거**를 엽니다.  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle의 Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  SSMA를 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩 제거  
마이그레이션된 데이터베이스가 **sysdb. ssma_oracle** 스키마의 개체를 사용 하지 않는 경우 **프로그램 추가/제거**를 사용 하 여 확장 팩을 제거할 수 있습니다.  
  
**확장 팩을 제거 하려면**  
  
1.  제어판에서 **프로그램 추가 또는 제거**를 엽니다.  
  
2.  **Oracle 확장 팩의 Microsoft SQL Server Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  확장 팩을 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
4.  유틸리티 데이터베이스 스크립트를 사용 하는 인스턴스 페이지에서 인스턴스를 선택 하 고 **다음**을 클릭 합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.  
  
    Windows 인증에서는 Windows 자격 증명을 사용 하 여 인스턴스에 로그온을 시도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증을 선택 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이름 및 암호를 입력 해야 합니다.  
  
6.  작업 완료 페이지에서 **확인**을 클릭 합니다.  
  
7.  마침 페이지에서 **끝내기**를 클릭 합니다.  
  
제거 후에는를 사용 하 여 **ssma_oracle** 스키마 및 전체 **sysdb** 데이터베이스의 개체가 제거 되었는지 확인할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . 그러나 다른 SSMA 제품을 사용 하는 경우 **sysdb** 데이터베이스도 사용 합니다. 데이터베이스가 있고 다른 데이터베이스에서이 데이터베이스의 개체를 참조 하지 않는 경우 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 용 SSMA 클라이언트 &#40;설치 OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server &#40;OracleToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
