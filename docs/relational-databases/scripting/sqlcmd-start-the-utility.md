---
title: "sqlcmd 유틸리티 시작 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: f7e35bb04d5ff169800d837b05a63320640adeff
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcmd---start-the-utility"></a>sqlcmd - 유틸리티 시작
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)를 사용하면 명령 프롬프트, SQLCMD 모드의 쿼리 편집기, Windows 스크립트 파일 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 운영 체제(Cmd.exe) 작업 단계에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.
> [!NOTE]  
>  **sqlcmd**에 대한 기본 인증 모드는 Windows 인증입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하려면 **-U** 및 **-P** 옵션을 사용하여 사용자 이름과 암호를 지정해야 합니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 는 명명된 인스턴스인 **sqlexpress**로 설치됩니다.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>sqlcmd 유틸리티를 시작하고 SQL Server의 기본 인스턴스에 연결  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다. **열기** 상자에 **cmd**를 입력한 다음 **확인** 을 클릭하여 명령 프롬프트 창을 엽니다. 이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결한 적이 없는 경우 연결을 허용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성해야 할 수 있습니다.  
  
2.  명령 프롬프트에서 **sqlcmd**을(를) 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
     이제 트러스트된 연결을 사용하여 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에 연결되었습니다.  
  
     **1>**은 줄 번호를 지정하는 **sqlcmd** 프롬프트입니다. Enter 키를 누를 때마다 번호가 1씩 증가합니다.  
  
4.  **sqlcmd** 세션을 종료하려면 **sqlcmd** 프롬프트에 **EXIT** 을(를) 입력합니다.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>sqlcmd 유틸리티를 시작하고 SQL Server의 명명된 인스턴스에 연결  
  
1.  명령 프롬프트 창을 열고 **sqlcmd -S***myServer\instanceName*을 입력합니다. *myServer\instanceName* 을 연결하려는 컴퓨터 이름 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 바꿉니다.  
  
2.  Enter 키를 누릅니다.  
  
     **sqlcmd** 프롬프트(1>)에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 지정된 인스턴스에 연결되었다고 표시됩니다.  
  
    > [!NOTE]  
    >  입력한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 버퍼에 저장되며 GO 명령이 발견되면 일괄 처리로 실행됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행](../../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)  
  
  
