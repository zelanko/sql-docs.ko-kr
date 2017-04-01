---
title: "sqlcmd 유틸리티 시작 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 41
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# sqlcmd 유틸리티 시작
    
> [!NOTE]  
>  **sqlcmd**에 대한 기본 인증 모드는 Windows 인증입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하려면 **-U** 및 **-P** 옵션을 사용하여 사용자 이름과 암호를 지정해야 합니다.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]는 명명된 인스턴스인 **sqlexpress**로 설치됩니다.  
  
### sqlcmd 유틸리티를 시작하고 SQL Server의 기본 인스턴스에 연결  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다. **열기** 상자에 **cmd**를 입력한 다음 **확인** 을 클릭하여 명령 프롬프트 창을 엽니다. 이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결한 적이 없는 경우 연결을 허용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성해야 할 수 있습니다.  
  
2.  명령 프롬프트에서 **sqlcmd**을(를) 입력합니다.  
  
3.  Enter 키를 누릅니다.  
  
     이제 트러스트된 연결을 사용하여 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에 연결되었습니다.  
  
     **1>**은 줄 번호를 지정하는 **sqlcmd** 프롬프트입니다. Enter 키를 누를 때마다 번호가 1씩 증가합니다.  
  
4.  **sqlcmd** 세션을 종료하려면 **sqlcmd** 프롬프트에 **EXIT** 을(를) 입력합니다.  
  
### sqlcmd 유틸리티를 시작하고 SQL Server의 명명된 인스턴스에 연결  
  
1.  명령 프롬프트 창을 열고 **sqlcmd -S***myServer\instanceName*을 입력합니다. *myServer\instanceName*을 연결하려는 컴퓨터 이름 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 바꿉니다.  
  
2.  Enter 키를 누릅니다.  
  
     **sqlcmd** 프롬프트(1>)에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 지정된 인스턴스에 연결되었다고 표시됩니다.  
  
    > [!NOTE]  
    >  입력한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 버퍼에 저장되며 GO 명령이 발견되면 일괄 처리로 실행됩니다.  
  
## 참고 항목  
 [sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행](../../relational-databases/scripting/run-transact-sql-script-files-using-sqlcmd.md)  
  
  