---
title: SSMA 콘솔 (AccessToSQL)의 명령줄 옵션 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: fc8065bcfda3066fae31be982e25f054c07bca3a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532014"
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>SSMA 콘솔 (AccessToSQL)의 명령줄 옵션
Microsoft는 강력한 명령줄 옵션을 실행 하 고 제어 SSMA 작업 집합을 제공 합니다. 결과 섹션 추가 세부 정보를 제공합니다.  
  
## <a name="command-line-options-in-the-ssma-console"></a>SSMA 콘솔의 명령줄 옵션  
여기에 설명 된은 콘솔 명령 옵션입니다.  
  
이 섹션 'option' 용어는 또한 'switch' 라고 합니다.  
  
옵션 대/소문자 구분 하지 않으며 사용 하 여 시작할 수는 '**-**'또는'**/**' 문자입니다.  
  
옵션을 지정 하는 경우에 해당 옵션 매개 변수를 지정 하는 필수입니다.  
  
옵션 매개 변수는 옵션 문자에서 공백으로 구분 되어야 합니다.  
  
**구문 예제:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml" -c "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml"`  
  
공백이 포함 된 폴더 또는 파일 이름은 큰따옴표로 지정 해야 합니다.  
  
명령줄 항목 및 오류 메시지의 출력은 STDOUT에서 또는 지정된 된 파일에 저장 됩니다.  
  
### <a name="script-file-option--sscript"></a>스크립트 파일 옵션:-s/스크립트  
필수 스위치를 스크립트 파일 경로/이름 SSMA에서 실행할 명령 시퀀스의 스크립트를 지정 합니다.  
  
**구문 예제:**  
  
`C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>변수 값 파일 옵션:-v/변수  
변수 값 파일 스크립트 파일에서 사용 되는 변수를 구성 합니다. 스위치는 선택 사항입니다. 변수는 변수 파일에 선언 된을 스크립트 파일에서 사용 하지 않고에 하는 경우 응용 프로그램 오류가 생성 되 고 콘솔 실행을 종료 합니다.  
  
**구문 예제:**  
  
-   기본값은 아마도 하나 및 해당 하는 경우 인스턴스 관련 값을 사용 하 여 다른 여러 변수 값 파일에 정의 된 변수입니다. 명령줄 인수에 지정 된 변수 파일을 마지막 변수의 중복이 발생 한 경우 기본 설정에 사용 합니다.  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>서버 연결 파일 옵션:-c/serverconnection  
이 파일에는 각 서버에 대 한 서버 연결 정보가 들어 있습니다. 각 서버 정의 ID로 식별 됩니다는 고유한 서버 서버 Id는 연결 관련 명령에 대 한 스크립트 파일에서 참조 됩니다.  
  
서버 정의는 서버 연결 파일 및/또는 스크립트 파일에 포함할 수 있습니다. 스크립트 파일에 서버 id 서버 id의 중복이 발생 한 경우 서버 연결 파일 보다 우선 합니다.  
  
**구문 예제:**  
  
-   서버 Id는 스크립트 파일에 사용 됩니다. 별도 서버 연결 파일에 정의 됩니다. 이 파일에는 변수 값 파일에 정의 된 변수를 사용 합니다.  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   서버 정의 스크립트 파일에 포함 됩니다.  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 출력 옵션:-x / xmloutput [xmloutputfile]  
이 명령은 콘솔 또는 xml 파일에 xml 형식에서 명령 출력 메시지를 출력 하는 중에 사용 됩니다.  
  
두 가지 옵션이 있습니다 xmloutput를 사용할 수 있습니다 즉:  
  
-   Filepath xmloutput 전환 된 후 출력을 파일로 리디렉션할 제공 인 경우  
  
    **구문 예제:**  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   없는 filepath xmloutput 전환 된 후 제공 된 경우는 xmlout 본체 자체에 표시 됩니다.  
  
    **구문 예제:**  
  
    `C:\>SSMAforAccessConsole.EXE -s "C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>로그 파일 옵션:-l/로그  
콘솔 응용 프로그램의 모든 SSMA 작업이 로그 파일에 기록 되 고 스위치는 선택 사항입니다. 로그 파일 및 해당 경로 명령줄에 지정 된 경우 로그는 지정된 된 위치에 생성 됩니다. 그렇지 않으면 해당가 기본 위치에 생성 됩니다.  
  
**구문 예제:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>프로젝트 환경 폴더 옵션:-e/projectenvironment  
이 선택적 스위치는 현재 SSMA 프로젝트의 프로젝트 환경 설정 폴더를 나타냅니다.  
  
**구문 예제:**  
  
`C:\>SSMAforAccessConsole.EXE -s`  
  
`"C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option--psecurepassword"></a>안전한 암호 옵션:-p/securepassword  
이 옵션에는 서버 연결에 대 한 암호화 된 암호를 나타냅니다. 마이그레이션 프로젝트에 사용 되는 서버 연결에 대 한 암호 암호화를 관리할 수 있습니다 하지만 모든 스크립트를 실행 하지 않거나 모든 마이그레이션 관련 작업에 도움이 되 고 다른 모든 옵션에서 다릅니다.  
  
명령줄 매개 변수로 옵션 또는 암호를 입력할 수 없습니다. 그렇지 않으면 오류가 발생합니다. 자세한 내용은 참조는 [관리 암호](managing-passwords-accesstosql.md) 섹션입니다.  
  
다음 하위 옵션에 대 한 지 `-p/securepassword`:  
  
-   암호를 추가 하거나 서버 연결 파일에 정의 된 모든 서버 Id 또는 지정 된 서버 ID에 대 한 보호 된 저장소에 기존 암호를 업데이트 합니다.  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   에 지정 된 서버 ID 또는 모든 서버 Id에 대 한 보호 된 저장소에서 암호화 된 암호를 제거 합니다.  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   암호를 암호화 하는 서버 Id의 목록을 표시 합니다.  
  
    `-p/securepassword -l/list`  
  
-   보호 된 저장소 암호화 된 파일에 저장 된 암호를 내보내려면 합니다. 이 파일은 사용자가 지정한 암호를 사용 하 여 암호화 됩니다.  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   암호화-내보낸 파일은 이전 사용자 지정 암호를 사용 하 여 로컬 보호 된 저장소를 가져옵니다. 파일의 암호를 해독 한 후 로컬 컴퓨터에서 암호화 되는 새 파일에 저장 됩니다.  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    쉼표 구분 기호를 사용 하 여 여러 서버 Id는 지정할 수 있습니다.  
  
### <a name="help-option--help"></a>Help 옵션:-? / h  
SSMA 콘솔 옵션의 구문 요약 정보를 표시합니다.  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
SSMA 콘솔 명령줄 옵션의 테이블 형식으로 출력을 참조 하세요 [부록-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)합니다.  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword 도움말 옵션:-securepassword-? / h  
SSMA 콘솔 옵션의 구문 요약 정보를 표시합니다.  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
SSMA 콘솔 명령줄 옵션의 테이블 형식으로 출력을 참조 하세요 [부록-1 &#40;AccessToSQL&#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>다음 단계  
다음 단계는 프로젝트 요구 사항에 따라 달라 집니다.  
  
1.  암호 또는 내보내기 지정 하기 위한 암호 가져오기 /를 참조 하십시오 [관리 암호 &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md)합니다.  
  
2.  보고서 생성을 참조 하세요 [보고서 생성 &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md)합니다.  
  
3.  콘솔에서 문제 해결을 참조 하세요 [문제 해결 &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md)합니다.  
  
