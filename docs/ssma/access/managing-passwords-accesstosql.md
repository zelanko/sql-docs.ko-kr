---
title: 암호 관리 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/01/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0023e6d04b2f339fbd67337b7b241da2df275a79
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938047"
---
# <a name="managing-passwords-accesstosql"></a>암호 관리 (AccessToSQL)
이 섹션에서는 데이터베이스 암호를 보호 하는 방법과 서버에서 데이터베이스를 가져오거나 내보내는 절차에 대해 설명 합니다.  
  
1.  암호 보안  
  
2.  암호화 된 암호 내보내기 또는 가져오기  
  
## <a name="securing-password"></a>암호 보안  
SSMA를 사용 하면 데이터베이스의 암호를 보호할 수 있습니다.  
  
다음 절차를 사용 하 여 보안 연결을 구현 합니다.  
  
다음 세 가지 방법 중 하나를 사용 하 여 올바른 암호를 지정 합니다.  
  
1.  **텍스트 지우기:** ' 암호 ' 노드의 값 특성에 데이터베이스 암호를 입력 합니다. 스크립트 파일 또는 서버 연결 파일의 서버 섹션에서 서버 정의 노드 아래에 있습니다.  
  
    일반 텍스트의 암호는 안전 하지 않습니다. 따라서 콘솔 출력에 다음과 같은 경고 메시지가 표시 됩니다. *"서버 &lt; 서버-id &gt; 암호는 비보안 일반 텍스트 형식으로 제공 됩니다. ssma 콘솔 응용 프로그램은 암호화를 통해 암호를 보호 하는 옵션을 제공 합니다. 자세한 내용은 ssma 도움말 파일에서-securepassword 옵션을 참조 하세요."*  
  
    **암호화 된 암호:** 이 경우 지정 된 암호는 ProtectedStorage의 로컬 컴퓨터에 암호화 된 형식으로 저장 됩니다.  
  
    -   **암호 보안**  
  
        -   를 사용 하 여를 실행 `SSMAforAccessConsole.exe` `-securepassword` 하 고 명령줄에 스위치를 추가 하 여 서버 정의 섹션에서 password 노드를 포함 하는 서버 연결 또는 스크립트 파일을 전달 합니다.  
  
        -   메시지가 표시 되 면 사용자에 게 데이터베이스 암호를 입력 하 고 확인 하 라는 메시지가 표시 됩니다.  
  
            서버 정의 id와 해당 암호화 된 암호가 로컬 컴퓨터의 파일에 저장 됩니다.  

            &nbsp;

            _예제 1:_
            
            암호 지정

            ```console
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
            ```

            ' XXX_1 ' server_id에 대 한 암호 입력: xxxxxxx
                
            ' XXX_1 ' server_id에 대 한 암호를 다시 입력: xxxxxxx  

            &nbsp;

            _예 2:_

            ```console
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
            ```

            ' Source_1 ' server_id에 대 한 암호 입력: xxxxxxx
                
            ' Source_1 ' server_id에 대 한 암호를 다시 입력: xxxxxxx
                
            ' Target_1 ' server_id에 대 한 암호 입력: xxxxxxx
                
            ' Target _1 ' server_id에 대 한 암호를 다시 입력: xxxxxxx  
  
    -   **암호화 된 암호 제거**  
  
        를 사용 하 여를 실행 하 `SSMAforAccessConsole.exe` `-securepassword` 고 `-remove` 명령줄에서 서버 id를 전달 하는 스위치를 사용 하 여 로컬 컴퓨터에 있는 보호 된 저장소 파일에서 암호화 된 암호를 제거 합니다.  

        ```console
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove all
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove "source_1,target_1"
        ```
  
    -   **암호가 암호화 된 서버 Id 나열**  
  
        를 사용 하 여 SSMAforAccessConsole.exe를 실행 하 `-securepassword` 고 `-list` 명령줄에서 스위치를 실행 하 여 암호가 암호화 된 모든 서버 id를 나열 합니다.  

        ```console
        C:\SSMA\SSMAforAccessConsole.EXE -securepassword -list
        ```
  
    > [!NOTE]  
    > 1.  스크립트 또는 서버 연결 파일에 언급 된 일반 텍스트의 암호는 보안 파일의 암호화 된 암호 보다 우선 적용 됩니다.  
    > 2.  서버 연결 파일이 나 스크립트 파일의 서버 섹션에 암호가 없거나 로컬 컴퓨터에서 보안이 유지 되지 않은 경우에는 콘솔에 암호를 입력 하 라는 메시지가 표시 됩니다.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>암호화 된 암호 내보내기 또는 가져오기  
SSMA 콘솔 응용 프로그램을 사용 하면 로컬 컴퓨터의 파일에 있는 암호화 된 데이터베이스 암호를 보안 파일로 내보낼 수 있으며 그 반대의 경우도 마찬가지입니다. 암호화 된 암호를 컴퓨터와 독립적으로 만드는 데 도움이 됩니다. 내보내기 기능은 로컬에서 보호 되는 저장소에서 서버 id와 암호를 읽고 암호화 된 파일에 정보를 저장 합니다. 사용자에 게 보안 파일에 대 한 암호를 입력 하 라는 메시지가 표시 됩니다. 입력 한 암호가 8 자 길이 이상 인지 확인 합니다. 이 보안 파일은 여러 컴퓨터에서 이식할 수 있습니다. 가져오기 기능은 보안 파일에서 서버 id와 암호 정보를 읽습니다. 사용자에 게 보안 파일에 대 한 암호를 입력 하 라는 메시지가 표시 되 면 보호 된 로컬 저장소에 정보가 추가 됩니다.  

### <a name="export-password"></a>암호 내보내기

1. 내보낸 파일을 보호 하는 데 사용할 암호 입력

2. `C:\SSMA\SSMAforAccessConsole.EXE -securepassword -export all "machine1passwords.file"`

3. 내보낸 파일을 보호 하는 데 사용할 암호 입력: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

4. 암호를 확인 하세요.

5. `C:\SSMA\SSMAforAccessConsole.EXE -p -e "AccessDB_1_1,Sql_1" "machine2passwords.file"`

6. 내보낸 파일을 보호 하는 데 사용할 암호 입력: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

7. 암호를 확인 하세요.  

### <a name="import-an-encrypted-password"></a>암호화 된 암호 가져오기

1. 가져온 파일을 보호 하는 데 사용할 암호 입력

2. `C:\SSMA\SSMAforAccessConsole.EXE -securepassword -import all "machine1passwords.file"`

3. 암호화 된 파일에서 서버를 가져오려면 암호 입력: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

4. 암호를 확인 하세요.

5. `C:\SSMA\SSMAforAccessConsole.EXE -p -i "AccessDB_1,Sql_1" "machine2passwords.file"`

6. 암호화 된 파일에서 서버를 가져오려면 암호 입력: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

7. 암호를 확인 하세요.  

## <a name="see-also"></a>참고 항목  
[SSMA 콘솔 실행 (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
