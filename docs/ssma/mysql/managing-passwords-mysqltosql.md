---
title: "암호 (MySQLToSQL) 관리 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Password management, importing or exporting encrypted password
- Password management, securing password
ms.assetid: 4ffbc587-ea3f-49ad-bc42-a654f672325e
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 866254a6a8675e8bbeb017443c66c54a825d0a7d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="managing-passwords-mysqltosql"></a>암호 (MySQLToSQL) 관리
데이터베이스 암호와 가져오기 또는 서버에서 내보내야 하는 절차를 보안에 대 한이 섹션은:  
  
1.  암호 보안  
  
2.  내보내기 또는 암호화 된 암호 가져오기  
  
## <a name="securing-password"></a>암호 보안  
SSMA를 사용 하면 데이터베이스의 암호를 보호할 수 있습니다.  
  
보안 연결을 구현 하려면 다음 절차를 따르십시오.  
  
다음 세 가지 방법 중 하나를 사용 하 여 올바른 암호를 지정 합니다.  
  
1.  **일반 텍스트로:** 'password' 노드의 value 속성에 데이터베이스 암호를 입력 합니다. 스크립트 파일 또는 서버 연결 파일의 서버 섹션에서 서버 정의 노드 아래에서 발견 되었습니다.  
  
    일반 텍스트로 암호가 안전 하지 않습니다. 콘솔 출력에 다음과 같은 경고 메시지가 발생 합니다 따라서: *"서버 &lt;서버 id&gt; 암호가 제공 SSMA 콘솔 응용 프로그램에 안전 하지 않은 일반 텍스트 형식 암호화를 통해 암호를 보호, SSMA 도움말 파일에 대 한 자세한 내용은의 – securepassword 옵션을 참조 하십시오는 옵션을 제공 합니다."*  
  
    **암호화 된 암호:** 이 경우 지정 된 암호가 ProtectedStorage.ssma에서 로컬 컴퓨터에 암호화 된 형태로 저장 됩니다.  
  
    -   **암호를 보호**  
  
        -   실행의 `SSMAforMySQLConsole.exe` 와 `–securepassword` 연결 또는 스크립트 파일의 서버 정의 섹션에서 password 노드를 포함 하는 서버를 전달 하는 명령줄에서 스위치를 추가 합니다.  
  
        -   프롬프트에서 사용자는 데이터베이스 암호를 입력 하 고 확인 하 라는 메시지가 표시 됩니다.  
  
            서버 정의 id 및 해당 하는 암호화 된 암호는 로컬 컴퓨터에 있는 파일에 저장 됩니다.  
            
            예 1:
            
                Specify password
                
                C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            예 2:
            
                C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for MySQL\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx
            
    -   **암호화 된 암호를 제거합니다.**  
  
        실행 된 `SSMAforMySQLConsole.exe` 와`–securepassword` 및 `–remove` 로컬 컴퓨터에 있는 보호 된 저장소 파일에서 암호화 된 암호를 제거 하려면 서버 id를 전달 하는 명령줄에서 전환 합니다.  
  
        예:  

            C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **해당 암호를 암호화 하는 서버 Id를 나열 합니다.**  
  
        실행 된 `SSMAforMySQLConsole.exe` 와 `–securepassword` 및 `–list` 해당 암호가 암호화 된 모든 서버 id를 나열 하려면 명령줄에서 전환 합니다.  
  
        예:  
        
            C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  암호를 일반 텍스트로 서버 또는 연결 파일에 언급 된 보안된 파일에서 암호화 된 암호 보다 우선 합니다.  
    > 2.  암호가 없는 서버 연결 파일 또는 스크립트 파일의 서버 섹션에 있는 경우 또는 로컬 컴퓨터에 보호 하지 콘솔 암호를 입력 하 라는 메시지를 표시 합니다.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>내보내기 또는 암호화 된 암호 가져오기  
SSMA 콘솔 응용 프로그램을 사용 하면 반대로 보안된 파일을 로컬 컴퓨터에서 파일에 있는 암호화 된 데이터베이스 암호를 내보낼 수 있습니다. 독립 암호화 된 암호 컴퓨터를 만들 때의 수 있습니다. 내보내기 기능은 서버 id를 읽고 암호는 로컬 컴퓨터에서 저장소를 보호 하 고 암호화 된 파일에 정보를 저장 합니다. 사용자는 보안된 파일에 대 한 암호를 입력 하 라는 메시지가 표시 됩니다. 입력 한 암호가 8 자 이상 인지 확인 합니다. 이 보안된 파일은 여러 컴퓨터에서 이식 가능 합니다. 가져오기 기능은 보안된 파일에서 서버 id와 암호 정보를 읽습니다. 사용자 보안된 파일에 대 한 암호를 입력 하 라는 메시지가 표시 되 고 보호 된 로컬 저장소에 정보를 추가 합니다.  
  
예:  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforMySQLConsole.EXE –p –e "MySQLDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
예:  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforMySQLConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforMySQLConsole.EXE –p –i "MySQLDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>관련 항목:  
[SSMA 콘솔 (MySQL)를 실행합니다.](http://msdn.microsoft.com/en-us/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
