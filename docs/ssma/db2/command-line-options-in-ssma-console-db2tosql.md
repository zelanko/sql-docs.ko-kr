---
description: SSMA 콘솔의 명령줄 옵션 (DB2ToSQL)
title: SSMA 콘솔의 명령줄 옵션 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 237354e9-25c4-4386-9d1f-ca0618d4a9a0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5dde1168e8107f01f06d5e60fb2b1853d47abc43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472526"
---
# <a name="command-line-options-in-ssma-console-db2tosql"></a>SSMA 콘솔의 명령줄 옵션 (DB2ToSQL)
Microsoft에서는 SSMA 활동을 실행 하 고 제어 하는 강력한 set 명령줄 옵션을 제공 합니다. 결과 섹션에서 자세히 설명 합니다.  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 콘솔의 명령줄 옵션  
콘솔 명령 옵션에 대해서는 여기에서 설명 합니다.  
  
이 섹션에서는 ' option ' 이라는 용어를 ' 스위치 ' 라고도 합니다.  
  
옵션은 대/소문자를 구분 하지 않으며 ' ' **-** 또는 ' ' 문자로 시작할 수 있습니다 **/** .  
  
옵션이 지정 된 경우 해당 옵션 매개 변수를 지정 해야 합니다.  
  
옵션 매개 변수는 공백으로 구분 해야 합니다.  
  
**구문 예제:**  
  
`C:\> SSMAforDB2Console.EXE -s scriptfile`  
  
`C:\> SSMAforDB2Console.EXE -s "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \AssessmentReportGenerationSample.xml" -v "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \VariableValueFileSample.xml" -c "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ServersConnectionFileSample.xml"`  
  
공백을 포함 하는 폴더 또는 파일 이름은 큰따옴표로 지정 해야 합니다.  
  
명령줄 항목의 출력과 오류 메시지는 STDOUT 또는 지정 된 파일에 저장 됩니다.  
  
### <a name="script-file-option--sscript"></a>스크립트 파일 옵션:-s/스크립트  
필수 스위치, 스크립트 파일 경로/이름은 SSMA에서 실행할 명령 시퀀스의 스크립트를 지정 합니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE -s "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>변수 값 파일 옵션:-v/변수  
이 파일은 스크립트 파일에 사용 된 변수로 구성 됩니다. 이는 선택적 스위치입니다. 변수가 변수 파일에 선언 되지 않고 스크립트 파일에 사용 되는 경우 응용 프로그램은 오류를 생성 하 고 콘솔 실행을 종료 합니다.  
  
**구문 예제:**  
  
-   여러 변수 값 파일에 정의 된 변수 (해당 하는 경우 기본값은 1이 고 다른 하나는 인스턴스별 값) 변수가 중복 된 경우 명령줄 인수에 지정 된 마지막 변수 파일은 기본 설정을 사용 합니다.  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>서버 연결 파일 옵션:-c/serverconnection  
이 파일에는 각 서버에 대 한 서버 연결 정보가 포함 되어 있습니다. 각 서버 정의는 고유한 서버 ID로 식별 됩니다. 서버 Id는 연결 관련 명령에 대 한 스크립트 파일에서 참조 됩니다.  
  
서버 정의는 서버 연결 파일 및/또는 스크립트 파일의 일부일 수 있습니다. 서버 id가 중복 되는 경우 스크립트 파일의 서버 id가 서버 연결 파일 보다 우선적으로 적용 됩니다.  
  
**구문 예제:**  
  
-   서버 Id는 스크립트 파일에 사용 되며 별도의 서버 연결 파일에 정의 됩니다. 서버 연결 파일은 변수 값 파일에 정의 된 변수를 사용 합니다.  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   서버 정의는 스크립트 파일에 포함 되어 있습니다.  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 출력 옵션:-x/xmloutput [xmloutputfile]  
이 명령은 콘솔 또는 xml 파일에 xml 형식의 명령 출력 메시지를 출력 하는 데 사용 됩니다.  
  
Xmloutput에 사용할 수 있는 두 가지 옵션은 시각화입니다.  
  
-   Xmloutput 스위치 뒤에 filepath가 제공 되는 경우 출력이 파일로 리디렉션됩니다.  
  
    **구문 예제:**  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Xmloutput 스위치 다음에 filepath를 제공 하지 않으면 xmloutput이 콘솔 자체에 표시 됩니다.  
  
    **구문 예제:**  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>로그 파일 옵션:-l/log  
콘솔 응용 프로그램의 모든 SSMA 작업은 로그 파일에 기록 됩니다. 이는 선택적 스위치입니다. 로그 파일과 해당 경로가 명령줄에서 지정 된 경우 로그는 지정 된 위치에 생성 됩니다. 그렇지 않으면 기본 위치에 생성 됩니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE`  
  
`"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>프로젝트 환경 폴더 옵션:-e/projectenvironment  
현재 SSMA 프로젝트에 대 한 프로젝트 환경 설정 폴더를 나타냅니다. 이 스위치는 선택 사항입니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE -s`  
  
`"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option--psecurepassword"></a>보안 암호 옵션:-p/securepassword  
이 옵션은 서버 연결에 대 한 암호화 된 암호를 나타냅니다. 다른 모든 옵션과 다릅니다. 옵션은 모든 스크립트를 실행 하거나 마이그레이션 관련 작업을 지원 하지는 않지만 마이그레이션 프로젝트에 사용 되는 서버 연결에 대 한 암호 암호화를 관리 하는 데 도움이 됩니다.  
  
다른 옵션 또는 암호를 명령줄 매개 변수로 입력할 수 없습니다. 그렇지 않으면 오류가 발생 합니다. 자세한 내용은 [암호 관리](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) 섹션을 참조 하세요.  
  
에 대해 지원 되는 하위 옵션은 다음과 `-p/securepassword` 같습니다.  
  
-   지정 된 서버 ID 또는 서버 연결 파일에 정의 된 모든 서버 id에 대해 보호 된 저장소에 암호를 추가 합니다. -Overwrite 옵션이 이미 있는 경우 암호를 업데이트 합니다.  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   지정 된 서버 ID 또는 모든 서버 id의 보호 된 저장소에서 암호화 된 암호를 제거 하려면 다음을 수행 합니다.  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   암호가 암호화 된 서버 Id 목록을 표시 하려면:  
  
    `-p/securepassword -l/list`  
  
-   보호 된 저장소에 저장 된 암호를 암호화 된 파일로 내보냅니다. 이 파일은 사용자 지정 암호문으로 암호화 됩니다.  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   이전에 내보낸 암호화 된 파일을 사용자 지정 암호문을 사용 하 여 로컬 보호 된 저장소로 가져옵니다. 해독 된 파일은 새 파일에 저장 된 후 로컬 컴퓨터에서 암호화 됩니다.  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    쉼표 구분 기호를 사용 하 여 여러 서버 Id를 지정할 수 있습니다.  
  
### <a name="help-option--help"></a>도움말 옵션:-?/Help  
SSMA 콘솔 옵션의 구문 요약 정보를 표시 합니다.  
  
`C:\>SSMAforDB2Console.EXE -?`  
  
SSMA 콘솔 명령줄 옵션이 표 형식으로 표시 되는 경우 [부록-1 &#40;DB2ToSQL&#41;](../../ssma/db2/appendix-1-db2tosql.md)를 참조 하세요.  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword 도움말 옵션:-securepassword-?/Help  
SSMA 콘솔 옵션의 구문 요약 정보를 표시 합니다.  
  
`C:\>SSMAforDB2Console.EXE -securepassword -?`  
  
SSMA 콘솔 명령줄 옵션이 표 형식으로 표시 되는 경우 [부록-1 &#40;DB2ToSQL](../../ssma/db2/appendix-1-db2tosql.md) 를 참조 하세요&#41;  
  
### <a name="next-step"></a>다음 단계  
다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
1.  암호 또는 내보내기/가져오기 암호를 지정 하려면 [DB2ToSQL&#41;&#40;암호 관리 ](../../ssma/db2/managing-passwords-db2tosql.md)를 참조 하세요.  
  
2.  보고서를 생성 하려면 [DB2ToSQL&#41;&#40;보고서 생성 ](../../ssma/db2/generating-reports-db2tosql.md)을 참조 하세요.  
  
3.  콘솔의 문제 해결에 대해서는 [문제 해결 &#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md)을 참조 하세요.  
  
