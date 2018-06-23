---
title: 마스터 서버에 대상 서버 등록 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f51d0175c1d71f9c0dfaed4ea9a38aad14f8e31b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091857"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>마스터 서버에 대상 서버 등록
  이 항목에서는 대상 서버를 다중 서버 관리 구성에 추가하는 방법에 대해 설명합니다. 이 절차는 마스터 서버에서 실행하십시오. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]또는 SMO(SQL Server 관리 개체)를 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 사용되는 Windows 계정이 다중 서버 환경에 미치는 영향에 대한 자세한 내용은 [다중 서버 환경 만들기](create-a-multiserver-environment.md)를 참조하세요.  
  
 전체 SSL(Secure Sockets Layer) 암호화 및 인증서 확인은 기본적으로 마스터 서버와 대상 서버 간 연결에서 사용할 수 있습니다. 자세한 내용은 [대상 서버의 암호화 옵션 설정](set-encryption-options-on-target-servers.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **대상 서버를 등록하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-enlist-a-target-server"></a>대상 서버를 등록하려면  
  
1.  **개체 탐색기**에서 마스터 서버로 구성된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리**를 가리킨 다음 **대상 서버 추가**를 클릭합니다.  
  
3.  전체 프로세스를 안내하는 대상 서버 마법사를 완료합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-enlist-a-target-server"></a>대상 서버를 등록하려면  
  
1.  `sp_msx_enlist` 저장 프로시저를 사용합니다.  자세한 내용은 참조 [sp_msx_enlist &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> SQL Server Management Objects (SMO)를 사용 하 여  
  
## <a name="see-also"></a>관련 항목  
 [기업 내 관리 자동화](automated-administration-across-an-enterprise.md)  
  
  
