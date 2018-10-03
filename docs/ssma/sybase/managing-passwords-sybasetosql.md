---
title: 암호 관리 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Exporting or Importing Encrypted Passwords
- Sybase Console,Managing Passwords
- Sybase Console,Securing Password
ms.assetid: 9b6a70f9-6840-4140-a059-bb7bd7ccc67c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 44d322b0be32c362aba34b243a643bbe7bcd10fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847261"
---
# <a name="managing-passwords-sybasetosql"></a>암호 관리(SybaseToSQL)
데이터베이스 암호와 가져오기 또는 서버에서 내보내야 하는 절차를 보호 하는 방법에 대 한이 섹션은:  
  
1.  암호 보안  
  
2.  암호화 된 암호를 가져오거나 내보내기  
  
## <a name="securing-password"></a>암호 보안  
SSMA를 사용 하면 데이터베이스의 암호를 보호할 수 있습니다.  
  
보안 연결을 구현 하려면 다음 절차를 따르십시오.  
  
다음 세 가지 방법 중 하나를 사용 하 여 올바른 암호를 지정 합니다.  
  
1.  **일반 텍스트로:** 'password' 노드의 값 특성에서 데이터베이스 암호를 입력 합니다. 찾은 스크립트 파일 또는 서버 연결 파일의 서버 섹션에서 서버 정의 노드에서 합니다.  
  
    일반 텍스트로 암호 보호 되지 않습니다. 따라서 다음과 같은 경고 메시지가 콘솔 출력에 나타나는: *"Server &lt;서버 id&gt; 암호가 안전 하지 않은 일반 텍스트 형태로 SSMA 콘솔 응용 프로그램에서는 보호 하는 옵션이 제공 합니다 암호화를 통해 암호 하세요 – securepassword 옵션이 표시 SSMA의 도움말 파일에 대 한 자세한 내용은. "*  
  
    **암호화 된 암호:** 이 경우 지정된 된 암호 ProtectedStorage.ssma에서 로컬 컴퓨터의 암호화 된 형태로 저장 됩니다.  
  
    -   **암호를 보호 하기**  
  
        -   실행 합니다 `SSMAforSybaseConsole.exe` 사용 하 여를 `–securepassword` 서버 서버 정의 섹션에서 암호 노드를 포함 하는 연결 또는 스크립트 파일을 전달 하는 명령줄에서 스위치를 추가 합니다.  
  
        -   프롬프트에서 사용자는 데이터베이스 암호를 입력 하 고 확인 하 라는 메시지가 표시 됩니다.  
  
            서버 정의 id 및 해당 하는 암호화 된 암호는 로컬 컴퓨터의 파일에 저장 됩니다.  
            
            예 1:  
            
                Specify password
                
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            예 2:
            
                C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Sybase\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **암호화 된 암호를 제거합니다.**  
  
        실행 된 `SSMAforSybaseConsole.exe` 사용 하 여는`–securepassword` 및 `–remove` 로컬 컴퓨터에 있는 보호 된 저장소 파일에서 암호화 된 암호를 제거 하는 서버 id를 전달 하는 명령줄에서 전환 합니다.  
  
        예:  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **해당 암호를 암호화 하는 서버 Id를 나열 합니다.**  
  
        실행 된 `SSMAforSybaseConsole.exe` 사용 하 여는 `–securepassword` 및 `–list` 암호 암호화 된 모든 서버 id를 나열 하려면 명령줄에서 전환 합니다.  
  
        예:  
        
            C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  스크립트 또는 서버 연결 파일에 언급 된 일반 텍스트로 암호 보안 된 파일의 암호화 된 암호 보다 우선 합니다.  
    > 2.  암호 없이 서버 연결 파일 또는 스크립트 파일의 서버 섹션에 있는 경우 또는 로컬 컴퓨터에 보안 되지 콘솔 암호를 입력 하 라는 메시지를 표시 합니다.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>암호화 된 암호를 가져오거나 내보내기  
SSMA 콘솔 응용 프로그램을 사용 하면 반대로 보안된 파일을 로컬 컴퓨터의 파일에 있는 암호화 된 데이터베이스 암호를 내보낼 수 있습니다. 독립 암호화 된 암호가 컴퓨터를 만들 수 있습니다. 내보내기 기능은 서버 id를 읽고 로컬에서 암호 저장소를 보호 하 고 암호화 된 파일에 정보를 저장 합니다. 사용자는 보안된 파일에 대 한 암호를 입력 하 라는 메시지가 표시 됩니다. 입력 한 암호가 8 자 이상 인지 확인 합니다. 이 보안된 파일은 서로 다른 컴퓨터에서 이식 가능 합니다. 가져오기 기능은 보안된 파일에서 서버 id와 암호 정보를 읽습니다. 사용자 보안된 파일에 대 한 암호를 입력 하 라는 메시지가 표시 되 고 로컬 보호 된 저장소에 정보를 추가 합니다.  
  
예:  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –e "SybaseDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
예:  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforSybaseConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforSybaseConsole.EXE –p –i "SybaseDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>관련 항목  
[SSMA 콘솔 (Sybase) 실행](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
