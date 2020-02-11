---
title: Sybase 용 SSMA 구성 요소 제거 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0c76b6b2e4e5295bf7db2d7857a73223fc6f8c7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028646"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Sybase용 SSMA 구성 요소 제거(SybaseToSQL)
Sybase ASE (적응 서버 엔터프라이즈)에서로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스를 마이그레이션한 후에는 ssma 구성 요소를 제거 하는 것이 좋습니다. 언제 든 지 클라이언트 구성 요소를 제거할 수 있지만, 마이그레이션된 데이터베이스가 **sysdb** 데이터베이스의 **ssma_syb** 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 함수를 더 이상 사용 하지 않을 경우에는에서 확장 팩을 제거 하면 안 됩니다.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Sybase 클라이언트용 SSMA 제거  
**프로그램 추가/제거**를 사용 하 여 ssma를 제거할 수 있습니다.  
  
**SSMA를 제거 하려면**  
  
1.  제어판에서 **프로그램 추가/제거**를 엽니다.  
  
2.  **Sybase에 Microsoft SQL Server Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  SSMA를 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
## <a name="uninstalling-the-extension-pack"></a>확장 팩 제거  
마이그레이션된 데이터베이스가 **sysdb. ssma_syb** 스키마의 개체를 사용 하지 않는 경우 **프로그램 추가/제거**를 사용 하 여 확장 팩을 제거할 수 있습니다.  
  
확장 팩을 제거 하려면  
  
1.  제어판에서 **프로그램 추가/제거**를 엽니다.  
  
2.  **Sybase 확장 팩의 Microsoft SQL Server Migration Assistant**을 선택 하 고 **제거**를 클릭 합니다.  
  
3.  확장 팩을 제거할 것인지 확인 하려면 **예**를 클릭 합니다.  
  
4.  유틸리티 데이터베이스 스크립트를 사용 하는 인스턴스 페이지에서 **다음**을 클릭 합니다.  
  
5.  연결 매개 변수 페이지에서 인증 방법을 선택 하 고 **다음**을 클릭 합니다.  
  
    Windows 인증은 SQL Server 인스턴스에 로그온 하는 데 Windows 자격 증명을 사용 합니다. SQL Server 인증을 선택 하는 경우 SQL Server 로그인 이름 및 암호를 입력 해야 합니다.  
  
6.  작업 완료 페이지에서 **확인**을 클릭 합니다.  
  
7.  마침 페이지에서 **끝내기**를 클릭 합니다.  
  
을 제거한 후에는를 사용 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하 여 **sysdb ssma_syb** 스키마 및 전체 **sysdb** 데이터베이스가 제거 되었는지 확인할 수 있습니다. 그러나 다른 SSMA 제품을 사용 하는 경우 **sysdb** 데이터베이스도 사용 합니다. 데이터베이스가 있고 다른 데이터베이스에서이 데이터베이스의 개체를 참조 하지 않는 경우 데이터베이스를 분리할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[Sybase 용 SSMA 클라이언트 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server &#40;SybaseToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
